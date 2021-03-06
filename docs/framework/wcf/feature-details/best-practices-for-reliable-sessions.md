---
description: '詳細情報: 信頼できるセッションのベストプラクティス'
title: 信頼できるセッションのベスト プラクティス
ms.date: 03/30/2017
ms.assetid: b94f6e01-8070-40b6-aac7-a2cb7b4cb4f2
ms.openlocfilehash: 4b05dd914d2c5b8ec7941417b727bec1e5b43ba4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643671"
---
# <a name="best-practices-for-reliable-sessions"></a>信頼できるセッションのベスト プラクティス

このトピックでは、信頼できるセッションのベストプラクティスについて説明します。

## <a name="setting-maxtransferwindowsize"></a>MaxTransferWindowSize の設定

Windows Communication Foundation (WCF) の信頼できるセッションでは、転送ウィンドウを使用して、クライアントとサービスでメッセージを保持します。 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> プロパティは、この転送ウィンドウに保持できるメッセージの最大数を表します。

送信側では、これは、受信確認を待機している間に転送ウィンドウが保持できるメッセージの数を示します。受信側では、サービスに対してバッファーに格納するメッセージの数を示します。

適切なサイズを選択すると、ネットワークの効率とサービスの最適な容量に影響します。 以下のセクションでは、このプロパティの値と値の影響について詳しく説明します。

既定の転送ウィンドウサイズは8メッセージです。

### <a name="efficient-use-of-the-network"></a>ネットワークの効率的な使用

このコンテキストでは、 *ネットワーク* という用語は、クライアント (送信側) とサービス (受信側) の間の通信の基礎として使用されるすべてのものに対応します。 これには、SOAP ルーターや HTTP プロキシ/ファイアウォールを含む、間のトランスポート接続と仲介またはブリッジが含まれます。

ネットワーク効率が高いとは、その伝送容量を最大限に活用できるということです。 ネットワークで1秒間に転送できるデータの量 (*データ速度*) と、送信側から受信側にデータを転送するためにかかる時間 (*待機* 時間) は、ネットワークがどの程度効果的に使用されるかに影響します。

送信側については、転送ウィンドウに保持できる受信確認の到着を待機しているメッセージの数が <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> プロパティによって表されます。 ネットワーク待機時間が長く、応答の送信側とネットワーク使用率が高いことを確認するために、転送ウィンドウのサイズを大きくする必要があります。

たとえば、送信側がデータ速度を維持している場合でも、送信側と受信側の間に複数の中継局が存在すると待機時間が長くなる可能性があります。または、データが損失を伴う仲介やネットワークを通過する必要があります。 このため、送信側は、ネットワーク上で新しいメッセージを受信する前に、転送ウィンドウ内のメッセージの受信確認を待機する必要があります。 待機時間が長いバッファーが小さくなるほど、ネットワーク使用率が低下します。 一方、転送ウィンドウのサイズが大きすぎると、サービスがクライアントから送信されたデータを大量に捕捉する必要が生じる可能性があるため、サービスに影響を与える可能性があります。

### <a name="running-the-service-to-capacity"></a>容量に対してサービスを実行しています

ネットワークが効率的に使用されるほど、最適な容量でサービスを実行することも理想的です。 受信側の転送ウィンドウ サイズは、処理待ちのメッセージをいくつまで保持しておけるかを表します。 メッセージをこのようにバッファーに保持することは、ネットワークのフロー制御だけでなく、処理能力を最大限に活用したサービス稼働にも役立ちます。 たとえば、バッファーが1つのメッセージであり、サービスが処理できる速度よりもメッセージが高速に到着した場合、ネットワークはメッセージを破棄し、容量が浪費されたり過小使用されたりする可能性があります。

バッファーを使用すると、以前に受信したメッセージの処理中にメッセージを同時に受信してバッファーに格納できるため、サービスの可用性が向上します。

送信側と受信側の両方で同じを使用することをお勧めし `MaxTransferWindowSize` ます。

### <a name="enabling-flow-control"></a>フロー制御を有効にする

*フロー制御* は、送信側と受信側が相互に通信できるようにするメカニズムであり、メッセージが生成されたときと同じ速度で処理され、処理されます。 クライアントとサービスの転送ウィンドウ サイズは、送信側と受信側が妥当な許容範囲内で同期できるように設定しなければなりません。

<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled%2A> `true` Wcf クライアントと wcf サービスの間で信頼できるセッションを使用している場合は、プロパティをに設定することを強くお勧めします。

## <a name="setting-maxpendingchannels"></a>MaxPendingChannels の設定

さまざまなクライアントからの信頼できるセッション通信を可能にするサービスを作成する場合、多数のクライアントが同時にサービスに対して信頼できるセッションを確立することができます。 このとき、サービスの応答性は、`MaxPendingChannels` プロパティによって決まります。

信頼できるセッション チャネルが送信側によって作成されると、両者のハンドシェイクによって信頼できるセッションが確立します。 これが終わるとチャネルは保留チャネル キューに入り、サービス側からの応答を待機する状態になります。 `MaxPendingChannels` プロパティは、この状態にできるチャネルの数を表します。

サービスが、より多くのチャネルを受け入れられない状態になる可能性があります。 キューがいっぱいの場合は、信頼できるセッションを確立しようとしても拒否され、クライアントは再試行する必要があります。

キュー内の保留中のチャネルがキューに保持されている期間が長くなる可能性もあります。 それまでの間は、信頼できるセッションで非アクティブなタイムアウトが発生し、チャネルが faulted 状態に遷移します。

複数のクライアントに同時にサービスを実行するサービスを作成する場合は、ニーズに合った値を設定する必要があります。 設定値が高すぎると、 `MaxPendingChannels` 作業セットに影響します。

の既定値 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxPendingChannels%2A> は4チャネルです。

## <a name="reliable-sessions-and-hosting"></a>信頼できるセッションとホスト

信頼できるセッションを使用するサービスを web でホストする場合は、次の重要な考慮事項に注意してください。

- 信頼できるセッションはステートフルであり、状態は AppDomain で管理されます。 したがって、信頼できるセッションでやりとりするメッセージはすべて、同じ AppDomain で処理する必要があります。 ファームまたはガーデンのサイズが1つのノードより大きい web ファームと web ガーデンは、この制約を保証できません。

- (たとえば、を使用して) デュアル HTTP チャネルを使用する信頼できるセッション `WsDualHttpBinding` では、クライアントごとに2つの http 接続の既定値よりも多くの設定が必要になる場合があります。 これは、双方向の信頼できるセッションでは、同時実行アプリケーションとプロトコルメッセージがいつでも転送される可能性があるため、最大で2つの接続が必要になることを意味します。 サービスのメッセージ交換パターンによっては、特定の条件下で、デュアル HTTP と信頼できるセッションを使用して web ホストサービスをデッドロックできることを意味します。 クライアントごとに許可される HTTP 接続の数を増やすには、関連する構成ファイル (たとえば、問題のサービスの *web.config* ) に次のコードを追加します。

  ```xml
  <configuration>
    <system.net>
      <connectionManagement>
        <add name="*" maxconnection="4" />
      </connectionManagement>
    </system.net>
  </configuration>
  ```

  属性の値 `maxconnection` は、必要な接続の数です。 この場合の最小値は4つの接続にする必要があります。
