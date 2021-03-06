
# Sensible 开发进展会议 (2/n)

## 1. 高级方案目前存在的问题 

- 伪造哈希（攻击可能性）
- 尺寸过大（有无现实手段优化或缓解）
- 结论：暂时先放放，后续再看是否值得跟进

## 2. 昨晚更新 token 合约

- 正式的 token 使用更新后的新版本
- 结论：后续暂先采用类似 ETH 的合约更新方式，小需求等大版本时一起更新

## 3. 后续计划

- query-transaction-status 可用 (可直接调 TAAL 接口，无需 key)
- 三方测试存在的问题，后续步骤 (最晚下周二可以三方测试)
    + SDK 内的 FT 加上支持 metaid 选项
- CoinGeek 宣传的必要准备工作 
    + 宣传是怎么个形式？是给我们一个 speech 吗？
        * 给 speech 比较困难。应该是可以做 announcement 新闻稿和 press release 媒体发布
        * 互通，有互操作性，interoperability
        * (有材料的话发顾露整合汇总)
- 是否针对 Ying 方案做后续研究 (不用讨论，重大问题先搞清楚，暂放一下)
- NFT 支持计划 
    + (metaid 已支持，可测试互通)
- 6月1日三方联调进度没问题

## 补充

- 签名器的服务地址写到 metaid 里 (oracle 升级，创世交易留好入口，换地址时可以及时更新)
    + 正式签名器部署情况
        * 小聪 (香港腾讯云) volt (香港阿里云) show (目前在香港阿里云，已经建议改到国内，下周一完成)
- 蒋杰问：大家的签名器的私钥怎么生成的？
    + 建议用 sensible 的 c 代码修改版生成 (512位)
    + volt 用 scrypt 的 rabin 签名生成 (长度可能太短，需要复查是否够长)
- 陈耀欢问：NFT 和 FT 是否应该用不一样的签名器？
    + 结论：可以一样，签名器应该是通用的，不管你用什么用途
- 王福强问：如果另外一个独立开发者发了一个 token，用了他自己的签名器怎么办？钱包需要大改吗？
    + 结论：不用，直接用他提供好的就行。
- 冯新宇问：交易所需要自己运行签名器吗 (希望类似 usdt 那样自己控制一个签名器)？
    + 蒋杰回应：交易所即使拥有一个签名器，也没法控制什么东西，3选2完全可以绕过他，达不到控制的目的。
    + 结论：不需要。可以弄个核心机制无关的开源的验证器给他们 (监督用)。
- 王宇问：非法交易发生时如何？
    + 攻击发生，如果有一家签名器私钥被泄漏，这时立刻开始迁移过程 (暂时还是安全的) 
    + 只要有一笔作恶，后续被污染的交易全部不被认可 (ETH 分叉出来是从出问题之前完整快照)
    + 只要有一个泄漏发生，可以停掉所有相关的签名器，这时候就没法开始新的转账了
- 王宇问：API 服务有时有问题 (前几天有问题后回滚了) 怎么处理？
    + 需要更多的独立部署，避免单点
    + 目前需要 64GB (如果不是 redis 备份，可以只需要 25GB+) 磁盘需求 1T
    + 备份起作用情况下，无需重扫 (需要 5 小时，优先级低)
    + 结论：show 会部署一个 (无需 redis 备份)
    + 后续也会有更多方部署 (go 程序部署非常容易)
- 王福强问：现在架构不鼓励钱包自己管理 utxo？
    + cc: 自己想管理也是可以的，API 服务节点多几个就没问题了
    + 蒋杰补一下 readme 写篇文章发到官网 (如何部署 API 服务)
