---
title: '軽減策: XML スキーマ検証'
description: .NET Framework 4.6 では、複合キーが使用され、1 つのキーが空の場合、XSD スキーマ検証によって一意制約の違反が検出されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b73dd4f4-f2dc-47a2-9425-3896e92321fb
ms.openlocfilehash: 0744a703c1e9dc35a8accc448d34f1a736e77e4d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253532"
---
# <a name="mitigation-xml-schema-validation"></a>軽減策:XML スキーマ検証

.NET Framework 4.6 では、複合キーが使用され、1 つのキーが空の場合、XSD スキーマ検証で一意制約の違反が検出されます。  
  
## <a name="impact"></a>影響  

 この変更の影響は最小限のものになります。スキーマの仕様に基づき、複合キーが空のキーと共に使用されて `xsd:unique` の違反が発生した場合、スキーマの検証エラーの発生が予期されます。  
  
## <a name="mitigation"></a>軽減策  

 複合キーに空の 1 つのキーがある場合にスキーマ検証エラーが検出されるようにするかどうかは、構成可能な機能です。  
  
- .NET Framework 4.6 以降を対象とするアプリでは、スキーマ検証エラーの検出が既定で有効になっていますが、この動作を無効にして、スキーマ検証エラーが検出されないようにすることも可能です。  
  
- .NET Framework 4.6 の下で実行されているものの、.NET Framework 4.5.2 以前のバージョンを対象とするアプリでは、既定ではスキーマ検証エラーが検出されませんが、この動作を有効にして、スキーマ検証エラーが検出されるようにすることも可能です。  
  
 この動作は、<xref:System.AppContext> クラスを使用して `System.Xml.IgnoreEmptyKeySequences` スイッチの値を定義することにより構成できます。 スイッチの既定値が `false` (空のキー シーケンスが無視されない) であるため、.NET Framework 4.6 を対象とするアプリは、以下のコードを使用してスイッチの値を `true` に設定することにより、その動作を無効にすることができます。  
  
 [!code-csharp[AppCompat.IgnoreEmptyKeySequences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/cs/program.cs#1)]
 [!code-vb[AppCompat.IgnoreEmptyKeySequences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/vb/module1.vb#1)]  
  
 .NET Framework 4.5.2 以前のバージョンを対象とするアプリでは、スイッチの既定値が `true` (空のキー シーケンスが無視される) であるため、以下のコードを使用してスイッチの値を `false` に設定することにより、複合キーに空のキーがある場合にスキーマ検証エラーを生成させることが可能です。  
  
 [!code-csharp[AppCompat.IgnoreEmptyKeySequences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/cs/program.cs#2)]
 [!code-vb[AppCompat.IgnoreEmptyKeySequences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/vb/module1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [アプリケーションの互換性](application-compatibility.md)
