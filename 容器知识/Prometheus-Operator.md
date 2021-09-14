# Prometheus-Operator

## 为什么使用?

原生Prometheus不支持分布式，不支持数据导入、导出，不支持通过 API 修改监控目标和报警规则，所以在使用它时，通常需要写脚本和代码来简化操作。

## 做了什么？

1. 提供了简易的方式启动Prometheus实例

2. 可通过K8s资源配置Prometheus的基本信息

3. 可基于k8s label查询自动生成监控目标配置

## 组成结构

Operator根据自定义资源来部署和管理Prometheus Server, 同时监控这些自定义资源事件的变化来做相应的处理，是整个系统的控制中心

- Prometheus由Operator部署的Prometheus Server

- ServiceMonitor描述了一组被Prometheus监控的目标列表，它通过labels来选取对应的service endpoint， 让Prometheus Server通过选取来的Service来获取Metrics信息

- ServicePrometheus的监控对象

- AlertManager

## k8s自定义资源

Prometheus它通过ServiceMonitor底下声明的endpoint来搜集指标，并用指标去匹配通过Rules，当发现rule生效时，通知AlertManager，ServiceMonitor指定了通过什么label来匹配service endpoint，PrometheusRule定义报警规则，定义了多长时间检查什么东西
