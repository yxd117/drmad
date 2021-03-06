# DrMAD

![](https://github.com/bigaidream-projects/drmad/blob/master/docs/shortcut.jpg)

[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/bigaidream/drmad?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE)

> Source code for the paper: [Distilling Reverse-Mode Automatic Differentiation for Optimizing Hyperparameters of Deep Neural Networks](http://arxiv.org/abs/1601.00917).

> :smirk: NEWS: Sep 18, 2016, We are refactoring it to support hyperparameters tuning on VGG on CIFAR-10, and on ImageNet with residual networks. The beta-versions are in other branches. 

## What's DrMAD?

DrMAD is a hyperparameter tuning method based on automatic differentiation, which is a most [criminally underused tool](https://justindomke.wordpress.com/2009/02/17/automatic-differentiation-the-most-criminally-underused-tool-in-the-potential-machine-learning-toolbox/) for machine learning.

DrMAD can tune any continuous hyperparameters (L1 norms for every neuron or learning rates for every neuron at every iteration) for deep models on GPUs.

### AD vs Bayesian optimization (BO)

BO, as a global optimization approach, can hardly support tuning more than 20 hyperparameters, because it treats the learning algorithm being tuned as a black-box and can only get feedback signals after convergence. Also, the learning rate tuned by BO is fixed for all iterations.

AD is different from symbolic differentiation (used by TensorFlow and Theano), and numerical differentiation. AD, as a local optimization method based on gradient information, can make use of the feedback signals after every iteration and can tune thounsands of hyperparameters by using (hyper-)gradients with respect to hyperparameters. Checkout this [paper](https://arxiv.org/abs/1502.05767) if you want to understand AD techniques deeply.

Therefore, AD can tune hundreds of thousands of constant (e.g. L1 norm for every neuron) or dynamic (e.g. learning rates for every neuron at every iteration) hyperparameters.

The standard way of computing these (hyper-)gradients involves a forward and backward pass of computations. However, the backward pass usually needs to consume unaffordable memory (e.g. TBs of RAM for MNIST dataset) to store all the intermediate variables to `exactly` reverse the forward training procedure.

### Hypergradient with an approximate backward pass

![](https://github.com/bigaidream-projects/drmad/blob/master/docs/fig.jpg)


We propose a simple but effective method, DrMAD, to distill the knowledge of the forward pass into a shortcut path, through which we `approximately` reverse the training trajectory. When run on CPUs, DrMAD is at least 45 times faster and consumes 100 times less memory compared to state-of-the-art methods for optimizing hyperparameters with minimal compromise to its effectiveness.

DrMAD is the only gradient-based hyperparameter optimizer that can tune learning rates for every neuron at every iteration on GPUs.

## CPU code for reproducing

For reproducing the original result in the paper, please refer to [CPU version](https://github.com/bigaidream-projects/drmad/tree/master/cpu_ver)

## TODO

We are refactoring the code with Theano/TensorFlow/Torch to support GPU. Currently, the Torch version may not work correctly. 

---

## Citation
```
@article{drmad2016,
  title={DrMAD: Distilling Reverse-Mode Automatic Differentiation for Optimizing Hyperparameters of Deep Neural Networks},
  author={Fu, Jie and Luo, Hongyin and Feng, Jiashi and Low, Kian Hsiang and Chua, Tat-Seng},
  journal={arXiv preprint arXiv:1601.00917},
  year={2016}
}

```

## Contact

If you have any problems or suggestions, please contact: jie.fu A_T u.nus.edu~~cation~~
