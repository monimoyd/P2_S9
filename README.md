# P2_S9
Phase2 Assignment 9 - T3D algorithm

# T3D Algorithm

I will explain step by step of T3D algorithm. 

## Step0: Initialization

I this step all the modules are initialized

## Step1: Populate Experience Replay

Experience replay is a buffer for storing transitions. In this step a set of transitions of tuple (State, Action, Reward, Next action) are created and populated. 

Experience Raply has two method:
i. add: This method is used for adding transition to the Replay Buffer 
![ReplayBuffer Add](/ReplayBuffer.add.png)
ii. Sample : This method is used randomly selecting as a list of transition of batch size
![ReplayBuffer sample](/ReplayBuffer.sample.png)

