---
layout: summary
title: Summary
paper: sutskever2013on_1
# Please fill out info below
author: specfazhou
score: 9/10
---

TODO: Summarize the paper:
* What is the core idea? <br/>
The paper points that out classical momentum (CM) or Nesterov's accelerated gradient (NAG) can train DNNs and RNNs if initialization is well-designed and momentum coefficients are carefully chosen. It can achieve the performance only has been achieved by using Hessian-Free optimization (HF) before. Before this paper, people considered it was impossible to train DNNs and RNNs by using first-order method. 

* How is it realized (technically)? <br/>
To show the performance achieved, the authors used CM and NAG to train deep autoencoders, which use sigmoid activication functions. They initialized parameters by using sparse initilization technique (SI), which makes each unit connect to 15 randomly chosen units in previous layer, and because input doesn't depend on the size of previous layer, they can't be easily saturated. the authors also chose momentum coefficient $$\mu_{t} = \min(1-2^{-1-log_{2}([t/250]+1)}, \mu_{max})$$ with $$\mu_{max} \in {0.999, 0.995, 0.99, 0.9, 0}$$. <br/>
To show the effectiveness of CM and NAG, the authors trained typical RNNs by using EGN-based initilization, and momentum methods with various different momentum coefficients and learning rates. One thing to notice is that in EGN-based initilization, it is important to carefully choose spectral radius of hidden-to-hidden matrix, and the scale of initial input-to-hidden connections to make the training effective. 

* How well does the paper perform?<br/>
From the results obtained from the training of Autoencoders, it seems if we use larger value of $$\mu_{max}$$, we will get better result, and NAG usually outperform CM. It is a surprise that the best results achieved by NAG is at the same level of best results gotten by HF. The authors also found that in the last several updates, it is beneficial to reduce momentum coefficient, but should be careful because if it happens too early, it can actually increase the error rates. <br/>
From the results obtained from the training typical RNNs, it seems RNNs can actually be trained by using ESN-based initialization, and momentum methods with large momentum coefficients and small learning rates. Better results can be achieved by NAG with larger momentum coefficient but not for CM probably because NAG has better tolerance of momentum coefficient. <br/>

* What interesting variants are explored? <br/>
The authors explains why NAG avoids oscillations (thus, more tolerant of large momentum coefficient) during training intuitively and theoretically in the paper.   

## TL;DR
* Three
* Bullets
* To highlight the core concepts
1. Use momentums method with well-designed initialization to train DNNs and RNNs that previously thought impossible. But it turns out that first-order method just as good as truncated Newton methods like HF. <br/>
2. Compare the differences between classical momentum and Nesterov's accelerated gradient. <br/>
3. Large momentum coefficient will make momentum methods achieve better performance especially for NAG, because it has better tolerance for large momentum.
