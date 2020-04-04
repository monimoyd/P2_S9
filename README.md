# P2_S9
Phase2 Assignment 9 - T3D algorithm

# T3D Algorithm

T3D (Twin Delayed Deep Deterministic Policy Gradient Algorithm)  is an Deep Reinforcment Learning algorithm which concurrently learns a Q-function and a policy. It uses Actor Critic approach where Actor function specifies action given the
current state of the environments. Critic value function specifies a signal (TD
Error) to criticize the actions made by the actor.

T3D uses experience replay where experience tuples (S,A,R,S`) are added to
replay buffer and are randomly sampled from the replay buffer so that samples
are not correlated.

T3D also uses separate target neural network for both Actor and Critic. As
target values are determined for both the critic and actor networks, copy of both
of these networks and soft update their weights are periodically updated to the
respective target networks.

There are six neural networks used in T3D
i. Local network for Actor
ii. Target network for Actor
iii. Two network for Critic
iv. Two Target network for Critic

Also, this algorithm uses time delay for updating Actor after a certain number of iterations. Also, Target Actor and Critic networks are updated periodically after certain number of iterations using Polyak averaging.

There are two objectives of the algorithm:
i. Minimize the Critic loss which is sum of mean squared error between Q value of target Critic and the the two Critics. Here Gradient descend is used
ii. Maximize the performance of Actor. Here Gradient ascent is used

I will draw an analogy with an real world exmaple. 

Let us say an child is trying to learn walking by and his parents are helping him to learn by giving feedback like clapping every time he is successfully standup.

![Kid Learning walk](/kid_learning_walking_from_parents.jfif)

Here 

Actor is the child who is instantly learning actions based on various states. Actor target is the permanent learning of policy by the child

Two Critics are Parents i.e. Father and Mother who are evaluating the performances of Child and giving him Thumbs up or (or say chocolates) if the child succeeds or give him solace if he fails.

Critic targets are the permanent learnings by parent.

Actor (child) gets positive rewards from environment (like chocolates or thumbs up from parent) and negative reward when he fell down and gets pain

![Kid learning ](/thumbs_up.jfif)

Experience replay contain various experiences of Child like Successfully standup, Fell down etc

![Kid learning standup](/standup_successful.jfif)
![Kid learning fell down](/fell_down.jfif)


Objective is :
i. Parents (i.e. Critics) should make less mistakes i.e. minimize critic loss
ii. Child should try to get better performance i.e. more number of successes in walking




Step by step of T3D algorithm. 

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

Actor model is a neural network which takes input as state and outputs the action. This is updated using backpropagation.
Target Actor model is neural network which is similar to Actor model but it is updated less frequently and mainly used for stability. 
Target Actor Model is updated using Polyak averaging from the Actor model

Worflow for Actor forward is as below:
![Actor Model](/Actor.forward.png)

## Step3: Define Critic Model

The role of Critic is predict Q value based on state and action. It is based on value function.

There are two critic neural networks and two critic target neural networks which are updated slower than the critic models

![Critic Model](/Critic.forward.png)

Method Q1 of Critic takes state and action as input and updates the Q value

The flowchart for Q1 is as below:
![Critic Q1](/Critic.Q1.png)

## Step4 -Step 15

T3D is the main class which performs T3D algorithm 

init method is used for initializing actor, target actor, critic1, critic2, critic1 target, critic2 taret.
Flowchart for Init method of T3D is as below:
![T3D class](/T3D.init.png)

train method of T3D class is used for trainig T3D algorithm. This is the main method for training
Flowchart for train method of T3D is as below:
![T3D train](/T3D.Train.png)

## Step4: Sample from Replay Buffer

In this step a list of transtions of lenght batch size are randomly selected from experience replay and are converted to tensor

## Step5: 
Using the actor target network, given a  next state s', next action a' is determined


## Step6: 
Adding adaptive noise to the parameters of reinforcement learning algorithms in general boosts performance.
In this steo Gaussian noise is added to next action a' and clamp betwen negative and positive value of maxmium action values.

## Step7: 
In this step, two critic networks take the next state and next action as input and return Q balues for target1 and target2

## Step8: Take conservative estimate of target Qs
In this step the minimum of target Q1 and target Q2 is deterimined and kept as target Q value. Minimum of two target Q values ensure that conservative estimate is taken by Critic

## Step10: Determine Final Q value
In this step the final target Q value is determined after the epsidode is over where equation similar to Bellman equation is used fopr updating Final Q value

Final Q value  = Reward + Discount factor * target Q value

## Step11: 
In  this step, state and action are input to the critic model and which will give current Q1 and current Q2 values

## Step12: Determine Critic Loss

In this step Critic Loss is calculated by taking Mean Square Error (MSE) between current Q and target Q for both the critic network and summing them together. i.e.

Critic Loss = Mean Square Error( Current Q1, target Q) + Mean Square Error(Current Q2, target Q)


## Step13: Perform Gradient Ascent on Actor

Once every two iterations do the following:
- Detemine actor loss by taking negative value of output of first critic model and passing state and action as input. 
- Initialize gradient to zero
- Perform gradient ascent on Actor model
- Update the weights of Actor Model

# Step14: Update weights of target Critic using Polyak averaging

Once every two iterations, weights in  Critic Target model is updated using Polyak Averaging using the formular

New Weight of Critic Target Model = tau * Weight of Actor Model + (1-tau) * Current Weight of Critic Target Model

Where tau is a hyperparameter between value 0 and 1 which detemines how much weightage needs to be given to weights of current Critic 
Model

# Step15: Update weights of target Actor using Polyak averaging

Once every two iterations, weights in  Actor Target model is updated using Polyak Averaging using the formula

New Weight of Actor Target Model = tau * Weight of Actor Model + (1-tau) * Current Weight of Critic Target Model

Where tau is a hyperparameter between value 0 and 1 which detemines how much weightage needs to be given to weights of current Actor 
Model



















