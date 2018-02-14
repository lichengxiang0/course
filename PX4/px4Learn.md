# uavcan  

首先了解uavcan协议，在了解协议的用法，看官网的文档  
单词：  
	maintenance:维护，维修  
	specification:规范  
	
## 核心设计目标  
* Democratic network（明主网络）：不应该有主节点。在网络中所有的节点都应该有同样的交流权限，这样就没有单点故障。  
* Node can exchange long payloads(节点可以交换长的有效载荷)：节点必须提供一个简单的方式交换大量的数据结构，这些数据结构不能不能适应单个CAN帧（例如GNSS解决方案，3D向量等）。在隐藏的相关复杂的应用层的协议中，UAVCAN应该表现为自动转换分解和重组。
* Support for redundant interface and redundant nodes(支持冗余接口和冗余节点):这是与相关安全连接应用程序的公共要求。  
* High throughput,low latency communication(高吞吐量，低延迟的通讯):依赖于高频硬实时控制回环的应用程序，需要一个低延迟高吞吐量的交流方式。  
* Simple logic,low computational requirements(简单的逻辑，较低的计算要求):UAVCAN的目标为各种嵌入式系统，包括来自于资源有限的微控制器对于加强数据处理的（例如高性能的linux驱动机）高性能嵌入的机载计算机。后者对需要执行的协议在大量逻辑上施加严格的约束。  
* Common high-level functions should be clearly define(常见的高级功能应该被明确的定义):UAVCAN对于常见的高级功能定义了标准的服务和消息，例如网络发现，节点配置，节点固件更新，节点状态监测（自然生长成车宽的健康监测），全网时间同步，动态节点ID分配（也就是即插即用），等。  
* Open specification and reference implementations(开放的规格和参考实现):UAVCAN的规范是开源和免费的，参考实现是在MIT的许可条款下发布。  


## 规范的更新和审批流程  
UAVCAN开发团队负责推进基于输入用户的规范。这一反馈通过邮件列表收集，对每个用户开放。  
标准数据定义集是规范的基石概念之一（看数据结构描述语言（DSDL））。在同一个主要版本里面，规范只能通过以下方式扩展：  
* 只要默认的数据类型ID与现有的数据类型不冲突，就可以添加一个新的数据类型，可能是默认的数据类型id。  
* 只要修改的数据类型不破坏向后兼容，现有的数据类型就可以 被修改。  
* 现有的数据类型可以被声明成弃用。    
	* 一旦声明成弃用，数据类型将维持至少两年。