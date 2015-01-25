## courseproject

##Reads files
test_subjects <- read.table("UCI HAR Dataset/test/subject_test.txt", header = FALSE)
test_x <- read.table("UCI HAR Dataset/test/X_test.txt", header = FALSE)
test_y <- read.table("UCI HAR Dataset/test/Y_test.txt", header = FALSE)

train_subjects <- read.table("UCI HAR Dataset/train/subject_train.txt", header = FALSE)
train_x <- read.table("UCI HAR Dataset/train/X_train.txt", header = FALSE)
train_y <- read.table("UCI HAR Dataset/train/Y_train.txt", header = FALSE)

##Merges the training and the test sets to create one data set.
activity <- rbind(train_y, test_y)
features <- rbind(train_x, test_x)
subject <- rbind(train_subjects, test_subjects)

##Names the subject and activity data frames
names(subject) <- c("subject")
names(activity) <- c("activity")

##Names the features data frame
feature_names <- read.table("UCI HAR Dataset/features.txt", header = FALSE)
names(features) <- feature_names$V2

##Final merge for whole data
subject_activity <- cbind(subject, activity)
all_data <- cbind(subject_activity, features)

##Extracts only the measurements on the mean and standard deviation for each measurement. 
mean_std <- feature_names$V2[grep("mean\\(\\)|std\\(\\)", feature_names$V2)]

##Subsets the whole data with selected features.
sel_features <- c(as.character(mean_std), "subject", "activity" )
all_data <- subset(all_data, select = sel_features)

##Uses descriptive activity names to name the activities in the data set.
activity_labels <- read.table("UCI HAR Dataset/activity_labels.txt", header = FALSE)
all_data[,"activity"] <- factor(all_data[,"activity"], labels = activity_labels$V2)

##Appropriately labels the data set with descriptive variable names.
names(all_data)<-gsub("^t", "time", names(all_data))
names(all_data)<-gsub("^f", "frequency", names(all_data))
names(all_data)<-gsub("Acc", "Accelerometer", names(all_data))
names(all_data)<-gsub("Gyro", "Gyroscope", names(all_data))
names(all_data)<-gsub("Mag", "Magnitude", names(all_data))
names(all_data)<-gsub("BodyBody", "Body", names(all_data))


##From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
library("plyr")

all_data2 <- aggregate(. ~subject + activity, all_data, mean)
all_data2 <- all_data2[order(all_data2$subject, all_data2$activity),]
write.table(all_data2, file = "tidydata.txt", row.name = FALSE)
