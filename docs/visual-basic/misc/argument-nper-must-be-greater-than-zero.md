---
title: 引数 'NPer' は 0 より大きくなければなりません
ms.date: 07/20/2015
f1_keywords:
- vbrRate_NPerMustBeGTZero
ms.assetid: d49242df-dbd1-4b26-bd8c-ed56d24fdfcd
ms.openlocfilehash: f0185e30cb711472105955f5febf8d7702b29c72
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91087142"
---
# <a name="argument-nper-must-be-greater-than-zero"></a>引数 'NPer' は 0 より大きくなければなりません

`NPer` 関数 (定期定額払いおよび固定金利に基づいて年金の期間を指定する `Double` を返します) には、0 を超える引数が必要です。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 式の引数のスペルを確認します。 変数名のスペルが間違っていると、0 に初期化される数値型の変数が暗黙的に生成されることがあります。  
  
- 式の変数 (特に、他のプロシージャから引数としてプロシージャに渡されたもの) に対してこれまで実行した操作を確認します。  
  
## <a name="see-also"></a>こちらもご覧ください

- [引数の値渡しと参照渡し](../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
