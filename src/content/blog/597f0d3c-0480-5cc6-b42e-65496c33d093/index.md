---
title: 'Gatsby + Contentful で childMdx が表示されない原因と解決策'
publishedAt: '2022-09-17T19:00:15.731Z'
updatedAt: '2023-09-20T19:46:19.085Z'
heroImage: './7d30957f.png'
---

## 1. はじめに

Gatsby では，gatsby-source-contentful と gatsby-plugin-mdx を用いることによって，Contentful に保存されている Markdown を MDX で読み込むことが出来ます。しかし，公式ドキュメントに従って  gatsby-source-contentful と gatsby-plugin-mdx をインストールしても  GraphiQL 上で childMdx が表示されません。本記事は，この問題に対する原因と解決策をめとめた記事です。

本記事では，以下の環境が整っていることを前提に記述しています。ツールのインストール方法やアカウントの登録方法は割愛していますので，以下の環境が整っていない場合は，各自で準備をお願います。

- Git と Yarn はインストール済み
- Contentful のアカウントは作成済み
- Contentful を操作するのに必要な  Access Tokens を取得済み
  - Space ID
  - Content Management API Access Token
  - Content Delivery API Access Token

## 2. テスト環境構築

テスト環境として，Contentful が公開している  Gatsby Theme である  [Contentful Gatsby Starter Blog](https://github.com/contentful/starter-gatsby-blog) を用います。ドキュメントに従い，ローカル環境に Contentful Gatsby Starter Blog をクローン，Node Package をインストール，必要なコンテンツモデルのセットアップと構成ファイルの作成を行います。セットアップ中に Locale エラーが発生した場合は，ブログ記事 [^1] を参考に **export.json** を書き換えます。実行後，**http://localhost:8000/** にアクセスしてコンテンツが表示されれば成功です。

[^1]: minamo, GatsbyJS + Contentful を試してみる。, [https://zenn.dev/minamo173](https://zenn.dev/minamo173), 2020.

```bash
$ git clone https://github.com/contentful/starter-gatsby-blog
$ cd starter-gatsby-blog
$ yarn
$ yarn setup
? Your Space ID [SPACE_ID]
? Your Content Management API access token [CONTENT_MANAGEMENT_API_ACCESS_TOKEN]
? Your Content Delivery API access token [CONTENT_DELIVERY_API_ACCESS_TOKEN]
$ yarn dev
```

次に，gatsby-plugin-mdx をドキュメント [^2] に従ってインストールします。

[^2]: Gatsby, gatsby-plugin-mdx, [https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/](https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/).

```bash
$ yarn add gatsby-plugin-mdx @mdx-js/react
```

```jsx title="gatsby-config.js" {23}
require('dotenv').config({
  path: `.env.${process.env.NODE_ENV}`,
})

module.exports = {
  siteMetadata: {
    title: 'Gatsby Contentful Starter',
    description: 'Official Contentful Gatsby Starter',
  },
  plugins: [
    'gatsby-transformer-sharp',
    'gatsby-plugin-react-helmet',
    'gatsby-plugin-sharp',
    'gatsby-plugin-image',
    {
      resolve: 'gatsby-source-contentful',
      options: {
        spaceId: process.env.CONTENTFUL_SPACE_ID,
        accessToken: process.env.CONTENTFUL_ACCESS_TOKEN,
        host: process.env.CONTENTFUL_HOST,
      },
    },
    `gatsby-plugin-mdx`,
  ],
}
```

## 3. 問題点

**<http://localhost:8000/___graphql>** にアクセスすることで GraphiQL が立ち上がり，取得可能なデータがリストで表示されます。既存のブログ記事 [^3] では，**allContentfulBlogPost.nodes.body.body** の直下に **childMdx** が表示されると記述されていますが，表示されません。

[^3]: Ayumi Takahashi, Gatsby + Contentful のブログ記事を MDX で書く方法, [https://ayumitk.com/ja/blog/mdx-blog-posts-with-contentful/](https://ayumitk.com/ja/blog/mdx-blog-posts-with-contentful/), 2020.

![09840185](09840185.png)

## 4. 原因

gatsby-plugin-mdx の公式ドキュメント [^2] より，gatsby-plugin-mdx Ver.4.X.X では，ファイルシステム以外の MDX を読み込むことが出来ないようです。

> Please Note: Loading MDX from other sources as the file system is not yet supported in gatsby-plugin-mdx@^4.0.0.

## 5. 解決策

本記事では，gatsby-plugin-mdx を Ver.3.X.X にダウングレードすることで解決する方法を記述します。gatsby-plugin-mdx Ver.3.X.X でサポートされている MDX は Ver.1.X.X であり，gatsby-plugin-mdx Ver.4.X.X で対応している MDX Ver.2.X.X は使用出来ない点に注意ください。

gatsby-plugin-mdx Ver.3.20.0 のドキュメント [^4] に記載されているインストールコマンドを，そのまま実行すると最新バージョンの gatsby-plugin-mdx がインストールされるため，バージョン指定を加えたインストールコマンドを以下に示します。**gatsby-config.js** は，gatsby-plugin-mdx Ver.4.X.X と同じです。

[^4]: npm, gatsby-plugin-mdx, [https://www.npmjs.com/package/gatsby-plugin-mdx/v/3.20.0](https://www.npmjs.com/package/gatsby-plugin-mdx/v/3.20.0).

```bash
$ yarn add gatsby-plugin-mdx@^3 @mdx-js/mdx@^1 @mdx-js/react@^1
```

```jsx title="gatsby-config.js" {numberLines:true} {23}
require('dotenv').config({
  path: `.env.${process.env.NODE_ENV}`,
})

module.exports = {
  siteMetadata: {
    title: 'Gatsby Contentful Starter',
    description: 'Official Contentful Gatsby Starter',
  },
  plugins: [
    'gatsby-transformer-sharp',
    'gatsby-plugin-react-helmet',
    'gatsby-plugin-sharp',
    'gatsby-plugin-image',
    {
      resolve: 'gatsby-source-contentful',
      options: {
        spaceId: process.env.CONTENTFUL_SPACE_ID,
        accessToken: process.env.CONTENTFUL_ACCESS_TOKEN,
        host: process.env.CONTENTFUL_HOST,
      },
    },
    `gatsby-plugin-mdx`,
  ],
}
```

**<http://localhost:8000/___graphql>** にアクセスし，**allContentfulBlogPost.nodes.body.body** の直下に **childMdx** が表示されていれば成功です。

![5ec88858](5ec88858.png)

## 6. おわりに

ここまで，GraphiQL 上で childMdx が表示されない問題に対する，原因と解決策について記述してきました。今後のアップデートで，ファイルシステム以外の MDX を読み込めるようになると思うので，それまでは Ver.3.0.0 で運用しようと思います。本記事が，同じ問題に直面している人の役に立てば幸いです。
