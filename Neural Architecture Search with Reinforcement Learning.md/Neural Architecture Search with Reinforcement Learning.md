Paper: [ArXiv Link](https://arxiv.org/abs/1611.01578)

### Motivation

* Designing NN architectures is hard
* Tuning them is harder
* Not a lot of intuition to how to design
* Can we learn new architectures automatically?

### Key Idea
- Use RNN to output strings that defined the network
  - This is called `Controller` in the paper
- This string is then used to train a model and error on validation is treated as (negative) reward.
  - called `Child` network in the paper
- The RNN is trained using this reward using policy gradient/REINFORCE.

![](resources/B42382AF22AE8BFA2E1291AF9B4A6A9E.jpg)

### Experiments
- Penn Treebank for RNNs
- CIFAR-10 for convolutional netwworks
  - allows for skip connection

![](resources/F488602A88F69ED6FA81B31876171C23.jpg)

### Results
- Cell found on Penn Treebank also worked for other datasets.
- Better results than Baysian Optimization (BO).
- More flexible than BO.

### Shortcomings

- Biased towards searches of models of particular kind. 
- Perhaps representing using string that represent arbitrary graph could be better.
- The goals was just to test this methodology, more work needs to be done.

### Similar
- Evolution ( Real et al, 2017)(5.4%)
- Q-learning (Baker et al, 2017)(6.92%)

## Neural Optimizer Search

![](resources/96A65AB47BB7E457A2A08A72FAACC55E.jpg)

![](resources/8A1EBD37D24CED13BE07EF6CEC54BE2C.jpg)

![](resources/70E68F4A5824A3F38BD736AA50223DAD.jpg)