---
layout: post
title:  "Sequential Query Expansion using Concept Graph"
date:   2017-11-06 22:44:23 -0500
categories: papers
---

*paper:  Sequential Query Expansion using Concept Graph [(pdf)](http://www.cs.wayne.edu/kotov/docs/balaneshinkordan-cikm16.pdf)*

## Objectives:

* To discover **effective latent concepts** for query
expansion from from manually and automatically constructed concept graphs (or semantic networks), in which the nodes correspond to words
or phrases and the typed edges designate semantic relationships between words and phrases.
* To leverage **large and dense concept graphs**, in which the number of candidate concepts that
are related to query terms and phrases and need to be examined increases exponentially with the distance from the
original query concepts.

### Example: Concept Graph for Query <span style="color:#528712">"poach wildlife preserve"</span>:

![Five Layers of Concept Graph]({{ "/assets/example.jpg" | absolute_url }})

## Optimization Problem:

* **Objective Function:** total number of **evaluated** concepts

* **Constraint:**
precision of retrieval results


$$
\begin{aligned}
\min_{\mathbb{\tilde C}_{k}^{ut}}\quad&\bigg\{\sum_{i=1}^k{N_i}\bigg\}\\
\text{s.t.}\quad& {\rm E}(\mathbb{\tilde R}_\Lambda;\mathbb{T})>\theta_Q
\end{aligned}
$$

### Approximate Solution (Sequential Concept Selection):

**STEP I**: concepts are **sorted** using computationally **"inexpensive" features**:

![Stage 1]({{ "/assets/s1.jpg" | absolute_url }})

**STEP II**: This sorting is utilized in the **second stage** to sequentially **select expansion concepts** by using computationally **"expensive" features**:

{:.mbtablestyle}
| Criterion                                                    | Decision                                                               |
|--------------------------------------------------------------|------------------------------------------------------------------------|
| If $$\tilde Q_r(C_{(i,j)})\ge\beta_U$$          | **Select** concept $$C_{(i,j)}$$ and **Continue** with the same concept layer  |
| If $$\beta_L\le {\tilde Q_r(C_{(i,j)})}<\beta_U$$ | **Discard** concept $$C_{(i,j)}$$ and **Continue** with the same concept layer |
| If $${\tilde Q_r(C_{(i,j)})}<\beta_L$$            | **Discard** concept $$C_{(i,j)}$$ and **Move** to the next concept layer       |

![Stage 2]({{ "/assets/s2.jpg" | absolute_url }})
