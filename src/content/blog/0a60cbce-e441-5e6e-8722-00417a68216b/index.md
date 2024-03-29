---
title: 'OGP と Twitter Card の設定に必要なメタタグに関する考察'
publishedAt: '2022-09-21T04:16:41.924Z'
updatedAt: '2022-09-21T04:16:41.924Z'
heroImage: './e1d7b85e.png'
---

## 1. はじめに

近年，Open Graph Protocol (OGP) と Twitter Card の設定は，Search Engine Optimization (SEO) の観点から必須となりつつあります。OGP と Twitter Card の設定に関する情報は，ネット上に多く散見されます。しかし，その情報の多くは一貫しておらず，表記揺れが存在します。本記事は，OGP と Twitter Card に関する一次情報を参照し，OGP と Twitter Card の設定に必要なメタタグに関する考察をまとめた記事です。

## 2. OGP

OGP は，Facebook (現 Meta) によって開発されたプロトコルであり，一次情報として，OGP の公式ドキュメント [^1] と Meta の開発者向けドキュメント [^2] が挙げられます。OGP の公式ドキュメント [^1] では，メタタグが Basic Metadata と Optional Metadata に分類されています。一部，抜粋したものを以下に示します。

- Basic Metadata
  - og:title
  - og:type
  - og:image
  - og:url
- Optional Metadata
  - og:audio
  - og:description
  - og:determiner
  - og:locale
  - og:locale:alternate
  - og:site_name
  - og:video

一方，Meta の開発者向けドキュメント [^2] では，メタタグが Basic Tags と Optional Tags に分類されています。一部，抜粋したものを以下に示します。

- Basic Tags
  - og:url
  - og:title
  - og:description
  - og:image
  - fb:app_id
- Optional Tags
  - og:type
  - og:locale

両者で重複しているメタタグは，`og:url`，`og:title`，`og:image` です。そのため，`og:url`，`og:title`，`og:image` は設定した方が良いと思います。重複していない `og:type`，`og:description`，`fb:app_id` は Meta が提供しているシェアデバッカー [^3] で必須プロパティとして検知されます。`fb:app_id` は Facebook Insights を利用するためのメタタグなので，利用しない人は無視して良いと思います。`og:type` と `og:description` はシェアデバッカー [^3] で必須となっているので，設定した方が良いと思います。`og:site_name` と `og:locale` に関しては，調査した範囲の中で必須とする根拠が見つけられなかったので，本記事ではオプションとします。

[^1]: Meta, The Open Graph protocol, [https://ogp.me/](https://ogp.me/).
[^2]: Meta, ウェブ管理者向けシェア機能ガイド, [https://developers.facebook.com/docs/sharing/webmasters/](https://developers.facebook.com/docs/sharing/webmasters/).
[^3]: Meta, シェアデバッカー, [https://developers.facebook.com/tools/debug/](https://developers.facebook.com/tools/debug/).

## 3. Twitter Card

Twitter Card の一次情報として Twitter の開発者向けドキュメント [^4] が挙げられます。Twitter の開発者向けドキュメント [^4] では，メタタグが Required と Not Required に分類されています。一部，抜粋したものを以下に示します。

- Required
  - twitter:card
- Not Required
  - twitter:site
  - twitter:creator

`twitter:card` は必須なので，設定した方が良いと思います。`twitter:site` と `twitter:creator` に関しては，調査した範囲の中で必須とする根拠が見つけられなかったので，本記事ではオプションとします。

[^4]: Twitter, ツイートをカードで最適化する, [https://developer.twitter.com/ja/docs/tweets/optimize-with-cards/guides/getting-started](https://developer.twitter.com/ja/docs/tweets/optimize-with-cards/guides/getting-started).

## 4. おわりに

ここまで，OGP と Twitter Card に関する一次情報を参照し，OGP と Twitter Card の設定に必要なメタタグを考察してきました。最後に，OGP と Twitter Card の設定に必要なメタタグを Required と Optional に分類した成果物を以下に示します。なお，以下の成果物は著者が調査した範囲で作成した成果物であり，SEO の品質を保証するものではないことに注意ください。

- Required
  - og:url
  - og:title
  - og:image
  - og:type
  - og:description
  - twitter:card
- Optional
  - og:type
  - og:description
  - twitter:site
  - twitter:creator
