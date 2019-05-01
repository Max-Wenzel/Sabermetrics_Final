# Sabermetrics_Final
### Maxwell Wenzel

[Here is a video demo/explanation of my stat](https://youtu.be/fIRL56sfnII)

The data folder holds the batter_data.csv file that has all of the data needed for the stat generation file as well as BPC.csv which is the file including the stat and the stats used to compare against it.

The data generation file is not meant to be run as it is simply to show the code I used to extract the batter_data stats from both the Lahman and statcast data sets.

The stat_creation file is the main file that I used to develop the stat.

final_product is the file which can be run to observe the stat in action 

## Explanation of BPC

### Original goal
The original objective of my statistic was to find a way to somewhat accurately predict the performance of batters. The approach I took to this was to first produce a single base statistic that I would later use in the prediction. I wanted this stat to be unique in that it balances both performance and skill. For the purpose of this assignment, I was thinking of the difference between these two things as performance is how they have done for the teams they have been on and skill is what they can do in terms of raw, batting related skill. After creating this stat I would then use trends in how this stat changed over several years to predict how the stat would change the next year and therefore predict a change in a player's performance

### Creating BPsum: Batter Performance Summary

As I mentioned above the first step of creating this statistic that would combine both performance and skill. I wanted to collect five years of data with four being used to create the stat and then the fifth year could be used to perform validation to see if the stat was correctly predicting. I will start with how I developed the skill-based statistics as they are the ones that took the most effort to produce as I do not believe there are many pre-existing stats that properly encapsulate the concepts I was trying for when referring to skill.

I settled on creating three stats that I felt represented and conveyed three very important skills for batters. The first of these being DPH% which is Difficult Pitches Hit percentage, this was a stat that is essentially a batting average for only the pitches that are particularly difficult to hit such as pitches that tend to break a lot. I hoped to capture a batters skill and ability to deal with pitches that move in an unpredictable way and still manage to hit them as a player that is able to do this is likely to contribute more to their team.

The next stat that I created was FBH% which is Fast Balls Hit%, which is very similar to the previous stat in that it is batting average but only on balls that have a very high release velocity making them a more challenging hit.  A batter who can hit very fast pitches shows that they have the skill to go up against a pitcher who is very good at throwing fast pitches and not be too hindered by this additional challenge. 

The final stat that I created was BCA or Ball Call Ability. This I believe is the most indicative of a highly skilled batter as it is essentially a representation of how well a batter can recognize a pitch as one that would be called as a ball. A batter who is good at this is much less likely to strike out and is more likely to get walks which are both good features to have with a batter

#### DPH%

This stat required the statcast data as it was based on the pitch type of specific pitches and how batters performed in each situation. For this statistic, I categorized difficult pitches as Curve, Split, Screw, and Knuckle balls. I chose these pitch types as they tend to break a lot and/or deceive the batter. The way to calculate this for each player and for each year for that player find every time one of those pitch types was pitched to them and if that pitch resulted in a hit or not. To calculate this was fairly simple as all was required was to find the total times the given batter had gone up against a a pitch of one of those types and then the number of those were a hit and then find the ratio between the two numbers. 

#### FBH%

The Fast Balls Hit stat also requires the use of statcast as you need the release speed of each pitch and the outcome of that pitch. This is quite similar to DBH% as it is dealing with batting average in a specific case, however, in this case, it is a bit simpler as you only need to consider pitches above a certain speed. For this value, I chose 95mph as it seemed, from exploring the data, that most pitches are slower than this and only a small fraction are faster. I felt for this reason any ball with a release speed of at least 95mph would be indicative of an unusually fast pitch that would pose a challenge for a hitter. So much the same to DBH% I found the total number of times a pitch to a player in a year was above this speed and then the number of times this resulted in a hit. The final stat was then the ratio between those two numbers.

#### BCA

Arguably the most complex of the skill-based stats is Ball Call Ability as it based on a more in-depth part of the statcast data. The core of this stat is a way to represent how good a batter is at recognizing a pitch as outside of the strike zone. This is a difficult thing to do and is a crucial skill needed in becoming a great batter. For this, I needed the zone column from stat cast. The zone value is a number that represents roughly where the ball passed over the home plate. 

![alt text](https://baseballsavant.mlb.com/sections/statcast_search_v2/images/zones.png "Image From BaseballSavant")

As you can see in the image, the values 11, 12, 13, and 14 represent areas outside of the strike zone and should, therefore, it would be in the batters best interest to not swing at them. To produce this stat I took all the times where the ball was pitched to a batter in one of these zones and then I found the subset of those where the batter got a ball by not swinging. The ratio between the count of these is the stat and it represents how often a batter correctly does not swing at a pitch that would result in a ball. 

#### The performance based components

For the components meant to measure the performance of a batter, I used pre-existing stats that I believe are a simple and accurate summary of how a batter performs.

The first of these is Runs Batted In per At Bat, this is exactly what it sounds like as it measures how many runs a player bats in on average when they go up to bat. This is calculated by dividing a player’s RBI by their AB. I feel that this gives a good measure of how much a batter contributes to their team normalized by how often they go up to bat. This is essentially a fair way to compare how many runs players score, or in this case comparing a player from year to year. 

The second statistic that I used was OPS. I chose this as it combines firstly OBP or On Base Percentage which is reflective of how well a batter can get on base. It also combines SLG or slugging percentage which is just a batting average that has been weighted to value better hits more. Both of which I believe are very indicative of performance so it works nicely that they can fit together well by just summing them


#### Collecting Data

The first part of the data collection was quite easy as it was just dealing with Lahman data. All I had to do was filter out only the years I needed and then only the players that had data present in all years. I did this as I wanted to guarantee that there would be enough data to predict for each player. I also had to do some minor processing in order to combine rows in the cases where one player played for multiple teams in a season. I also only used players who had at least twelve hundred at-bats across the five years as that seemed to make sure that each player played a good amount in each of the five years.

The much more challenging portion of the data collection was in the statcast data which was excruciating in two different ways. First I decided that I should download all of the statcast data I would need first as it takes a very long time to download it each time even just for a few months. That way I would be able to test things out and not need to redownload the data each time I ran all of my code. I did this by breaking each of the five years into chunks and then downloading each one until I had all five years saved as CSVs. Another difficulty with the statcast data presented itself when querying it as I had to calculate each of the three stats for all players across all fifteen files which in total takes quite a long time. 

#### Combining the pieces

The way I combined these separate pieces together was rather simple, I just added all of the previous components. I felt this was sufficient as all of the components have a value that was around the same range and I didn’t think any one of these components was more important than another. I did encounter one small problem at this point: something seemed to have gone wrong in the calculation of DPH% as it was in several instances throughout the data was larger than one. This shouldn’t be possible as the numerator is the length of a subset of the denominator. Even after lots of checking for bugs, I could not find the source of this problem so I, unfortunately, had to leave it out of the final stat.

### Finding BPC from bpcsum and The Great Pivot

I initially planned for BPC to be used for prediction but my hopes for that quickly faded. Upon using the correlation of bpcsum over the first four years to predict the fifth I found some really bad results. No matter how I tweaked the parameters the best I could get from a binary prediction of if a person’s performance will increase or decrease was barely above fifty percent. 

So I decided to see what the results were from looking at the top players ranked by bpcsum and found all the players considered to be the best batters for their year were at the top, I also tried to see how it correlated to some stats like Runs, BA, and BABIP and I found there was a pretty high positive correlation for all. This led me to pivot to use bpcsum just as what it was created as: a simple to understand stat that can be used to see how a person performance as changed over time and how it compares from person to person. 

#### Value of Using BPC for Evaluation

While it may just be another stat measuring performance. I think BPC is able to stand out among the crowd by providing a unique combination of skill and performance. There are many stats that are used to compare players, but none of them I believe are able to accurately compare the player as a whole. This stat differs in that it provides a single number that encompasses everything from how often the batter gets runs for their team to how good they are at making swinging decisions. By being a combination of several disconnected stats, you can essentially black box the whole thing when using it for seeing a players trend over time or comparing players. It may not be able to definitively say one player performed better than another, but it can give a person a very good of idea of how several batters stack up. This was, after all, my original goal: be able to in one simple stat get a quick idea of how one batter compares to another and see how they’ve changed over time. This is exactly the sort of stat I wished I had back when we were choosing our fantasy teams. 
