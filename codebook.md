# Introduction

The script `run_analysis.R`performs the 5 steps described in the course project's definition.

* First, get the data.
* Second, read the data from targeted files.
  - Read data from the files into the variables.
    test_subjects
    test_x
    test_y
    train_subjects
    train_x
    train_y
* Third, Merges the training and the test sets to create one data set.
  - Merge by rows
  - Set names to variables
  - Merge by column to obtain whole data.
* Fourth, extracts only the measurements on the mean and standard deviation for each measurement.
  - Subset Name of Features by measurements on the mean and standard deviation.
  - Subset the data frame Data by seleted names of Features
  - Check the structures of the data frame Data
* Uses descriptive activity names to name the activities in the data set
Read descriptive activity names from “activity_labels.txt”
facorize Variale activity in the data frame Data using descriptive activity names
Appropriately labels the data set with descriptive variable names
prefix t is replaced by time
Acc is replaced by Accelerometer
Gyro is replaced by Gyroscope
prefix f is replaced by frequency
Mag is replaced by Magnitude
BodyBody is replaced by Body
Creates a second,independent tidy data set and ouput it
Package "plyr" is used.

* Then, only those columns with the mean and standard deviation measures are taken from the whole dataset. After extracting these columns, they are given the correct names, taken from `features.txt`.
* As activity data is addressed with values 1:6, we take the activity names and IDs from `activity_labels.txt` and they are substituted in the dataset.
* On the whole dataset, those columns with vague column names are corrected.
* Finally, we generate a new dataset with all the average measures for each subject and activity type (30 subjects * 6 activities = 180 rows). The output file is called `averages_data.txt`, and uploaded to this repository.

# Variables

* `x_train`, `y_train`, `x_test`, `y_test`, `subject_train` and `subject_test` contain the data from the downloaded files.
* `x_data`, `y_data` and `subject_data` merge the previous datasets to further analysis.
* `features` contains the correct names for the `x_data` dataset, which are applied to the column names stored in `mean_and_std_features`, a numeric vector used to extract the desired data.
* A similar approach is taken with activity names through the `activities` variable.
* `all_data` merges `x_data`, `y_data` and `subject_data` in a big dataset.
* Finally, `averages_data` contains the relevant averages which will be later stored in a `.txt` file. `ddply()` from the plyr package is used to apply `colMeans()` and ease the development.
