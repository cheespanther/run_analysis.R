run_analysis.R
==============
runanalysis <- function(){
## 1. Merges data into one data frame

## Reads and Combines "Train" Data
setwd("~/R/R/UCI HAR Dataset/train")
  trainx <- read.table("X_train.txt")
  trainy <- read.table("y_train.txt")
  train <- data.frame (trainy, trainx)

## Reads and Combines "Test" Data
setwd("~/R/R/UCI HAR Dataset/test")
  testx <- read.table("X_test.txt")
  testy <- read.table("y_test.txt")
  test <- data.frame (testy, testx)

## Combines "Test" and "Train" data
totaldata <- rbind(train,test, header = TRUE)

## Sets column headers for better organization
numbercolumnstotal <- ncol(totaldata)
numbercolumnstotal <- numbercolumns - 1
columnheadertotal <- c("activity", 1:numbercolumnstotal)
colnames(totaldata) <- columnheadertotal

## 2. Extracts Mean and Standard Deviation for each Measurment by "Activity" 

## Subsets data by "Activity" into arrays
totalwalk <- subset(totaldata, activity == 1)
totalwalkmean <- array(totalwalk[,-1])
totalwalkup <- subset(totaldata, activity == 2)
totalwalkupmean <- array(totalwalkup[,-1])
totalwalkdown <- subset(totaldata, activity == 3)
totalwalkdownmean <- array(totalwalkdown[,-1])
totalsit <- subset(totaldata, activity == 4)
totalsitmean <- array(totalsit[,-1])
totalstand <- subset(totaldata, activity == 5)
totalstandmean <- array(totalstand[,-1])
totallaying <- subset(totaldata, activity == 6)
totallayingmean <- array(totallaying[,-1])

##Calculates means of each Activity
promediototalwalk <- as.numeric(lapply(totalwalkmean, mean))
promediototalwalkup <- as.numeric(lapply(totalwalkupmean, mean))
promediototalwalkdown <- as.numeric(lapply(totalwalkdownmean, mean))
promediototalsit <- as.numeric(lapply(totalsitmean, mean))
promediototalstand <- as.numeric(lapply(totalstandmean, mean))
promediototallaying <- as.numeric(lapply(totallayingmean, mean))

## Calculates Standard Deviation of each Activity
sdtotalwalk <- as.numeric(lapply(totalwalkmean, sd))
sdtotalwalkup <- as.numeric(lapply(totalwalkupmean, sd))
sdtotalwalkdown <- as.numeric(lapply(totalwalkdownmean, sd))
sdtotalsit <- as.numeric(lapply(totalsitmean, sd))
sdtotalstand <- as.numeric(lapply(totalstandmean, sd))
sdtotallaying <- as.numeric(lapply(totallayingmean, sd))

## 3. Use Descriptive Data to Name Activities in the Data Set

setwd("~/R/R/UCI HAR Dataset")
  activitylabel <- read.table("activity_labels.txt")
  activitylabel <- as.matrix(activitylabel[2])

## 4. Creates Labels for the Data Set

  labelwalk <- activitylabel[1]
  labelwalkup <- activitylabel[2]
  labelwalkdown <- activitylabel[3]
  labelsit <- activitylabel[4]
  labelstand <- activitylabel[5]
  labellaying <- activitylabel[6]

## 5. Create a new "Tidy" Data Set with "Activity Labels"

## Combines the Mean and Standard Deviation into seperate Matrices by Activity

walk <- cbind(promediototalwalk, sdtotalwalk)
walkup <- cbind(promediototalwalkup, sdtotalwalkup)
walkdown <- cbind(promediototalwalkdown, sdtotalwalkdown)
sit <- cbind(promediototalsit, sdtotalsit)
stand <- cbind(promediototalstand, sdtotalstand)
laying <- cbind(promediototallying, sdtotallying)

walkmeans <- colMeans(walk)
walkupmeans <- colMeans(walkup)
walkdownmeans <- colMeans(walkdown)
sitmeans <- colMeans(sit)
standmeans <- colMeans(stand)
layingmeans <- colMeans(lying)

## Adds "Activity" labels to resulting Data Frames

walk <- cbind(labelwalk, promediototalwalk, sdtotalwalk)
walkup <- cbind(labelwalkup, promediototalwalkup, sdtotalwalkup)
walkdown <- cbind(labelwalkdown, promediototalwalkdown, sdtotalwalkdown)
sit <- cbind(labelsit, promediototalsit, sdtotalsit)
stand <- cbind(labelstand, promediototalstand, sdtotalstand)
laying <- cbind(labellaying, promediototallaying, sdtotallaying)

## Adds "Headers" to resulting Data Frames

columnheadersummary <- c("Activity", "Means", "Standard Deviation")
colnames(walk) <- columnheadersummary
colnames(walkup) <- columnheadersummary
colnames(walkdown) <- columnheadersummary
colnames(sit) <- columnheadersummary
colnames(stand) <- columnheadersummary
colnames(laying) <- columnheadersummary

## Combines all Data Sets into one Data Set 
allmeans <- cbind(promediototalwalk, promediototalwalkup, promediototalwalkdown, 
                  promediototalsit,promediototalstand, promediototallaying)
##allmeans <- data.frame(cbind(activitylabel, allmeans))
totalsummary <- rbind(walkmeans, walkupmeans, walkdownmeans, sitmeans, standmeans, layingmeans)
##totalsummary <- data.frame(rbind(activitylabel, totalsummary))
colnames(allmeans) <- c(activitylabel)

## Creates .csv Files of "Tidy" Data in a Seperate Folder

setwd("~/R/R/Results_Run_Analysis")
write.table(walk, file = "walk.txt")
write.table(walkup, file = "walkup.txt")
write.table(walkdown, file = "walkdown.txt")
write.table(sit, file = "sit.txt")
write.table(stand, file = "stand.txt")
write.table(laying, file = "laying.txt")
write.table(allmeans, file = "allmeans.txt")

message("New Data Sets can be Found in Results_Run_Analysis Folder")
return(totalsummary)

}
