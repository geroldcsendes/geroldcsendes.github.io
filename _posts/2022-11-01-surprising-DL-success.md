---
title: "Surprising Success of Deep Learning"
categories:
  - Blog
tags:
  - Meta
---

I have recently applied to [SERIMATS](https://www.serimats.org/) where I was tasked to answer the question _Why is it surprising, from the perspective of classic machine learning, that neural networks work so well? And why do they work so well?_  
Had some fun thinking about this topic and I decided to share my thoughs in public.

## TL;DR

It is surprising that NNs work so well because classic ML theory would suggest them to overfit.
NNs are powerful because they can learn data representations successfully. Their success is amplified by 1) their parallelizable nature and competitive hardware (GPU) 2) abundance of data 3) iterative training procedure.

## Why is it surprising, from the perspective of classic machine learning, that neural networks work so well?

Neural nets' superior performance is surprising from the perspective of classic ML because it manages to do so while "overparameterized" compared to classic ML algos. In other words, NNs have too much capacity and classic ML theory suggests that they should overfit. As an example, the VGG net [1], a former state-of-the-art CV architecture, had ca. 140 million trainable parameters while only about 1.2 million images as training data on the Imagenet challenge. This already enters the reign of **p >> n**, meaning that we have far more dimensions than data. Generally, **classic ML algorithms would severely overfit**; just take linear regression for example. The linear system would be undetermined in that case, and there wouldn't even exist a unique solution for such a problem.

As a quick side note, there even exists the phenomenon of the "degradation problem". It says that NNs train fit starts degrading upon adding too much capacity. This problem is nicely explained and even given a remedy against in the ResNet architecture [2]. This again contradicts classic ML intuition where one would expect training performance to improve upon increasing model capacity.

## Why are neural nets so powerful?

We don't have a clear understanding why exactly NNs work so well. To be more precise, there is no extensive mathematical derivation that points out why NNs can be trained so well so that they are able to generalize. There exists the **Universal Function Approximator** [3] theory which states that a wide enough NN can approximate arbitrary functions with 2 layers already. However, this does not say anything if there is any guarantee that the training procedure will end up with the weights facilitating that specific function approximation. Still, in many applications the training procedure manages to find the set of weights that seem to approximate the function of the given task. 

## Representation learning

There are a few things that seem to power NNs but probably the most important is that they are able to learn useful data representations that aid downstream tasks. This is called representation/features learning. Let's put representation learning and NNs together in a toy example. The task is face detection where we want to match a face to a "reference" one. In order to do this NN should be able to identify important facial attributes which it can compare to the reference face. If someone with a mustache steals my Iphone and wants to unlock it via face ID, the NN should be able to detect the mustache at least and say, "Gerold does not  have a mustache, I am not letting you in ''. 

We can think of facial features as representations of the data, in this case the image taken by the thief, and the combinations of these features can result in prediction; is this Gerold's face or not? In a CV problem, representations are usually learnt by convolutional layers that are powerful feature detectors; and upon stacking them, you can end up with a hierarchy of features. By going deeper, CNN can derive features of growing complexity. In the first layer it may learn edges then corners and contours then maybe even mustaches. Upon reaching features that are sufficiently complex, we can just add an output layer to map these features to predictions.

Representation learning is something novel to classic ML. There, features need to be engineered which is very tedious and given the complexity of the problem, a very hard task. Imagine if you had to design a mustache feature detectors yourself. Even if you managed to come up with a great engineering solution it is quite likely it would fail to generalize. Additionally, this is just a single feature that matters and there are hundreds or even thousands more. One would need to feature engineer them all to be able to compete with NNs when using classic ML algos.

## Inductive bias

If we accept the fact that representation learning is important then it begs the question what makes NNs great representation learners? In my opinion, this has to do with their flexible architecture through which you can introduce **inductive bias(es)** that are useful for the given task. CNNs have weights sharing and locality inductive biases that, in my opinion, are very useful for CV tasks. In self-attention (key mechanism of the Transformer), the inductive bias may be defined as attending to entities based on context which again seems to make sense in an NLP task (and in others, too e.g. computer vision).

## Little detour
This paragraph is a detour and just tries to further support the argument that representation learning is a key factor. You will still understand my main points if you skip this section. Feel free to skip.

I want to make a case for why representation learning is so important for NNs. There is still a "domain" where NNs are not performing better than classic ML algorithms. This domain is structured data. NNs just work a lot better on unstructured data e.g. text, image, video, audio etc...

I am making the point that learning structured data is generally an easier problem than unstructured. Usually we end up having structured data in domains where data is stored in databases with “content” defined by experts like business analysts or researchers. Take a marketing problem, for instance churn prediction. In that case we want to predict future customer behavior from past patterns. Now, data is usually available in tabular format with features like customer age, purchase history, customer rating etc.. In such a case, you already get your data feature engineered in the first place - people decide to measure what they think matters in the first place. These scenarios don’t require much feature engineering in the first place because the “raw” features themselves already contain enough information. (Note: I am not trying to make the point that feature engineering would not help. I am rather trying to convey that their added value is not as high.)

Let me elaborate on my previous point. My point is that in cases where classical ML algos work is usually where we already got the feature engineered in the first place and we don’t work with raw (unstructured) data. In the churn prediction problem, raw data would be something like a full history of product’s prices, supply, opening hours of shops, clickstream data of online shoppers etc.. In that case, I am sure a deep learning solution would outperform a classical ML one.

## Others
Though from my point of view representation is the key in the success of NNs, there are still a few other factors that are essential, too. These are mostly technical and somewhat of similar natures, so I will not go into too much detail.
- The most successful architectures can be massively parallelized and GPUs do just that perfectly (also TPUs lately). Without this kind of hardware, we would most certainly not be able to train NNs on scale.
- Thanks to the internet, we have lots of data that we can train on. For most tasks, we need to feed NNs with an abundance of data to get satisfactory results or even better. Models like GPT3 would most likely not exist if data collection on the internet was not possible.
- Iterative training procedure. NNs are not only flexible in architecture but they are also quite flexible on the "input" side. We can do batching, so we don't have to load all the dataset into memory. We can also re-use weights mostly for fine-tuning for downstream tasks. Neither of these are possible with classic ML algos.

## References
[1] Karen Simonyan, Andrew Zisserman. Very Deep Convolutional Networks for Large-Scale Image Recognition. arXiv, 2015. arXiv:1409.1556.

[2] Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun. Deep Residual Learning for Image Recognition. arXiv 2015. arXiv:1512.03385.

[3] Hornik K., Stinchcombe M., White H. Multilayer feedforward networks are universal approximators. Neural Networks 1989,  2  (5) , pp. 359-366.
