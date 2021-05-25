# A/B testing Project in Python 

## Backgrand

**Cookie Cats** is a mobile puzzle game developed by Tactile Entertainment.   
It's a classic "connect three"- a style puzzle game where the player must connect tiles of the same color to clear the board and win the level.   
As players progress through the levels of the game, they will occasionally encounter gates that force them to wait a non-trivial amount of time or make an in-app purchase to progress.   
In addition to driving in-app purchases, these gates serve the important purpose of giving players an enforced break from playing the game, hopefully resulting in that the player's enjoyment of the game being increased and prolonged.  

## Goal & Design problem      

#### Improve retention rate and conversion rate (in-purchase rate).  

Initially, the first gate was placed at level 30, and we're going to analyze an A/B test to figure out that should we moved the first gate in Cookie Cats from level 30 to level 40? Can we improve the retention rate and conversion rate by shift the gate?          

#### Should we move the gate from level 30 to level 40 in the game?      

Let the retention rate for gate_30 be P_30 and gate_40 be P_40    
The hypothesis will be:   
**H0:P_30=P_40**
**HA:P_30>P_40**

## Data Preparation

#### Assumptions   

- **User has been assigned to level 30 or 40 is random**: When a player installed the game, he or she was randomly assigned to either gate_30 or gate_40.     
- **Each experiment unit are independent**: Each user is independent and not the same person.    
- **The factor to test is the only reason for the difference**: The only difference between the two groups of users is the gate.

#### Data Description   

The data we have is from 90,189 players that installed the game while the AB-test was running.   
When a player installed the game, he or she was randomly assigned to either **gate_30** or **gate_40**.   

The variables are:   
- **userid**: a unique number that identifies each player.
- **version**: whether the player was put in the control group (gate_30 - a gate at level 30) or the group with the moved gate (gate_40 - a gate at level 40).
- **sum_gamerounds**: the number of game rounds played by the player during the first 14 days after install.
- **retention_1**: did the player come back and play 1 day after installing?
- **retention_7**: did the player come back and play 7 days after installing?

#### Data Summary


## 


## Reference

This mobile game data for this analysis was sourced from [DataCamp Projects](https://projects.datacamp.com/projects).   


