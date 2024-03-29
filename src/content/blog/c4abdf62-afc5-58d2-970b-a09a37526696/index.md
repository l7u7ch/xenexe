---
title: 'ブログサイト開発フレームワークとして Gatsby と Hugo を比較する'
publishedAt: '2022-09-12T07:56:02.310Z'
updatedAt: '2022-09-16T23:38:54.821Z'
heroImage: './52cbc1f3.png'
---

## 1. はじめに

近年，多種多様な Static Site Generator (SSG) が登場しています [^1] 。その中から，自分の目的に合った SSG を選択するのは非常に難しいと思います。筆者は，これまで Gatsby と Hugo を用いてブログサイトを開発してきました。その開発過程で，両者の共通点と相違点をいくつか発見しました。本記事は，その開発過程で発見した，いくつかの共通点と相違点を開発過程をまとめた記事です。

[^1]: Jamstack, Site Generators, https://jamstack.org/generators/.

## 2. 比較対象概要

[Gatsby](https://github.com/gatsbyjs/gatsby) と [Hugo](https://github.com/gohugoio/hugo) は，Static Site Generator (SSG) と呼ばれるジャンルに属する Free/Libre and Open Source Software (FLOSS) です。Gatsby は，Javascript/Typescript を用いた React をテンプレートエンジンを採用しています。一方，Hugo は Go を用いた独自のテンプレートエンジンを採用しています。

## 3. 機能性・連携性

本章では，機能性と連携性の観点から Gatsby と Hugo の共通点と相違点を記述していきます。本記事では，機能性を，ブログサイトを開発する際に実装できる機能のカバー率。連携性を，ブログサイトを開発する際に連携できる外部アプリのカバー率と定義しています。まず初めに，Gatsby と Hugo の両者で実装・連携できるものを以下に示します。いずれも，著者が開発過程で確認したものを列挙しているので，読者の関心対象が含まれていない場合が多々あると思いますが，ご容赦ください。

- 実装可能な機能一覧
  - Markdown，LaTeX，Syntax Highlight の表示
  - 目次 (TOC)，カテゴリー，タグクラウド，年別・月別アーカイブの実装
  - 人気記事，最新記事，関連記事の実装
  - RSS，sitemap.xml，robots.txt の生成
  - AMP，PWA の実装

* 連携可能な外部アプリ一覧
  - [Tailwind CSS](https://tailwindcss.com/): ユーティリティ思考の CSS フレームワーク
  - [Contentful](https://www.contentful.com/): ヘッドレスコンテンツ管理システム
  - [Algolia](https://www.algolia.com/): 検索エンジン提供サービス
  - [Disqus](https://disqus.com/): コメント機能提供サービス

次に，Gatsby と Hugo の特徴的な機能について記述していきます。Gatsby の特徴として，MDX に対応している点が挙げられます。MDX [^2] は Markdown 上に JSX を記述可能に拡張したものです。プレーンな Markdown と比較して，表現力が格段に向上します。この機能は JSX を用いるため，Hugo で同様の機能を実現することは，執筆時点では出来ないないようです。Hugo の特徴として，ビルド時間の速さが挙げられます。Hugo は Google が開発している Go 言語を用いて開発されているため，その他の SSG と比較してもビルド時間が格段に速いです [^3] 。数値的には数秒の差ですが，実行を繰り返す開発期間やブログ記事が増えてきた際に顕著な差として現れます。

[^2]: Markdown for the component era, https://mdxjs.com/.
[^3]: Sean C Davis, Comparing Static Site Generator Build Times, https://css-tricks.com/comparing-static-site-generator-build-times/, 2020.

## 4. 学習コスト・開発コスト

ブログサイトを開発する際，Gatsby を採用する場合も Hugo を採用する場合も，基本的な HTML と CSS の事前知識は必要になります。Gatsby を採用する場合は，基本的な HTML と CSS の事前知識に加え，Node.js，React，GraphQL などの事前知識が推奨されます。これらの事前知識を前提として Gatsby 本体の勉強に着手可能です。一方，Hugo を採用する場合は，基本的な HTML と CSS の事前知識があれば，すぐに Hugo 本体の勉強に着手可能です。よくある質問で「Hugo を採用する場合は Go の事前知識が必要ですか？」という質問が存在します。個人的には，Hugo を採用する際に，Go の事前知識は必要ありません。これらの経験から，学習コストに関しては Gatsby が総合的に高くなると思います。

Gatsby と Hugo は，共に開発コストが増大するラインが存在すると経験則的に感じます。Gatsby は公開されているプラグインの機能以上を実装しようとすると開発コストが増大します。Hugo は 公式ドキュメントに記述されている機能以上を実装しようとすると開発コストが増大します。また，Gatsby と Hugo は設計思想が異なります。Gatsby は，開発しようとしているブログサイトの目的に応じてプラグインをインストールするマイクロアーキテクチャです。一方，Hugo は，最初から Hugo 本体にブログサイトを開発する際に必要となる機能が実装されているモノリシックアーキテクチャです。拡張性が高いのは，プラグインシステムを採用している Gatsby だと思います。

## 5. 注目度

Gatsby と Hugo に対する注目度を「GitHub Star」「Qiita に投稿されている記事数」「Zenn に投稿されている記事数」「出版されている 日本語書籍」という観点から定量化しました。なお，以下に示した数値は執筆時点 (2022 年 9 月 14 日) の数値であり，変動する可能性があることを，ご注意ください。

|                                                |   Gatsby    |    Hugo     |
| :--------------------------------------------: | :---------: | :---------: |
| <span className="font-bold">GitHub Star</span> | 53,500 Star | 61,800 Star |
|    <span className="font-bold">Qiita</span>    |  544 記事   |  277 記事   |
|    <span className="font-bold">Zenn</span>     |  127 記事   |   41 記事   |
| <span className="font-bold">日本語書籍</span>  |    5 冊     |    1 冊     |

2020 年ごろまでは，Gatsby と Hugo の GitHub Star は拮抗していました [^4] 。しかし，現在は 10,000 Star 以上の差が発生しています。その一方で，「Qiita に投稿されている記事数」「Zenn に投稿されている記事数」「出版されている 日本語書籍」は，Gatsby に関するものが多い傾向です。以上のデータから，グローバルでは Hugo への注目が高く，国内においては Gatsby への注目が高いという可能性が考えられます。

[^4]: Rachel Stephens, Static Site Generator Trends, https://redmonk.com/rstephens/2020/05/18/static-site-generators/, 2020.

## 6. おわりに

ここまで，ブログサイト開発フレームワークとして Gatsby と Hugo の共通点と相違点を記述してきました。最後に，著者が最終的に Gatsby を採用した理由を述べて終わりたいと思います。Hugo で Contentful や Algolia と連携する場合，既存の Node Package を利用します。そうすると 1 プロジェクトに Go の開発環境と Node.js の開発環境が混在するようになります。であれば，最初から Node.js 環境で統一したい思い，Gatsby を採用することにしました。長々と執筆してきましたが，本記事が SSG 選びの参考になれば幸いです。
