# DQN_on_Breakout-v0
---
## Overview

In this project we try to learn the control policies from high dimensional sensory input space (image3D) using reinforcement learning. It combines the state-of-the-art Convolutional Neural Network (can use any SOTA CNN ResNet/DenseNet/Inception etc.) with Q learning with raw pixels as inputs and estimated future states/actions as outputs. This method is validated on the Atari environment in OpenAI Gym with PyTorch as the deep learning framework. Also, it was a groundbreaking work by Deep Mind in the field of RL because it outperformed human experts and gave us new insights on how AI agents can discover novel ways of playing these games. For detailed report checkout [this link](https://github.com/savnani5/DQN_on_Breakout-v0/blob/main/Report.pdf).

---
## Methodology

● Deep Reinforcement Learning: The goal here is to combine the reinforcement learning algorithm with a deep neural network that operates directly on RGB images and processes the training data 
by using some optimization technique like Adam or SGD/SGD with momentum. Here, this paper  uses a technique called experience replay where the agent’s experience is stored at each time step
𝑒𝑡 = (𝑠𝑡, 𝑎𝑡, 𝑟𝑡, 𝑠𝑡+1) in a dataset 𝒟 = 𝑒1, … , 𝑒𝑁, pooled over many episodes into a replay memory. And we are applying the Q-learning updates to the sampled experience. 

![algorithm](git_gifs/algo.PNG)

● Using experience replay has several advantages over online learning, so primarily each step of experience is potentially used in many weight updates, and it allows for good data efficiency, also 
learning directly from the consecutive examples is not efficient due to high correlation with temporally preceding data. This also prevents the algorithm to diverge and smoothens out the 
learning process.

● As a data preprocessing step this algorithm tries to reduce the input dimensionality. The raw frames are preprocessed by first converting the RGB to grayscale and down-sampling it. The final input representation is a cropped
84*84 region of the image that captures the playing area. Also, the input is produced by stacking 4 frames from history and feeding them to the Q-function. 

● For this problem we use a Convolutional neural network with an input dimension of 84*84*4 image. The first hidden layer convolves 16 8*8 filters with stride 4 with the input image and applies a Relu non-linearity. The second hidden layer convolves 32 4*4 filters with stride 2 and followed by a Relu 
non-linearity. The final hidden layer is fully connected and consists of 256 rectifier units. The output layer is a fully connected linear layer with a single output for each valid action. The number of valid actions is 4 for breakout-v1.

![architecture](git_gifs/cnn.PNG)

---
## Simulation
Please refer to [this link](https://drive.google.com/drive/folders/1Dal_qOqrQoGFAZdeixM6TL_GMnfB24o4) for the simulation videos
###      Before Training ----------------------------------- After Training      
<img src="git_gifs/before.gif" width="350" height="450">    <img src="git_gifs/after.gif" width="350" height="450">


---
## Results

We use a learning rate of 0.0001 with epsilon decaying from 1 to 0.1 in 14 million steps. We also use a batch size of 32 with replay buffer size as 50,000. Also, we are able to get an 
average reward of 45 at around 9M steps. Following plots show the evolution of the agent  during the 14M steps, we also save the checkpoints between training to recover best weights if the average reward starts to go down due to overfitting. Please refer to this [link] for the 
video simulation.

![dataset2](git_gifs/res1.PNG)
![dataset2](git_gifs/res2.PNG)

---
## Referenes

[1] [Open AI gym Environment Documentation](https://gym.openai.com/docs/)

[2] [PyTorch API Tutorials](https://pytorch.org/tutorials/index.html)

[3] [ImageNet Classification with Deep Convolutional Neural Networks – Alex Krizhevsky]()

[4] [Reinforcement Learning: An Introduction – Richard S. Sutton and Andrew G. Barto](http://incompleteideas.net/book/bookdraft2017nov5.pdf)

[5] [An Introduction to Markov Decision Processes – Bob Givan and Ron Parr](https://www.cs.rice.edu/~vardi/dag01/givan1.pdf)

[6] [Deep Reinforcement Learning – David Silver – Google Deepmind](https://icml.cc/2016/tutorials/deep_rl_tutorial.pdf)

[7] [Residual algorithms: Reinforcement learning with function approximation](http://www.cs.utsa.edu/~bylander/cs6243/baird95residual.pdf)

[8] [A neuro-evolution approach to general Atari game playing](https://www.cs.utexas.edu/~mhauskn/papers/atari.pdf)

[9] [Actor-critic reinforcement learning with energy-based policies](https://proceedings.mlr.press/v24/heess12a/heess12a.pdf)

[10] [Deep Reinforcement Learning in Action – GitHub Repository](https://github.com/DeepReinforcementLearning/DeepReinforcementLearningInAction)

[11] [Bayesian Learning of recursively factored environments – Marc Bellamare, Joel Venes](https://proceedings.mlr.press/v28/bellemare13.html)

[12] [Machine Learning for Aerial Image Labeling - Volodymyr Mnih’s thesis](https://www.cs.toronto.edu/~vmnih/docs/Mnih_Volodymyr_PhD_Thesis.pdf)
