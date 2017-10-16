---
title: "Reproducible Research: Peer Assignment 1"
output:
  html_document:
    keep_md: true
---

## Load and Process Data

```r
setwd("D:/Coursera")
stepData <- read.csv("activity.csv")
stepData$date <- as.Date(stepData$date, format = "%Y-%m-%d")
```

## What is the total number of steps taken per day?
rm.na = TRUE to ignore missing values.

```r
steps <- aggregate(steps ~ date, rm.na = TRUE, data = stepData, FUN = sum)
```

### Histogram of steps per day

```r
plot(steps, type = "h", lwd = 5,
	xlab = "Date", ylab = "Steps", main = "Total Steps per Day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

### Calculate and report the mean and median of the total number of steps per day

```r
aggregate(steps ~ date, data = stepData, FUN = mean)
```

```
##          date      steps
## 1  2012-10-02  0.4375000
## 2  2012-10-03 39.4166667
## 3  2012-10-04 42.0694444
## 4  2012-10-05 46.1597222
## 5  2012-10-06 53.5416667
## 6  2012-10-07 38.2465278
## 7  2012-10-09 44.4826389
## 8  2012-10-10 34.3750000
## 9  2012-10-11 35.7777778
## 10 2012-10-12 60.3541667
## 11 2012-10-13 43.1458333
## 12 2012-10-14 52.4236111
## 13 2012-10-15 35.2048611
## 14 2012-10-16 52.3750000
## 15 2012-10-17 46.7083333
## 16 2012-10-18 34.9166667
## 17 2012-10-19 41.0729167
## 18 2012-10-20 36.0937500
## 19 2012-10-21 30.6284722
## 20 2012-10-22 46.7361111
## 21 2012-10-23 30.9652778
## 22 2012-10-24 29.0104167
## 23 2012-10-25  8.6527778
## 24 2012-10-26 23.5347222
## 25 2012-10-27 35.1354167
## 26 2012-10-28 39.7847222
## 27 2012-10-29 17.4236111
## 28 2012-10-30 34.0937500
## 29 2012-10-31 53.5208333
## 30 2012-11-02 36.8055556
## 31 2012-11-03 36.7048611
## 32 2012-11-05 36.2465278
## 33 2012-11-06 28.9375000
## 34 2012-11-07 44.7326389
## 35 2012-11-08 11.1770833
## 36 2012-11-11 43.7777778
## 37 2012-11-12 37.3784722
## 38 2012-11-13 25.4722222
## 39 2012-11-15  0.1423611
## 40 2012-11-16 18.8923611
## 41 2012-11-17 49.7881944
## 42 2012-11-18 52.4652778
## 43 2012-11-19 30.6979167
## 44 2012-11-20 15.5277778
## 45 2012-11-21 44.3993056
## 46 2012-11-22 70.9270833
## 47 2012-11-23 73.5902778
## 48 2012-11-24 50.2708333
## 49 2012-11-25 41.0902778
## 50 2012-11-26 38.7569444
## 51 2012-11-27 47.3819444
## 52 2012-11-28 35.3576389
## 53 2012-11-29 24.4687500
```

```r
aggregate(steps ~ date, data = stepData, FUN = median)
```

```
##          date steps
## 1  2012-10-02     0
## 2  2012-10-03     0
## 3  2012-10-04     0
## 4  2012-10-05     0
## 5  2012-10-06     0
## 6  2012-10-07     0
## 7  2012-10-09     0
## 8  2012-10-10     0
## 9  2012-10-11     0
## 10 2012-10-12     0
## 11 2012-10-13     0
## 12 2012-10-14     0
## 13 2012-10-15     0
## 14 2012-10-16     0
## 15 2012-10-17     0
## 16 2012-10-18     0
## 17 2012-10-19     0
## 18 2012-10-20     0
## 19 2012-10-21     0
## 20 2012-10-22     0
## 21 2012-10-23     0
## 22 2012-10-24     0
## 23 2012-10-25     0
## 24 2012-10-26     0
## 25 2012-10-27     0
## 26 2012-10-28     0
## 27 2012-10-29     0
## 28 2012-10-30     0
## 29 2012-10-31     0
## 30 2012-11-02     0
## 31 2012-11-03     0
## 32 2012-11-05     0
## 33 2012-11-06     0
## 34 2012-11-07     0
## 35 2012-11-08     0
## 36 2012-11-11     0
## 37 2012-11-12     0
## 38 2012-11-13     0
## 39 2012-11-15     0
## 40 2012-11-16     0
## 41 2012-11-17     0
## 42 2012-11-18     0
## 43 2012-11-19     0
## 44 2012-11-20     0
## 45 2012-11-21     0
## 46 2012-11-22     0
## 47 2012-11-23     0
## 48 2012-11-24     0
## 49 2012-11-25     0
## 50 2012-11-26     0
## 51 2012-11-27     0
## 52 2012-11-28     0
## 53 2012-11-29     0
```
Note that the median function does not seem to be working properly with data tables.  It returns all 0's here.

## What is the average daily activity pattern?

```r
plot(aggregate(steps ~ interval, data = stepData, FUN = mean), type = "l",
	xlab = "Interval", ylab = "Steps", main = "Average Number of Steps Across All Days")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

### Which 5-minute interval, on average across all days, contains the maximum number of steps?

```r
max(stepData$steps, na.rm = TRUE)
```

```
## [1] 806
```

## Imputing Missing Values
### Calculate and report the total number of missing values in the dataset

```r
sum(is.na(stepData))
```

```
## [1] 2304
```

### Fill in missing data
I'm using the mean steps of the original dataset as a constant to fill in every missing value.

```r
stepData <- read.csv("activity.csv")
stepData2 <- stepData
meanStep <- mean(na.omit(stepData$steps))
stepData2$steps[is.na(stepData2$steps)] <- meanStep
stepData2$date <- as.Date(stepData2$date, format = "%Y-%m-%d")
```

### Make a histogram of total number of steps for each day with filled dataset

```r
steps2 <- aggregate(steps ~ date, data = stepData2, FUN = sum)

par(mfrow = c(1, 2))
plot(steps, type = "h", lwd = 5, xlab = "Date", ylab = "Steps",
	main = "Total Steps with NAs")
plot(steps2, type = "h", lwd = 5, xlab = "Date", ylab = "Steps",
	main = "Total Steps with NAs Filled")
```

![](PA1_template_files/figure-html/unnamed-chunk-9-1.png)<!-- -->
The filled dataset has less gaps overall, making for a somewhat smoother curve.

## Are there differences in activity patterns between weekdays and weekends?

### Create a new factor variable in the dataset with two levels - "weekday" and "weekend"
Using the filled dataset

```r
stepData2$dayOfWeek <- factor(format(stepData2$date, "%A"))
levels(stepData2$dayOfWeek) <- list(weekday = c("Monday", "Tuesday", "Wednesday",
											                        "Thursday, Friday"),
								                    weekend = c("Saturday", "Sunday"))
```

### Make a times series panel plot of average number of steps taken across all weekdays or weekend days.

```r
par(mfrow = c(2, 1))
with(stepData2[stepData2$dayOfWeek == "weekday",],
	plot(aggregate(steps ~ interval, FUN = mean), type = "l",
		xlab = "Interval", ylab = "Steps", main = "Weekday Step Totals"))
with(stepData2[stepData2$dayOfWeek == "weekend",],
	plot(aggregate(steps ~ interval, FUN = mean), type = "l",
		xlab = "Interval", ylab = "Steps", main = "Weekend Step Totals"))
```

![](PA1_template_files/figure-html/unnamed-chunk-11-1.png)<!-- -->
