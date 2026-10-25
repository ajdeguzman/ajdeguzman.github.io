---
layout: post
title: 'Decision Trees: More Than Just If-Else'
date: 2026-10-25 21:51 +0800
categories:
  - notebook
tags:
  - machine-learning
  - decision-trees
  - classification
  - gini-impurity
  - entropy
math: true
---

Decision trees are one of those machine learning algorithms that look familiar even before we formally study them.

Most of us have probably followed some kind of decision tree without calling it one:

> Is it raining?
>
> If yes, bring an umbrella.
>
> If no, continue pretending Baguio City weather is predictable.

This is another topic in our **SC03 (Non-Linear Techniques in ML)** course. I already had an overview of what a decision tree was. I knew it looked like a flowchart, asked a series of questions, and eventually arrived at a prediction.

What I had never really explored was how the tree *learns* those questions.

Who decides which feature should appear at the top? Why does the tree ask about one value before another? And when a feature contains numbers, where does a condition such as `rain chance > 55%` come from?

Apparently, the tree does not choose a question because it looks sensible to us. It chooses one because, according to a mathematical measure, that question separates the training data better than the alternatives.

That was the part I wanted to understand.

## A Tree Is Just a Series of Questions

Suppose we want to predict whether it will rain during a morning commute in Baguio City. We might have information such as:

- the weather app's chance of rain;
- the humidity;
- whether dark clouds are visible;
- the month of the year; and
- the time of day.

A small decision tree might look like this:

```text
Is the chance of rain greater than 55%?
├── Yes  → Predict Rain
└── No   → Are dark clouds visible?
    ├── Yes  → Predict Rain
    └── No   → Predict Dry
```

At first glance, a trained tree looks like a series of `if-else` statements. The important difference is that we do not manually choose the questions, their order, or their thresholds. The tree learns them from the training data.

The first question is called the **root node**. The questions below it are **decision nodes** or **internal nodes**. The lines connecting the questions are **branches**, and the final predictions are **leaves**.

An observation starts at the root and follows one branch at a time until it reaches a leaf. If the weather app shows a 70% chance of rain, for example, it follows the `Yes` branch immediately and lands on `Predict Rain`.

That explains how we use an existing tree. It still does not explain how the tree decided that 55% should be its first question.

## Let Us Give the Tree Some Data

Imagine that we recorded ten previous morning commutes. To keep the example manageable, we will use only the weather app's chance of rain and whether it actually rained during the commute.

| Commute | Chance of rain | Actual result |
|:---:|:---:|:---:|
| 1 | 20% | Dry |
| 2 | 30% | Dry |
| 3 | 40% | Rain |
| 4 | 45% | Dry |
| 5 | 50% | Dry |
| 6 | 60% | Rain |
| 7 | 65% | Rain |
| 8 | 70% | Rain |
| 9 | 80% | Rain |
| 10 | 90% | Rain |

This is only a tiny made-up dataset. It is just large enough to see what the decision tree is doing.

At the beginning, all ten observations are in one group. Six are labeled `Rain`, while four are labeled `Dry`.

The group is mixed. In decision-tree language, it is **impure**.

The tree now tries possible questions. For a numerical feature, candidate thresholds are usually placed between consecutive values after the values have been sorted. Between 50% and 60%, for example, the tree can test a threshold of 55%:

```text
Is the chance of rain less than or equal to 55%?
```

That question divides the data into two groups:

- **Left child (`≤ 55%`)**: 1 Rain and 4 Dry
- **Right child (`> 55%`)**: 5 Rain and 0 Dry

The right child is now perfectly pure. Every observation in it belongs to the same class. The left child is not perfect, but it is much less mixed than the original group.

The remaining question is how the tree puts a number on that improvement.

## Then We Met Gini Impurity

One common way to measure how mixed a node is uses **Gini impurity**.

For a node <em>t</em>, the proportion of observations belonging to class <em>k</em> is:

$$
\hat{p}(k \mid t) = \frac{N_{tk}}{N_t}
$$

Here, <em>N</em><sub>t</sub> is the total number of observations in the node, while <em>N</em><sub>tk</sub> is the number belonging to class <em>k</em>.

Gini impurity is then calculated as:

$$
\operatorname{Gini}(t) = 1 - \sum_{k=1}^{K} \hat{p}(k \mid t)^2
$$

The formula looked a little intimidating to me at first, but the idea is simpler than it appears:

- a node containing only one class has a Gini impurity of **0**;
- a node containing a mixture of classes has a higher impurity; and
- for two equally represented classes, Gini impurity reaches **0.5**.

In other words, lower is better. The tree wants its questions to create groups that are more certain and less mixed.

## Calculating the Parent Node

Our original node contains 6 Rain and 4 Dry observations. Its Gini impurity is:

$$
\begin{aligned}
\operatorname{Gini}(\text{parent})
&= 1 - \left(\frac{6}{10}\right)^2 - \left(\frac{4}{10}\right)^2 \\
&= 1 - 0.36 - 0.16 \\
&= 0.48
\end{aligned}
$$

So the starting impurity is **0.48**.

## Calculating the Two Child Nodes

After splitting at 55%, the left child contains 1 Rain and 4 Dry observations:

$$
\begin{aligned}
\operatorname{Gini}(\text{left})
&= 1 - \left(\frac{1}{5}\right)^2 - \left(\frac{4}{5}\right)^2 \\
&= 0.32
\end{aligned}
$$

The right child contains 5 Rain and 0 Dry observations:

$$
\begin{aligned}
\operatorname{Gini}(\text{right})
&= 1 - \left(\frac{5}{5}\right)^2 - \left(\frac{0}{5}\right)^2 \\
&= 0
\end{aligned}
$$

That zero tells us the right child is completely pure.

We cannot simply average 0.32 and 0, though. If one child contained nine observations and the other contained only one, they should not contribute equally. We therefore calculate a **weighted impurity** based on the number of observations in each child:

$$
\begin{aligned}
\operatorname{Gini}(\text{children})
&= \frac{5}{10}(0.32) + \frac{5}{10}(0) \\
&= 0.16
\end{aligned}
$$

Finally, we compare the impurity before and after the split:

$$
\begin{aligned}
\text{Gini decrease}
&= \operatorname{Gini}(\text{parent})
 - \operatorname{Gini}(\text{children}) \\
&= 0.48 - 0.16 \\
&= 0.32
\end{aligned}
$$

The split reduces impurity by **0.32**.

That is the part I had been missing. The tree does not look at the data and somehow "feel" that 55% is a reasonable cutoff. It calculates the result of this candidate split, compares it with other thresholds and features, and selects the one that gives the largest improvement.

## So the Tree Tries Every Question?

Not every question imaginable, but it does examine the candidate splits allowed by the algorithm.

For the rain-chance feature, it could test thresholds between 20 and 30, between 30 and 40, between 40 and 45, and so on. If we also include humidity, it can test possible humidity thresholds. If we include a feature such as `dark clouds visible`, it can test the two groups created by `Yes` and `No`.

The basic learning process is:

1. Start with all training observations in the root node.
2. Try the available feature-and-threshold combinations.
3. Measure the impurity produced by each possible split.
4. Choose the split with the largest impurity decrease.
5. Repeat the process separately inside each child node.
6. Stop when a stopping condition is reached.

This repeated splitting is called **recursive partitioning**.

The word *recursive* makes it sound more mysterious than it is. The tree is essentially repeating the same task inside smaller and smaller groups: find the question that best separates the observations currently in this node.

## Gini Is Not the Only Option

Another common measure for classification trees is **entropy**:

$$
H(t) = -\sum_{k=1}^{K} \hat{p}(k \mid t) \log_2 \hat{p}(k \mid t)
$$

Entropy measures uncertainty. Like Gini impurity, it becomes 0 when a node is pure. A split can be evaluated by comparing the parent's entropy with the weighted entropy of its children. The reduction is commonly called **information gain**.

Gini and entropy use different formulas, so their numerical results are different. But their central goal is similar: prefer questions that create child nodes whose labels are more homogeneous.

For this introduction, Gini was enough to make the learning process click for me. The tree is searching for cleaner groups, and impurity gives it a way to compare which question does that best.

## The Tree Is Greedy

There is one important detail in this process: a classical decision tree is usually **greedy**.

At each node, it chooses the split that looks best *right now*. It does not normally build and compare every possible complete tree before selecting the globally best one. That search would become impractical very quickly.

This makes decision trees efficient and relatively easy to explain. But it also creates a weakness. A locally good first split may not lead to the best possible tree later, and a small change in the training data can sometimes produce a different first split and a very different set of branches.

So although a finished tree can look calm and certain, the path used to build it is more sensitive than the diagram suggests.

## When the Tree Keeps Asking Questions

If we allow a tree to continue splitting without much restriction, it can create very specific rules:

```text
Is rain chance greater than 55%?
Is humidity greater than 81%?
Is it October?
Is the time before 7:13 a.m.?
Did someone wash their car yesterday?
```

The last question is not a real feature, but it captures the problem. A sufficiently deep tree can keep creating smaller leaves until it memorizes unusual details in the training data.

It may perform extremely well on observations it has already seen while performing poorly on new ones. That is **overfitting**.

Some common ways to control the tree include:

- limiting its maximum depth;
- requiring a minimum number of observations before a node can split;
- requiring each leaf to contain a minimum number of observations;
- requiring a split to produce a minimum impurity decrease; and
- pruning branches that add complexity without enough predictive value.

A shallow tree may be too simple and underfit. A very deep tree may memorize noise and overfit. The goal is not to grow the largest tree possible. It is to grow one that captures useful patterns and still works on data it has not seen.

Like choosing the value of \(K\) in K-means or tuning \(C\) and gamma in SVM, tree depth is another reminder that machine learning rarely gives us one setting where "more" automatically means "better."

## What About Regression Trees?

So far, our example has been a **classification tree** because the result is a category: `Rain` or `Dry`.

A **regression tree** follows the same general process but predicts a numerical value. Instead of predicting whether the commute will be rainy, we might predict how many minutes the trip will take.

Inside a regression leaf, the prediction is commonly the mean of the training values that reached that leaf:

$$
\hat{y}_t = \frac{1}{N_t}\sum_{i \in t} y_i
$$

Rather than reducing class impurity, the tree looks for splits that reduce prediction error, often using squared error:

$$
\operatorname{SSE}(t) = \sum_{i \in t}(y_i - \hat{y}_t)^2
$$

The target changes, and so does the split criterion, but the underlying idea remains the same: divide the data into smaller regions whose outcomes are more similar.

## Putting the Pieces Together

Before this topic, I understood a decision tree mostly from the finished diagram. I could follow a path from a root node to a leaf and explain why a particular prediction came out.

But that is only the prediction part.

The learning part happens before the neat diagram exists. The algorithm repeatedly asks:

> Among the questions I can ask here, which one makes the resulting groups less mixed?

For classification, Gini impurity or entropy can answer that question. For regression, a measure such as squared error can do it. The tree chooses the best immediate split, repeats the process in each new group, and stops before its questions become too specific to the training data.

That also explains why decision trees are considered nonlinear. They do not rely on one global straight-line relationship. Different branches can apply different rules to different parts of the data. A 50% chance of rain might lead to one question when dark clouds are visible and another when they are not.

The tree builds its prediction from those interacting conditions.

I used to look at a decision-tree diagram and think the questions were the simple part. Now I see that the questions are the model. The order, the feature, and the threshold are all learned from data.

What eventually appears as a simple collection of `if-else` rules is the result of recursive partitioning, impurity calculations, and repeated comparisons between possible splits.

So the next time a tree asks whether the chance of rain is greater than 55%, I will know where that number came from.

Whether I will actually remember to bring an umbrella is a different classification problem.

## References

1. L. Breiman, J. H. Friedman, R. A. Olshen, and C. J. Stone. “[Classification and Regression Trees](https://books.google.com/books?id=8k1DvQEACAAJ).” Wadsworth, 1984.
2. G. James, D. Witten, T. Hastie, R. Tibshirani, and J. Taylor. “[An Introduction to Statistical Learning: with Applications in Python](https://doi.org/10.1007/978-3-031-38747-0).” Springer, 2023.