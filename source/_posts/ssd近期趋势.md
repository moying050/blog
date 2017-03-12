---
title: ssd近期趋势
date: 2017-03-12 15:39:57
tags: [云存储, 硬件评估]
categories: [系统组建]
---
# SSD相关趋势
## intel ssd种类以及定位
- 从性能上从低到高依此为HDD->3d nand -> optane -> 非易失性ram
- 3D NAND ssd是TLC的ssd，从TCO看已经可以代替10000转的sas硬盘，容量也很大，目前最大是16TB
- optane ssd是高性能ssd，会在17年二季度发布，随机读写性能都很强，为目前S3700十倍以上（之前的P3600读性能很好，但写只有S3700的2倍）
- intel在18年还会发布非易失性ram，据他们说性能与DDR2差不多，但掉电不会丢数据

## 自己做OP来延长ssd的寿命
- OP指的是自己划出一块空间，保留给ssd，让ssd用来做加速/坏块映射等
- 百度自己的测试数据是他们拿10%的空间做OP，在他们的应用场景延长了1倍的寿命，随机写性能也有30%左右的提升,在我们的场景中也验证了
- 这种方式不论PCIE/sata ssd都是支持的
- 这种方式对于我们感觉有一定意义，可以以大空间换取高寿命
- 寿命计算也可以通过高版本smartctl工具的新字段（nand数据写入量）来自己近似计算

## PCIE ssd会很快代替sata ssd
17年2季度后pcie ssd可以使用raid/热插拔，已经可以完全取代sata ssd。
- 后续intel新技术不会再用到sata ssd上，只搞pcie ssd，性价比上pcie ssd也比sata ssd更好
- 供应上，即使在路线图中sata ssd还存在，但可能也会缺货
- 目前pcie ssd已经支持热插拔（m.2接口的pcie ssd）
- 17年二季度发布的v5系列cpu自带raid控制器，支持pcie ssd组raid（VMD/VROC），激活费用另算，raid1在99美元左右，raid性能也比raid卡的优秀稳定，不过可能对linux内核版本有一定要求

## ssd的新形态支持1U服务器插32块ssd
- intel会推出ruler ssd，1U服务器最多可以插入32块ssd，每块ssd32TB，则可以支持1PB
- 会有新的nvme驱动方式来降低cpu吞吐这么多ssd的压力
