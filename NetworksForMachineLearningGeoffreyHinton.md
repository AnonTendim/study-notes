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
A neural network with two layers of neurons

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzOTE3NjE1OSwtMTc3MDAzMzUyLDE5Mj
UwNzY2MDcsLTIwODg3NDY2MTIsLTE3NDM0NjQ0NjldfQ==
-->