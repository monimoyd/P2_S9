# P2_S9
Phase2 Assignment 9 - T3D algorithm

# T3D Algorithm

I will explain step by step of T3D algorithm. 

## Step0: Initialization

I this step all the modules are initialized

## Step1: Populate Experience Replay

Experience replay is a buffer for storing transitions. In this step a set of transitions of tuple (State, Action, Reward, Next action) are created and populated. 

Experience Raply has two method:
i. Add 
Flowchart for add is as:

![ReplayBuffer Add](/ReplayBuffer.add.png)

ii. Sample

