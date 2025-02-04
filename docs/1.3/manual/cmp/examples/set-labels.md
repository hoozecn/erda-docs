# 为节点设置调度标签

进入 **多云管理平台 > 资源管理 > 集群管理 > 选择集群 > 节点列表**，点击列表 **节点** 栏中的 **+** 图标。

## 场景一：将机器资源池按环境进行划分

Erda 将部署环境分为四个：

- 开发环境：development
- 测试环境：test
- 预发环境：staging
- 生产环境：production

以 Erda DevOps 平台为例，分支规则缺省时，对应调度方式如下：

- feature/* 分支的代码通过 CICD 流程会自动部署到开发环境
- develop 分支的代码通过 CICD 流程会自动部署到测试环境
- release/* 分支的代码通过 CICD 流程会自动部署到预发环境
- master 分支的代码通过 CICD 流程会自动部署到生产环境

在多云管理平台可以为节点设置对应的环境标签，以允许 Erda 将对应环境的部署调度到该节点上，如图所示，在分类中选择环境标签后，选择对应环境即可。

![](http://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/09/29/66c7dc3f-ce36-4045-a959-2ecabbef2266.png)

一个节点上可以同时打上四个环境的标签，以此表明这台机器是给四个环境的服务部署共用的。

::: tip K8S 标签值

具体标签对应的真实 K8S 标签值，请参考 [节点标签说明](../guide/cluster/cluster-node-labels.md)。
以给节点打上`开发环境`标签为例，实际上对应的 K8S 标签为`dice/workspace-dev=true`，下述场景类似。

:::

## 场景二：将流水线任务调度到指定机器上

将流水线任务调度到没有业务服务部署的机器上，是一种比较推荐的做法，因为流水线任务大多是一些 IO 密集型任务，运行在有业务服务部署的机器上，可能会影响业务稳定。

可以使用多云管理平台，为节点设置对应的任务标签，来控制流水线任务的调度，如图所示，在分类中选择任务标签后，再选择具体任务类型即可。

![](http://terminus-paas.oss-cn-hangzhou.aliyuncs.com/paas-doc/2021/09/29/7f54d364-c2b9-4cca-9bd8-4dd4242ec367.png)

::: tip 提示

流水线任务类型：

* CICD 任务是在 Erda DevOps 平台中，代码编译、镜像构建以及最终服务部署的流水线任务。

* 大数据任务是在 Erda 快数据平台中，flink 流批处理等数据处理任务。

:::

