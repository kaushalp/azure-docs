---
title:  "Multiclass Decision Forest: Module Reference"
titleSuffix: Azure Machine Learning service
description: Learn how to use the Multiclass Decision Forest module in Azure Machine Learning service to create a machine learning model based on the *decision forest* algorithm. 
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference

author: xiaoharper
ms.author: zhanxia
ms.date: 05/02/2019
ROBOTS: NOINDEX
---
# Multiclass Decision Forest module

This article describes a module of the visual interface (preview) for Azure Machine Learning service.

Use this module to create a machine learning model based on the *decision forest* algorithm. A decision forest is an ensemble model that rapidly builds a series of decision trees, while learning from tagged data.

## More about decision forests

The decision forest algorithm is an ensemble learning method for classification. The algorithm works by building multiple decision trees and then *voting* on the most popular output class. Voting is a form of aggregation, in which each tree in a classification decision forest outputs a non-normalized frequency histogram of labels. The aggregation process sums these histograms and normalizes the result to get the “probabilities” for each label. The trees that have high prediction confidence have a greater weight in the final decision of the ensemble.

Decision trees in general are non-parametric models, meaning they support data with varied distributions. In each tree, a sequence of simple tests is run for each class, increasing the levels of a tree structure until a leaf node (decision) is reached.

Decision trees have many advantages:

+ They can represent non-linear decision boundaries.
+ They are efficient in computation and memory usage during training and prediction.
+ They perform integrated feature selection and classification.
+ They are resilient in the presence of noisy features.

The decision forest classifier in Azure Machine Learning consists of an ensemble of decision trees. Generally, ensemble models provide better coverage and accuracy than single decision trees. For more information, see [Decision trees](https://go.microsoft.com/fwlink/?LinkId=403677).

## How to configure Multiclass Decision Forest



1. Add the **Multiclass Decision Forest** module to your experiment in the interface. You can find this module under **Machine Learning**, **Initialize Model**, and **Classification**.

2. Double-click the module to open the **Properties** pane.

3. For **Resampling method**, choose the method used to create the individual trees.  You can choose from bagging or replication.

    + **Bagging**: Bagging is also called *bootstrap aggregating*. In this method, each tree is grown on a new sample, created by randomly sampling the original dataset with replacement until you have a dataset the size of the original. The outputs of the models are combined by *voting*, which is a form of aggregation. For more information, see the Wikipedia entry for Bootstrap aggregating.

    + **Replicate**: In replication, each tree is trained on exactly the same input data. The determination of which split predicate is used for each tree node remains random, creating diverse trees.

   

4. Specify how you want the model to be trained, by setting the **Create trainer mode** option.

    + **Single Parameter**: Select this option if you know how you want to configure the model, and provide a set of values as arguments.


5. **Number of decision trees**: Type the maximum number of decision trees that can be created in the ensemble. By creating more decision trees, you can potentially get better coverage, but training time might increase.

    This value also controls the number of trees displayed in the results, when visualizing the trained model. To see or print a single tree, you can set the value to 1; however, this means that only one tree can be produced (the tree with the initial set of parameters), and no further iterations are performed.

6. **Maximum depth of the decision trees**: Type a number to limit the maximum depth of any decision tree. Increasing the depth of the tree might increase precision, at the risk of some overfitting and increased training time.

7. **Number of random splits per node**: Type the number of splits to use when building each node of the tree. A *split* means that features in each level of the tree (node) are randomly divided.

8. **Minimum number of samples per leaf node**: Indicate the minimum number of cases that are required to create any terminal node (leaf) in a tree. By increasing this value, you increase the threshold for creating new rules.

    For example, with the default value of 1, even a single case can cause a new rule to be created. If you increase the value to 5, the training data would have to contain at least five cases that meet the same conditions.



10. Connect a labeled dataset, and one of the training modules:

    + If you set **Create trainer mode** to **Single Parameter**, use the [Train Model](./train-model.md) module.

11. Run the experiment.

## Results

After training is complete:

+ To see the tree that was created on each iteration, right-click the output of the [Train Model](./train-model.md) module, and select **Visualize**.
+ To see the rules for each node, click each tree to drill down into the splits.


## Next steps

See the [set of modules available](module-reference.md) to Azure Machine Learning service. 