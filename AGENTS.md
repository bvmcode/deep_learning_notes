# AGENTS.md — Educational Markdown Notes Style Guide

## Purpose

When converting lectures, transcripts, course material, or technical explanations into Markdown notes, produce **clean, structured, study-friendly notes** that emphasize intuition, mathematical reasoning, and key takeaways.

The output should feel like polished course notes rather than a transcript.

Do not preserve timestamps, filler language, repetition, or conversational phrasing unless it is important to understanding the concept.

The goal here is to have summarized notes of the lectures.

---

## Notebook Markdown Format

- Bullet point structure
- Enclose LaTeX in `$...$` when it is part of a prose sentence.
- Put standalone equations, including variable definitions and derivative mappings, in centered `$$...$$` blocks rather than equation-only bullet points.
- If a centered equation needs connecting words such as "and," "therefore," or "we then need to," include those words in `\text{}` within the `$$...$$` block.
- Do not add subheaders. Bolded bullet points are fine.
- Create one or more relevant images for every transcript summarization to reinforce the main concepts visually.
- Embed the images in the same Markdown cell as the summarized notes, not in separate notebook cells.
- A demonstration, algorithm, or numerical check may be added as a notebook **code cell** immediately after the markdown it illustrates. Execute that cell so the saved output is part of the notes.
- Keep each code cell short and tied to the concept in the markdown above it.

Example: 
```markdown
### Logistic Regression

* Logistic regression is a statistical and machine learning method used to predict a categorical outcome. It calculates the probability that a data point belongs to a specific class, usually resulting in a value between 0 and 1. 
* Here $\hat{y}$ is the probability an input belongs to class 1.

$$\hat{y} = P(y=1 | x)$$
$$
x \in \mathbb{R}^{n_x}
$$

* The model has two parameters where $w$ is a vector of weights with the same number of dimensions as the input feature and $b$ is a scalar bias and intercept.

$$
w \in \mathbb{R}^{n_x}
$$
$$b \in \mathbb{R}$$

* The simple linear model $z = w^T x + b$ doesn't work well as a probability because its output can be less than 0 or greater than 1. So we must introduce a non-linear activation that outputs values between 0 and 1, which is the sigmoid.

$$\hat{y} = \sigma(z) = \frac{1}{1+e^z}$$

* The sigmoid maps any real number into the range 0 to 1:
    * If `z>>0` then $\hat{y} \to 1$.
    * If `z=0`then $\hat{y} =.5$.
    * If `z<<00` then $\hat{y} \to 0$.

<img src="./images/2.png" height=500 width=800/>

* The superscript `i` means a single example

$$z^{(i)} = w^T x^{(i)} + b$$
$$\hat{y} = \sigma(w^T x^{(i)} + b) = \frac{1}{1+e^{z^{(i)}}} $$


### Logistic Regression Cost Function

* A loss function calculates the error for a single data point, while a cost function measures the average or total error across the entire training dataset.
* We need a loss function to see how good $\hat{y}$ is compared to $y$. From that We need to use a cost function that is convex so we can find the minimum with gradient descent.
* Logistic regression uses **log loss**, also called binary cross-entropy loss. This loss strongly rewards confident correct predictions and strongly penalizes confident incorrect ones.

$$
L(\hat{y},y)
=
-\left[
y\log(\hat{y})
+
(1-y)\log(1-\hat{y})
\right]
$$

$$
L\left(\hat{y}^{(i)},y^{(i)}\right)
=
-\left[
y^{(i)}\log\left(\hat{y}^{(i)}\right)
+
\left(1-y^{(i)}\right)
\log\left(1-\hat{y}^{(i)}\right)
\right]
$$

* Case 1 - The true label is $y=1$. So when the actual label is 1, training encourages the model to predict a probability close to 1.

$$
L(\hat{y},1)
=
-\log(\hat{y})
$$

$$
\hat{y} \rightarrow 1
$$

* Case 2 - The true label is $y=0$. So when the actual label is 0, training encourages the model to predict a probability close to 0.

$$
L(\hat{y},0)
=
-\log(1-\hat{y})
$$

$$
\hat{y} \rightarrow 0
$$

* The cost function measures performance over the entire training set by averaging the individual losses:

$$
J(w,b)
=
\frac{1}{m}
\sum_{i=1}^{m}
L\left(\hat{y}^{(i)},y^{(i)}\right)
$$

$$\text{Substituting the logistic loss gives:}$$

$$
J(w,b)
=
-\frac{1}{m}
\sum_{i=1}^{m}
\left[
y^{(i)}
\log\left(\hat{y}^{(i)}\right)
+
\left(1-y^{(i)}\right)
\log\left(1-\hat{y}^{(i)}\right)
\right]
$$

* Training logistic regression means finding `w` and `b` that minimize the cost:

$$
\min_{w,b} J(w,b)
$$

* In short: **Linear model → Sigmoid → Prediction → Loss per example → Average loss (cost) → Minimize cost to learn $w,b$.**

* This logistic regression model can also be interpreted as a very small neural network, which provides a bridge from logistic regression to more general neural-network architectures.
```
