# 修订记录
<table border="1" width="100%">
<tr>
<th bgcolor="#EEEEEE">修订版本</th>
<th width="70%" bgcolor="#EEEEEE">修订摘要</th>
<th bgcolor="#EEEEEE">修订日期</th>
<th bgcolor="#EEEEEE">修订人</th>
</tr>
<tr>
<td align="center">V0.0.9</td>
<td>1. 初稿编写。</td>
<td align="center">2013/12/23</td>
<td align="center">唐成</td>
</tr>
</table>

# 软件需求规格说明书

# 1. 文档概述

---

## 1.1. 目的  

本需求规格说明书对整个基础型网络摄像机的软件规格进行说明，主要包括网络摄像机设备固件以及PC端工具两部分。通过对该系统的规格进行详细的描述，对后续的设计与编码工作提供指导。

## 1.2. 范围

本文档的描述范围包含基础型网络摄像机内部功能和对外接口，以及使用这些接口来实现功能的PC端工具。本文档还会涉及基础型网络摄像机所必须遵循的一些标准。

## 1.3. 定义、首字母缩写词和缩略语

<table border="1" width="100%">
<tr>
<th width="15%" bgcolor="#EEEEEE">缩写</th>
<th width="30%" bgcolor="#EEEEEE">全称</th>
<th bgcolor="#EEEEEE">说明</th>
</tr>

<tr>
<td align="center">IPC</td>
<td align="center">IP Camera</td>
<td>网络摄像机</td>
</tr>

<tr>
<td align="center">PTZ</td>
<td align="center">Pan/Tilt/Zoom</td>
<td>代表云台全方位的移动以及镜头变倍变焦</td>
</tr>

</table>

## 1.4. 参考资料


## 1.5. 概述

* 第2章，将对基础型网络摄像机的整体业务流程进行详细的说明，通过描述完整的业务用例从而得到领域模型和系统用例。  
* 第3章，从系统用例进一步推导出功能需求，包含用例、活动和时序，此为后续设计之基石。  
* 第4章，提出基础型网络摄像机浏览器用户界面的观感要求。  
* 第5章，提出基础型网络摄像机浏览器用户界面的操作要求。  
* 第6章，提出软件的性能要求，从速度、精度、安全性和可靠性几个方面进行约束。  
* 第7章，提出环境要求，对软件运行的软、硬件环境进行约束。  
* 第8章，提出可维护性和可移植性的要求。  
* 第9章，提出政策和法规方面的要求，包括针对社会和政策的因素的规格说明，这些因素会影响产品的可接受性。  
* 第10章，提出法律需求，明确待开发软是否受到某些法律管制，是否需要符合某些标准。  
* 第11章，描述To be defined问题，还未明确但确实会对软件产生影响的问题。
* 第12章，描述成本问题，考虑是否可以购买某些成熟的商业模组，或者使用成熟的开源模组，以及是否存在可被复制的产品。  
* 第13章，描述软件产品是否对已有的环境和系统产生何种影响，考虑软件产品是否会带来新的问题。  
* 第14章，描述需要跟随产品发布的用户文档。  
* 第15章，描述软件产品将来的发展方向和待实现的功能。
* 第16章，支持信息，包含附录、索引等。

# 2. 整体说明

---
IPC最为核心和基础的功能，莫过于将感光元件采集到的光学数字信号经过编码，组帧之后通过IP数字网络传输到监控终端或者存储服务器。在此基础之上，提供其它的一些帮助用户更好更方便使用IPC的辅助功能，例如用户管理、参数配置、固件升级等。

## 2.1. 产品的用户

### 2.1.1. 产品的用户

* IPC操作者

### 2.1.2. 对用户设的优先级

* 关键用户：IPC操作者

## 2.2. 用例模型

### 2.2.1. IPC业务用例
![alt text "IPC业务用例"](pics/buc.png "IPC业务用例")

### 2.2.2. IPC业务用例描述

#### 2.2.2.1. 搜索设备
|用例编号|UC01|
|:-----:|:---|
|用例名称|搜索设备|
|前置条件|无|
|后置条件|响应搜索消息。|
|用例说明|用户通过搜索工具在局域网内搜索设备，被搜索的设备需要响应搜索消息，使得设备可被发现和管理。|

#### 2.2.2.2. 配置参数
|用例编号|UC02|
|:-----:|:---|
|用例名称|配置参数|
|前置条件|无|
|后置条件|新参数正确保存，可以立即生效的参数要立即生效。|
|用例说明|用户通过设备配置界面能够查看和修改设备运行参数，非必要情况下，参数修改后应能立即生效，不需重启设备。|

#### 2.2.2.3. 预览图像
|用例编号|UC03|
|:-----:|:---|
|用例名称|预览图像|
|前置条件|无|
|后置条件|用户从客户端看到正确播放的视频图像。|
|用例说明|用户能够取得正确的视频url，通过此url能够连接到设备并取得正确的网络视频流。|

#### 2.2.2.4. 软件升级
|用例编号|UC04|
|:-----:|:---|
|用例名称|软件升级|
|前置条件|无|
|后置条件|新版本软件运行正常。|
|用例说明|用户可以通过上传新版本软件和指定升级服务器两种方式对设备进行软件升级，待升级的软件能够进行校验，以防止错误的文件被写入导致设备无法运行。|

#### 2.2.2.5. 查询运行日志
|用例编号|UC05|
|:-----:|:---|
|用例名称|查询运行日志|
|前置条件|无|
|后置条件|取得运行日志列表。|
|用例说明|用户可以查询一段时间内的运行日志。|

#### 2.2.2.6. 查询调试日志
|用例编号|UC06|
|:-----:|:---|
|用例名称|查询调试日志|
|前置条件|记录调试日志功能开启。|
|后置条件|去的调试日志列表。|
|用例说明|开发人员可以打开、查询、关闭调试日志。|

#### 2.2.2.7. 量产
|用例编号|UC07|
|:-----:|:---|
|用例名称|量产|
|前置条件|无|
|后置条件|量产设备信息正确记录管理。|
|用例说明|开发人员通过量产工具为设备写入MAC地址和序列号，并且将其与客户信息绑定后记录至数据库。|

#### 2.2.2.8. 老化
|用例编号|UC08|
|:-----:|:---|
|用例名称|老化|
|前置条件|无|
|后置条件|老化记录可被查询。|
|用例说明|老化工具应能自动记录老化过程中的异常状况。|

#### 2.2.2.9. 开启调试功能
|用例编号|UC09|
|:-----:|:---|
|用例名称|开启调试功能|
|前置条件|无|
|后置条件|调试功能开启。|
|用例说明|通过开启调试功能，设备可远程登录且运行过程中会自己调试日志。|


## 2.3. 假设与依赖关系

### 2.3.1. 技术可行性假设

#### 2.3.1.1. 视频流

为了使得用户能够使用绝大多数的通用播放器即能预览设备之画面，设备之视频数据流需要符合以下规范：

* H.264标准
* RTSP协议（[RFC2326](http：//www.rfc-editor.org/rfc/rfc2326.txt)）

通过预研，目前市面上的解决方案基本都通过硬件编码的形式支持标准的H.264编码格式（Baseline/Main Profile/High Profile)。传输层面，通过开源项目[Live555](www.live555.com)可以实现符合标准的RTSP传输。因此视频数据流的RTSP传输是可行的。

#### 2.3.1.2. 对外接口

现有的市场上，[Onvif](http://www.onvif.org)协议与~~[GB/T 28181-2011](http://about:blank)协议~~越来越占据主导地位，从目前的预研看来，通过[gSoap](http://www.cs.fsu.edu/~engelen/soap.html)来实现Onvif也是可行的。

同时，还需要私有化的接口以便提供一些标准未定义的功能调用，通过[FastCGI](www.fastcgi.com)来提供[JSON](http://www.json.org)格式的API是可行的。为此，还需要用到C语言的Json库——[YAJL](http://lloyd.github.io/yajl)。

网络设备的默认规则之一，就是需要提供一个简单的可使用其基础功能的Web界面，那么必不可少的就是要内置一个Web Server，考虑到嵌入式设备的资源有限，[Lighttpd](http://www.lighttpd.net)可以作为首选。其提供的自定义Plugin开发框架，能够满足开发上的灵活性，同时资源消耗又极小。

#### 2.3.1.3. 内部通信

设备内部，各个模块之间需要通信的桥梁，而单纯的Posix IPC或者System V IPC太过于底层，不利于开发，因此使用现代新型的Message Queue就势在必行，经过研究对比，[ØMQ](http://zeromq.org)能够很好的胜任。

#### 2.3.1.4. 开发语言

基于设备资源有限性与性能的考虑，整个系统框架基于C语言来编写，为了便于实现面向对象之设计，所有的程序尽量构建于[GObject](https://developer.gnome.org/gobject/stable)之上。如某个模块所使用之开源代码基于其它语言，则不受此限制。

### 2.3.2. 依赖关系

结合2.3.1所述，整个系统依赖以下开源模块：

* [Linux Kernel](http://kernel.org)
* 硬件厂商之驱动
    * Hi3518 Drivers
* [GObject](https://developer.gnome.org/gobject/stable)
* [ØMQ](http://zeromq.org)
* [Lighttpd](http://www.lighttpd.net)
* [Live555](www.live555.com)
* [gSoap](http://www.cs.fsu.edu/~engelen/soap.html)
* [YAJL](http://lloyd.github.io/yajl)

# 3. 功能需求

---

## 3.1. [UC01]搜索设备
### 3.1.1. 特征信息
#### 3.1.1.1. 用例在系统中的目标

IPC使用者通过搜索工具在局域网内搜索，每个在网的IPC响应自身的IP地址和MAC地址给到搜索工具；搜索工具收到响应后，查询其序列号、设备名称、备注信息、网络掩码、网关地址和软件版本。搜索工具将上述信息条目化后展示给IPC使用者。  
只要运行搜索工具的电脑与IPC处于同一个物理局域网内（不存在广播过滤节点），无论是否在一个子网，都要能够搜索到IPC。

#### 3.1.1.2. 范围

IPC及其搜索工具

#### 3.1.1.3. 级别(概要任务/首要任务/子功能)

概要任务

#### 3.1.1.4. 前置条件(用例执行前系统应具有的状态)

* IPC网络设备处于正常运行状态，具备合法的网络地址。

#### 3.1.1.5. 成功后置条件(用例成功执行后应具有的状态)

* 搜索工具列出搜索到的IPC及其相关信息。
* 可以通过搜索工具对IPC的部分参数进行配置
	* IP地址、掩码地址和网关地址修改
	* 软件版本升级
	* 产品调试功能开启（高级版本）
	* 产品高级功能开启（高级版本）

#### 3.1.1.6. 失效后置条件(用例没有完成目标的状态)

无

#### 3.1.1.7. 首要角色(与该用例关联的首要角色)

+ 搜索工具

#### 3.1.1.8. 触发(启动该用例执行的系列动作)

用户试用搜索工具搜索IPC。

### 3.1.2. 主要步骤
![alt text "搜索设备主要步骤"](pics/搜索设备顺序图.png "搜索设备顺序图")

### 3.1.3. 扩展

无

## 3.2. [UC02]配置参数
### 3.2.1. 特征信息
#### 3.2.1.1. 用例在系统中的目标

用户通过搜索工具或者IPC提供的界面对IPC的运行参数进行修改，修改后的参数应能立即生效，尽量避免需要重启IPC的情况出现。

搜索工具可配置的参数有

* IP地址
* 子网掩码
* 网关

界面可配置的参数有

+ 设备信息
	+ 设备名称
	+ 备注信息
+ OSD显示设置
	+ 各项是否显示
	+ 各项的字体大小
	+ 各项的左上角点坐标（以像素为单位）
	+ 各项的颜色
+ 视频设置
	+ 视频编码级别（Baseline/Main profile）
	+ 视频垂直和左右翻转
	+ 视频质量（高、中、低）
	+ 视频帧率（1 ~ 30fps）
	+ 视频码率（CBR、VBR）
+ 场景设置
	+ 50Hz
	+ 60Hz
	+ 混合模式
+ 网络地址和端口
    + DHCP
    + 静态地址
    + PPPoE
    + Http端口
    + Rtsp端口
    + Rtp端口
    + Onvif端口
+ 时间和日期
    + 指定日期时间
    + NTP自动同步
+ 用户
    + 管理员
    + 来宾


#### 3.2.1.2. 范围

IPC及其搜索工具

#### 3.2.1.3. 级别(概要任务/首要任务/子功能)

概要任务

#### 3.2.1.4. 前置条件(用例执行前系统应具有的状态)

* IPC网络设备处于正常运行状态，具备合法的网络地址。

#### 3.2.1.5. 成功后置条件(用例成功执行后应具有的状态)

+ IPC按照修改后的参数运行
+ 向搜索工具或者界面给出配置成功的应答

#### 3.2.1.6. 失效后置条件(用例没有完成目标的状态)

+ IPC按照修改前的参数运行
+ 向搜索工具或者界面给出配置失败的应答

#### 3.2.1.7. 首要角色(与该用例关联的首要角色)

* 搜索工具
* 用户

#### 3.2.1.8. 触发(启动该用例执行的系列动作)

用户通过搜索工具或者界面进行配置操作。

### 3.2.2. 主要步骤
![alt text "配置参数主要步骤"](pics/配置参数顺序图.png "配置参数顺序图")

### 3.2.3. 扩展

无


# 4. 观感需求

---
<font color="blue">
*一些与产品的用户界面相关的需求描述。*  
</font>

# 5. 易用性需求

---

## 5.1. 易于使用

<font color="blue">
*描述如何构建符合最终用户期望的产品。*  
</font>

## 5.2. 学习的容易程度

<font color="blue">
*学习使用该产品应该多容易的说明。通常是用学习时间来衡量。*  
</font>

# 6. 性能要求

---

## 6.1. 速度需求

<font color="blue">
*明确完成特定任务需要的时间，这常常指响应时间。*  
</font>

## 6.2. 安全性的需求

<font color="blue">
*对可能造成人身伤害、财产损失和环境破坏所考虑到的风险进行量化描述。*  
</font>

### 6.2.1. 该产品是保密的吗？

<font color="blue">
*关于该被授权使用该产品，以及在什么样的情况下授权等方面的描述。*
</font>

### 6.2.2. 文件完整性需求

<font color="blue">
*关于需要的数据库和其他文件完整性方面的说明。*
</font>

### 6.2.3. 审计需求

<font color="blue">
*关于需要的审计检查方面的说明。*
</font>


## 6.3. 精度需求

<font color="blue">
*对产品产生的结果期望的精度进行量化描述。*
</font>

## 6.4. 可靠性和可用性需求

<font color="blue">
*本节量化产品所需的可靠性。这常常表述为允许的两次失败之间无故障运行时间，或允许的总失败率。*
</font>

## 6.5. 容量需求

<font color="blue">
*本节明确处理的吞吐量和产品存储数据的容量。*
</font>

# 7. 环境需求

---

## 7.1. 预期的物理环境

<font color="blue">
*本节明确产品将操作的物理环境，以及这种环境引起的任何特殊需求。*
</font>

## 7.2. 预期的技术环境

<font color="blue">
*硬件和其它组成新产品操作环境的设备的规范。*
</font>

## 7.3. 伙伴应用程序

<font color="blue">
*对产品必须与之交互的其它应用程序的描述。*
</font>

# 8. 可维护性和可移植性需求

---

## 8.1. 维护该产品需要多容易

<font color="blue">
*对产品作特定修改所需时间的量化描述。*
</font>

## 8.2. 是否存在一些特殊情况适用于该产品的维护

<font color="blue">
*关于预期的产品发布周期和发布将采取的形式的规定。*
</font>

## 8.3. 可移植性需求

<font color="blue">
*对产品必须支持的其他平台或环境的描述。*
</font>

# 9. 文件和政策需求

---

<font color="blue">
*本节包括针对社会和政策的因素的规格说明，这些因素会影响产品的可接受性。如果你开发的产品是针对外国市场的，可能要特别注意这些需求。*  
*问一下是否产品的目标是你所不熟悉的文化环境，是否其它国家的人或其他类型的组织的人会使用该产品。人们是否有与你的文化不同的习惯、节日、迷信、文化上的社会行为规范。*
</font>

# 10. 法律需求

---

## 10.1. 该产品是否受到某些法律的管制

<font color="blue">
*明确该产品的法律需求的描述。*
</font>

## 10.2. 是否有一些必须符合的标准

<font color="blue">
*明确适用的标准和参考的详细标准的描述。*
</font>

# 11. Opend问题

---

<font color="blue">
*对未确定但可能对产品产生重要影响的因素的问题描述。按照需求分析的术语还说，就是TBD（To Be Define）的问题。*
</font>

# 12. COTS解决方案

---

## 12.1. 是否有一些制造好的产品可以购买

<font color="blue">
*应该调查现存产品清单，这些产品可以作为潜在的解决方案。*
</font>

## 12.2. 该产品是否可使用制造好的组件

<font color="blue">
*描述可能用于该产品的候选组件，包括采购的和公司自己的产品。列出来源。*
</font>

## 12.3. 是否有一些我们可以复制的东西

<font color="blue">
*其他相似产品的清单。*
</font>

# 13. 新问题

---

## 13.1. 新产品会在当前环境中带来什么问题

<font color="blue">
*关于新产品将怎样影响当前的实现环境的描述。*
</font>

## 13.2. 新的开发是否将影响某些已实施的系统

<font color="blue">
*关于新产品将怎样与现存系统协同工作的描述。*
</font>

## 13.3. 是否我们现有的用户会受到新开发的敌对性影响

<font color="blue">
*关于现有用户可能产生的敌对性反应的细节。*
</font>

## 13.4. 预期的实现环境会存在什么限制新产品的因素

<font color="blue">
*关于新的自动化技术、新的组织结构方式的任何潜在问题的描述。*
</font>

## 13.5. 是否新产品会带来其他问题

<font color="blue">
*确定我们可能不能处理的情况。*
</font>

# 14. 用户文档

---

<font color="blue">
*用户文档的清单，这些文档将作为产品的一部分交付。*
</font>

# 15. 后续版本的需求

---

<font color="blue">
*一些需要在将来版本实现的需求*
</font>

# 16. 支持信息

---

<font color="blue">
*支持信息用于使软件需求规格说明书更易于使用。它包括：目录、索引、附录等。*
</font>
