
Combining Data into one Data Frame
1. "X_test.txt" and "y_test.txt" from the "test" folder were combined into one data frame named "test"
2. "X_test.txt" and "y_test.txt" from the "train" folder were combined into one data frame named "train"
3. "test" and "train" data frames were combined into one data frame

Extracting Mean and Standard Deveation from Data Frame
1. Data was subset according to activity label 1 - 6
      1 - Walking, 2 - Walking Upstairs, 3 - Walking Downstairs, 4 - Sitting, 5 - Standing, 6 - Laying
2. Smaller Data Frames for subset data were created
3. Mean and Standard deveation were calculated for each smaller Data Frame

Extracting "Activities" Labels
1. "activity_labels.txt" file was opened from the files folder
2. a list of labels was created from this file

Combinding Data
1. Mean and Standard Deveation Data Frames for each activity were combined, creating 6 data frames (one for each
activity)
2. All "mean" Data Frames were combined into one large data frame with all means
3. Means of The combined Data Frames were were calculated and combined into a "summary" Data Frame

Extracting Data
1. All "Tidy" Data Frames were exported to a seperate folder
