+++
date = "15 Feb 2018"
draft = false
title = "Class 3: Privacy in Machine Learning"
author = "Team Gibbon"
slug = "class3"
+++

introduction

## Section title

> Authors. _Title_. IEEE Symposium on Security and Privacy ("Oakland") 2017. [[PDF](https://www.cs.cornell.edu/~shmat/shmat_oak17.pdf)]

[Shokri et al.](https://www.cs.cornell.edu/~shmat/shmat_oak17.pdf) attempt to ...

## Distillation as a Defense
> Nicolas Papernot and
               Patrick D. McDaniel and
               Xi Wu and
               Somesh Jha and
               Ananthram Swami. Distillation as a Defense to Adversarial Perturbations against Deep
               Neural Networks.CoRR .2015 [[PDF](https://arxiv.org/abs/1511.04508)]
 ### What is Distillation          

Neural networks typically produce class probabilities by using a “softmax” output layer that converts the logit, zi, computed for each class into a probability, qi, by comparing zi with the other logits.				
$$ q_i=\frac{exp(z_i/T)}{\sum_{j}{exp(z_j/T)}} $$
where T is a temperature that is normally set to 1. Using a higher value for T produces a softer probability distribution over classes. 
In the simplest form of distillation, knowledge is transferred to the distilled model by training it on a transfer set and using a soft target distribution for each case in the transfer set that is produced by using the cumbersome model with a high temperature in its softmax. The same high temperature is used when training the distilled model, but after it has been trained it uses a temperature of 1. It could reduce the computing resources required to run a network, allowing usage on a smaller scale like in embedded chips and IoT devices.

### How does Distillation Work?
1)A Deep Neural Network(DNN) is trained with a high temperature, the T we mentioned before.The training of this first DNN is a high temperature because the high temperature forces the DNN to produce probability vectors with relatively large values for each class. The high temperature of a softmax is, the more ambiguous its probability distribution will be. The smaller the temperature of a softmax is, the more discrete its probability distribution will be. 

2)A second Deep Neural Network is trained by replacing the hard labels of the training set with class probabilities output by the first Deep Neural Network.
![](https://github.com/jindingars/secML.github.io/blob/master/src/content/images/DNN.png )

### Softmax Function under distillation 
Softmax function is the Last layer of network. It’s used to normalize the outputs of the second to last layer. Under distillation situation, it has a parameter temperature (T)
To perform distillation in softmax layer, a large network whose output layer is softmax is first trained on the original dataset. The softmax layer is a layer that considers a vector Z(X) of outputs produced by the last hidden layer of a DNN. Then we normalizes them into a probability vector F(X), the output of DNN assigning a probability to each class of dataset for input X. T means temperature and shared across the softmax layer.

$$ F(X)=\left [\frac{exp(z_i(X)/T)}{\sum_{l=0}^{N-1}{exp(z_l(X)/T)}  }\right ]_{i\epsilon 0,1...N-1} $$

![](https://github.com/jindingars/secML.github.io/blob/master/src/content/images/softmax.png )

### Using Distillation as a Defense
In distillation as a defense, the same network architecture is used in the distilled DNN as in the original DNN. First, this paper trained an initial network F on data X with a softmax temperature of T. Then, this paper use the probability vector F(X), which includes additional knowledge about classes compared to a class label, predicted by network F to train a distilled network  at temperature T on the same data X. The definition and calculation of F(X) can be found in softmax part and  the detailed training process is described in “how distillation works” part. 

![](https://github.com/jindingars/secML.github.io/blob/master/src/content/images/defense.png )

### Results
This paper evaluated Resilience, Sensitivity and Robustness on 2 datasets: MNIST and CIFAR10

![](https://github.com/jindingars/secML.github.io/blob/master/src/content/images/table.png )
<div class="caption">
Resilience: success rate of adversarial crafting.\n
Sensitivity: amplitude of adversarial gradients.\n
Robustness: amount of perturbation required to achieve adversarial targets.\n
</div>

This paper also evaluated effect of Temperature on Adversarial Success
Success of adversarial samples when changing at most 112 features.

![](https://github.com/jindingars/secML.github.io/blob/master/src/content/images/res.png )
But actually Defensive Distillation is not robust to adversarial examples.

### Why Distillation Seems to Work
First some attacks use the gradient of the logits, where softmax do not work here. Second, big difference in relative impact of changes in input to the softmax layer. Third, training at temperature T effectively increases all inputs to the softmax layer by a factor of T, for example, Undistilled logits with Mean of 5.8/std of 6.4 and Distilled logits (T=100) with Mean of 482/std of 457
### Breaking Distillation
Instead of using the gradient of the input to the softmax layer, the gradient of the output of the softmax layer was used.Due to the problem of vanishing gradients, artificially divide the inputs to the softmax by T. This method achieves a successful misclassification rate of 96.4%.


## Conclusion

...

— Team Nematode: \\
Austin Chen, Ethan Lowman, Aditi Narvekar, Jin Ding, Suya

## References

[[1]](https://www.cs.cornell.edu/~shmat/shmat_oak17.pdf) R. Shokri, M. Stronati, C. Song, V. Shmatikov, "Membership Inference Attacks Against Machine Learning Models." May 2017.
