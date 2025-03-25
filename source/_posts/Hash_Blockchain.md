---
title: 【区块链】  Hash哈希算法
date: 2025-03-25 23:07:30
tags: [区块链,学习]
categories: [学习]
sticky: 9
excerpt: "指针也就是内存地址，指针变量是用来存放内存地址的变量。"
---
## Hash 哈希

Crypto - currency

> 加密货币

  <br>

比特币中主要用到了密码学中的两个功能：

- [**哈希**（全名密码哈希函数：cryptographic hash fuction）](#hash)

- [**签名**]()

<br>

<br>

<a id="hash"></a>

## 哈希

其中，**哈希**具有两个重要的性质 ：

 <br>

### Collision resistance - **抗碰撞性**（实际上指的是冲突）

​	hash没有什么高效的方法人为的制造碰撞（指的是产生冲突），

​	可以通过brute-force（穷举）来获取到两个值的哈希碰撞

​	这里的碰撞指的是x，y两个不同的值经过哈希算法后结果相等

​	即： 
$$
x ≠ y  \quad 与 \quad  hash（x） = hash（y）
$$
> ​	在这里，`hash`指的是哈希函数，经过hash函数计算出的哈希值很难在参数不同的情况下获得相	同的值

​	这种特性可以实现 **massage digest** - 信息摘要（又称信息指纹），用来检测文件完整性，是否被篡改	等等

 <br>

 <br>

### Hiding - 隐藏

​	是指哈希函数的计算过程是单向的，不可逆的

​	例如 `x -> hash（x）`是十分容易计算出来的

​	但反过来就不可行

 <br>

> 这两个性质可以结合在一起，用来实现 ：
>

### Digital Commitment - 数字签名

例如想要确定x是否等于y，但又不想公开x和y的信息；可以通过hash（x）与 hash（y）进行比对，
$$
当 \quad hash（x） = hash（y），那么\quad x = y
$$
<br>

> 针对于比特币，它要求哈希函数拥有第三个特性:

### Puzzle Friendly

它的意思是说，哈希值的计算，事先是不可预测的；

光是看这个输入值，是很难看出来计算后的哈希值的

 <br>

 <br>

## PoW证明

因此，比特币通过这样的特性

实现
$$
hash（block header）<= target
$$
比特币会先设置一个`target`，

随后在`blockheader`中，给予了一个由用户自由设置的随机数（Nonce），通过这个Nonce的`block header`计算出的哈希值如果小于`target`则代表一个工作量，

**这个过程就是挖矿**

由于**PuzzleFriendly**特性，在挖矿的过程中，没有捷径，只能通过不停的尝试修改随机值来获取到符合要求的解，因此，这个过程才可以用来作为工作量的证明

总的来说~~（说人话）~~，PoW证明就是不断的尝试不同的`blockheader`（这个参数可以被由用户设置的随机数改变）来运行hash函数，当达到比特币的目标`target`，则代表这次挖矿成功了

>  **PuzzleFriendly**特性保证了每个挖矿行为的工作量都是足够多的，因此也可以说挖矿这种行为实际上是进行“无意义”的行为

<br>

<br>

虽然挖矿需要很多工作量才能找到合格的随机值，但是证明它却很容易，因此，每次有人找到合格的随机值后会向其他人发布这个随机数，其他人来证明这是否合格，当合格率超过5 0%则意味着这个随机值是合法的

 <br>

**Difficult to solve，but easy to verify（难解,但易验证）**

 <br>

 <br>

## SHA-256

> SHA-256，哈希算法的一种，它满足上文所说的三个哈希特性，因此被比特币采用

 <br>

 <br>

![Static Badge](https://img.shields.io/badge/状态-待更新-brightgreen?style=flat-square)