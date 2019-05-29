# NFV 测试方法

测试内容

* VNF 生命周期
* VNF 数据和控制层基准测试

### 传统测试方法

#### 使用物理测试端点的测试方法

* 数据层验证
* 控制层一致性和扩展能力测试
* 管理层验证

## 虚拟化测试解决方案

虚拟化测试解决方案 （测试 VNF）是一种运行在基于x86商用市售服务器上的纯软件产品。这些测试 VNF 可在基于监视程序或容器的 NFVI 上执行，并用于验证其他的 VNF、NFVI 组件、NFV MANO 和 E2E 网络服务。与对应的物理组件一样，测试 VNF 可包围被测 VNF 或 NFVI，发起用户层和控制层流量，并验证接收到的流量是否与协议标准和预期的服务水平协议（SLA）保持一致。

## ETSI 测试标准

* ETSI GR NFV-TST 004
  * Latency Measurements
    * The Latency measurements reported here are Round-Trip Time (RTT) measured using the simple ICMP Echo Request/Reply supported in ping tools.
* 

