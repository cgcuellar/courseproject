The script `run_analysis.R`performs the 5 steps described in the course project's definition.

* First, get the data.
* Second, read the data from targeted files.
  - Read data from the files into the variables:
    test_subjects,
    test_x,
    test_y,
    train_subjects,
    train_x,
    train_y.
* Third, Merges the training and the test sets to create one data set.
  - Merge by rows:
    activity,
    features,
    subject.
  - Set names to variables:
    subject,
    activity,
    features_names.
  - Merge by column to obtain whole data.
    subject_activity,
    all_data
* Fourth, extracts only the measurements on the mean and standard deviation for each measurement.
  - Subset Name of Features by measurements on the mean and standard deviation:
    mean_std.
  - Subset the data frame Data by seleted names of Features:
    sel_features,
    all_data(subset)
- Read descriptive activity names from “activity_labels.txt”
* Uses descriptive activity names to name the activities in the data set
  - facorize variale activity in the data frame all_data using descriptive activity names:
    factor function is used.
* Appropriately labels the data set with descriptive variable names
  - prefix t is replaced by time
  - Acc is replaced by Accelerometer
  - Gyro is replaced by Gyroscope
  - prefix f is replaced by frequency
  - Mag is replaced by Magnitude
  - BodyBody is replaced by Body
* Creates a second,independent tidy data set and ouput it
  - Package "plyr" is used.
