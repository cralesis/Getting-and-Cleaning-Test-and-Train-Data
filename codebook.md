Code Book for run_analysis.R

The script performs the data preparation and then followed by the 5 steps required as described in the 
	course project's definition.

Download the data set - Data set downloaded and extracted under the folder called UCI HAR Dataset

Assign each data to variables
	1. features <- features.txt (561 rows, 2 columns)
	The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals 
	tAcc-XYZ and tGyro-XYZ

	2. activities <- activity_labels.txt (6 rows, 2 columns)
	List of activities performed when the corresponding measurements were taken and its codes

	3. subject_test <- test/subject_test.txt (2947 rows, 1 column)
	Contains test data of 9/30 volunteer test subjects being observed

	4. x_test <- test/X_test.txt (2947 rows, 561 columns)
	Contains recorded features test data

	5. y_test <- test/y_test.txt (2947 rows, 1 column)
	Contains test data of activities code labels

	6. subject_train <- train/subject_train.txt (7352 rows, 1 column)
	Contains train data of 21/30 volunteer subjects being observed

	7. x_train <- train/X_train.txt (7352 rows, 561 columns)
	Contains recorded features train data

	8. y_train <- train/y_test.txt (7352 rows, 1 column)
	Contains train data of activities code labels

Merges the training and the test sets to create one data set
	1. x (10299 rows, 561 columns) is created by merging x_train and x_test using the rbind() function
	2. y (10299 rows, 1 column) is created by merging y_train and y_test using the rbind() function
	3. subject (10299 rows, 1 column) is created by merging subject_train and subject_test using the rbind()
	function
	4. mergeddata (10299 rows, 563 columns) is created by merging subject, y, x using the cbind() function

Extracts only the measurements on the mean and standard deviation for each measurement - tidydata (10299 rows, 88 
	columns) is created by subsetting mergeddata, selecting only the subject and code columns and the 
	measurements on the mean and standard deviation (std) for each measurement

Uses descriptive activity names to name the activities inthe data set - Entire numbers in code column of the 
	tidydata replaced with corresponding activity taken from second column of the activities variable

Appropriately labels the data set with descriptive variable names
	1. code column in tidydata is renamed activity
	2. All Acc in columns name replaced by Accelerometer
	3. All Gyro in columns name replaced by Gyroscope
	4. All BodyBody in columns name replaced by Body
	5. All Mag in columns name replaced by Magnitude
	6. All start with character t in columns name replaced by Time
	7. All start with character f in columns name replaced by Frequency
	8. All tBody in columns name replaced by TimeBody
	9. All columns name with the character string -mean() replaced by Mean
	10. All columns name with the character string -std() replaced by Standard Deviation
	11. All columns name with the character string -freq() replaced by Frequency
	12. All angle in columns name replaced by Angle
	13. All gravity in columns name replaced by Gravity

From the data set in Step 4, create a second, independent tidy data set with the average of each variable for each 
	activity and each subject
	1. finaldata (180 rows, 88 columns) is created by summarizing tidydata taking the means of each variable 
	for each activity and each subject, after grouped by subject and activity
	2. Export finaldata into finaldata.txt file
