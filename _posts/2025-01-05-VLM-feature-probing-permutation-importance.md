---
layout: post
title: "Enhance VLM with classification, feature probing, and permutation feature importance"
date: 2025-01-05
categories: today-i-learn
---

# Enhance VLM with classification, feature probing, and permutation feature importance

## Why are Visually-Grounded Language Models Bad at Image Classification?

I start from this [paper](https://yuhui-zh15.github.io/VLMClassifier-Website/) on empowering VLMs with classification data. In short, the authors investigate various factors, such as inference strategies, training objectives, data, and find that the reason for poor performance of VLMs compared to CLIP is data-related. They add classification data to the training procedure and bridge the gap between VLMs and CLIP in terms of classification capability such as on ImageNet.

<figure>
  <img src="/assets/images/today-i-learn/2025-01-05-VLM-feature-probing-permutation-importance/overview.png" 
       alt="The paper can be summarized into three main points: (Left) Different visually-grounded language models (VLMs) underperform CLIP in classification by a large margin, though they often use CLIP as a vision encoder. (Middle) The authors investigate several hypotheses about why VLMs are bad classifiers and find that the main reason is data. Critical information for image classification is encoded in the VLM's latent space but can only be decoded with enough data during VLM training. (Right) Based on their analysis, we improve a VLM by integrating classification data into its training, and find that the improved classification capabilities serve as foundations for more advanced capabilities such as visual question answering." 
       width="800">
  <figcaption>
    The paper can be summarized into three main points: (Left) Different visually-grounded language models (VLMs) underperform CLIP in classification by a large margin, though they often use CLIP as a vision encoder. (Middle) The authors investigate several hypotheses about why VLMs are bad classifiers and find that the main reason is data. Critical information for image classification is encoded in the VLM's latent space but can only be decoded with enough data during VLM training. (Right) Based on their analysis, we improve a VLM by integrating classification data into its training, and find that the improved classification capabilities serve as foundations for more advanced capabilities such as visual question answering.
  </figcaption>
</figure>

Some important findings are:
- VLMs exhibit poor performance in image classification, significantly lagging behind CLIP models.
- Prompt variation such as wording, label order, or chain-of-thought has limited impact on the performance. Probabilistic inference strategy improves the performance but still fails to close the gap between VLMs and CLIPs.
- The information required for classification is mostly preserved in the VLM's latent space. The text generation training objective is as effective as the traditional cross-entropy for learning classification.
- A strong correlation between the ImageNet class frequency in the VLM training data and the VLM's classification performance on those classes indicates that **data determines VLM classification performance**. (Data type, such as classification or captioning data, is unimportant.)

<figure>
    <img src="/assets/images/today-i-learn/2025-01-05-VLM-feature-probing-permutation-importance/data.png" alt="The authors find a strong correlation between class exposure in training and model performance. Moreover, VLMs can achieve the same level of performance as CLIPs when trained with enough data. These results suggest that data is the primary cause of the poor classification performance of VLMs." width="800">
    <figcaption>
        The authors find a strong correlation between class exposure in training and model performance. Moreover, VLMs can achieve the same level of performance as CLIPs when trained with enough data. These results suggest that data is the primary cause of the poor classification performance of VLMs.
    </figcaption>
</figure>

## Feature Probing

- One interesting point from the paper to me is how they experiment whether information required for classification is preserved in the VLM's latent space by feature probing: https://blog.dailydoseofds.com/p/the-probe-method-a-reliable-and-intuitive
- A supported library API for this method is here: https://feature-engine.trainindata.com/en/1.8.x/user_guide/selection/ProbeFeatureSelection.html

## Permutation Feature Importance

The feature probing method uses permutation feature importance technique in interpretable ML:
- https://blog.dailydoseofds.com/p/a-reliable-and-efficient-technique
- https://scikit-learn.org/stable/modules/permutation_importance.html
- https://christophm.github.io/interpretable-ml-book/feature-importance.html