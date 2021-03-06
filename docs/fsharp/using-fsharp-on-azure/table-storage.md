---
title: F を使用して Azure Table Storage を使ってみる#
description: Azure Table Storage または Azure Cosmos DB を使用して、構造化データをクラウドに格納します。
author: sylvanc
ms.date: 03/26/2018
ms.custom: devx-track-fsharp
ms.openlocfilehash: bc8e111636013930f7c7d4f59d1ef0720298cb9f
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899283"
---
# <a name="get-started-with-azure-table-storage-and-the-azure-cosmos-db-table-api-using-f"></a>F を使用して Azure Table Storage と Azure Cosmos DB Table API を使ってみる\#

Azure Table Storage は、構造化された NoSQL データをクラウドに格納するサービスです。 Table Storage は、スキーマなしの設計によるキーまたは属性ストアです。 Table Storage はスキーマがないため、アプリケーションの進化のニーズに合わせてデータを容易に修正できます。 あらゆる種類のデータに、高速かつ経済的にアクセスできます。 Table Storage は、通常、従来の SQL と比較して、同様の容量のデータをはるかに低コストで保存できます。

テーブル ストレージを使用すると、Web アプリケーションのユーザー データ、アドレス帳、デバイス情報、およびサービスに必要なその他の種類のメタデータなど、柔軟なデータセットを保存できます。 ストレージ アカウントの容量の上限を超えない限り、テーブルには任意の数のエンティティを保存でき、ストレージ アカウントには任意の数のテーブルを含めることができます。

Azure Cosmos DB は、Azure Table Storage 向けに作成され、次のような premium 機能を必要とするアプリケーションの Table API を提供します。

- ターンキー グローバル配信。
- 世界規模での専用スループット。
- 99 パーセンタイルで 10 ミリ秒未満の待ち時間。
- 高可用性の保証。
- 自動セカンダリ インデックス作成。

Azure Table Storage 用に作成されたアプリケーションは、コードを変更せずに Table API を使用して Azure Cosmos DB に移行し、premium 機能を活用できます。 Table API には、.NET、Java、Python、および Node.js で利用可能なクライアント SDK があります。

詳細については、「 [Azure Cosmos DB Table API の概要](/azure/cosmos-db/table-introduction)」を参照してください。

## <a name="about-this-tutorial"></a>このチュートリアルについて

このチュートリアルでは、Azure Table Storage または Azure Cosmos DB Table API を使用して、テーブルの作成と削除、テーブルデータの挿入、更新、削除、クエリなど、いくつかの一般的なタスクを実行する F # コードを記述する方法について説明します。

## <a name="prerequisites"></a>前提条件

このガイドを使用するには、最初に [Azure ストレージアカウント](/azure/storage/storage-create-storage-account) または [Azure Cosmos DB アカウント](https://azure.microsoft.com/try/cosmosdb/)を作成する必要があります。

## <a name="create-an-f-script-and-start-f-interactive"></a>F # スクリプトを作成して F# インタラクティブを開始する

この記事のサンプルは、F # アプリケーションと F # スクリプトのどちらでも使用できます。 F # スクリプトを作成するには、 `.fsx` `tables.fsx` f # 開発環境で、などの拡張子を持つファイルを作成します。

次に、[パケット](https://fsprojects.github.io/Paket/)や[NuGet](https://www.nuget.org/)などの[パッケージマネージャー](package-management.md)を使用して、 `WindowsAzure.Storage` ディレクティブを使用してスクリプトにパッケージと参照をインストールし `WindowsAzure.Storage.dll` `#r` ます。 Microsoft Azure 名前空間を取得するために、に対してもう一度実行し `Microsoft.WindowsAzure.ConfigurationManager` ます。

### <a name="add-namespace-declarations"></a>名前空間宣言の追加

次の `open` ステートメントを `tables.fsx` ファイルの先頭に追加します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L1-L5)]

### <a name="get-your-azure-storage-connection-string"></a>Azure Storage 接続文字列を取得する

Azure Storage Table service に接続している場合は、このチュートリアルで使用する接続文字列が必要になります。 Azure portal から接続文字列をコピーできます。 接続文字列の詳細については、「 [ストレージ接続文字列の構成](/azure/storage/storage-configure-connection-string)」を参照してください。

### <a name="get-your-azure-cosmos-db-connection-string"></a>Azure Cosmos DB 接続文字列を取得する

Azure Cosmos DB に接続している場合は、このチュートリアルで使用する接続文字列が必要になります。 Azure portal から接続文字列をコピーできます。 Azure portal の Cosmos DB アカウントで、[**設定**  >  ] [**接続文字列**] にアクセスし、[**コピー** ] ボタンを選択してプライマリ接続文字列をコピーします。

このチュートリアルでは、次の例のように、スクリプトに接続文字列を入力します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L11-L11)]

ただし、実際のプロジェクトではこの方法は **お勧めできません** 。 ストレージ アカウント キーは、ストレージ アカウントの root パスワードに似ています。 ストレージ アカウント キーは常に慎重に保護してください。 このキーを他のユーザーに配布したり、ハードコーディングしたり、他のユーザーがアクセスできるプレーン テキスト ファイルに保存したりしないでください。 侵害された可能性があると思われる場合は、Azure portal を使用してキーを再生成することができます。

実際のアプリケーションでは、ストレージ接続文字列を維持する最善の方法は構成ファイルにあります。 構成ファイルから接続文字列を取得するには、次の手順を実行します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L13-L15)]

Azure Configuration Manager の使用はオプションです。 .NET Framework の型などの API を使用することもでき `ConfigurationManager` ます。

### <a name="parse-the-connection-string"></a>接続文字列を解析する

接続文字列を解析するには、次のように指定します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L21-L22)]

これにより、が返さ `CloudStorageAccount` れます。

### <a name="create-the-table-service-client"></a>Table service クライアントを作成する

クラスを使用すると、 `CloudTableClient` テーブルストレージ内のテーブルとエンティティを取得できます。 サービス クライアントを作成する方法の 1 つを次に示します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L28-L29)]

これで、Table Storage に対してデータの読み取りと書き込みを実行するコードを記述する準備が整いました。

### <a name="create-a-table"></a>テーブルを作成する

この例は、テーブルが存在しない場合に作成する方法を示しています。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L35-L39)]

### <a name="add-an-entity-to-a-table"></a>エンティティをテーブルに追加する

エンティティは、から継承される型を持つ必要があり `TableEntity` ます。 は任意の `TableEntity` 方法で拡張できますが、型にはパラメーターのないコンストラクターが *必要* です。 との両方を持つプロパティのみ `get` `set` が Azure テーブルに格納されます。

エンティティのパーティションキーと行キーは、テーブル内のエンティティを一意に識別します。 同じパーティション キーを持つエンティティは、異なるパーティション キーを持つエンティティよりも迅速に照会できます。一方、多様なパーティション キーを使用すると、並列操作の拡張性が向上します。

をパーティションキーとして使用し、を行キーとして使用するの例を次に示し `Customer` `lastName` `firstName` ます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L45-L52)]

次 `Customer` に、テーブルにを追加します。 これを行うには、 `TableOperation` テーブルで実行するを作成します。 この場合は、操作を作成し `Insert` ます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L54-L55)]

### <a name="insert-a-batch-of-entities"></a>エンティティのバッチを挿入する

1回の書き込み操作を使用して、エンティティのバッチをテーブルに挿入できます。 バッチ操作を使用すると、複数の操作を1回の実行にまとめることができますが、いくつかの制限があります。

- 同じバッチ操作で、更新、削除、および挿入を実行できます。
- バッチ操作には、最大100のエンティティを含めることができます。
- バッチ操作内のすべてのエンティティは、同じパーティションキーを持つ必要があります。
- バッチ操作でクエリを実行することはできますが、バッチ内の唯一の操作である必要があります。

バッチ操作に2つの挿入を結合するコードを次に示します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L62-L71)]

### <a name="retrieve-all-entities-in-a-partition"></a>パーティション内のすべてのエンティティを取得する

テーブルに対してパーティション内のすべてのエンティティを照会する場合は、`TableQuery` オブジェクトを使用します。 ここでは、"Smith" がパーティションキーであるエンティティをフィルター処理します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L77-L82)]

結果は次のように印刷されます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L84-L85)]

### <a name="retrieve-a-range-of-entities-in-a-partition"></a>パーティション内の一定範囲のエンティティを取得する

パーティション内の一部のエンティティのみを照会する場合は、パーティション キー フィルターと行キー フィルターを組み合わせて範囲を指定できます。 ここでは、2つのフィルターを使用して、行キー (名) がアルファベットの "M" よりも前の文字で始まる "Smith" パーティション内のすべてのエンティティを取得します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L91-L100)]

結果は次のように印刷されます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L102-L103)]

### <a name="retrieve-a-single-entity"></a>単一のエンティティを取得する

単一の特定のエンティティを取得するクエリを記述することができます。 ここでは、を使用し `TableOperation` て、"Ben Smith" という顧客を指定します。 コレクションではなく、が返さ `Customer` れます。 クエリでパーティションキーと行キーの両方を指定することは、Table service から単一のエンティティを取得する最速の方法です。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L109-L111)]

結果は次のように印刷されます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L113-L115)]

### <a name="replace-an-entity"></a>エンティティを置換する

エンティティを更新するには、エンティティを Table service から取得し、エンティティオブジェクトを変更した後、操作を使用して Table service に変更を保存し `Replace` ます。 これにより、サーバー上でエンティティが完全に置換されます。ただし、取得後にサーバー上のエンティティが変更された場合、操作は失敗します。 このエラーは、他のソースからの変更がアプリケーションによって誤って上書きされないようにするためのものです。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L121-L128)]

### <a name="insert-or-replace-an-entity"></a>エンティティを挿入または置換する

場合によっては、テーブルにエンティティが存在するかどうかがわかりません。 その場合、現在格納されている値は不要になります。 を使用してエンティティを作成することも、 `InsertOrReplace` 状態に関係なく、エンティティが存在する場合は置き換えることもできます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L134-L141)]

### <a name="query-a-subset-of-entity-properties"></a>エンティティ プロパティのサブセットを照会する

テーブルクエリでは、エンティティのすべてではなく、いくつかのプロパティのみを取得できます。 射影と呼ばれるこの手法は、特に大規模なエンティティの場合に、クエリのパフォーマンスを向上させることができます。 ここでは、とを使用して電子メールアドレスのみを返し `DynamicTableEntity` `EntityResolver` ます。 プロジェクションはローカルストレージエミュレーターではサポートされていないため、このコードは Table service でアカウントを使用している場合にのみ実行されます。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L147-L158)]

### <a name="retrieve-entities-in-pages-asynchronously"></a>ページ内のエンティティを非同期的に取得する

多数のエンティティを読み取っているときに、すべてのエンティティが返されるのを待機するのではなく、取得時に処理する場合は、セグメント化されたクエリを使用できます。 ここでは、非同期ワークフローを使用してページ内の結果を返し、多数の結果が返されるのを待機している間に実行がブロックされないようにします。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L163-L178)]

ここで、この計算を同期的に実行します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L180-L180)]

### <a name="delete-an-entity"></a>エンティティを削除する

エンティティは、取得後に削除できます。 エンティティの更新と同様に、エンティティを取得した後にエンティティが変更された場合、これは失敗します。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L186-L187)]

### <a name="delete-a-table"></a>テーブルを削除する

ストレージアカウントからテーブルを削除できます。 削除されたテーブルは、削除後の一定期間は再作成できなくなります。

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L193-L193)]

## <a name="next-steps"></a>次のステップ

これで、Table storage の基本を学習できました。さらに複雑なストレージタスクと Azure Cosmos DB Table API については、次のリンク先を参照してください。

- [Azure Cosmos DB Table API の概要](/azure/cosmos-db/table-introduction)
- [.NET 用ストレージ クライアント ライブラリ リファレンス](/dotnet/api/overview/azure/storage)
- [Azure Storage 型プロバイダー](https://fsprojects.github.io/AzureStorageTypeProvider/)
- [Azure Storage Team Blog](/archive/blogs/windowsazurestorage/)
- [接続文字列の構成](/azure/storage/common/storage-configure-connection-string)
