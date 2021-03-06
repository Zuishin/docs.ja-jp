---
description: '詳細について: ICorProfilerInfo2:: EnumModuleFrozenObjects メソッド'
title: ICorProfilerInfo2::EnumModuleFrozenObjects メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.EnumModuleFrozenObjects
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::EnumModuleFrozenObjects
helpviewer_keywords:
- EnumModuleFrozenObjects method [.NET Framework profiling]
- ICorProfilerInfo2::EnumModuleFrozenObjects method [.NET Framework profiling]
ms.assetid: 920b6483-7064-4d64-8613-fcc38ccf9b1e
topic_type:
- apiref
ms.openlocfilehash: b68571544c00c8c234a73404a95433e91f0cfdcf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753212"
---
# <a name="icorprofilerinfo2enummodulefrozenobjects-method"></a>ICorProfilerInfo2::EnumModuleFrozenObjects メソッド

指定したモジュール内の固定されたオブジェクトを反復処理できる列挙子を取得します。このメソッドは互換性のために残されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumModuleFrozenObjects(  
    [in] ModuleID moduleID,  
    [out] ICorProfilerObjectEnum** ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  

 `moduleID`  
 から列挙される固定オブジェクトを含むモジュールの ID。  
  
 `ppEnum`  
 入出力固定されたオブジェクトを列挙する [ICorProfilerObjectEnum](icorprofilerobjectenum-interface.md) インターフェイスのアドレスへのポインター。  
  
## <a name="requirements"></a>要件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 3.5、3.0 SP1、3.0、2.0 SP1、2.0  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
