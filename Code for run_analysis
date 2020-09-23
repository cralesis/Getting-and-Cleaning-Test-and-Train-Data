## Loading required packages
library(dplyr)

## Downloading the data set
Dataname <- "getdata_projectfiles_UCI HAR Dataset.zip"

dataurl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(dataurl, Dataname, method = "curl")
unzip(Dataname)

dir()
setwd("C:/Users/cristina.rider./OneDrive/OneDrive - United States Department of the Navy/Training/John Hopkins R RStudio/Coursera")

## Assigning all data frames
features <- read.table("UCI HAR Dataset/features.txt", col.names = c("n", "functions"))
activities <- read.table("UCI HAR Dataset/activity_labels.txt", col.names = c("code", "activity"))
subject_test <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject")
x_test <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = features$functions)
y_test <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "code")
subject_train <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject")
x_train <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = features$functions)
y_train <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "code")

## the rest on run_analysis.R script

## Step 1 - Merges the training and test sets to create one data set
x <- rbind(x_train, x_test)
y <- rbind(y_train, y_test)
subject <- rbind(subject_train, subject_test)
mergeddata <- cbind(subject, y, x)

## Step 2 - Extracts only the measurements on the mean and standard deviation for each measurement
tidydata <- mergeddata %>%
     select(subject, code, contains("mean"), contains("std"))

## Step 3 - Uses descriptive activity names to name the activities in the data set
tidydata$code <- activities[tidydata$code, 2]

## Step 4 - Appropriately labels the data set with descriptive variable names
names(tidydata)[2] = "activity"
names(tidydata) <- gsub("Acc", "Accelerometer", names(tidydata))
names(tidydata) <- gsub("Gyro", "Gyroscope", names(tidydata))
names(tidydata) <- gsub("BodyBody", "Body", names(tidydata))
names(tidydata) <- gsub("Mag", "Magnitude", names(tidydata))
names(tidydata) <- gsub("^t", "Time", names(tidydata))
names(tidydata) <- gsub("^f", "Frequency", names(tidydata))
names(tidydata) <- gsub("tBody", "TimeBody", names(tidydata))
names(tidydata) <- gsub("-mean()", "Mean", names(tidydata), ignore.case = T)
names(tidydata) <- gsub("-std()", "Standard Deviation", names(tidydata), ignore.case = T)
names(tidydata) <- gsub("-freq()", "Frequency", names(tidydata), ignore.case = T)
names(tidydata) <- gsub("angle", "Angle", names(tidydata))
names(tidydata) <- gsub("gravity", "Gravity", names(tidydata))

## Step 5 - From the data set in Step 4, create a second, independent tidy data
## set with the average of each variable for each activity and each subject
finaldata <- tidydata %>%
     group_by(subject, activity) %>%
     summarize_all(list(mean))
write.table(finaldata, "finaldata.txt", row.names = F)

## Checking variable names
str(finaldata)
