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
 - The perceptron learning procedure cannot be generalized to hidden layers as multi-layer neural networks do not use the perceptron learning procedure
 - A new way can show that a learning procedure makes progress: instead of showing the weights get closer to a good set of weights, show that the actual output values get closer to the target values
 - Example: Linear neurons with squared error measure
	 - $y = \sum_i w_i x_i$
	 - Randomly initialize $w_i$'s
	 - Residual error $E = \frac{1}{2}\sum_{n \in \text{training}} (t^n-y^n)^2$
	 - batch update delta rule: $\frac{\partial E}{\partial w_i} = -\sum_n x_i^n (t^n-y^n) \to \Delta{w_i} = -\epsilon \frac{\partial E}{\partial w_i} = \sum_n \epsilon x_i^n (t^n-y^n)$ where $\epsilon$ is the learning rate
	 - How quickly do the weights converge to their correct values? It can be very slow if two input dimensions are highly correlated. if you almost always have the same value of two features, it is hard to decide how to divide them.

# Lecture 3.2 The error surface for a linear neuron
- error surface: horizontal axis for each weight and one vertical axis for the error
	- example: for a linear neuron with a squared error, the error surface is a quadratic bowl. Vertical cross-sections are parabolas and horizontal cross-sections are ellipses

- adaptive delta rule is a derivative of error function with respect to the weights

- batch learning: if we change the weights in proportion to the batch error derivative, it's equivalent to doing steepest descent on the error surface
	- if we look at the surface error from above, we get elliptical contour lines and the delta rule is going to take us at right angles to those elliptical contour lines [insert]
- online learning: after each training case, we zig-zag update the weights in proportion to the gradient of that single case. The changes in the weights moves us perpendicular  towards one of the constraint planes. [insert]

- why learning can be slow [insert]
	- if the ellipse is very elongated, which happens if the lines that correspond to two training cases are almost parallel, the gradient vector has a large component along the short axis of the ellipse and a small component along the long axis of the ellipse

# Lecture 3.3 Learning the weights of a logistic output neuron
logistic neurons
: $z = b+\sum_i x_iw_i$
: $y = \frac{1}{1+e^{-z}}$
: $\frac{\partial y}{\partial w_i} = \frac{\partial z}{\partial w_i}\frac{dy}{dz} = x_iy(1-y)$
: $\frac{\partial E}{\partial w_i} = \sum_n \frac{\partial y^n}{\partial w_i}\frac{\partial E}{\partial y^n} = -\sum_n x_i^n y^n (1-y^n)(t^n-y^n)$[insert]

# Lecture 3.4 The backpropagation algorithm
Want to automate the loop of designing features for a particular task and seeing how well they work
- (an inefficient way) to learn by perturbing weights: randomly perturb one weight and see if it improves performance. If so, save the change
- (another inefficient way) to perturb all weights in parallel and correlate the performance gain with the weight changes
- (a better way) to randomly perturb the activities of the hidden units so that once we know how we want a hidden activity to change on a given training case, we can compute how to change the weights
- (the best way) to backpropagate: we use error derivatives w.r.t. hidden activities 
	- first, convert eh discrepancy between each output and its target value into an error derivative
	- then compute error derivatives in each hidden layer from error derivatives in the layer above
	- Backpropagating $\frac{dE}{dy}$
		- $y_j$ is the output of unit j, $z_j$ is the total input received by unit j
		- $\frac{\partial E}{\partial w_{ij}} = \frac{\partial E}{\partial z_j}\frac{\partial z_j}{\partial w_{ij}} = \frac{\partial E}{\partial z_j}y_i = \frac{\partial E}{\partial y_j}\frac{\partial y_j}{\partial z_j}y_i = \frac{\partial E}{\partial y_j}y_j(1-y_j)y_i$
		- $\frac{\partial E}{\partial y_i} = \sum_j \frac{\partial E}{\partial z_j}\frac{dz_j}{dy_i}=\sum_j \frac{\partial E}{\partial z_j}w_{ij} = \sum_j \frac{\partial E}{\partial y_j}\frac{\partial y_j}{\partial z_j}w_{ij} = \sum_j \frac{\partial E}{\partial y_j}y_j(1-y_j)w_{ij}$

# Lecture 3.5 How to use the derivatives computed by the backpropagation algorithm
- Optimization issues: How do we use the error derivatives on individual cases to discover a good set of weights?
	- How often to update the weights?
		- online: after each training case
		- full batch: after a full sweep through the training data
		- mini-batch: after a small sample of training cases
	- How much to update?
		- use a fixed learning rate?
		- adapt the global learning rate? decrease the learning rate if we oscillate around and increase the learning rate if we make steady progress
		- don't use steepest descent?
- Generalization issues: How do we ensure that the learned weights work well for cases we did not see during training? 
	- problem of overfitting
		- sampling error 
		- if the model is very flexible, it can model the sampling error really well -> overfit
		- ways to reduce overfitting
			- weight-decay (set a lot of weights 0)
			- weight-sharing (many weights have the same values)
			- early-stopping (stop once the performance gets worse on the fake test set)
			- weight averaging (train many different neural networks )
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjU2NDg1NDEzLC01OTEwNTg4NzcsNDQwMD
M0NTcsLTY5NTUwNTU1LDExNzU3OTA4NjQsLTE3MzE0NjQ5MzIs
MTI0ODgxMzYxNCwtMTA1MTMyMzk3NCwxMTE2ODAwMDk2LC0xNT
YzNTE1MDAsMjY2MDU2OTAsLTEyNTIyNTI2OTgsOTA3ODA1NTkz
LDIxNDQ1ODUxNzUsMzE4MzcxODk1LDE3NzE4MTU5NCwtMTI0ND
EwODEyOSwyMjU3MDIyNjQsNTI2NzcyNDY5LDE5MzExNjkxODVd
fQ==
-->