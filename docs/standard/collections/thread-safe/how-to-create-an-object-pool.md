---
title: 使用 ConcurrentBag 创建目标池
ms.date: 05/01/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: 2c060dc901f8d06a5f9c51db1cd563cb28e4fda3
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728476"
---
# <a name="create-an-object-pool-by-using-a-concurrentbag"></a>使用 ConcurrentBag 创建目标池

本示例演示如何使用 <xref:System.Collections.Concurrent.ConcurrentBag%601> 来实现对象池。 在需要某个类的多个实例并且创建或销毁该类的成本很高的情况下，对象池可以改进应用程序性能。 客户端程序请求新对象时，对象池先尝试提供一个已创建并返回到该池的对象。 仅在没有可用对象时，才会创建一个新对象。

<xref:System.Collections.Concurrent.ConcurrentBag%601> 用于存储对象，因为它支持快速插入和删除，特别是在同一线程既添加又删除项时。 本示例可进一步扩充为以包数据结构实现的 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> 为依据生成，就像 <xref:System.Collections.Concurrent.ConcurrentQueue%601> 和 <xref:System.Collections.Concurrent.ConcurrentStack%601> 一样。

> [!TIP]
> 本文定义了如何使用底层并发类型编写你自己的对象池实现以存储要重用的对象。 但是，<xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> 命名空间下已存在 <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> 类型。 在创建你自己的实现前，考虑使用可用类型，其中包括许多其他功能。

## <a name="example"></a>示例

[!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
[!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]

## <a name="see-also"></a>请参阅

- [线程安全集合](../../../../docs/standard/collections/thread-safe/index.md)
