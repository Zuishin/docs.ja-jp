---
title: Windows 7 SP1 への .NET Framework のインストール
description: Windows 7 SP1 に .NET Framework をインストールする方法について説明します。
ms.date: 04/18/2019
ms.openlocfilehash: 900b38110626a93f37829045a8676ea87101d7e9
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899088"
---
# <a name="install-the-net-framework-on-windows-7-sp1-and-windows-server-2008-r2"></a>Windows 7 SP1 と Windows Server 2008 R2 に .NET Framework をインストールする

.NET Framework は、Windows でさまざまなアプリケーションを実行するために必要です。 次の手順を使用してインストールすることができます。 このページをご覧になっている理由は、アプリケーションを実行しようとして次のようなダイアログがコンピューターに表示されたからではないでしょうか。

![このアプリケーションを開始できませんでした。](./media/this-application-could-not-be-started.png)

これらの手順は、必要な .NET Framework バージョンをインストールする場合に役立ちます。 [.NET Framework 4.8](https://github.com/Microsoft/dotnet/tree/master/releases/net48) が最新バージョンです。 これは Windows 7 SP1 と Windows Server 2008 R2 でサポートされており、[Windows 10 May 2019 Update](https://support.microsoft.com/help/4028685/windows-10-get-the-update) に付属します。

## <a name="net-framework-48"></a>.NET Framework 4.8

> [!div class="button"]
> [.NET Framework 4.8 のダウンロード](https://dotnet.microsoft.com/download/dotnet-framework/net48)

[.NET Framework 4.8](https://github.com/Microsoft/dotnet/tree/master/releases/net48) は、.NET Framework 4.0 以降用に構築されたアプリケーションを実行するために使用できます。

### <a name="offline-installer"></a>オフライン インストーラー

Windows 7 で .NET Framework 用のオフライン インストールを実行する場合は、まず最新の [Microsoft Root Certificate Authority 2011](https://www.microsoft.com/pkiops/Docs/Repository.htm) がターゲット コンピューターにインストールされていることを確認する必要があります。

_certmgr.exe_ ツールを使用すると、証明書のインストールを自動化できます。これは、Visual Studio または Windows SDK から取得されます。 .NET Framework インストーラーを実行する前に、次のコマンドを使用して証明書をインストールします。

```console
certmgr.exe /add MicRooCerAut2011_2011_03_22.crt /s /r localMachine root
```

## <a name="net-framework-35"></a>.NET Framework 3.5

[.NET Framework 3.5](https://dotnet.microsoft.com/download/dotnet-framework/net35-sp1) は、Windows 7 に含まれています。

.NET Framework 3.5 は、.NET Framework 1.0 から 3.5 用に構築されたアプリケーションをサポートします。

## <a name="help"></a>Help

インストールされている .NET Framework の正しいバージョンがわからない場合は、[Microsoft にお問い合わせください](mailto:dotnet-install-help@service.microsoft.com?subject=Install-Help)。

## <a name="see-also"></a>関連項目

- [.NET Framework のダウンロード](https://dotnet.microsoft.com/download)
- [.NET Framework のインストールおよびアンインストールのブロックのトラブルシューティング](troubleshoot-blocked-installations-and-uninstallations.md)
- [開発者向けの .NET Framework のインストール](guide-for-developers.md)
