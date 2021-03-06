---
description: '詳細について: ICorProfilerInfo3:: GetFunctionLeave3Info メソッド'
title: ICorProfilerInfo3::GetFunctionLeave3Info メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetFunctionLeave3Info Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetFunctionLeave3Info
helpviewer_keywords:
- GetFunctionLeave3Info method [.NET Framework profiling]
- ICorProfilerInfo3::GetFunctionLeave3Info method [.NET Framework profiling]
ms.assetid: df7083d2-fd43-44c7-9ce5-912c25cef0ff
topic_type:
- apiref
ms.openlocfilehash: 3031190a3603bedb3f58e7a86747542831c72291
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646795"
---
# <a name="icorprofilerinfo3getfunctionleave3info-method"></a>ICorProfilerInfo3::GetFunctionLeave3Info メソッド

[FunctionLeave3WithInfo function](functionleave3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームと戻り値を提供します。 このメソッドは、`FunctionLeave3WithInfo` コールバック中にのみ呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunctionLeave3Info(  
            [in]  FunctionID functionId,  
            [in]  COR_PRF_ELT_INFO eltInfo,  
            [out] COR_PRF_FRAME_INFO *pFrameInfo,  
            [out] COR_PRF_FUNCTION_ARGUMENT_RANGE *pRetvalRange);  
```  
  
## <a name="parameters"></a>パラメーター  

 `functionId`  
 からを `FunctionID` 返す関数の。  
  
 `eltInfo`  
 [in] 特定のスタック フレームに関する情報を表す不透明ハンドル。 プロファイラーは、 `eltInfo` [FunctionLeave3WithInfo](functionleave3withinfo-function.md) 関数によってプロファイラーに与えられたものと同じを提供する必要があります。  
  
 `pFrameInfo`  
 [out] 特定のスタック フレームに関するジェネリック情報を表す不透明ハンドル。 このハンドルは、プロファイラーが `FunctionLeave3WithInfo` メソッドを呼び出した `GetFunctionLeave3Info` コールバック内でのみ有効です。  
  
 `pRetvalRange`  
 入出力関数から返される値を格納している [COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md) 構造体へのポインター。 戻り値の情報にアクセスするには、 `COR_PRF_ENABLE_FUNCTION_RETVAL` フラグを設定する必要があります。 プロファイラーは、 [ICorProfilerInfo:: SetEventMask メソッド](icorprofilerinfo-seteventmask-method.md) を使用してイベントフラグを設定できます。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
