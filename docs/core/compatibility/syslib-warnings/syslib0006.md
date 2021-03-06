---
title: SYSLIB0006 警告
description: コンパイル時の警告 SYSLIB0006 が生成される旧型式について説明します。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: c1eecade9280ac37917bc24aa2973756c7f08d87
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596303"
---
# <a name="syslib0006-threadabort-is-not-supported"></a>SYSLIB0006: Thread.Abort はサポート対象外

.NET 5.0 以降、次の API は古いものとしてマークされています。 これらの API を使用すると、コンパイル時に警告 `SYSLIB0006` が生成されます。

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workarounds"></a>回避策

<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> を呼び出す代わりに、<xref:System.Threading.CancellationToken> を使用して作業単位の処理を中止します。 次の例は、<xref:System.Threading.CancellationToken>の使用方法を示しています。

```csharp
void ProcessPendingWorkItemsNew(CancellationToken cancellationToken)
{
    if (QueryIsMoreWorkPending())
    {
        // If the CancellationToken is marked as "needs to cancel",
        // this will throw the appropriate exception.
        cancellationToken.ThrowIfCancellationRequested();

        WorkItem work = DequeueWorkItem();
        ProcessWorkItem(work);
    }
}
```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>関連項目

- [Thread.Abort は古い形式です](../core-libraries/5.0/thread-abort-obsolete.md)
- [マネージド スレッドのキャンセル](../../../standard/threading/cancellation-in-managed-threads.md)
