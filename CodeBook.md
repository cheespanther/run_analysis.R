The program run_analysis.R is a function that is divided into the following parts: 


I. Combining Data into one Data Frame
  1. Reads "X_test.txt" and "y_test.txt" from the "test" folder and combines them into one data frame named "test"
  2. Reads "X_test.txt" and "y_test.txt" from the "train" folder and combines them into one data frame named "train"
  3. Combines "test" and "train" data frames into one data frame named "totaldata"

Extracting Mean and Standard Deveation from Data Frame
  1. Data was subset according to activity label 1 - 6
        1 - Walking, 2 - Walking Upstairs, 3 - Walking Downstairs, 4 - Sitting, 5 - Standing, 6 - Laying
  2. 6 smaller data frames were created from the 6 subsets according to label
  3. Mean were calculated for each smaller Data Frame creating 6 new data frames with Means by Activity
  4. Standard Deviation were calculated for each smaller Data Frame creating 6 new data frames with Standard Devations by Activity

Extracting "Activities" Labels
  1. "activity_labels.txt" file was opened from the files folder
  2. A list of labels was created from this file named "activitylabel"
  3. This list was used to add columns with names to Data Frames

Combinding Data
  1. Mean and Standard Deveation Data Frames for each activity were combined, creating 6 data frames (one for each
  activity)
  2. All "mean" Data Frames were combined into one large data frame with all means
  3. Means of The combined Data Frames were were calculated and combined into a "summary" Data Frame

Extracting Data
  1. All "Tidy" Data Frames were exported to a seperate folder creating a total of 8 files. 

      * One file for each activity with mean and standard deviation columns
      * One file with means for all activities
      * One file with the Mean of the Means and Standard Deveations by Activity
