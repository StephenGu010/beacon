# beacon

Beacon是一种基于BLE的技术，以固定间隔广播发送固定格式的数据。信号强弱以RSSI相对强度来表示，遇到障碍物信号会很弱。
---
Beacon信标本质是一种蓝牙广播标准，该标准不是蓝牙技术联盟所制定的标准，它被称为“虚拟标准”，是由大型供应商或企业集团为首，针对广泛的Beacon应用所正式提出的蓝牙应用规范。
---
由苹果公司封装形成的标准是iBeacon，而Eddystone是谷歌公司制定的标准。Eddystone相对于iBeacon功能更为广泛，可以广播自定义唯一的信标ID（UID）、广播网址（URL）、广播自身数据（TLM/ETLM）、加密的临时标识符（EID）。
----



### 当前UUID分类
![5437738c42f14bc3a59e7498380a1cf1](https://github.com/StephenGu010/beacon/assets/105930694/f129b1e4-d78a-4f35-a879-4dc420af0128)

### AD structrue 类型
![2c00ec13930846a4914f19ee2237f2f0](https://github.com/StephenGu010/beacon/assets/105930694/62982957-820e-475b-b655-658eadd00db8)


# BLE广播包格式
如下图所示为广播包的格式，它最终会被封装在LL层packet中的PDU中
![e0d3ebfb5df4452f82be8ce80edb1de1](https://github.com/StephenGu010/beacon/assets/105930694/77ff1b4d-4696-4a77-8631-bd45b91386ca)

### 前导
前导是一个8bit的交替序列，根据接入地址的第一个bit为0或者1，分为01010101和10101010两种，接收机可以根据前导的无线信号强度来配置自动增益控制。

### 接入地址
接入地址有两种类型：广播接入地址和数据接入地址。

- 广播接入地址：固定为0x8E89BED6，在广播、扫描、发起连接时使用
- 数据接入地址：随机值，不同的连接有不同的值，在连接建立后两个设备间使用。
### 报头
广播报文报头格式如下：
![d4aadda82a5c48b5bbfaca6f5c25f654](https://github.com/StephenGu010/beacon/assets/105930694/ec7c3d13-2b55-455c-b65d-c27f86628d94)

### 报文类型（PDU Type）:  
![86ac79e000ba40629e8f6722c0758f22](https://github.com/StephenGu010/beacon/assets/105930694/cb2a8ed6-d9c9-4e61-9bb4-39d1254918a0)

- 发送地址类型（TxAdd）：如果广播设备的地址是随机的，该位置1，如果是公共的，该位置0。
- 接收地址类型（RxAdd）：如果目标设备的地址是随机的，该位置1，如果是公共的，该位置0。
###原理说明（可选）
阐述项目是基于什么思路设计的


### 下载安装
Gradle:  
``` xml
compile 'xxx'
```
(说明项目的配置方法，android开源库多用Gradle导入)

### 使用方法
怎么使用，有哪些步骤哪些接口。

### 注意事项
比如混淆方法等

### TODO（可选）
接下来的开发/维护计划。

## License
遵守的协议
————————————————
原文链接：https://blog.csdn.net/yplwrt/article/details/129107710
