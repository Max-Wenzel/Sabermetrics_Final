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


