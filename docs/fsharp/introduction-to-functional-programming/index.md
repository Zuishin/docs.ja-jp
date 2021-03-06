---
title: F# の関数型プログラミングの概要
description: F# での関数型プログラミングの基礎について説明し ます。
ms.date: 10/29/2018
ms.openlocfilehash: 44242a4319a331312a003a555d1483f2a3f1a90d
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110586"
---
# <a name="introduction-to-functional-programming-in-f"></a>F\# の関数型プログラミングの概要

関数型プログラミングは、関数と不変のデータの使用を重視するプログラミングのスタイルです。 F# を使用するなど、関数型プログラミングが静的な型と組み合わされる場合が、型指定される関数型プログラミングです。 関数型プログラミングでは、一般に、以下の概念が重視されています。

* 使用する主要コンストラクトとしての関数
* ステートメントの代わりの式
* 変数よりも不変の値が優先
* 命令型プログラミングよりも宣言型プログラミングが優先

このシリーズを通して、F# を使用する関数型プログラミングの概念とパターンについて説明します。 その間に、F# についても多少学習します。

## <a name="terminology"></a>用語

他のプログラミング パラダイムと同様に、関数型プログラミングには、いつかは学ぶ必要がある用語があります。 ここでは、頻繁に目にすることになる一般的用語の一部を示します。

* **関数** - 関数は、入力が与えられたときに出力を生成するコンストラクトです。 より正式には、1 つのセットから別のセットに項目を _マッピング_ するものです。 こうした形式的な点は、データのコレクションに対する操作を行う関数の使用時には特に、いろいろな意味で具体的なものに置き換えられます。 これが、関数型プログラミングにおける最も基本的 (および重要) な概念です。
* **式** - 式は、値を生成するコード内のコンストラクトです。 F# では、この値は、バインドするか明示的に無視する必要があります。 式は、関数呼び出しで普通に置き換えることができます。
* **純粋性** - 純粋性は、同じ引数に対しては戻り値が常に同じであり、その評価に副作用がないような関数のプロパティです。 純粋関数は、その引数に完全に左右されます。
* **参照の透過性** - 参照の透過性は、プログラムの動作に影響を与えずにその出力で置き換えることができるような、式のプロパティです。
* **不変性** - 不変性とは、その位置で値を変更できないことを意味します。 これは、その位置で変化することができる変数とは対照的です。

## <a name="examples"></a>例

これらの中心概念について、以下の例で具体的に説明します。

### <a name="functions"></a>機能

関数型プログラミングの最も一般的で基礎的なコンストラクトは関数です。 次に示すのは、整数に 1 を加算する単純な関数です。

```fsharp
let addOne x = x + 1
```

その型のシグネチャは次のとおりです。

```fsharp
val addOne: x:int -> int
```

このシグネチャは、"`addOne` は `x` という名前の `int` を受け取り、`int` を生成する" と読むことができます。 より正式には、`addOne` は整数のセットからの値を、整数のセットに _マッピング_ しています。 `->` トークンが、このマッピングを意味します。 F# では、通常、関数シグネチャを調べると、それが何を行うかが何となくわかります。

では、なぜシグネチャが重要なのでしょうか。 型指定される関数型プログラミングでは、多くの場合、関数の実装の重要度は、実際の型シグネチャよりも低くなります。 `addOne` によって整数に値 1 を追加するという事実は実行時には重要ですが、プログラムを構築しているときには、それが `int` を受け取って返すという事実が、この関数を実際にどう使用するかを伝えることになります。 さらに、この関数を (その型のシグネチャに関して) 正しく使用すれば、`addOne` 関数の本体内だけで、すべての問題の診断を行えます。 これが、型指定される関数型プログラミングを後押しする推進力となっています。

### <a name="expressions"></a>式

式は、1 つの値へと評価されるコンストラクトです。 アクションを実行するステートメントとは対照的に、式は、値を返すアクションを実行すると考えることができます。 関数型プログラミングでは、ステートメントではなく式がほとんど常に使用されます。

前の関数 `addOne` について考えてみます。 `addOne` の本体は式です。

```fsharp
// 'x + 1' is an expression!
let addOne x = x + 1
```

これはこの式の結果であり、それが `addOne` 関数の結果の型を定義しています。 たとえば、この関数を構成する式は、`string` などの異なる型に変更できます。

```fsharp
let addOne x = x.ToString() + "1"
```

これで関数のシグネチャは次のようになります。

```fsharp
val addOne: x:'a -> string
```

F# のどの型でもそれに対して `ToString()` を呼び出せるため、`x` の型はジェネリック ([自動ジェネリック化](../language-reference/generics/automatic-generalization.md)と呼ばれます) になり、結果の型は `string` になります。

式は、関数の本体であるだけではありません。 他の場所で使用する値を生成する式を用意できます。 一般的なものは `if` です。

```fsharp
// Checks if 'x' is odd by using the mod operator
let isOdd x = x % 2 <> 0

let addOneIfOdd input =
    let result =
        if isOdd input then
            input + 1
        else
            input

    result
```

`if` 式では、`result` という名前の値が生成されます。 `result` を完全に省略し、`if` 式を `addOneIfOdd` 関数の本体にできることに注意してください。 式について覚えておく必要がある重要なことは、式によって値が生成されるという点です。

特殊な型として `unit` があります。これは、返すものがない場合に使用されます。 たとえば、次の単純な関数について考えてみます。

```fsharp
let printString (str: string) =
    printfn $"String is: {str}"
```

シグネチャは次のようになります。

```fsharp
val printString: str:string -> unit
```

`unit` 型は、返される実際の値がないことを示します。 これが便利なのは、その作業の結果として返す値がなくても "作業を行う" 必要のあるルーチンがある場合です。

これは、同等の `if` コンストラクトがステートメントであり、変化する変数を使用して値が生成される場合が多い命令型プログラミングとは著しい対照をなしています。 たとえば C# では、コードは次のように記述されることがあります。

```csharp
bool IsOdd(int x) => x % 2 != 0;

int AddOneIfOdd(int input)
{
    var result = input;

    if (IsOdd(input))
    {
        result = input + 1;
    }

    return result;
}
```

C# やその他の C スタイルの言語では、式ベースの条件付きプログラミングを可能にする[三項式](../../csharp/language-reference/operators/conditional-operator.md)がサポートされることに注意してください。

関数型プログラミングでは、ステートメントを使用して値を変化させることはまれです。 一部の関数言語ではステートメントと変化がサポートされていますが、関数型プログラミングでこれらの概念を使用するのは一般的ではありません。

### <a name="pure-functions"></a>純粋関数

前に触れたように、純粋関数は次のような関数です。

* 同じ入力に対しては、常に同じ値に評価されます。
* 副作用がありません。

この文脈においては、数学関数のことを考えると参考になります。 数学では、関数は引数にのみ依存しており、副作用は一切ありません。 数学関数 `f(x) = x + 1` では、`f(x)` の値は `x` の値にのみ左右されます。 関数型プログラミングの純粋関数も同様です。

純粋関数の記述時には、関数はその引数にのみ依存し、副作用が発生するアクションを実行しないようにする必要があります。

次は、グローバルで変更可能な状態に依存しているため、非純粋関数の例です。

```fsharp
let mutable value = 1

let addOneToValue x = x + value
```

`addOneToValue` 関数は明確に純粋ではありません。`value` は、いつでも 1 とは異なる値に変更できるためです。 グローバルな値に依存するこのパターンは、関数型プログラミングでは回避する必要があります。

次は、副作用が実行されるため、非純粋関数の別の例となっています。

```fsharp
let addOneToValue x =
    printfn $"x is %d{x}"
    x + 1
```

この関数はグローバルな値に依存していませんが、`x` の値をプログラムの出力に書き込みます。 これを行うことに本質的な問題はありませんが、関数は確かに純粋ではないことになります。 プログラムの別の部分が、出力バッファーなど、プログラム外部の何かに依存している場合は、この関数を呼び出すと、プログラムのそうした他の部分に影響を与える可能性があります。

`printfn` ステートメントを削除すると、この関数は純粋になります。

```fsharp
let addOneToValue x = x + 1
```

この関数は、`printfn` ステートメントを含む前のバージョンよりも本質的に _優れている_ わけではありませんが、この関数で行うのは値を返すことがすべてであることが確かに保証されます。 この関数を何度呼び出しても同じ結果が生成されます。ただ値が生成されます。 純粋性によって得られる予測可能性は、多くの関数プログラマが得ようと努めているものです。

### <a name="immutability"></a>不変性

最後に挙げる、型指定される関数型プログラミングの最も基本的な概念の 1 つは不変性です。 F# では、既定ですべての値が不変です。 つまり、明示的に変更可能とマークしない限り、これらをインプレースで変化させることはできません。

実際には、変更できない値を使用して作業することは、プログラミングに対するアプローチを、"私は何かを変更する必要があります" から、"私は新しい値を生成する必要があります" に変えることを意味します。

たとえば、値に 1 を追加することは、既存の値を変更することではなく、新しい値を生成することを意味します。

```fsharp
let value = 1
let secondValue = value + 1
```

F# では、次のコードで `value` 関数は変更され **ません**。代わりに、等価性チェックが実行されます。

```fsharp
let value = 1
value = value + 1 // Produces a 'bool' value!
```

一部の関数型プログラミング言語では、変化が一切サポートされていません。 F# ではサポートされていますが、値についての既定の動作ではありません。

この概念はさらに、データ構造にさえ拡張されています。 関数型プログラミングでは、セット (やさらに多くのもの) などの変更できないデータ構造の実装は、最初に予期したのとは異なるものになります。 概念上、セットに項目を 1 つ追加するなどのことではセットは変更されません。追加された値を含む _新しい_ セットが生成されるのです。 内部的には、これは多くの場合、結果としてデータの適切な表現が得られるように、値の効率的な追跡を可能にする異なるデータ構造によって実現されます。

このスタイルでの値とデータ構造の操作は、何かを変更するすべての操作を、それの新しいバージョンを作成するかのように扱うことが求められるため、非常に重要です。 これで、プログラム内で等価性や比較可能性のようなことがらの一貫性を保てます。

## <a name="next-steps"></a>次のステップ

次のセクションでは、関数型プログラミングで使用できるさまざまな方法を紹介しながら、関数について詳しく説明します。

「[ファーストクラス関数](first-class-functions.md)」では、関数について深く掘り下げて、さまざまなコンテキストでそれらを使用できる方法を示します。

## <a name="further-reading"></a>参考資料

「[関数型での思考](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/)」シリーズは、F# を使用した関数型プログラミングについて学習するもう 1 つの優れたリソースです。 関数型プログラミングの基礎について、F# の機能を使用して概念を説明し、実用的で読みやすい方法で解説します。
