---
title: 'LLM Literature Review'
subtitle: 'Large language model'
layout: post
date: 2024-03-31
header-img: "img/post-bg-halting.jpg"
catalog: true
tag: 
    - review
    - LLM
---





**step 1：**搜集关于这个方向的信息，判断发展潜力。

​				`哪些公司在这方面有投入？`，`参与研究的团队有哪些？`，`是否是领域内核心团队（可以用发的论文数量量化）`，

​				`方向是否已经发展得比较完善`

**step 2：**和周围人 & 这个方向的人讨论，进一步获得信息，尤其是要`能把一个方向整理和讲解出来`，可以做pre在组会上讲，也可以写literature review。

**step 3：**熟练以上步骤



## Survey

### `basic`

`基本概念`：Large Language Models，可以流畅准确生成内容。

`领域目标`：AIGC，**Transfer Learning**，**Ethical AI**，**Privacy and Security**



### `steps of developing LLM`

`pre-training`：trained on a large dataset

`fine-tuning`:

`inference`



### `concerns of LLM`

`leakage` `attack`

<img src="https://raw.githubusercontent.com/BugProducer2/PicBed/main/img/image-20240407144251186.png" alt="image-20240407144251186" style="zoom:100%;" />



看看老师的survey的参考文献



## 顶会论文

*ACM CCS*

> Session 2: Machine Learning Applications I 里面两篇是关于如何基于ML做malware检测，一篇是用微小形变泄漏信息，一篇是基于ML做电池认证。。

> Session 8: Machine Learning Applications II 里面一篇基于ML做风险检测，AI可解释性、头戴式设备泄漏隐私。

> Session 14: Machine Learning Attacks I 经过这四种安全属性训练的AI模型、后门攻击一个，

> Session 20: Machine Learning Attacks II

> Session 26: Federated Learning 
>
> 多个检测指标来对 poison-attack-assistant 模型更新,新型联邦学习(FL)架构

[The RefinedWeb Dataset for Falcon LLM: Outperforming Curated Corpora with Web Data Only]():`ml 顶会 NeurIPS 2023`

[Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://proceedings.neurips.cc/paper_files/paper/2023/hash/91f18a1287b398d378ef22505bf41832-Abstract-Datasets_and_Benchmarks.html)：`NeurIPS`

[NExT-GPT: Any-to-Any Multimodal LLM]():` ICLR在投`
