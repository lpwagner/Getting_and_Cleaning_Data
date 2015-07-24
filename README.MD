README.MD
=========================
run_analysis()
=========================

The purpose of the run_analysis function is to generate a data frame that presents the averages for each subject and for each activity for all the varaiables.

==========================

The first task the function performs is to check if the appropriate file exists in the working directory. If no such file exists, then the function loads the data from the website, https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip, saves it to a zip file, then unzips the zip file.

Once the file has been unzipped, the function reads in the 8 data sets that will be cleaned and combined, using the read.table() function. The 8 data sets are:
	X_test.txt
	X_train.txt
	y_test.txt
	y_train.txt
	subject_test.txt
	subject_train.txt
	features.txt
	activity_labels.txt

The second task the function performs is to combine the y_, activity and features information with the raw data, X_test and X_train.To do this, the function first takes the names in the features file and imposes them as the column names of the raw data. It then combines the y_ data with the activity labels by joining the two data frames, using the join() function, into a new data frame called labels_. It does this for the train and test data separately. 

The third task for the function is to then bind the subject_, labels_ and X_ data to gether. This is a simply cbind() call, creating the new data frames data_train and data_test. The function then binds these two data frames one on top of the other with a simple rbind() call. This we call data.

The forth task for the function is to find those column names of data that contain either "mean" or "std". This is accomplished by creating an index vector of 1s and 0s. For any column, if it contains "mean" or "std" or it is one of the first two columns, the corresponding element of the index vector is set to a value of 1; otherwise 0. With this index vector, the function then subsets data. This subsetted data frame is called data1.

Finally, the function can call ddply(), on data1 to take the column means for all rows that have the same subject number and activity description. This results in our tidydata data frame.