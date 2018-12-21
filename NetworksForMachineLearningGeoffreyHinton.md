# Lecture 1.2 What are neural networks?
From brain to computer science

# Lecture 1.3 Some simple models of neurons
- Linear neurons	
	- $y = b + \sum_{i=1} x_iw_i$
	- y: output
	- b: bias
- Binary threshold neurons (McCulloch-Pitts 1943)
	- $y = \textbf{1}[b+\sum_{i=1}x_iw_i\geq 0]$
	- 1 above 0, 0 below 0
- Rectified Linear Neurons (linear threshold neurons)
	- $y=\begin{cases}b+\sum_{i} x_iw_i & b+\sum_{i} x_iw_i\geq 0\\ 0 & \text{otherwise}\end{cases}$
	- linear above 0, 0 below 0
- Sigmoid neurons
	- $z = b+\sum_{i} x_iw_i$
	- $y = \frac{1}{1+e^{-z}}$
- Stochastic binary neurons
	- treat the output of the logistic as the probability of a decision
	- $z = b+\sum_{i} x_iw_i$
	- $\Pr(s=1) = \frac{1}{1+e^{-z}}$

# Lecture 1.4 A simple example of learning
A neural network with two layers of neurons and a single winner in the top layer is equivalent to having a rigid template for each shape.

# Lecture 1.5 Three types of learning
- supervised learning
	- regression
	- classification
	- start by choosing a model-class
	- minimize discrepancy between the target output and the actual output
		- for regression, $\frac{1}{2}(y-h(x))^2$
		- for classification, several measures
- reinforcement learning
	- the output is an action or sequence of actions and the only supervisory signal is an occasional scalar reward
	- the goal in selecting each action is to maximize the expected sum of the future rewards
	- it is difficult because rewards are delayed and do not supply much information 
- unsupervised learning
	- create an internal representation of the input that is useful for the subsequent supervised or reinforcement learning
	- provide a compact, low--dimensional representation of the input
	- provide an economical high-dimensional representation of the input in terms of learned features
	- find sensible clusters in the input 

# Lecture 2.1 An overview of the main types of neural network architecture

- feed-forward neural networks (commonest type of neural network in practice)
- ![enter image description here](https://lh3.googleusercontent.com/QIY0sh8Y_Ijok0JXDGmfll1zTf9_JU6a7Y4eQoCI_al4hPRAv7bSyOgKj5BbBoB3DhtwclI5OcHw)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3NDEzMDMyNSwxNDI2OTE4MDk1LC05Mj
c0Njg3NjEsLTgxMzk1OTU3MywtMTkwMjQ5NzYxNiwxOTEwNDI3
Mzc3LC0xNzcwMDMzNTIsMTkyNTA3NjYwNywtMjA4ODc0NjYxMi
wtMTc0MzQ2NDQ2OV19
-->