---
title: Kubernetes 群集上连接到 SQL Server Always On 可用性组
description: 此文章介绍了如何连接到 Alwayson 可用性组
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d13f89a1297d21c882075821a681886dc95c4c76
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049587"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>连接到 SQL Server Alwayson 可用性组在 Kubernetes 上

若要连接到 SQL Server 实例上的 Kubernetes 群集的容器中，创建[负载平衡器服务](http://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 负载均衡器将转发到 pod 正在运行的 SQL Server 实例的 IP 地址的请求。

若要连接到可用性组副本，请创建另一副本类型的服务。 您所见的不同类型的副本中的服务示例[sql server 示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)。

* `ag1-primary` 指向主副本。
* `ag1-secondary-sync` 指向以同步辅助副本。
* `ag1-secondary-async` 指向以异步辅助副本。

如果存在多个相同类型的辅助副本，Kubernetes 会将你的连接路由到以轮循机制方式的不同副本。

## <a name="create-a-load-balancer-service"></a>创建负载平衡器服务

若要创建主副本的负载均衡器服务，请将复制`ag1-primary.yaml`从[sql server 示例]()和更新可用性组。

以下命令适用于你的群集的.yaml 文件：

```kubectl
kubectl apply -f ag1-primary.yaml
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>为负载均衡器服务获取的 IP 地址

若要获取负载均衡器服务的负载均衡器 IP 地址，请运行

```kubectl
kubectl get services
```

标识你想要连接到该服务的 IP 地址。

## <a name="connect-to-primary-replica"></a>连接到主副本

若要连接到 SQL 身份验证的主副本，请使用`sa`帐户、 的值为`sapassword`从所创建的机密和此 IP 地址。

例如：

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>后续步骤

[管理 Kubernetes 群集上的 SQL Server 可用性组](sql-server-linux-kubernetes-manage.md)

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)