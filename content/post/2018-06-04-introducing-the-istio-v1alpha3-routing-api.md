---
showonlyimage: true
title:      "Yolo：从XVS事件看借贷协议的治理与清算"
subtitle:   ""
excerpt: "介Yolo：从XVS事件看借贷协议的治理与清算"
description: "Yolo：从XVS事件看借贷协议的治理与清算"
date:       2020-05-05
author:     "Yolo"
image: "https://img-s-msn-com.akamaized.net/tenant/amp/entityid/AALefSb.img?h=801&w=1438&m=6&q=60&o=f&l=f&x=419&y=150"
published: true 
tags:
    - XVS
    - Lending 
    - risk

categories: [ Tech ]
URL: "/2020/05/05/introducing-XVS-risk-event/"
---



## 事件回顾
Venus大幅的涨跌引发了无数讨论，各类阴谋论层出不穷。这里不概述事件了，用一个圈友的比喻作为引子。
> 就是本来100个鸡蛋一个10块钱的，去花1w块钱把鸡蛋单价拉到一个20块。这样我100个鸡蛋就值2000块，然后我用价值2k的100个鸡蛋去抵押。换来的btc在我口袋里别人拿不走。抵押出去的鸡蛋被强制清算。
[![g5VJqf.md.png](https://z3.ax1x.com/2021/05/19/g5VJqf.md.png)](https://imgtu.com/i/g5VJqf)

事件当中有一些大家关心的核心的问题：
1. 为什么XVS治理流程中会允许作为抵质押物的XVS拥有高达80%的质押率？怎么规避？
2. 这是什么问题？是中心化的问题？还是去中心化不成功的问题。
3. 如何避免连环清算的问题？

## 随手记录
官方也在第一时间出了报告。[Venus Incident Report — XVS Liquidations](https://blog.venus.io/venus-incident-report-xvs-liquidations-451be68bb08f)
(https://blog.venus.io/venus-incident-report-xvs-liquidations-451be68bb08f)

[![g5ViG9.md.png](https://z3.ax1x.com/2021/05/19/g5ViG9.md.png)](https://imgtu.com/i/g5ViG9)
从官方观点来看，他们认为弥补的方式有以下几种：1）加强抵质押品的监测。2）与预言机方面一同合作，降低价格的偏离。3）清算机制的再思考。沿着这些方向继续思考，站在Lending赛道的立场，有几个建设性的想法：
	- 抵质押品相关要素的确定是一个治理问题。什么样的币能够成为抵质押品？成为抵质押品以后低质押率是多少？从本次案例来看，XVS授权允许XVS币，并且治理机制授予XVS80%的质押率。通常来讲提案都通过了社区的审议，XVS的大户就会占据话语权，而经过审议的币种就带着更多大户的利益诉求。大户占据主要话语权并不是绝对的坏事，因为大户对于协议的治理贡献提升了协议的效率。但是我们需要警惕的是，大户的审议是否伤害了散户的利益，我的建议是，协议通过应当要增加一个前提要件：**既需要有一定比例的投票通过率和参与率，同时也要设置一个小额持有人的反对比率。**当小额持有人，反对数量or比例超过一定范围的时候，协议不予通过。为了激励小额持有人的参与，当有人提案的时候需要提交一定比例的保证金，当协议恰好是被小额持有人否决的时候，这部分项目代币需要分配给小额持有人。gwy提交zf工作报告交由rmdbdh审议，最弱小的一部分人，如果有一定比例反对，那么协议也可以被搁置。赋能弱者也是Dao的一个特色，他保证了整个协议的可持续运行。
	- 预言机的思考。这个问题我觉得是借贷协议的核心，之前文章[《预言机设计--从Libor改制吸取经验》](https://mp.weixin.qq.com/s/GlkX1lLu6V6to5KMFfcaJQ)和[《Uni成为预言机以后的世界》](https://mp.weixin.qq.com/s/F4AibkmIt5HpexFGozSd7g) 都提过。好的预言机和坏的语言机差别在哪里？其中一个维度是作恶难度。好的预言机，不太容易被小资金利用。至于其他维度效率和准确性，这里不做展开。在Venus的案例当中，预言机不是主要问题，大量的200万的XVS流通在市场上，约占20%的总量，这么大的流通盘根本不能被预言机机制所规避，真金白银就能有真金白银的成交。
	- 清算机制。**清算人对于抵质押物缺乏信心，容易形成连环清算。**本例中，当抵质押物XVS下跌时，协议清算线被触发，清算人清算后获取了XVS。如果清算人当中有一部分是抵质押物XVS的基石支持者，那么边际上来看，全体清算人在获得抵质押物之后，卖出缩小敞口的动力都会相对弱化，也就不容易进一步造成抵质押物价格的下降。之前也看到过，做清算优化的协议，我认为可以关注下Liquity和LiquityValut。Liquity主要引入稳定池（Stability Pool）的概念，用户在稳定池子中存入稳定币，当触发清算线时，自动清算抵质押物。由于用户在稳定池中为整体借贷协议提供了稳定性，用户一方面可以得到平台的代币线性激励，另一方面也可以以低于市场价10%-20%的价格获取抵质押品。站在协议全局来看，这一部分用户就是奔着获取低成本的抵质押品来的，相对来说对于抵质押品本身会更认可。并且由于清算是自动发生的，抵质押物并未拍卖或者卖出进入市场流通，不会进一步造成抵押品价格下跌，从而引发次生的灾难。我自己写过简略的[《资产负债表角度看Liquity》](https://mp.weixin.qq.com/s/pB2Y_ZJBC81mvhMvnoY6Ng)，推荐太和资本一篇文章[《太和观察 | Liquity:稳定币分级清算机制探索》](https://mp.weixin.qq.com/s/NaU6-g_j6tnsNVJ9WG97lQ)，这篇写的更深入。


参考：
1. [Venus Incident Report — XVS Liquidations](https://blog.venus.io/venus-incident-report-xvs-liquidations-451be68bb08f)

