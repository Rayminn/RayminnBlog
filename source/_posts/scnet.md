---
title: 让算力像水电一样即取即用——超算互联网使用（白嫖）指北
date: 2024-05-09
categories:
- 人工智能
tag: 
- 云计算
- 算力
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1363948882&auto=0&height=66"></iframe>

> 算力是AI时代的石油

要想对AI大模型部署、训练、调参，需要大量的算力，难以在本地部署。一般个人出于爱好学习或者规模较小的组织都会选择用云计算的方式来解决这个问题。

但云计算尤其GPU算力价格通常较高（本人曾经为体验自部署ChatGLM模型花费二百元），而且GPU资源一般不提供免费试用，这对于学生党或者小团队来说是一个不小的负担。

本文将介绍一个可以算力便宜且可以免费试用的平台——超算互联网 [SCNet](https://scnet.cn/)。

<!--more-->

# 什么是SCNet

SCNet 是继东数西算工程后，由部委指导并发起成立的联合体。

在SCNet上，你可以试用、购买各种云计算资源、应用软件、应用平台、数据资产，以及技术服务支持。

# 友商对比

![![scnet1](https://raw.githubusercontent.com/Rayminn/img/main/scnet1.png)](https://cdn.jsdelivr.net/gh/Rayminn/img/scnet1.png)

![![scnet2](https://raw.githubusercontent.com/Rayminn/img/main/scnet2.png)](https://cdn.jsdelivr.net/gh/Rayminn/img/scnet2.png)

租赁GPU价格普遍较高，较为广泛应用的[AutoDL](https://www.autodl.com/)中，24GB显存价格为2.29元/卡\*时，在SCNet中，32GB异构计算价格为2元/卡\*时(但16GB也是此价格，对此笔者表示不理解)。

![![scnet3](https://raw.githubusercontent.com/Rayminn/img/main/scnet3.png)](https://cdn.jsdelivr.net/gh/Rayminn/img/scnet3.png)

上图的实例提供免费试用，写作本文时每个CPU实例提供2000核时，DCU实例提供200核时（经试验同一实例的不同地区可以重复申请试用）。

> DCU：专门用于AI人工智能和深度学习的加速卡。

# 使用体验

提供命令行（可SSH）、桌面、Jupyter、code-server等多种方式连接实例。

对于提供支持的软件也可以一键炼丹。

有一个坑点在于，`Torch`库默认是GPU运行的，在DCU上运行需要在应用市场中下载专用版。

总体体验良好（免费试用暴赞）。