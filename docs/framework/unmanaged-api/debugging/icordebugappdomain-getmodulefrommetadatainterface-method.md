---
description: '詳細については、次のページを参照してください: いいね。:、GetModuleFromMetaDataInterface メソッド'
title: ICorDebugAppDomain::GetModuleFromMetaDataInterface メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetModuleFromMetaDataInterface
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetModuleFromMetaDataInterface
helpviewer_keywords:
- ICorDebugAppDomain::GetModuleFromMetaDatainterface method [.NET Framework debugging]
- GetModuleFromMetaDatainterface method [.NET Framework debugging]
ms.assetid: f35225b3-5dda-4d5a-913d-b3373e9ab81e
topic_type:
- apiref
ms.openlocfilehash: 7b0c74bd04024f9f4bf26b5ee8abe18a3a7059e7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754239"
---
# <a name="icordebugappdomaingetmodulefrommetadatainterface-method"></a>ICorDebugAppDomain::GetModuleFromMetaDataInterface メソッド

指定されたメタデータインターフェイスに対応するモジュールを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetModuleFromMetaDataInterface (  
    [in] IUnknown           *pIMetaData,  
    [out] ICorDebugModule  **ppModule  
);  
```  
  
## <a name="parameters"></a>パラメーター  

 `pIMetaData`  
 から [メタデータインターフェイス](../metadata/metadata-interfaces.md)の1つであるオブジェクトへのポインター。  
  
 `ppModule`  
 入出力指定されたメタデータインターフェイスに対応するモジュールを表す、モジュールオブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>要件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
