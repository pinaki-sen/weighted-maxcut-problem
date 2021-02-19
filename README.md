# QOSF Mentorship Selection Task
# weighted-maxcut-problem


## Theoretical Discussion
The main moto of this problem is to seperate the whole set of nodes in two subsets $A$ and $B$ such that the sum of weights of edges that have different types of nodes at their ends become the maximum possible value.

In other words, we have to find a partition through the whole graph, such that sum of weights of edges that the partition passes becomes the maximum among all possible cuts.

We can convert this to a simple mathematical expression.

![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/eqn_1.png?raw=true)

Here $C(z)$ represents the score of a specific partition through the graph. $\alpha$ iterates from 1 to m where m is the number of edges present. for each edge, $C_{\alpha}(z)$ represents the score associated with each edge. $C_{\alpha}(z)$ is equal to the weight of the edge if the partition passes through that edge and equal to $0$, if not.

## Representing in terms of Quantum Circuit
As we have already defined a score value for a cut, we have to define that in terms of unitary ooperators that can be implemented on the quantum circuit.

While representing the partition using computational basis states, we can represent the terms in $C(z)$ as operators acting on the states.

![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/eqn_2.png?raw=true)

Here the $\alpha$th edge is the edge connecting $j$th and $k$th nodes. For each node $C_{\alpha}$ will be equal to the weight of the edge if the partition goes between $j$th and $k$th nodes and equal to $0$ if doesn't pass because the operator $(1-\sigma_z^j \sigma_z^k)$ has eigenvalue $1$, iff $j$th and $k$th qubit have different z-axis measurement values.

Initially the circuit is converted to equal superposition state by applying Hadamard gate in each individual qubit, also known as $|+_{n}&gt;$ state.

The circuit consists of $L$ layers of $U_B$ and $U_C$ gates. In each layer, one $U_B$ and one $U_C$ is associated with one $\beta$ and $\gamma$ parameter. Therefore each layers having 2 params $\beta$ and $\gamma$, the whole $L$ layered circuit is consist of $2L$ parameters.

Now coming to each of the layers, $U_B$ is single qubit operator, implemented on each of the individual qubits and it is basically a $R_X$ gate with parameter $2\beta$. $U_C$ whereas acts on two qubits. It is implemented on those two nodes who are connected by an edge in the graph. $U_C$ consists of a $R_Z$ gate with parameter $(-w\gamma)$ sandwitched between two CNOT gates.

## Detailed discussion and respective code, you can access [here](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/weighted_maxcut.ipynb)

## Test Case - 1
### Unpartitioned Graph 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case1_unsolved.png?raw=true)

### Partitioned Grpah, solved using QAOA 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case1_solved.png?raw=true)

### Historgram for output of circuit with various number of layers
Here the MAXCUT solution is quite simple and sum of weiights of cut edges is $(10+10)=20$. Here as we can see from single layer circuit upto 5 layers, the probablity amplitude of states other than the targetted was decreasing. But unexpectedly at six layered circuit, those states got amplified a little bit.
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/histogram_1.png?raw=true)


# Test Case - 2
### Unpartitioned Graph 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case2_unsolved.png?raw=true)

### Partitioned Grpah, solved using QAOA 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case2_solved.png?raw=true)

### Historgram for output of circuit with various number of layers
The partition passes through all four edges present in the graph. Sum of weights herre is $4$ which is the maximum possible value. Here its clear that two layered circuit is enough to get the solution as the graph is simple, still we tried upto six only for the sake of experimental results.
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/histogram_2.png?raw=true)


# Test Case - 3
### Unpartitioned Graph 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case3_unsolved.png?raw=true)

### Partitioned Grpah, solved using QAOA 
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/case3_solved.png?raw=true)

### Historgram for output of circuit with various number of layers
In this test case, the solution partition passes through $4$ out of $6$ edges, summing the weights to $(5+7+4+3) = 19$. Also its clear that with increasing no. of layers, probablity amplitudes of states other than the targetted one is reducing drastically.

For complex graphs like this test case 3, circuits with lesser number of layers doesn't have 100% accuracy, its possible that sometimes they give incorrect result, as seen from previous experimental results.
![alt text](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/images/histogram_3.png?raw=true)

# For more detailed discussion, Look into this [Notebook](https://github.com/senpinaki222/weighted-maxcut-problem/blob/main/weighted_maxcut.ipynb)
