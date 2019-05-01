# Sabermetrics_Final
### Maxwell Wenzel

The data folder holds the batter_data.csv file that has all of the data needed for the stat generation file as well as BPC.csv which is the file including the stat and the stats used to compare against it.

The data generation file is not meant to be run as it is simply to show the code I used to extract the batter_data stats from both the lahman and statcast data sets.

Sabermetrics Stat Creation file is the main file that I used to develop the stat.

final_product is the file which can be run to observe the stat in action 


## Explanation of BPC

### Original goal
The original objective of my statistic was to find a way to somewhat accurately predict the performance of batters. The approach I took to this was to first produce a single base statistic that I would later use in the prediction. I wanted this stat to be unique in that it balances both performance and skill. For the purpose of this assignment, I was thinking of the difference between these two things as performance is how they have done for the teams they have been on and skill is what they can do in terms of raw, batting related skill. After creating this stat I would then use trends in how this stat changed over several years to predict how the stat would change the next year and therefore predict change in a player's performance

### Creating BPsum: Batter Performance Summary

As I mentioned above the first step of creating this statistic that would combine both performance and skill. I wanted to collect five years of data with four being used to create the stat and then the fifth year could be used to perform validation to see if the stat was correctly predicting. I will start with how I developed the skill-based statistics as they are the ones that took the most effort to produce as I do not believe there are many pre-existing stats that properly encapsulate the concepts I was trying for when referring to skill.

I settled on creating three stats that I felt represented and conveyed three very important skills for batters. The first of these being DPH% which is Difficult Pitches Hit percentage, this was a stat that is essentially a batting average for only the pitches that are particularly difficult to hit such as pitches that tend to break a lot. I hoped to capture a batters skill and ability to deal with pitches that move in an unpredictable way and still manage to hit them as a player that is able to do this is likely to contribute more to their team.

The next stat that I created was FBH% which is Fast Balls Hit%, which is very similar to the previous stat in that it is batting average but only on balls that have a very high release velocity making them a more challenging hit.  A batter who can hit very fast pitches shows that they have the skill to go up against a pitcher who is very good at throwing fast pitches and not be too hindered by this additional challenge. 

The final stat that I created was BCA or Ball Call Ability. This I believe is the most indicative of a highly skilled batter as it is essentially a representation of how well a batter can recognize a pitch as one that would be called as a ball. A batter who is good at this is much less likely to strike out and is more likely to get walks which are both good features to have with a batter

#### DPH%

This stat required the statcast data as it was based on the pitch type of specific pitches and how batters performed in each situation. For this statistic, I categorized difficult pitches as Curve, Split, Screw, and Knuckle balls. I chose these pitch types as they tend to break a lot and/or deceive the batter. The way to calculate this for each player and for each year for that player find every time one of those pitch types was pitched to them and if that pitch resulted in a hit or not. To calculate this was fairly simple as all was required was to find the total times the given batter had gone up against a a pitch of one of those types and then the number of those were a hit and then find the ratio between the two numbers. 

#### FBH%

The Fast Balls Hit stat also requires the use of statcast as you need the release speed of each pitch and the outcome of that pitch. This is quite similar to DBH% as it is dealing with batting average in a specific case, however, in this case, it is a bit simpler as you only need to consider pitches above a certain speed. For this value, I chose 95mph as it seemed, from exploring the data, that most pitches are slower than this and only a small fraction are faster. I felt for this reason any ball with a release speed of at least 95mph would be indicative of an unusually fast pitch that would pose a challenge for a hitter. So much the same to DBH% I found the total number of times a pitch to a player in a year was above this speed and then the number of times this resulted in a hit. The final stat was then the ratio between those two numbers.


