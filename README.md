# Capstone Project for Google's Data Analytics course



## Overview
Bellabeat is a health-focused tech company specializing in fitness products for women founded by Urška Sršen in 2013. They sell a variety of fitness trackers meant for gathering information on the wearers' activity, sleep and stress. Their main products include the leaf tracker, a stylish wellness tracker that can be worn as a bracelet, necklace or clip; Time, a wellness tracker tha takes the look of a classic time piece; and the Bellabeat App, a smartphone app that houses all of the trackers data and helps the user better understand their current habits so they can make better, healthier decisions.

Sršen has tasked our team with analyzing smart device usage data so that we can provide insight on how consumers our using non-Bellabeat smart devices. We will analyize the data provided and produce insights that will help the Bellabeat marketing strategy. 
## Ask
    
**Business Task:** Analyze the data provided and produce insights into smart device usages to the marketing team at Bellabeat that will help the company grow on the international stage. 

**Stakeholders:** 

Urška Sršen: Cofounder and Chief Creative Officer 

Sando Mur: Cofounder, Mathematician and key member of Bellabeat's executive team.

Bellabeat's Marking Team

##  Prepare

The data provided shows the activity, heart rate and sleep of thirty participants provided by "Mobius" on Kaggle: [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)

### _Does the data "ROCCC"?_

**Reliability:** The data was provided by participants who constented to having their fitbit tracker data gathered from Mar 2016 to May 2016, by a survey via Amazon Mechanical Turk. 

**Original:** The data was taken directly from the fitbit trackers of the participants.

**Comprehensive:** The data contains information on the participants step count, calories burned, weight and sleep monitoring, given in daily, hourly and minute breakdowns. This data corresponds to activity and sleep, which can give insights into the participants usage habbits but the sample size is small and the data is some what inconsistent.

**Current:** The dataset is from March 2016 to May 2016. This data is old, not current. Usage habbits might have changed.

**Cited:** Unclear

#
The data is broken down in two different sets, one from March to April and the other from April to May. The March to April dataset does not contain data on participants sleep. Data on participants sleep is important in order to give a complete report to the martketing team, so that means we will focus on the dataset from April to May.

This dataset contains 18 CSV files. The wide formatted files dailyActivity, sleepDay, and weightLogInfo will be focused on, as they give a plethora of information on the participants activity, sleep and usage of smart devices. 

There are some issues with the data. The dataset contains 30 participants, meaning its at the minimum requirements for a sample size. A data set with 20 to 30 more participants would be more ideal. Out of the 30 participants, only 24 participants monitored their sleep and only 8 recorded their weights. These sample sizes might be too small to extrapolate meaningful data from. There is also no data on the gender and age of the participants. The former being more important due to Bellabeat's focus on creating products for women. 

## Process

Our team will be using R and Tableau during this analysis. R will be used to examine, combine and clean the data and it will be used in conjugation with Tableau to showcase the resulting datasets using different visualizations. 

We will clean the data first. This includes formatting the data properly, and cleaning the data, such as removing any duplicate entries and checking for any errors. After a short glance at the datasets, it appears that the "Fat" column contains multiple NA responses. This will not interfer with our analysis so we will leave the column as is. The rest of the cleaning process will be documented in a R Markdown file. 

## Analysis



Let's look at a summary of the data in the daily_data dataset. Using the following code will give statistical information, including mins, maxes and averages of all of the columns in the set. 

```
daily_data %>%
  select(
    Weekday, TotalSteps, TotalDistance, VeryActiveMinutes, 
    FairlyActiveMinutes, LightlyActiveMinutes, SedentaryMinutes, 
    Calories, TotalMinutesAsleep, TotalTimeInBed, WeightPounds, BMI
  ) %>%
  summary()
  ```

Let's focus on the averages of the Calories, and TotalStep to get a better understanding of the participants' general health. 
The participants burned about 2304 calories and took about 7638 steps daily. According to the CDC, healthy amounts of daily calories burned for men ranges from 2000 to 2450 and 1600 - 1950 for Women.
The average calories burned in our data set then falls within healthy ranges for men, but outside healthy ranges for women. The CDC also recommends 10000 steps daily for all adults. We can definitely say that the average steps taken by the participants fall short of the recommended amount.
The combination of fewer steps on average and a higher average of calories burned could mean that the average participant in this survey is overweight, but without data on the participants age and gender we can't know for certain.

Factoring in the information about the particpants' weights, we see that the average weight is 158lb with an average BMI of 25 (overweight).
We found in our analysis before that only 8 individuals out of the 30 total marked down information about their weight.
This means that it would be more accurate to say that the individuals who tracked their weight were on average over-weight. 
#

Let's look at how often and when the participants logged their activity data. 

![Sheet 4](https://github.com/user-attachments/assets/197873dd-7c15-4627-be4b-d7dfc3b2a2f9)

From this chart we see that the total minutes tracked is much higher from Tuesday to Thursday. Participants in the survey tracked their activities much more on these days than any other. This is most likely due to less active participants, who might not have regular exercise routines, deciding to make healthier choices on these days. Looking at the averages tells a different story. Let's take a look at the average calories burned broken down by weekday.

![Sheet 3 copy](https://github.com/user-attachments/assets/e335b6b2-8544-4e4f-862e-286ad9246e05)


By looking at the average calories burned, we see that actually Thursday has the lowest average calories burned and that Saturday rivals Tuesday as the most active day (accounting for calories burned). This corresponds with our previous hypothesis, that it is merely more people inputing data between Tuesday-Thrusday than those days being more active. Let's see if this trend also applies to the average steps taken.

![Sheet 2](https://github.com/user-attachments/assets/15d9744d-510c-4783-8c80-175e6795c00b)

Looking further into the chart we see that the average steps taken on Tuesday is 8,125 and the average for Saturday is 8,153. Looking at the average calories again we see that the calories burned for Saturday and Tuesday are virtually identical. This means that Tuesday and Saturday are on average the most active days. The correlation between Tuesday and Saturday having the highest step counts and calories burned count is what we expected; The more steps taken, the more calories burned. 

![totalCaloriesVSteps](https://github.com/user-attachments/assets/564ebf97-de21-4b6e-b013-ce8818e1fd65)


As we see there is a expected positive correlation between the amount of steps a person takes and the amount of calories that person burns. 

Now let's look at the hourly data, specifically what the average steps taken by hour looks like.

![Heatmap Avg Steps](https://github.com/user-attachments/assets/e95d46bd-99c0-461a-8817-57a44570881f)


We see from this heatmap some expected results: The highest steps taken are taken between 9am and 7pm for most days, we see higher steps taken on the weekend nights and we see fewer steps on weekend mornings than on weekday mornings. There are some surprising results: Even though Tueday has the highest on average step count, Wednesday afternoon between 5pm and 6pm and Saturday between noon and 2pm have the highest on average step counts. These seem to be the most active parts of the week for the participants. We also see a dip in the hourly steps on the weekdays around 3pm. This could correspond with the participants' lunch times. 

Let's factor in the data we have on intensities and add it to the data on steps and calories burned.
![stepsCaloriesIntensities](https://github.com/user-attachments/assets/597aa0f3-dd72-4375-a8e7-51df80ea7243)

As we can see, the intensity levels follow the amount of steps taken almost perfectly. There is also a shown correlation between the steps and the calories burned, which was shown in another chart previously. We can see in this chart that the most active time of the day on average is around 6pm, with the second most active time being around noon.

#

The data we have on sleep is limited, but still might provide useful information. 

![sleep_plot](https://github.com/user-attachments/assets/a83b6837-efb8-4c44-8ead-73e31e7501b2)


What we see from this chart, which was created by plotting the number of days tracked by every Id how how much sleep on average they got per sleep cycle. What we see is that out of the 30 participants, only 3 of them tracked their sleep for the entire 30 days. On average, the participants tracked 17 out of the 30 days. Also, only 24 participants out of the 30 even tracked any days at all. 

We do see a correlation between the amount of days tracked and how much sleep on average the participants got. The more days tracked, the more sleep on average the participants got. Its important to note that the amount of data on sleep that we have might be too small to make any meaningful comments about the data itself, but the lack of data itself can be useful to look into. 


## Share

Findings: 

- 80% of the participants tracked at minimum one day while only 26% of the participants tracked any information about their weight.

- On average, the participants took about 7,638 steps daily, less than the recommended 10,000. Participants were also most active on Tuesdays and Saturdays.


![stepsWeekday](https://github.com/user-attachments/assets/db2109a2-5a66-4431-9478-4acde323143c)

- Participants were most likely to use their smart devices to track their data between Tuesday and Thursday.

![Sheet 4 (1)](https://github.com/user-attachments/assets/77f7600d-12e7-4b3a-a167-eb00700f10da)


- The most active hour on average was 6pm and the second most active hour was noon. There is also a noticable dip in step count in the afternoon weekdays around 3pm.

![heatmap2](https://github.com/user-attachments/assets/8aca7e55-ea0c-4574-bb43-9b9df4804e8f)

- Participants spent an average of 81% of their day being sedentary, 16% lightly active, 1% fairly active, and 2% very active. 

![Sheet 6](https://github.com/user-attachments/assets/7abdda71-762d-4aec-a607-8b91444d6808)

- There is a direct correlation between the amount of steps taken and the amount of calories burned.

![CaloriesSteps](https://github.com/user-attachments/assets/7a420422-14b2-433f-a4f5-f4f94f8cb4ce)



## Act

Based on our findings:
- Tracking devices were most utlitized in the middle of the week. 

 Recommendation: Finding a way to promote device usages on the Monday, Friday during the week and entirety of the weekend to promote better overall health of the user but also to gain more fitness tracking data to help out analyses like this in the future. 

- Participants on average performed less than the recommended 10,000 step daily goal. 

Recommendation: Notify the user on the tracking device after a prolonged state of sedentary active. For example, devices can vibrate and show an alert to get the user up and moving. Participants saw a dip in afternoon step counts in the weekday afternoons around 3pm. An additional alert at this time could be warranted. 


- Insufficent data on sleep and weight tracking

Recommendation: Promote the use of smart devices like bluetooth scales that can automatically update the weights of the users. Also, promote the use of sleep tracking device.

