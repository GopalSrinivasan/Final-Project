# Final-Project (Data Science)

## Why Do Some Batters Age Better Than Others?

When signing a free agent or extending a player's contract, front offices are always weary of how many years they offer. In the back-half of the contract, players are less likely to be worth their annual salary. However, some players age better than others and are able to produce results at a relatively high level. 

Our goal here is to find attributes certain players have that enable them to sustain a high level of performance relative to others based on an array of advanced statistics.

# Data Source and Terminology

*website: fangraphs.com*

**Wins Above Replacement (WAR)** - an estimate of a player's total contribution to their team

**Exit Velocity (EV)** - how fast, in mph, a ball was hit by a batter

**Launch Angle (LA)** - how high/low, in degrees, a ball was hit by a batter

**Hard Hit % (HardHit%)** - percentage of hits that were had an exit velocity of 95mph or more 

**Outside-the-Zone Swing Rate (O-Swing%)** - percentage of swings on pitches outside of the strikezone

**Inside-the-Zone Contact (Z-Contact%)** - percentage of batted balls on pitches inside of the strikezone

**Pull Field Percentage (Pull%)** - percentage of batted balls pulled toward the hitter's batting side

**Center Field Percentage (Cent%)** - percentage of batted balls hit up-the-middle of the field

**Opposite Field Percentage (Oppo%)** - percentage of batted balls hit to the opposite to the hitter's batting side

# Read Files and Construct DataFrame

Five csv files were read, one for each year from 2015-2019. The data query from Fangraphs was limited to batters that had a qualified number of plate appearances - meaning they were qualified for the batting title. This is 3.1 plate appearances for every game scheduled, or 502 plate appearances over a 162-game season. This was to avoid major skews in data because of a player's performance over a small set of games. Additionally, WAR is a cumulative stat over the course of the year.

Each file was read as a dataframe and cleaned up to be ultimately joined as one big dataframe. First, year columns had to be added. Secondly, I only wanted to analyze the subset of players that had data in each file. While this was not necessary, I believed it would be valuable to present five-years worth of progression for the subset of players. After identifying which players could be used in the analysis, the dataframes were joined together.

# Data Manipulation

* Data that were represented as percentages, such as hard-hit rate, were being read as strings rather than floats. In order to fix this issue, a function was created to remove the last character of the string (a "%" sign) and set the type to a float.
* As unrepentant cheaters, it was important to identify any Astros players in the subset by adding an asterisk to the team name. Thus, another function was created that simply added an asterisk to the team name.
* For the purposes of the data visualization, negative WAR values needed to be set as null. WAR values needed to be exponentiated in order to clearly see which players performed well, and which didn't. A function was created to do this as well.
* Methods were created for every single player across every single series that would be tested. While tedious, it provides an opportunity to dig deeper into the data and see trends at a player level in order to understand things such as outliers. Using these methods, standard deviation of every player's WAR over the five years was calculated and fed into a new dataframe.

# Visualization and Analysis

1. The 5 players with the highest and lowest standard deviations were found and the data was framed as a line chart.
2. All player WARs and ages were graphed in a scatterplot
3. Subsequent scatterplots were created in the following way: the x-axis would always be the age, the y-axis would always be a new series so we can see its behavior with age, and the data points themselves would be scaled by exponentiating the individual player's WAR for the given year by 2.5. This added dimension allows us to see if any patterns exist in relation to a player's certain skill and age to their performance.

# Findings

Standard Deviation - the players with the lowest standard deviation in their WAR were older than those with the highest standard deviation

Age x War - as players age, their WAR decreases

Age x Exit Velocity x WAR - it is clear that from the ages of 24-28, players with higher exit velocities generally produce more than those that do not. The data is not so clear from the ages of 28-30, but from 31-32 it is evident that players with lower exit velocities tend to produce at a relatively lower level than those with higher exit velocities

Age x Launch Angle x WAR - no clear pattern

Age x Hard Hit Rate x WAR - younger players who more frequently hit the ball hard produce more than other young players, but there is no discernable pattern for those from the ages of 28-32. Again, however, ages 31 and 32 show lower WAR associated with lower hard hit rates

Age x Swings Out of the Zone x WAR - players with relatively fewer swings on pitches outside of the strike zone seemed to perform better than those that chased pitches

Age x Contact in the Zone x WAR - overall trend of contact on pitches in the strike zone falling with age

Age x Pulled Ball Rate x WAR - consistent pull rates with age track with higher performance, where as increasing pull rates with age track with lower performance

Age x Center Ball Rate x WAR - higher performing players seem to hit the ball up the middle at a generally consistent rate as they age

Age x Opposite Ball Rate x WAR - higher performing players seem to revert back to hitting the ball the other way at the same rate that they did when they were younger

# Insight

Players with longevity tend to be steady performers - teams know what they are going to get from them. As a result, it makes sense that older players have smaller deviations in performance. Meanwhile, younger players both have to adjust to a higher quality of pitching, and the pitchers need to adjust to a new player coming up in the league. This makes it very reasonable that performance can vary in the beginning years of a player's career.

All else equal, exit velocity, consistency in contact, and the quality of contact seem to be important for players that want to continue playing well as they age. Discipline is also key. Aging players compensating for lower reflexes may extend the zone to get out in front of pitches. It is also why they may pull the ball more rather than having a balanced approach at the plate. Interestingly, there didn't seem to be a noticeable pattern with a player's performance and launch angle with age. This may be because of the "launch angle revolution" in the last few years, where every player is trying to get under the ball and have an optimal trajectory for a homerun. The focus could lead to consistency which results in little deviation with age, but does not necessarily aid or benefit performance.

# Thoughts and Next Steps

This analysis was done identifying patterns by sight. Deeper statistical analysis was not done, and so the patterns/assumed correlations may not hold true. A larger sample size could produce different results. Sabermetricians may even point to other underlying statistics that show the profile of a batter who ages better than most.

The next step would be to use traditional statistical analysis to see if any of the findings are statistically significant.










