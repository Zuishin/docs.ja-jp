---
description: 詳細については、次を参照してください
title: ICorDebugGCReferenceEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugGCReferenceEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGCReferenceEnum
helpviewer_keywords:
- ICorDebugGCReferenceEnum interface [.NET Framework debugging]
ms.assetid: 5f3c91c9-c035-454f-96cc-011cab1ea06b
topic_type:
- apiref
ms.openlocfilehash: ad4a61cdc2b30fb4c8e2be500eae878327c6b449
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801294"
---
# <a name="icordebuggcreferenceenum-interface"></a>ICorDebugGCReferenceEnum インターフェイス

ガベージ コレクトされるオブジェクトの列挙子を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[次のメソッド](icordebuggcreferenceenum-next-method.md)|ガベージコレクトされるオブジェクトに関する情報を格納している、指定した数の [COR_GC_REFERENCE](cor-gc-reference-structure.md) インスタンスを取得します。|  
  
## <a name="remarks"></a>解説  

 `ICorDebugGCReferenceEnum`インターフェイスは、"ICorDebugEnum" インターフェイスを実装します。  
  
 `ICorDebugGCReferenceEnum`インスタンスには、 [ICorDebugProcess5:: EnumerateGCReferences](icordebugprocess5-enumerategcreferences-method.md)メソッドを呼び出すことによって[COR_GC_REFERENCE](cor-gc-reference-structure.md)インスタンスが設定されます。 [COR_GC_REFERENCE](cor-gc-reference-structure.md) オブジェクトは、 [ICorDebugGCReference:: Next](icordebuggcreferenceenum-next-method.md) メソッドを呼び出すことによって列挙できます。  
  
 このメソッドによって設定されるコレクション内の [COR_GC_REFERENCE](cor-gc-reference-structure.md) オブジェクトは、次の3種類のオブジェクトを表します。  
  
- すべてのマネージスタックからのオブジェクト。 これには、マネージコードのライブ参照や、共通言語ランタイムによって作成されたオブジェクトが含まれます。  
  
- ハンドルテーブルのオブジェクト。 これには、モジュール内の厳密な参照 ( `HNDTYPE_STRONG` および `HNDTYPE_REFCOUNT` ) と静的変数が含まれます。  
  
- ファイナライザーキューからのオブジェクト。 ファイナライザーが実行されるまで、ファイナライザーはオブジェクトをキューに置いています。  
  
## <a name="requirements"></a>要件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
