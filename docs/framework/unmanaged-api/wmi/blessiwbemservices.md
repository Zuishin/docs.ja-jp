---
title: BlessIWbemServices 関数 (アンマネージ API リファレンス)
description: BlessIWbemServices 関数は、ユーザー資格情報が IWbemServices クラスへのアクセスを許可しているかどうかを示します。
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 43ef617ee754c9dcd661b31abba6b17434563c22
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708154"
---
# <a name="blessiwbemservices-function"></a>BlessIWbemServices 関数

ユーザー資格情報が、指定された [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) クラスへのアクセスを許可するかどうかを示します。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>パラメーター

`pIWbemServices`\
から権限が必要な [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) オブジェクトへのポインター。

`strUser`\
からユーザー名。

`strPassword`\
からに関連付けられているパスワード `strUser` 。

`strAuthority`\
からユーザーのドメイン名。 詳細については、「 [Connectserverwmi](connectserverwmi.md) 関数」を参照してください。

`impLevel`\
から偽装レベル。

`authnLevel`\
から承認レベル。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は、 *winerror.h* ヘッダーファイルで定義されています。また、コード内で定数として定義することもできます。

|定数  |値  |説明  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | 1 つ以上の引数が無効です。 |
| `E_POINTER` | 0x80004003 | `pIWbemServices` が `null`です。 |
| `E_FAIL` | 0x80000008 | 特定できないエラーが発生しました。 |
| `E_OUTOFMEMORY` | 0x80000002 | 操作を実行するのに十分なメモリがありません。 |
| `S_OK` | 0 | 関数の呼び出しに成功しました。 |

## <a name="requirements"></a>要件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils .idl  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
