# How to create a tidy file using the 'run_analysis.R'
Ana Karla Medeiros  
July 26, 2015  

This document explains how to create a tidy dataset from the training and test datasets in the 'UCI HAR dataset'. The explanations are divided into two parts:

1. How to run 'run_analysis.R'
2. How does 'run_analysis.R' works


### 1. Steps to run 'run_analysis.R'

1. Fork the git repository '<https://github.com/anakarlamedeiros/data-science-specialization>'
2. Make sure that the directory 'GettingAndCleaningDataProject' has been correctly copied
3. Set you R working directory to point your local copy of 'GettingAndCleaningDataProject'
4. Run 'run_analysis.R'


### 2. Logic behind 'run_analysis.R'

The code in 'run_analysis.R' is divided into 3 sections indicated by the headers :


```r
#############################################################
## Loading the needed libraries
#############################################################


#############################################################
## Auxiliary functions to create the tidy dataset 
## (see main body below for details on the actual processing of the tidy dataset)
#############################################################


#############################################################
### main body of the program to create the tidy dataset
#############################################################
```

The code's main logic can be found at the section *'main body of the program to create the tidy dataset'*. It works as follows:

1. Set the names for the columns containing the subject id, and the activity id and label.
2. Set the main directory containing the input test and the training datasets. This main location is used by the functions ``` processTestDataset``` and ``` processTrainingDataset``` as a basis to set the specific locations of the test and training datasets, respectively.
3. Process the test and training dataset such that they:
    1. include a column for the subject (volunteer) identifier
    2. include a column for the performed activity identifier
    3. include a column for the performed activity label
    4. keep only the measurements relating to the mean and standard deviation
4. Create a new dataset containing all the rows of the processed test and training datasets (see variable ```processedMergedDataset```)
5. Calculate the average of the measurements per unique subject, activity identifier and activity label (see variable ```tidyData```)
6. Rename the colums of the variable ```tidyData``` to contain the prefix 'AVERAGE_'
7. Write ```tidyData``` to the file location specified in the variable ```locationTidyDataset```.





```r
#############################################################
### main body of the program to create the tidy dataset
#############################################################

## setting the column names to use regarding the subjects and activities
colNameSubjectID <- "SUBJECT_IDENTIFIER"
colActivityID <- "ACTIVITY_IDENTIFIER"
colActivity <- "ACTIVITY_LABEL"

## setting the main location of the directory with the test and training sets
locationMainDirectoryDatasets <- "./UCI_HAR_Dataset"

## setting the output location for the tidy dataset
locationTidyDataset <- "./tidy_UCI_HAR_Dataset.txt"

## creating the processed test and training datasets
processedTestDataset <- processTestDataset(colNameSubjectID, colActivityID, colActivity, locationMainDirectoryDatasets)
processedTrainingDataset <- processTrainingDataset(colNameSubjectID, colActivityID, colActivity, locationMainDirectoryDatasets)

## merging the processed test and training datasets
processedMergedDataset <- rbind(processedTestDataset, processedTrainingDataset)

## creating the tidy data set with the averages for every unique combination (subject, activity)
meltedMergedData <- melt(processedMergedDataset, id.vars = c(colNameSubjectID, colActivityID, colActivity))
tidyData <- dcast(meltedMergedData, SUBJECT_IDENTIFIER + ACTIVITY_IDENTIFIER + ACTIVITY_LABEL ~ variable, fun=mean)

## renaming the columns of the tidy dataset to reflect that values are the averages of the variables
colnames(tidyData) <- createTidyDataColumns(colnames(tidyData))

## writing the tidy dataset to a file
write.table(tidyData,locationTidyDataset, row.names=FALSE, sep=",")
```

