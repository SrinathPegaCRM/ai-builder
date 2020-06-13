---
title: Understand category classification model performance - AI Builder | Microsoft Docs
description: Provides an understanding of how to evaluate and understand category classification model performance
author: raaourik 
ms.service: powerapps
ms.topic: conceptual
ms.custom: 
ms.date: 09/06/2019
ms.author: raaourik 
ms.reviewer: v-dehaas
---

# Understand category classification model performance

[!INCLUDE[cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

After each training, AI Builder uses the test dataset to evaluate the quality and accuracy of your AI model. A summary page for your model shows your model training results, including a **Performance** score.

AI Builder calculates your model's performance score based on the precision and recall of the prediction results:

- **Performance score**: The harmonic mean of the precision and recall scores. It balances both scores for an imbalanced class distribution. Performance score values are from 0 and 100. Generally, the higher the performance score, the better your model is.
- **Precision**: The fraction of correct predictions among all the positive predictions.
- **Recall**: The fraction of correct predictions among all true positive cases.

## Quick test

You can also select **Quick Test** to assess the quality of the model. Just enter text that you want to tag. The quick test generates a list of all tags that have a confidence score of 50&nbsp;percent or greater. More information: [Evaluate your model](manage-model.md#evaluate-your-model)

### Next step

[Improve the performance of your category classification model](improve-text-classification-performance.md)
