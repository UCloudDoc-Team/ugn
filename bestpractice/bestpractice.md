1. # 最佳实践

云联网的典型使用场景如下：

- VPC与VPC之间高速稳定的内网互联，例如：
  - 在线教育/在线直播行业的多地域业务部署，要求音视频系统实时同步
  - 游戏加速行业要求多地域内网互联，实现高速稳定的互通互访
  - 业务多地部署，要求实现多地域容灾

## 案例说明

某企业用户在广州、香港、洛杉矶设有办公室，并将部分业务放置在优刻得云上，需要将此三个地域的云上业务打通，以便统一管理。下面介绍详细操作步骤：

### 开通前检查

1. 确认广州、香港、洛杉矶三个可用区已有VPC实例，在“项目一”分别为“VPC-GZ”、“VPC-HK”、“VPC-LA”
2. 业务涉及跨境，确认已经完成跨境申请，详见**[跨境专线合规检查](https://docs.ucloud.cn/crossborder/README)**
3. 规划互通网段，确保网段之间没有重叠

### **步骤一：创建云联网实例并关联实例**

1. 进入控制台云联网管理界面

在控制台上点击【全部产品】--【网络】--【云联网】--【云联网实例】TAB页；

1. 新建云联网实例

点击【创建云联网实例】，输入“实例名称”，点击【确认】

### **步骤二：关联网络实例**

关联网络实例可以在创建云联网实例时同步完成，也可稍后进入网络实例页面进行关联

1. 在创建【创建云联网实例】界面下方关联网络实例，点击【确认】即可完成创建；
2. 在云联网实例管理界面点击【管理云联网】，选择并进入“网络实例”TAB页；

点击【关联网络实例】，选择待关联网络实例的“所属项目”、“地域”和“网络实例类型”，选中要关联的网络实例，【确认】即可；

| 配置项       | 说明                 | 配置                           |
| ------------ | -------------------- | ------------------------------ |
| 项目         | 选择关联实例所属项目 | 项目一                         |
| 地域         | 选择关联实例所属地域 | 分别选择广州、香港、洛杉矶     |
| 网络实例类型 | 选择关联实例类型     | 选择私有网络VPC                |
| 网络实例     | 选择关联的网络实例   | 分别选择VPC-GZ、VPC-HK、VPC-LA |

### **步骤三：检查路由表**

在云联网实例管理界面点击【管理云联网】，选择并进入“路由表”TAB页，该页面上会展示出相关的路由表信息，确认无误即可。

### **步骤四：创建并绑定带宽包**

在云联网实例管理界面点击【管理云联网】，选择并进入“带宽包”TAB页，点击【购买带宽包】，购买广州-香港、香港-洛杉矶、洛杉矶-香港互通带宽包。

| 配置项               | 说明                                                         | 配置                                                         |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 带宽包名称           | 填写带宽包名称                                               | 自定义名称                                                   |
| 计费方式             | 选择带宽包计费方式，分为固定带宽预付费，和第五峰值后付费两种模式 | 按需选择付费类型                                             |
| 带宽包类型及互通地域 | 选择带宽包类型，根据带宽包类型可选对应地域                   | 分别选择跨境-广州 ⇌香港、香港 ⇌洛杉矶                        |
| 带宽类型             | 选择带宽上下行限速方式和限速值                               | 按需填写限速方式和上限带宽值。目前除广州-香港外，其余线路限速方式均为对称限速，广州-香港非对称出口比例5:1 |
| 智能路径             | 选择跨域路径类型                                             | 目前默认通用线路                                             |
| 服务质量             | 选择带宽包服务等级，从高到低依次是钻石，铂金，黄金           | 按需选择服务等级                                             |

配置完成可预览账单金额，确认无误点击【立即购买】，即可完成带宽包购买。

### **步骤五：连通性验证**

在两端的网络实例下各创建一个资源实例，并彼此互ping，如果ping通，则连通性正常；反之，则连通性异常；
