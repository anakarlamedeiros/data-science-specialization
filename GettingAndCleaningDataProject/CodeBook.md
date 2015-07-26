# Creating tidy data for the 'UCI HAR Dataset'
Ana Karla Medeiros  
July 26, 2015  


### Tidy data: Introduction

**This document describes the tidy data '*tidy_UCI_HAR_Dataset.txt*' that has been created as part of the project for the course "Getting and Cleanining Data".**
The tidy data is based on the 'UCI HAR Dataset' available at <https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip>. 


As explained in the file 'README.txt' from 'UCI HAR Dataset':

*"(...) The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. (...)"*

For more details on the 'UCI HAR Dataset', please refer to the files 'README.txt', and 'features_info.txt' at <https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip>. 

The remainder of this document explains the variables, the data and the transformations that have been performed to the 'UCI HAR Dataset' when creating the tidy data **tidy_UCI_HAR_Dataset.txt**.

### Tidy data: Variables

There are 69 variables in the tidy data:

1. "SUBJECT_IDENTIFIER": subject (or volunteer) number            
2. "ACTIVITY_IDENTIFIER": identifier of the activity performed by the subject
3. "ACTIVITY_LABEL": label of the activity performed by the subject
  
The remaining 66 variables are **averages computed for the mean and the standard deviations measurements in the "UCI HAR Dataset" for the training and the test datasets**. Hereby the excerpt of the file 'features_info.txt' describing these variables:

*" (...) The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz.* 

*Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag).* 

*Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals).* 

*These signals were used to estimate variables of the feature vector for each pattern:  '-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.*

- *tBodyAcc-XYZ*
- *tGravityAcc-XYZ*
- *tBodyAccJerk-XYZ*
- *tBodyGyro-XYZ*
- *tBodyGyroJerk-XYZ*
- *tBodyAccMag*
- *tGravityAccMag*
- *tBodyAccJerkMag*
- *tBodyGyroMag*
- *tBodyGyroJerkMag*
- *fBodyAcc-XYZ*
- *fBodyAccJerk-XYZ*
- *fBodyGyro-XYZ*
- *fBodyAccMag*
- *fBodyAccJerkMag*
- *fBodyGyroMag*
- *fBodyGyroJerkMag*

*The set of variables that were estimated from these signals are:*

- *mean(): Mean value*
- *std(): Standard deviation*
*(...)*

### Tidy data: Data

The tidy dataset has 40 rows describing the averages for the mean's and standard deviation's measurements of 30 volunteers per performed activity. Note that not all subjects (or volunteers) have performed all the activities. 

The tidy dataset is based on the training and test datasets provided in the 'UCI HAR Dataset'. 

The test dataset consists of the files: 

- X_test.txt: contains the actual measurements, including the mean and standard deviations
- subject_test.txt: subject identifiers per row of 'X_test.txt'
- y_test.txt: activity identifier per row of 'X_test.txt'

In a similar way, the training dataset has the files : 

- X_train.txt: contains the actual measurements, including the mean and standard deviations
- subject_train.txt: subject identifiers per row of 'X_test.txt'
- y_train.txt: activity identifier per row of 'X_test.txt'


### Tidy data: Transformations

The tidy dataset **'tidy_UCI_HAR_Dataset.txt'** contains the averages of the mean and the standard deviations measurements for all the individuals per performed activity. Therefore, to get all this into one data, the following operations have been performed:

1. Combine the *test* files into one, where each row also contains the subject identifier,  the activity identifier, the activity label, mean values of the measurements and standard deviation values of the measurements.
2. Combine the *training* files as described in the previous step.
3. Compute the *average (or mean)* of these measurements per unique subject, activity identifier and activity label
4. Write the result to the textual file **'tidy_UCI_HAR_Dataset.txt'**


```r
tidyData <- read.table("./tidy_UCI_HAR_Dataset.txt", header=TRUE, sep=",")
head(tidyData, n=2)
```

```
##   SUBJECT_IDENTIFIER ACTIVITY_IDENTIFIER ACTIVITY_LABEL
## 1                  1                   1        WALKING
## 2                  2                   1        WALKING
##   AVERAGE_tBodyAcc.mean...X AVERAGE_tBodyAcc.mean...Y
## 1                 0.2656969               -0.01829817
## 2                 0.2731131               -0.01913232
##   AVERAGE_tBodyAcc.mean...Z AVERAGE_tBodyAcc.std...X
## 1                -0.1078457               -0.5457953
## 2                -0.1156500               -0.6055865
##   AVERAGE_tBodyAcc.std...Y AVERAGE_tBodyAcc.std...Z
## 1               -0.3677162               -0.5026457
## 2               -0.4289630               -0.5893601
##   AVERAGE_tGravityAcc.mean...X AVERAGE_tGravityAcc.mean...Y
## 1                    0.7448674                  -0.08255626
## 2                    0.6607829                  -0.14721989
##   AVERAGE_tGravityAcc.mean...Z AVERAGE_tGravityAcc.std...X
## 1                   0.07233987                  -0.9598594
## 2                   0.13486534                  -0.9630155
##   AVERAGE_tGravityAcc.std...Y AVERAGE_tGravityAcc.std...Z
## 1                  -0.9511506                  -0.9258176
## 2                  -0.9600336                  -0.9453654
##   AVERAGE_tBodyAccJerk.mean...X AVERAGE_tBodyAccJerk.mean...Y
## 1                    0.07709305                   0.016590844
## 2                    0.07853532                   0.007087712
##   AVERAGE_tBodyAccJerk.mean...Z AVERAGE_tBodyAccJerk.std...X
## 1                 -0.0091075873                   -0.5247219
## 2                  0.0007557607                   -0.5578096
##   AVERAGE_tBodyAccJerk.std...Y AVERAGE_tBodyAccJerk.std...Z
## 1                   -0.4704124                   -0.7173223
## 2                   -0.4918759                   -0.7418854
##   AVERAGE_tBodyGyro.mean...X AVERAGE_tBodyGyro.mean...Y
## 1                -0.02087641                -0.08807227
## 2                -0.05170307                -0.05684202
##   AVERAGE_tBodyGyro.mean...Z AVERAGE_tBodyGyro.std...X
## 1                 0.08626417                -0.6865557
## 2                 0.08725994                -0.7106489
##   AVERAGE_tBodyGyro.std...Y AVERAGE_tBodyGyro.std...Z
## 1                -0.4509798                -0.5974961
## 2                -0.7229437                -0.6348889
##   AVERAGE_tBodyGyroJerk.mean...X AVERAGE_tBodyGyroJerk.mean...Y
## 1                    -0.09711202                    -0.04171648
## 2                    -0.08755875                    -0.04339868
##   AVERAGE_tBodyGyroJerk.mean...Z AVERAGE_tBodyGyroJerk.std...X
## 1                    -0.04713940                    -0.6378127
## 2                    -0.05575418                    -0.6716791
##   AVERAGE_tBodyGyroJerk.std...Y AVERAGE_tBodyGyroJerk.std...Z
## 1                    -0.6344722                    -0.6645920
## 2                    -0.7835955                    -0.6746119
##   AVERAGE_tBodyAccMag.mean.. AVERAGE_tBodyAccMag.std..
## 1                 -0.4536329                -0.4970964
## 2                 -0.5352818                -0.5528125
##   AVERAGE_tGravityAccMag.mean.. AVERAGE_tGravityAccMag.std..
## 1                    -0.4536329                   -0.4970964
## 2                    -0.5352818                   -0.5528125
##   AVERAGE_tBodyAccJerkMag.mean.. AVERAGE_tBodyAccJerkMag.std..
## 1                     -0.5454316                    -0.5159222
## 2                     -0.5877774                    -0.5121153
##   AVERAGE_tBodyGyroMag.mean.. AVERAGE_tBodyGyroMag.std..
## 1                  -0.4754048                 -0.4998396
## 2                  -0.6147711                 -0.6805849
##   AVERAGE_tBodyGyroJerkMag.mean.. AVERAGE_tBodyGyroJerkMag.std..
## 1                      -0.6395174                     -0.6520508
## 2                      -0.7465595                     -0.7400887
##   AVERAGE_fBodyAcc.mean...X AVERAGE_fBodyAcc.mean...Y
## 1                -0.5318952                -0.4064354
## 2                -0.5737709                -0.4325666
##   AVERAGE_fBodyAcc.mean...Z AVERAGE_fBodyAcc.std...X
## 1                -0.5964112               -0.5530606
## 2                -0.6300812               -0.6197881
##   AVERAGE_fBodyAcc.std...Y AVERAGE_fBodyAcc.std...Z
## 1               -0.3901509               -0.4985831
## 2               -0.4647239               -0.6006786
##   AVERAGE_fBodyAccJerk.mean...X AVERAGE_fBodyAccJerk.mean...Y
## 1                    -0.5473489                    -0.5073436
## 2                    -0.5616820                    -0.5089038
##   AVERAGE_fBodyAccJerk.mean...Z AVERAGE_fBodyAccJerk.std...X
## 1                    -0.6953051                   -0.5439798
## 2                    -0.7157453                   -0.5951056
##   AVERAGE_fBodyAccJerk.std...Y AVERAGE_fBodyAccJerk.std...Z
## 1                   -0.4662517                   -0.7378619
## 2                   -0.5091475                   -0.7670870
##   AVERAGE_fBodyGyro.mean...X AVERAGE_fBodyGyro.mean...Y
## 1                 -0.6232192                 -0.5053094
## 2                 -0.6387177                 -0.7220690
##   AVERAGE_fBodyGyro.mean...Z AVERAGE_fBodyGyro.std...X
## 1                 -0.5535291                -0.7082634
## 2                 -0.6015949                -0.7345885
##   AVERAGE_fBodyGyro.std...Y AVERAGE_fBodyGyro.std...Z
## 1                -0.4298258                -0.6504762
## 2                -0.7271677                -0.6831145
##   AVERAGE_fBodyAccMag.mean.. AVERAGE_fBodyAccMag.std..
## 1                 -0.4784485                -0.5897102
## 2                 -0.5145699                -0.6466623
##   AVERAGE_fBodyBodyAccJerkMag.mean.. AVERAGE_fBodyBodyAccJerkMag.std..
## 1                         -0.4990758                        -0.5418231
## 2                         -0.5097464                        -0.5188008
##   AVERAGE_fBodyBodyGyroMag.mean.. AVERAGE_fBodyBodyGyroMag.std..
## 1                      -0.5350028                     -0.5665767
## 2                      -0.6997429                     -0.7253103
##   AVERAGE_fBodyBodyGyroJerkMag.mean.. AVERAGE_fBodyBodyGyroJerkMag.std..
## 1                          -0.6459707                         -0.6858113
## 2                          -0.7516151                         -0.7441950
```

