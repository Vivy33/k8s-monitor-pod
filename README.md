# k8s-monitor-pod
可视化的k8s pod监控

1. 性能分析需要监控的 Pod 指标
--资源使用指标--
-CPU 使用率：Pod 的 CPU 使用量（实时值和平均值）
-内存使用率：Pod 的内存使用量（实时值和平均值）
-内存使用率（百分比）：Pod 的内存使用量占分配内存的百分比
-网络流量：Pod 的网络接收和发送速率（如每秒接收/发送的字节数）
-磁盘 I/O：Pod 的磁盘读写速率（如每秒读写字节数）

--Pod 状态指标--
启动时间：Pod 的启动时间戳
运行状态：Pod 是否处于运行状态（Running、Pending、Failed 等）
重启次数：Pod 的重启次数
存活时间：Pod 从启动到当前的存活时间

2. 数据采集方式：Prometheus

3. 数据存储：本地存储
由于不需要长期存储，Prometheus 的本地存储功能可以满足需求
Prometheus 会将采集到的指标数据存储在本地磁盘中，并通过内存缓存来提高查询性能

4. 可视化工具：Grafana

5. 报警机制：邮件
可以通过 Prometheus 的 Alertmanager 配置邮件告警
当监控指标超过设定的阈值时，Alertmanager 会触发告警并通过邮件通知管理员

6. 用户权限：默认管理员

7. 多集群监控

----------------------------------------------------------------------------------

项目架构设计
基于 Prometheus 和 Grafana 的 Kubernetes Pod 监控系统的架构设计：

架构图
+-------------------+       +-------------------+       +-------------------+
|                   |       |                   |       |                   |
|  Kubernetes       |<----->|  Prometheus       |<----->|  Grafana          |
|  Cluster          |       |  (数据采集与存储) |       |  (可视化与告警)   |
|                   |       |                   |       |                   |
+-------------------+       +-------------------+       +-------------------+

组件说明
1. Kubernetes Cluster：
运行 Kubernetes 应用程序的集群
配置 Prometheus 的 ServiceMonitor，以便 Prometheus 自动发现 Pod 和服务

2. Prometheus：
负责采集 Kubernetes 集群中的 Pod 指标
将采集到的指标数据存储在本地磁盘中
配置告警规则，当指标超过阈值时触发告警

3. Grafana：
从 Prometheus 中获取监控数据
创建仪表盘，展示 Pod 的性能指标
配置告警通知，通过邮件发送告警信息

----------------------------------------------------------------------------------

项目部署
1. 安装 Kubernetes 集群

2. 在 Kubernetes 集群中部署 Prometheus
- 配置 Prometheus 的告警规则
- 配置 Alertmanager 以发送邮件告警

3. 在 Kubernetes 集群中部署 Grafana
- 配置 Grafana 数据源
- 创建 Grafana 仪表盘
- 配置 Grafana 告警
