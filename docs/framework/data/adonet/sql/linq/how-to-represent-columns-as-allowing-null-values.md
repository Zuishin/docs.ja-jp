---
description: '詳細情報: 方法:null 値を許可する列として列を表す'
title: '方法: null 値を許可する列として列を表す'
ms.date: 03/30/2017
ms.assetid: ebb71a37-1f4c-4fa7-b2d2-d903f13c4af1
ms.openlocfilehash: 019affd13fa9c2629c6a0ec66c42f19842a4d824
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695906"
---
# <a name="how-to-represent-columns-as-allowing-null-values"></a>方法: null 値を許可する列として列を表す

データベース列が null 値を保持できることを指定するには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性の <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> プロパティを使用します。  
  
 コード例については、「<xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A>」を参照してください。  
  
### <a name="to-designate-a-column-as-allowing-null-values"></a>null 値を許可する列を指定するには  
  
1. <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> 属性に <xref:System.Data.Linq.Mapping.ColumnAttribute> プロパティを追加します。  
  
2. <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> プロパティ値を `true` に設定します。  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
