# beacon

Beacon是一种基于BLE的技术，以固定间隔广播发送固定格式的数据。信号强弱以RSSI相对强度来表示，遇到障碍物信号会很弱。

Beacon信标本质是一种蓝牙广播标准，该标准不是蓝牙技术联盟所制定的标准，它被称为“虚拟标准”，是由大型供应商或企业集团为首，针对广泛的Beacon应用所正式提出的蓝牙应用规范。

由苹果公司封装形成的标准是iBeacon，而Eddystone是谷歌公司制定的标准。Eddystone相对于iBeacon功能更为广泛，可以广播自定义唯一的信标ID（UID）、广播网址（URL）、广播自身数据（TLM/ETLM）、加密的临时标识符（EID）。




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
### Eddystone数据结构
数据包格式如下：
![be403ff614ec47dab24a1e4441497156](https://github.com/StephenGu010/beacon/assets/105930694/f5bf68f9-8421-493f-8194-48b3ea4bdfe4)
#### UID
这是由三个字段组成的主要Eddystone框架，即命名空间标识符（10byte），实例标识符（6byte）和功率校准（1byte）。他将有助于将字段直接配置到BLE信标中，实例标识符旨在唯一地表示一个信标，因为他们具有不同的实例ID，功率校准字段用于根据RSSI帮助计算移动设备和Eddystone信标之间的距离。
#### URL
该框架的主要目的是提供一种传输URL的方法，以便蓝牙低功耗扫描仪设备检测和发现它，然后BLE设备将连接收到并为用户显示正确的网页。BLE信标发送Eddystone-URL资源，智能手机等移动设备在检测到信标数据后立即在浏览器中自动打开网址。同时该框架提供类似于Eddystone-UID的功率校准功能。
#### TLM
Eddystone-TML 框架的主要是提供关于Eddystone的健康状况的完整报告。当前温度, 当前电池电量, 正常运行时间 (信标已通电的秒数), 和 PduCount (信标在最后一次供电后部署的广告数据包的数量).
#### EID
这是负责小工具安全和隐私的框架。


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
