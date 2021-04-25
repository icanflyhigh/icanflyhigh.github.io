---
layout:     post
title:      Orthogonal Procrustes Problem
subtitle:   学习
date:       2021-04-25
author:     simplex
header-img: img/page_back.jpg
catalog: true
mathjax:  true
tags:
    - 日常 
    - 学习
---

# Orthogonal Procrustes Problem

https://blog.csdn.net/itnerd/article/details/104598742

你pad上ITQ那边也记了一遍

目标问题
$$
min || A\Omega - B||^2\\
s.t. \Omega^T\Omega = I
$$



$$ A, B \in R^{n\times m}$$ 代求$$ \Omega \in R^{n\times n}$$为正交阵

$$ ||A\Omega - B||^2  = tr((A\Omega - B)^T(A\Omega - B))$$ 

$$=tr((\Omega^TA^TA\Omega)) - tr(B^TA\Omega)-tr(\Omega^TA^TB) + tr(B^TB) $$

$$ =tr((\Omega\Omega^TA^TA)) - 2tr(B^TA\Omega) + tr(B^TB)$$

$$ =tr(A^TA) -  - 2tr(B^TA\Omega) + tr(B^TB)$$

所以原问题等价于

原问题
$$
\iff max tr(B^TA\Omega)\\
s.t. \Omega^T\Omega = I
$$


令$$C = B^TA对C做 svd：U\Sigma V^T = C$$, 

则
$$
tr(B^TA\Omega) = tr(U\Sigma V^T \Omega) \\
=tr(\Sigma V^T \Omega U)\\
=tr(\Sigma Z) (Z = V^T \Omega U)\\
=\Sigma_{i, j}\sigma_{ij}z_{ij}\\
=\Sigma_{i}\sigma_{ii}z_{ii}\\
\leqslant \Sigma_{i}\sigma_{ii}
$$
取等号的条件为：Z的对角元为1

令$$ Z =I = V^T\Omega U$$则有
$$
\Omega = VU^T
$$
