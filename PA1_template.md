---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

## Loading and preprocessing the data


```r
# 1. Load the data (i.e. \color{red}{\verb|read.csv()|}read.csv())
activityData <- read.csv("~/GitHub/RepData_PeerAssessment1/activity.csv")

# 2. Process/transform the data (if necessary) into a format suitable for your analysis
activityData$date <- as.Date(activityData$date)
```

## What is mean total number of steps taken per day?

1. Calculate the total number of steps taken per day

```r
TotalStepsPerDay <- aggregate(steps ~ date, activityData, sum, na.action = na.omit)
```

2. Make a histogram of the total number of steps taken each day

```r
hist(TotalStepsPerDay$steps, xlab = "Total number of steps taken per day", main = "Total number of steps taken per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

3. Calculate and report the mean and median of the total number of steps taken per day:

Mean number of steps per day:

```r
MeanStepsPerDay <- mean(TotalStepsPerDay$steps)
MeanStepsPerDay
```

```
## [1] 10766.19
```
Median number of steps per day:

```r
MedianStepsPerDay <- median(TotalStepsPerDay$steps)
MedianStepsPerDay
```

```
## [1] 10765
```

## What is the average daily activity pattern?

1. Make a time series plot (i.e. \color{red}{\verb|type = "l"|}type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
# calculate average steps by interval (all days)
AverageStepsAllDays <- aggregate(steps ~ interval, activityData, mean, na.action = na.omit)

plot(AverageStepsAllDays$interval, AverageStepsAllDays$steps, xlab = "Intervals (5-minutes)", ylab = "Average number of steps", main = "Average number of steps by interval" , type = "l")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
AverageStepsAllDays$interval[max(AverageStepsAllDays$steps)]
```

```
## [1] 1705
```

## Imputing missing values

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with \color{red}{\verb|NA|}NAs)

```r
sum(is.na(activityData$steps))
```

```
## [1] 2304
```

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

```r
#create copy of original data to modify
activityDataComplete <- activityData

# replace NAs with median steps for same day
#activityDataComplete$steps[is.na(activityDataComplete$steps)] <- activityDataComplete$steps[MedianStepsPerDay$date == activityDataComplete$date]
```

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

## Are there differences in activity patterns between weekdays and weekends?
1. Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.


2. Make a panel plot containing a time series plot (i.e. \color{red}{\verb|type = "l"|}type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.



