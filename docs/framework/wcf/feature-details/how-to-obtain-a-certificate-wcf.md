---
description: '詳細については、「方法: 証明書を取得する (WCF)」を参照してください。'
title: '方法 : 証明書 (WCF) を取得する'
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], obtaining
ms.assetid: d53762fd-15ea-42dc-b0ea-6a6597aa23f7
ms.openlocfilehash: 2ca40c9646bbdeb6c29a94966fd24ec00d9b5306
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793702"
---
# <a name="how-to-obtain-a-certificate-wcf"></a>方法 : 証明書 (WCF) を取得する

X.509 証明書を使用するの Windows Communication Foundation (WCF) 機能のいずれかを使用するには、最初に証明書を取得するだけです。  
  
### <a name="to-obtain-an-x509-certificate"></a>X.509 証明書を取得するには  
  
1. 次のいずれかを選択します。  
  
    - VeriSign, Inc. などの証明機関から証明書を購入します。  
  
    - 独自の証明書サービスを設定し、証明機関に証明書への署名を依頼します。 Windows Server 2003、Windows 2000 Server、Windows 2000 Server Datacenter、および Windows 2000 Datacenter Server にはすべて、公開キー基盤 (PKI) をサポートする証明書サービスが含まれています。 Windows Server 2008 では、 [Active Directory 証明書サービス](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731564(v=ws.10)) の役割を使用して、証明機関を管理します。  
  
    - 独自の証明書サービスを設定し、証明書には署名しません。  
  
    > [!NOTE]
    > どの方法を使用する場合でも、X.509 証明書を含む SOAP 要求の受信者は、その X.509 証明書を信頼する必要があります。 つまり、証明書チェーン内の X.509 証明書または発行者は、信頼されたユーザーの証明書ストア内に存在し、また X.509 証明書は信頼されない証明書ストア内には存在しないということを意味します。  
  
## <a name="see-also"></a>関連項目

- [証明書の使用](working-with-certificates.md)
- [方法: 開発中に使用する一時的な証明書を作成する](how-to-create-temporary-certificates-for-use-during-development.md)
