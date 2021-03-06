---
description: 低方差挖掘提高区块链安全性
---

# Bobtail: Improved Blockchain Securitywith Low-Variance Mining

## 01. 简介

| 标题 | Bobtail: Improved Blockchain Security with Low-Variance Mining |
| :--- | :--- |
| 作者 | George Bissias，Brian N. Levine |
| 发表会议名称 | 27th Annual Network and Distributed System Security Symposium |
| 发表时间 | February 2020 |
| 下载链接 | [https://www.ndss-symposium.org/wp-content/uploads/2020/02/23095-paper.pdf](https://www.ndss-symposium.org/wp-content/uploads/2020/02/23095-paper.pdf) |

## 02. Abstract

### a. Abstract

       Blockchain systems are designed to produce blocks at a constant average rate. The most popular systems currently employ a Proof of Work \(PoW\) algorithm as a means of creating these blocks. An unfortunate limitation of all deployed PoW blockchain systems is that the time between blocks has high variance. For example, Bitcoin produces, on average, one block every 10 minutes. However, 5% of the time, Bitcoin's inter-block time is at least 40 minutes.

         In this paper, we show that high variance is at the root of fundamental attacks on PoW blockchains. We propose an alternative process for PoW-based block discovery that results in an inter-block time with significantly lower variance. Our algorithm, called \_Bobtail\_, generalizes the current algorithm, which uses a single PoW sample, to one that incorporates $$k$$ samples. We show that the variance of inter-block times decreases as $$k$$ increases. Bobtail significantly thwarts doublespend and selfish mining attacks. For example, for Bitcoin and Ethereum, a doublespending attacker with 40% of the mining power will succeed with 53% probability when the merchant sets up an embargo of 1 block; however, when $$k\geq40$$ , the probability of success for the same attacker falls to less than 1%. Similarly, for Bitcoin and Ethereum currently, a selfish miner with 49% of the mining power will claim about 95% of blocks; however, when $$k\geq20$$ , the same miner will find that selfish mining is less successful than honest mining. We also investigate attacks newly made possible by Bobtail and show how they can be defeated. The primary costs of our approach are larger blocks and increased network traffic.

### b. 摘要

　　区块链系统被设计成以恒定的平均速率生产区块\(blocks\)。当前，最流行的系统采用工作量证明（PoW）算法来创建区块的。所有PoW区块链系统有一个不幸的限制，那就是块之间的生成时间差异很大。例如，比特币平均每10分钟产生一个区块。然而，有5％的概率，比特币的区块生成间隔\(Inter-block time\)至少为40分钟。

　　在本文中，我们表明\(区块生成时间的\)高差异性是对PoW区块链进行基本攻击的根源。我们提出了一种PoW区块\(PoW-based block\)生成的替代过程，该过程导致区块生成间隔\(Inter-block time\)的方差大大降低。我们的算法称为\_Bobtail\_，是将当前使用单个PoW样本的算法推广为包含k个样本的算法。我们表明，块间时间\(Inter-block time\)的方差随着k的增加而减小。Bobtail显著地阻止双重支付\(doublespend\)和私自采矿\(selfish mining\)攻击。例如，对于比特币和以太坊\(Ethereum\)，当商人设置1个区块禁运\(an embargo of 1 block\)时，拥有40％采矿能力的“双花”攻击者将以53％的概率成功；但是，当k ≥ 40时，同一攻击者的成功概率降至1％以下。同样，对于当前的比特币和以太坊，拥有49％采矿能力的自私矿工将拥有约71％的区块；然而，当k ≥ 20时，同一矿工会发现自私采矿不如诚实采矿成功。我们还调查Bobtail新近带来的攻击，并展示如何将其击败。我们方法的主要成本是更大的区块和增加的网络流量。

## 03. Conclusion

### a. Conclusion

        We have designed and characterized a novel method of low-variance blockchain mining called Bobtail. We have derived expressions for the expectation and variance of the Bobtail mining proof of work and its mining time for any value of k. Using these expressions, we have shown that Bobtail reduces variance in block inter-arrival time by a factor of O\(1/k\), compared to using k = 1. We have also shown that forks are inadvertently created by Bobtail miners no more often than existing systems, and that dishonest miners receive significantly lower rewards due to minor protocol adjustments. Furthermore, we have demonstrated that low-variance mining significantly reduces the effectiveness of doublespend and selfish mining attacks, and that our design thwarts withholding and denialof-service attacks. Finally we have introduced a policy for miner coordination in Bobtail that keeps network traffic to a minimum.

### b. 结论

　　我们设计并描述了一种新颖的低方差区块链挖掘方法——Bobtail。 我们已经推导出了\(在任意k值下\)Bobtail工作量证明及其挖掘时间的期望值和方差的表达式。使用这些表达式，我们已经表明，与使用k = 1相比，Bobtail将块到达时间\(block inter-arrival time\)的方差减少了O\(1/k\)倍。我们还表明，bobtail矿工在无意中创建分叉的频率比现有系统的低，而且由于协议的微小调整，不诚实的矿工得到的奖励明显降低。此外，我们已经证明，低方差挖掘极大地降低了双重支付攻击和私自挖矿攻击的有效性，并且我们的设计阻碍了扣留和拒绝服务攻击。最后，我们在Bobtail中引入了矿工协调策略，以将网络流量保持在最低水平。

## 04. 其他

* 作者主页：[我跳](https://people.cs.umass.edu/~gbiss/)
* 会议回放：[我跳](https://www.youtube.com/watch?v=GhJqNtYFcBw&list=PLfUWWM-POgQsz0H0uwSVQK5_ISMiW0m98&index=1)
* 有关视频：[我跳](https://www.youtube.com/watch?v=u8Gqm9NLY6Q&t=437s)

