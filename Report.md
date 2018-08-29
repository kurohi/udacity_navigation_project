# Report for the navigation project

## Description
This project consists in implementing an agent to play a game in where it need to catch yellow bananas while avoiding blue bananas.
The game was provided as a training environment by Unity. The version used by this project uses something attune to an array of lasers coming out from where the agent is facing saying the distance and existence of bananas in front of it.

### State and reward description
As stated above, the agent see the world through an array of lasers that identify and measure the distance of bananas in front of it.
Besides the "radar" the velocity of the agent is also in the array. All information together provide a state description with 37 values.
The reward is given when a banana is catch. For blue bananas the agent is penalized with a reward of -1.0, while for yellow bananas the agent is rewarded with +1.0.

### Actions
Four actions are available to the agent: 
- Walk forward
- Walk backward
- Turn left
- Turn right

## DQN agent
Here I would like to share some aspects of the implementation of the DQN agent.

### dqn_agent.py
This code is was copied from the udacity dqn task. A few changes were made to the code so that it can make use of the free layer definition of the model.
This gives it the ability to add layers without changing the code of the model or dqn_agent. 
A buffer with the states, actions and rewards is kept for later training.
When training only one of the networks are updated, also the buffered elements are selected at random.
After a predefined number of steps, the updated network is copied into the static one.

### model.py
This file implements a general sequential deep learning model in pytorch. 
It was implemented so that an arbitrary number of layers can be defined at the construction.
It also has convolutional layers implemented, but is still not working well enough so only the fully connected layers were used.

## Training results
The model was trained with 3000 episodes. The hyperparameters used were as follows:
- Number of fully connected layers: 4
- Number of neurons on each layer: 256, 128, 64, 32
- Epsilon-greedy start value: 1.0
- Epsilon-greedy decay: 0.995
- Epsilon-greedy minimal value: 0.01
- Gamma discount: 0.99
- Soft update tau value: 1e-3
- How often the network was updated: every 4 steps

Here is a graph of the rewards per trained episode:
![Average rewards][graphic.jpg]

By the end of the 3000 episodes of training, an average reward of 15.61 was achieved, which is higher than the 13.0 required.

## Future improvements
For the future I want to finish debugging the convolutional layers of the model.py in order to be able to do the same challenge but using the pixel information only.
Would be also nice to upgrade the dqn model into the rainbow algorithm which include 3 new improvements that have been demonstrated to improve accuracy and training stability to the agent.
These improvements are: Double DQN, Prioritized Experience Replay, and Dueling DQN.
