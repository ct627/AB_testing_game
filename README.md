# A/B testing Project in Python 

## Backgrand

**Cookie Cats** is a mobile puzzle game developed by Tactile Entertainment.   
It's a classic "connect three"- a style puzzle game where the player must connect tiles of the same color to clear the board and win the level.   
As players progress through the levels of the game, they will occasionally encounter gates that force them to wait a non-trivial amount of time or make an in-app purchase to progress.   
In addition to driving in-app purchases, these gates serve the important purpose of giving players an enforced break from playing the game, hopefully resulting in that the player's enjoyment of the game being increased and prolonged.  

## Goal & Design problem      

#### Improve retention rate and conversion rate (in-purchase rate).  

Initially, the first gate was placed at level 30, and we're going to analyze an A/B test to figure out that should we moved the first gate in Cookie Cats from level 30 to level 40? Can we improve the retention rate and conversion rate by shift the gate?          
Therefore, this analysis will be on how the gate placement affects player retention.   

#### Should we move the gate from level 30 to level 40 in the game?      

Let the retention rate for gate_30 be P_30 and gate_40 be P_40       
The hypothesis will be:   
H0:P_30=P_40   
HA:P_30>P_40   

## Data Preparation

#### Assumptions   

- **User has been assigned to level 30 or 40 is random**: When a player installed the game, he or she was randomly assigned to either gate_30 or gate_40.     
- **Each experiment unit are independent**: Each user is independent and not the same person.    
- **The factor to test is the only reason for the difference**: The only difference between the two groups of users is the gate.

#### Data Description   

<img width="650" style="text-align: center" alt="data shape" src="/images/dataShape.png">  

The data we have is from 90,189 players that installed the game while the AB-test was running.   
When a player installed the game, he or she was randomly assigned to either **gate_30** or **gate_40**.   

The variables are:   
- **userid**: a unique number that identifies each player.
- **version**: whether the player was put in the control group (gate_30 - a gate at level 30) or the group with the moved gate (gate_40 - a gate at level 40).
- **sum_gamerounds**: the number of game rounds played by the player during the first 14 days after install.
- **retention_1**: did the player come back and play 1 day after installing?
- **retention_7**: did the player come back and play 7 days after installing?

#### Data Summary

**Import Data**   
<img width="650" style="text-align: center" alt="data head" src="/images/dataHead.png">   
Each unique user id was assigned a version either gate_30 or gate_40 and was record their total game rounds.   
Then the retention status is that after installing day 1 and day 7, did the user come back and play the game?   

**Check Sanity**   
<img width="650" style="text-align: center" alt="check sanity" src="/images/checkSanity2.png">  
A sanity check is to see If there are roughly the same number of players in each gate_30 and gate_40 group.  
And it looks like there is roughly the same number of players in each group.  

## Measurement

#### Retention Rate     
   
<img width="650" style="text-align: center" alt="rentention rate 1" src="/images/rentention_1Rate.png">  
   
There is a little less than half of the players come back one day after installing the game.   
    
The retention rate in day_1 in two versions:   
gate_30:  44.8%    
gate_40:  44.2%   
  
<img width="650" style="text-align: center" alt="rentention rate 7" src="/images/rentention_7Rate.png">    

The retention rate in day_7 in two versions:   
gate_30:  19.0%    
gate_40:  18.2%  

**There is a slight decrease in retention when the gate was moved.**    

#### Bootstrap Method
  
Here we will use bootstrapping method to get at the certainty of these retention numbers.    
Because the data here is highly skewed and is hard to approximate with CLT, using bootstrapping method should give us a more accurate result than using an asymptotic normality-based approximation.   
Bootstrap: A resampling method with replacement. Same sample size as the original sample data.   
  
<img width="650" style="text-align: center" alt="bootstrap" src="/images/bootstrap.png">  
  
These two distributions above represent the bootstrap uncertainty over what the underlying 1-day retention could be for the two AB-groups.   
  
#### Result   
    
**The difference in 1-day retention**     
  
<img width="650" style="text-align: center" alt="diference" src="/images/difference.png">   
  
From this chart, we can see that the most likely % difference is around 1% – 2% and that most of the distribution is above 0%, in favor of a gate at level 30.   
  
<img width="650" style="text-align: center" alt="prob of diference" src="/images/probOfDifference.png">    
  
Calculating the probability that 1-day retention is greater when the gate is at level 30.  

The bootstrap analysis tells us that there is a high probability that 1-day retention is better when the gate is at level 30.  

However, since players have only been playing the game for one day, it is likely that most players haven't reached level 30 yet.   
That is, many players won't have been affected by the gate, even if it's as early as level 30.  
  
So how about the 7-day retention?  
  
**The difference in 7-day retention**    

After having played for a week, more players should have reached level 40, and therefore it makes sense to also look at 7-day retention. 
  
<img width="650" style="text-align: center" alt="7 diference" src="/images/7difference.png">  

The probability of a difference: 100% 7-day retention is greater when the gate is at level 30.   
   
<img width="650" style="text-align: center" alt="7 diference 2" src="/images/7 difference2.png">   

#### P-value of Hypothesis   

<img width="650" style="text-align: center" alt="formula" src="/images/formula.png">  

<img width="650" style="text-align: center" alt="1P" src="/images/1P.png">  

1 day Retention:  
**n_1=44700** sample size for group gate_30  
**n_2=45489** sample size for group gate_40  
**x_1=20034** retention count for group gate_30  
**x_2=20119** retention count for group gate_40  

<img width="650" style="text-align: center" alt="p1d" src="/images/p1d.png">  
  
Since the **p-value is 0.117 greater than 0.05**, we **fail to reject** the null hypothesis. There’s no enough evidence to support that the 1-day retention rate for the gate at level 40 is greater than that for the gate at level 30.  
  
<img width="650" style="text-align: center" alt="7P" src="/images/7P.png">  

7 day Retention:  
**n_1=44700** sample size for group gate_30  
**n_2=45489** sample size for group gate_40  
**x_1=8502** retention count for group gate_30  
**x_2=8279** retention count for group gate_40  

<img width="650" style="text-align: center" alt="p7d" src="/images/p7d.png">  
  
Since the **p-value is 0.086 greater than 0.05**, we **fail to reject** the null hypothesis. There’s no enough evidence to support that the 7-day retention rate for the gate at level 40 is greater than that for the gate at level 30.  

## Analisis and Decision   

The results for both bootstrapping method and hypothesis test are showing that there is no strong evidence to prove that the retention rate is higher when we move the gate from level 30 to level 40.   
Therefore, our decision is If we want to keep retention high (both 1-day and 7-day retention), we should **not** move the gate from level 30 to level 40.    
 

## Appendix  

Check the code [here](https://github.com/ct627/AB_testing_game/blob/main/code.ipynb)


## Reference

This mobile game data for this analysis was sourced from [DataCamp Projects](https://projects.datacamp.com/projects).   


