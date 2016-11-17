### This document provides related derivations for the sparse auto-encoder network model with an *KL* divergence constraint. Stochastic gradient descent algorithm is used for training this model.
---

### A three layer auto-encodernet work  is used as an example.

![](http://i65.tinypic.com/vrft6f.jpg)

### Loss function :

![](http://i66.tinypic.com/296d4xd.jpg)

### where (W,b) and (W',b') refer to coefficients in the encoding and decoding phases, ![](http://i64.tinypic.com/fyzlw7.png) refers to the number of units in hidden layer. The *KL* divergence can be expanded as 

![](http://i67.tinypic.com/1zvrbzn.png)

### where ![](http://i63.tinypic.com/mvj4lt.png) denotes the average activation of the *i*-th hidden unit (averaged over the training set). Assume ![](http://i68.tinypic.com/n4fwas.png) is activation of the *i*-th hidden unit with the *j*-th sample, thus ![](http://i63.tinypic.com/mvj4lt.png) can be expressed as

![](http://i68.tinypic.com/s0x7df.png)

### Assume ![](http://i67.tinypic.com/2u5w2lj.png) refers to the avtive function (We used *sigmoid* in the manuscript), we will provide the derivatives of ∂L/∂W', ∂L/∂b', ∂L/∂W and ∂L/∂b below.

### Note that the coefficients W' and b' have nothing to do with the term ![](http://i67.tinypic.com/hs3qmw.png), thus, for coefficients in the last layer, the derivatives  can be written as

![](http://i63.tinypic.com/246mkxz.png) ![](http://i63.tinypic.com/2e58keb.png)

![](http://i67.tinypic.com/2lazpf.png)

### Assume ![](http://i67.tinypic.com/2ibd92v.png) refers to residual of the *j*-th neuron in layer *l*, thus

![](http://i68.tinypic.com/35lrzoz.png)

![](http://i64.tinypic.com/2cpryf8.png)

### The partial derivatives of W,b can be expressed as

![](http://i68.tinypic.com/eznyih.png) ![](http://i64.tinypic.com/2s63uy0.png)

![](http://i68.tinypic.com/9tzndx.png)

