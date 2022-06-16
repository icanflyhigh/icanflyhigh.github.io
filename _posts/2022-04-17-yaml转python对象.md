---
layout:     post
title:      yaml转python对象
subtitle:   学习
date:       2022-04-17
author:     simplex
header-img: img/page_back.jpg
catalog: true
mathjax:  true
tags:
    - 学习	
---



# 问题描述

在使用python读取yaml的时候遇到问题，已知 yaml 文件，如何将其转化为 python 中的一个类。下面是一个yaml文件。

```yaml
MUTAG:
  batch_size: 64
  batchnorm_dim: 28
```




# 解决

首先，我使用了 pyyaml 包，pyyaml 不能直接将 yaml 文件读取为类。

## 1 改变yaml格式

根据 pyyaml 的[官方 doc](https://pyyaml.org/wiki/PyYAMLDocumentation)，在 ```Loading YAML``` 部分有如下方式：

```shell
>>> class Hero:
...     def __init__(self, name, hp, sp):
...         self.name = name
...         self.hp = hp
...         self.sp = sp
...     def __repr__(self):
...         return "%s(name=%r, hp=%r, sp=%r)" % (
...             self.__class__.__name__, self.name, self.hp, self.sp)
>>> yaml.load("""
... !!python/object:__main__.Hero
... name: Welthyr Syxgon
... hp: 1200
... sp: 0
... """)

```

```
Hero(name='Welthyr Syxgon', hp=1200, sp=0)
```

首先，可以看出，pyyaml 的作者是一个 RPG 游戏爱好者。不过我没有查到 Welthyr Syxgon 是什么东西。

其次，根据上面的方法，我们也可以模仿上面

* 在 py 文件当中定义一个类，类中属性包含了所有 yaml 中的对象
* 在 yaml 中以``` !!python/object:__main__.你的类名```开头

### 评价

两边都要定义，比较麻烦。不够优美。具体我也没有深究细节。



## 2  间接转化

首先读取 yaml 文件为 dict，再将其转化为 类。

这里面有很多方法，[stackoverflow: 将 yaml 转化为 python 类](https://stackoverflow.com/questions/6866600/how-to-parse-read-a-yaml-file-into-a-python-object)，[stackoverflow: python 将 dict 转化为 object](https://stackoverflow.com/questions/1305532/convert-nested-python-dict-to-object)

下面是高赞回答的方式：

通过 pyyaml 将其读取为 dict

```python
import yaml
with open('config.yaml') as f:
    # use safe_load instead load
    dataMap = yaml.safe_load(f)
```

创建中间类，目的是将 dict 转化为这个类

```python
class Struct:
    def __init__(self, **entries): 
        self.__dict__.update(entries)
```

转化

```python
# 注意这里的参数
args = Struct(**dataMap)
```

然后这个 `args ` 就是想要的类了



### 其他

根据其他的回答，还有专门用于转化的库。详情见上面的链接。



# 总结

以上是两种简单的将 yaml 文件转化为 python 类的方法，里面有一些细节可能有错误。权当是一种思路吧。

