---
description: 詳細については、「ICLRPolicyManager インターフェイス」を参照してください。
title: ICLRPolicyManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager
helpviewer_keywords:
- ICLRPolicyManager interface [.NET Framework hosting]
ms.assetid: 5c834aa1-f2db-408a-b230-c7bec093d364
topic_type:
- apiref
ms.openlocfilehash: 8823f1db8b15b327306ff3c592b46c94537f4331
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637379"
---
# <a name="iclrpolicymanager-interface"></a>ICLRPolicyManager インターフェイス

エラーやタイムアウトが発生した場合に実行されるポリシーアクションをホストが指定できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetActionOnFailure メソッド](iclrpolicymanager-setactiononfailure-method.md)|指定したエラーが発生したときに共通言語ランタイム (CLR) が実行するポリシーアクションを指定します。|  
|[SetActionOnTimeout メソッド](iclrpolicymanager-setactionontimeout-method.md)|指定された操作がタイムアウトしたときに CLR が実行するポリシーアクションを指定します。|  
|[SetDefaultAction メソッド](iclrpolicymanager-setdefaultaction-method.md)|指定された操作が発生したときに CLR が実行するポリシーアクションを指定します。|  
|[SetTimeout メソッド](iclrpolicymanager-settimeout-method.md)|指定された操作のタイムアウト値を設定します。|  
|[SetTimeoutAndAction メソッド](iclrpolicymanager-settimeoutandaction-method.md)|指定された操作のタイムアウト値を設定し、操作が発生したときに CLR が実行する必要があるポリシーアクションを指定します。|  
|[SetUnhandledExceptionPolicy メソッド](iclrpolicymanager-setunhandledexceptionpolicy-method.md)|未処理の例外が発生した場合の CLR の動作を指定します。|  
  
## <a name="requirements"></a>要件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** MSCorEE.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
