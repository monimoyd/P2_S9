# P2_S9
Phase2 Assignment 9 - T3D algorithm

# T3D Algorithm

I will explain step by step of T3D algorithm. 

## Step0: Initialization

I this step all the modules are initialized

## Step1: Populate Experience Replay

Experience replay is a buffer for storing transitions. In this step a set of transitions of tuple (State, Action, Reward, Next action) are created and populated. 

Experience Replay has two method:
i. add: This method is used for adding transition to the Replay Buffer 
![ReplayBuffer Add](/ReplayBuffer.add.png)
ii. Sample : This method is used randomly selecting as a list of transition of batch size
![ReplayBuffer sample](/ReplayBuffer.sample.png)

## Step2: Define Actor Model

Actor model is a neural network which takes input as state and outputs the action
Target Actor model is neural network which is similar to Actor model but it is updated less frequently and mainly used for stability

Worflow for Actor forward is as below:
![Actor Model](/Actor.forward.png)

## Step3: Define Critic Model

The role of Critic is predict Q value based on state and action. It is based on value function.

There are two critic neural networks and two critic target neural networks which are updated slower than the critic models

![Critic Model](/Critic.forward.png)

## Step4 -Step 15

T3D is the main class which performs T3D algorithm 

![T3D class](/T3D.init.png)









