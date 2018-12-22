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
![feed-forward neural networks](https://lh3.googleusercontent.com/QIY0sh8Y_Ijok0JXDGmfll1zTf9_JU6a7Y4eQoCI_al4hPRAv7bSyOgKj5BbBoB3DhtwclI5OcHw)
	- if there is more than one hidden layer, it is a deep neural networks
- Recurrent netowrks
![recurrent networks](https://lh3.googleusercontent.com/uNrVxJ28ZXkw3ehN3YN2xvXOcHPo-OJ-SRefLHf0mOADViBeq9lZgBpiTDjyiK6xrVXQtstME5cS "recurrent networks")
	- directed cycles in the graph
	- can sometimes get back to where you started by following the arrows
	- a very natural way to model sequential data: equivalent to very deep nets with one hidden layer per time slice except the same weights at every time slice are used and they get input at every time slice![enter image description here](https://lh3.googleusercontent.com/g5X8WTlRRc8j6QuXcJvn0vq_ot9Av7JxO_dQLBmuogYiGoDnKEen5UOx1CR3rPWtFwUaeox1qTu1)
	- has the ability to remember information in their hidden state for a long time
- symmetrically connected networks
	- like recurrent networks, but the connections between units are symmetrical (have the same weight in both directions)

# Lecture 2.2 Perceptrons: The first generation of neural networks

## The standard paradigm for statistical pattern recognition
1. Convert the raw input vector into a vector of feature activations
2. Learn how to weight each of the feature activations to get a single scalar quantity
3. if this quantity is above some threshold, decide that the input vector is a positive example of the target class

## The standard Perceptron architecture
#insert

## How to learn biases b?
#insert
- We can just learn them like normal weights. We treat them as weights on the first feature that always has a value of 1.
- Bias is like negative threshold, so we can ignore threshold.

## The Perceptron convergence procedure: Training binary output neurons as classifiers
- If the output unit is correct, leave its weights alone.
- If the output unit incorrectly outputs a zero, add the input vector to the weight vector 
- If the output unit incorrectly outputs a 1, subtract the input vector from the weight vector
- This is guaranteed to find a set of weights that gets the right answer for all the training cases if any such weight set exists
- But the difficulty is deciding which features to use as the bad choices of features makes it impossible to have a weight set.

# Lecture 2.3 A geometrical view of perceptrons
## weight-space
[insert]
- has one dimension per weight
- A point in the space represents a particular setting of all the weights (points <-> weight vectors)
- each training case is a hyperplane that passes through the origin in white space (training case <-> hyperplane )
- Average of two good weight vectors is a good weight vector as the problem is convex

# Lecture 2.4 Why the learning works
## Informal sketch of proof of convergence
- margin is $\delta$
- $w\cdot v\geq \delta \cdot M$
- $||w||^2 \leq M$
- $w \cdot v \leq ||w||$
- $M \leq \frac{1}{\delta^ 2}$

# Lecture 2.5 What perceptrons can't do
## The limitations of Perceptrons
- A binary threshold output unit cannot tell if two single bit features are the same (c(1,1)=1, c(0,0)=1, c(1,0)=0, c(0,1)=0) as this leads to contradictions in the inequalities
- A binary decision unit cannot discriminate patterns with the same number of on pixels assuming translation with wraparound
	- Proof: Let Pattern A have label 1. Each pixel (weight) can be activated as one of the 4 on-pixels (value 1). So total value received by the decision unit over all possibilities will be four times the sum of all weights. Let Pattern B have label 0. Again, each pixel (weight) can be activated by one of the 4 on-pixels (value 1). So total value received by the decision unit over all possibilities will be four times the sum of all weights, same as the Pattern A case. But to discriminate correctly, every single case of pattern must provide more value to the decision unit than every single case of pattern B. Contradiction.
	- The whole point of pattern recognition is to recognize patterns that goes under transformations like translation but Minsky and Papert's "Group Invariance Theorem" says that Perceptron cannot learn if the transformations from a group.
	- To deal with such transformations, a Perceptron needs to use multiple feature units to recognize transformations of informative sub-patterns
- Neural networks are only going to be really powerful if we can learn the feature detectors. It's not enough to just learn weights of feature detectors, we have to learn feature detectors themselves ( hidden units, multiple layers of adaptive, non-linear hidden units).

# Lecture 3.1 Learning the weights of a linear neuron
 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMxNTQ4MDMzNCwtMTI1MjI1MjY5OCw5MD
c4MDU1OTMsMjE0NDU4NTE3NSwzMTgzNzE4OTUsMTc3MTgxNTk0
LC0xMjQ0MTA4MTI5LDIyNTcwMjI2NCw1MjY3NzI0NjksMTkzMT
E2OTE4NSw3OTQ2NDc0MjEsMTYzMjQ0NDIwMCwtOTI5MjM4Mzg2
LDIwNzQxMzAzMjUsMTQyNjkxODA5NSwtOTI3NDY4NzYxLC04MT
M5NTk1NzMsLTE5MDI0OTc2MTYsMTkxMDQyNzM3NywtMTc3MDAz
MzUyXX0=
-->