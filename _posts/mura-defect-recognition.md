
### This document provides related derivations for the sparse auto-encoder network model with an *KL* divergence constraint. Stochastic gradient descent algorithm is used for training this model.
---

### A three layer auto-encodernet work  is used as an example.

![](http://i65.tinypic.com/vrft6f.jpg)

### Loss function :

<img src="http://www.forkosh.com/mathtex.cgi? \large L = \min\limits_{W,W',b,b'} \frac{1}{m} \sum\limits_{i=1}^{m}\|y_I^{(i)}-x_I^{(i)}\|^{2} + \lambda \sum\limits_{w\in{W,W'}}\|w\|_F^2
+ \beta\sum\limits_{i=1}^{N_H}KL(\rho\|\hat{\rho}_i),">


### where (W,b) and (W',b') refer to coefficients in the encoding and decoding phases, <img src="http://www.forkosh.com/mathtex.cgi? \large N_H"> refers to the number of units in hidden layer. The *KL* divergence can be expanded as 

<img src="http://www.forkosh.com/mathtex.cgi? \large KL(\rho\|\hat{\rho}_i) = \rho log\frac{\rho}{\hat{\rho}_i}+(1-\rho)log\frac{1-\rho}{1-\hat{\rho}_i},">

### where <img src="http://www.forkosh.com/mathtex.cgi? \large \hat{\rho}_i"> denotes the average activation of the *i*-th hidden unit (averaged over the training set). Assume <img src="http://www.forkosh.com/mathtex.cgi? \large h_i(X^{(j)})"> is activation of the *i*-th hidden unit with the *j*-th sample, thus <img src="http://www.forkosh.com/mathtex.cgi? \large \hat{\rho}_i"> can be expressed as

<img src="http://www.forkosh.com/mathtex.cgi? \large \hat{\rho}_i=\frac{1}{m}\sum_{j=1}^m{h_i\left( X^{\left( j \right)} \right)}.">

### Assume <img src="http://www.forkosh.com/mathtex.cgi? \large f(\cdot)"> refers to the avtive function (We used *sigmoid* in the manuscript), we will provide the derivatives of ∂L/∂W', ∂L/∂b', ∂L/∂W and ∂L/∂b below.

### Note that the coefficients W' and b' have nothing to do with the term <img src="http://www.forkosh.com/mathtex.cgi? \large KL(\rho\|\hat{\rho}_i)}">, thus, for coefficients in the last layer, the derivatives  can be written as

<img src="http://www.forkosh.com/mathtex.cgi? \large \frac{\partial L}{\partial W'_{i,j}}=\frac{1}{m}\sum_{k=1}^m{2\cdot \left( y_{Ii}^{\left( k \right)}-x_{Ii}^{\left( k \right)} \right) \cdot f'\left( \sum_{j=1}^{N_H}{h_j\cdot W'_{i,j} + b'_i} \right) \cdot h_{j}+2\cdot W'_{i,j}}">

<img src="http://www.forkosh.com/mathtex.cgi? \large \frac{\partial L}{\partial b'_{i}}=\frac{1}{m}\sum_{k=1}^m{2\cdot \left( y_{Ii}^{\left( k \right)}-x_{Ii}^{\left( k \right)} \right) \cdot f'\left( \sum_{j=1}^{N_H}{h_j\cdot W'_{i,j} + b'_i} \right)}">

### Assume <img src="http://www.forkosh.com/mathtex.cgi? \large \delta_j^{(l)}"> refers to residual of the *j*-th neuron in layer *l*, thus

<img src="http://www.forkosh.com/mathtex.cgi? \large \delta_j^{(3)}={2\cdot \left( y_{Ii}^{\left( k \right)}-x_{Ii}^{\left( k \right)} \right) \cdot f'\left( \sum_{j=1}^{N_H}{h_j\cdot W'_{i,j} + b'_i} \right)},">

<img src="http://www.forkosh.com/mathtex.cgi? \large \delta _{i}^{\left( 2 \right)}=\left( \sum_{j=1}^{N_I}{W_{i,j}^{'}\cdot \delta _{j}^{\left( 3 \right)}} \right)  \cdot f'\left( \sum_{j=1}^{N_I}{x_{Ij}^{(k)}\cdot W_{i,j} + b_i} \right)}.">

### The partial derivatives of W,b can be expressed as

<img src="http://www.forkosh.com/mathtex.cgi? \large \frac{\partial L}{\partial W_{i,j}}= \frac{1}{m}\sum_{k=1}^m{x_{Ij}^{(k)} \cdot \left( \delta _{i}^{\left( 2 \right)} + \beta \left( -\frac{\rho}{\hat{\rho}_i}+\frac{1-\rho}{1-\hat{\rho}_i}\right)\right)} + 2\cdot W_{i,j},">

<img src="http://www.forkosh.com/mathtex.cgi? \large \frac{\partial L}{\partial b_i}= \frac{1}{m}\sum_{k=1}^m{\delta _{i}^{\left( 2 \right)} + \beta \left( -\frac{\rho}{\hat{\rho}_i}+\frac{1-\rho}{1-\hat{\rho}_i}\right)}.">

