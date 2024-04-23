---
title: '密码分析实践笔记'
subtitle: '课程重点'
layout: post
date: 2024-03-07
header-img: "img/post-bg-2015.jpg"
catalog: true
tag: 
    - courses
---

## Week2
> present按照bit是因为适合硬件实现。
> 注意从左到右是63bit到0bit，我们在实现的时候把0bit放在最低位（pt[0])，可以把1bit放到一个字节去存。
>
> （会导致是S[0]S[1]S[2]S[3]或者S[3]S[2]S[1]S[0]）
>
> cp -rf hukai zhangsancdcp



需要换源自己的git仓库

```bash
git remote rm origin
git remote add origin git@gitee.com:bbeehappy-time/cryptographic-experiments.git   
git push origin master  
```



被fork的仓库更新了

```bash
git remote add upstream http...
git fetch upstream
git merge upstream/master
```



本地更新了，如何merge upstream

```bash
git clean -f -d	#force, also includes directory
git merge upstream/master
```



github被拒绝

```bash
cd ..
cd deps/
ls
# 所有都换成GitHubfast
```



提交pull request，如果把自己的commit push到仓库中，pull request也会相应更新。

## Week 3

### STP 

```mermaid
graph LR
    A[py] --> B[.cvc]
    B -->C[stp .cvc]

    C --> E[invalid]

```



## Week 4

skinny & AES 比较

|          | skinny       | aes                                      |
| -------- | ------------ | ---------------------------------------- |
| 操作     | nible        | byte                                     |
| MC       | 没有域乘操作 | 有                                       |
| 密钥扩张 | 纯线性       |                                          |
| 首尾轮   | 全部一致     | 末轮去掉MC，使得加解密能使用相似的组件。 |

线性分析的**基础**：轮的独立性假设

路线的列对称指的是输入输出掩码都可以按照列的方向移动且是对应的





## Week 5

### Cube attack

#### offline phase

> 寻找合适的cube，遍历所有cube的可能，因为cube项的系数是关于`k0...k79`的表达式，所以所有cube项异或的结果是这个表达式的值。
>
> 通过多个k，我们求解出这个表达式的系数。

####online phase

> 遍历cube项，向oracle提问，得到加密的结果。
>
> 因为offline阶段已经求出了表达式的系数，接下来只需把加密的结果异或，就能得到一个关于真正密钥`k0...k79`的方程。
>
> 解这个方程即可。



Q: 单项式预测看不懂

## Week 6

### 不可能差分

#### Branch Number

$$
BN = min(WT(X)+WT(Y)) for\  all \ Y = F(X)
$$


>`eg`:AES的mix column，对于一列，输入异或有一个1，输出异或为4，则BN大于等于5.

#### 活跃

> 输入差分不为0



