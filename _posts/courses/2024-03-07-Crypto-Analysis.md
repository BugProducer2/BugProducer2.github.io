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

#### 活跃位置

> 输入差分不为0的位置。

#### 4轮不可能差分 in small AES

> 在1️⃣的位置，由于branch number = 5，所以不可能有一个位置是白色的（输入差分为0），一直推到2的位置，仍然不可能有这个位置是白色的。
>
> 因此从后面推过来，如果是正确的密钥，经过invMC，在这个位置不可能是白色的；如果是错误的密钥，因为不满足这个branch number，所以在这个位置有可能是白色的。
>
> `概率计算`：
>
> ​					给定一个明密文对，尝试一个错误密钥，被这个过滤器过滤出来的概率(等价于找，1- pr{四个block都不是白的})是:$1 - (1- 2^{-4})^4\approx  0.23,\ where \ 2^{-4}\  is\  the\ probability\ of\ a\ block\ is\ white.$
>
> ​					在上述基础下，求解需要尝试的明密文对的数量为：N，其中N满足一下关系。
>
> ​					$(2^{16}-1)(1-(1-0.23)^N)\approx 0$
>
> ```mermaid
> graph LR
> A[猜测的密钥有2^16种可能]-->B[正确密钥1个]
> A-->C[错误密钥]
> C-->D[反推到2是白色的,不可能是正确密钥]
> C-->E[反推到2不是白色的,没被过滤器过滤出来]
> ```
>
> 

<img src="https://raw.githubusercontent.com/BugProducer2/PicBed/main/img/image-20240510124059635.png" alt="image-20240510124059635" style="zoom:67%;" />

## Week 7 : Walsh-Hadamard Transform
#### requirement

> 记住算法流程。能理解更好。

Q：为什么要用cov而不是概率来表示？优点在哪里。

Q：什么是well defined 的内积？

