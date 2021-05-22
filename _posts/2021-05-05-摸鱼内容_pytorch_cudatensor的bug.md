---
layout:     post
title:      pytorch_cudatensor的bug
subtitle:   学习
date:       2021-05-05
author:     simplex
header-img: img/page_back.jpg
catalog: true
mathjax:  true
tags:
    - 杂谈
    - 学习
---

# pytorch_cudatensor的bug

```python
def loss_function(preds, labels, mu, logvar, n_nodes, norm, pos_weight=None):
    cost = norm * F.binary_cross_entropy_with_logits(preds, labels, pos_weight=pos_weight)

    # see Appendix B from VAE paper:
    # Kingma and Welling. Auto-Encoding Variational Bayes. ICLR, 2014
    # https://arxiv.org/abs/1312.6114
    # 0.5 * sum(1 + log(sigma^2) - mu^2 - sigma^2)
    
    # 1
    KLD = -0.5 .to(torch.device('cuda')) / n_nodes * torch.mean(torch.sum(
        1 + 2 * logvar - mu.pow(2) - logvar.exp().pow(2), 1)) 
    
    # 2
    KLD = torch.tensor(-0.5).to(torch.device('cuda')) / n_nodes * torch.mean(torch.sum(
        1 + 2 * logvar - mu.pow(2) - logvar.exp().pow(2), 1))
    return cost + KLD
```

以上的变量都是在cuda中的tensor

在# 1下

输出是0，我逐步看了一下是，-0.5*cuda 的tensor的结果



在# 2下正常



### 有一个问题

为什么在里面的torch.sum(1 + 2 * logvar - mu.pow(2) - logvar.exp().pow(2), 1)这些东西是正常的，好怪