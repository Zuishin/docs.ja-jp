---
title: コンストラクターのデザイン
ms.date: 10/22/2008
helpviewer_keywords:
- member design guidelines, constructors
- constructors, design guidelines
- instance constructors
- type constructors
- virtual members
- constructors, types
- parameterless constructors
- static constructors
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
ms.openlocfilehash: 27fb73aa01adf31117d1b82724873db3a03fd269
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94821399"
---
# <a name="constructor-design"></a>コンストラクターのデザイン

コンストラクターには、型コンストラクターとインスタンスコンストラクターの2種類があります。

型コンストラクターは静的であり、型が使用される前に CLR によって実行されます。 インスタンスコンストラクターは、型のインスタンスが作成されるときに実行されます。

型コンストラクターはパラメーターを受け取ることができません。 インスタンスコンストラクターは使用できます。 パラメーターを受け取らないインスタンスコンストラクターは、通常、パラメーターなしのコンストラクターと呼ばれます。

コンストラクターは、型のインスタンスを作成する最も自然な方法です。 ほとんどの開発者は、インスタンスを作成する別の方法 (ファクトリメソッドなど) を検討する前に、コンストラクターを検索して使用しようとします。

✔️単純で、理想的な既定のコンストラクターを提供することを検討してください。

単純なコンストラクターには、ごく少数のパラメーターがあり、すべてのパラメーターはプリミティブまたは列挙型です。 このような単純なコンストラクターにより、フレームワークの使いやすさが向上します。

目的の操作のセマンティクスが新しいインスタンスの構築に直接マップされない場合、またはコンストラクターのデザインガイドラインに従って不自然な場合は、コンストラクターの代わりに静的ファクトリメソッドを使用することを✔️します。

✔️メインプロパティを設定するためのショートカットとしてコンストラクターパラメーターを使用します。

空のコンストラクターを使用した後にいくつかのプロパティセットを使用し、複数の引数を持つコンストラクターを使用すると、セマンティクスに違いはありません。

コンストラクターパラメーターを使用してプロパティを設定するだけの場合は、コンストラクターパラメーターとプロパティに同じ名前を使用✔️ます。

このようなパラメーターとプロパティの違いは、大文字と小文字を区別することだけです。

コンストラクターで✔️最小限の作業を実行します。

コンストラクターでは、コンストラクターパラメーターをキャプチャする以外に多くの作業を行うことはできません。 その他の処理のコストは、必要になるまで延期する必要があります。

✔️は、必要に応じてインスタンスコンストラクターから例外をスローします。

このようなコンストラクターが必要な場合は、クラスでパブリックのパラメーターなしのコンストラクターを明示的に宣言✔️ます。

型のコンストラクターを明示的に宣言しない場合、多くの言語 (C# など) によって、パブリックなパラメーターなしのコンストラクターが自動的に追加されます。 (抽象クラスは、保護されたコンストラクターを取得します)。

パラメーター化されたコンストラクターをクラスに追加すると、コンパイラはパラメーターなしのコンストラクターを追加できなくなります。 これにより、誤って重大な変更が行われることがよくあります。

❌ 構造体でパラメーターなしのコンストラクターを明示的に定義することは避けてください。

これにより、パラメーターなしのコンストラクターが定義されていない場合に、配列内のすべてのスロットで実行する必要がないため、配列の作成が高速になります。 多くのコンパイラ (C# を含む) では、この理由により、構造体にパラメーターなしのコンストラクターを含めることはできないことに注意してください。

❌ コンストラクター内のオブジェクトで仮想メンバーを呼び出さないでください。

仮想メンバーを呼び出すと、最も派生した型のコンストラクターがまだ完全には実行されていない場合でも、最も派生されたオーバーライドが呼び出されます。

## <a name="type-constructor-guidelines"></a>型コンストラクターのガイドライン

静的コンストラクターをプライベートに設定✔️ます。

静的コンストラクター (クラスコンストラクターとも呼ばれます) を使用して、型を初期化します。 CLR は、型の最初のインスタンスが作成される前、またはその型の静的メンバーが呼び出される前に、静的コンストラクターを呼び出します。 静的コンストラクターが呼び出されるタイミングは、ユーザーが制御できません。 静的コンストラクターがプライベートでない場合は、CLR 以外のコードで呼び出すことができます。 コンストラクターで実行される操作によっては、予期しない動作が発生する可能性があります。 C# コンパイラは、静的コンストラクターを強制的にプライベートにします。

❌ 静的コンストラクターから例外をスローしないでください。

型コンストラクターから例外がスローされた場合、その型は現在のアプリケーションドメインでは使用できません。

静的コンストラクターを明示的に使用するのではなく、静的フィールドをインラインで初期化することを検討してください。これは、明示的に定義された静的コンストラクターを持たない型のパフォーマンスをランタイムが最適化できるためです。✔️

*©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

*2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [メンバーデザインのガイドライン](member.md)
- [フレームワークデザインのガイドライン](index.md)
