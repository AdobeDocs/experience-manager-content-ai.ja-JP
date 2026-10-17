---
cloud: Experience Cloud
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: "Experience Manager"
usetq: true
type: Documentation
git-repo: https://github.com/AdobeDocs/experience-manager-content-ai.en
index: true
recommendations: noDisplay
source-git-commit: a47559544a9e972285ba570f16a38272b35794a8
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 2%
---

# 内部使用のためのメタデータ

GitHub オーサリングシステムのメタデータは階層であり、次のレベルの前例で定義されています。

1. metadata.md
1. ToC
1. 記事

metadata.md ファイルで定義されたメタデータは、リポジトリ全体に適用されますが、ToC レベルとアーティクルレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

experience-manager-content-ai.en リポジトリ内のメタデータは、必要な最小値です。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
