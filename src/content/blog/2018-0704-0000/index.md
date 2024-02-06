---
title: 'ASUSTOR NAS のアプリをマニュアルでダウングレードする'
publishedAt: '2018-07-04T00:00:00+0900'
updatedAt: '2020-12-21T02:40:00+0900'
heroImage: ''
---

## 1. はじめに

ASUSTOR 製の NAS では，多種多様な[アプリ](https://www.asustor.com/ja/admv2?type=1&subject=3&sub=11)が公式のアプリストアを通して配布されており，ユーザーは好きなアプリをインストールすることによって，NAS をカスタマイズすることが出来ます。しかし，アプリのダウングレードは，マニュアルで APK ファイルをダウンロードし，インストールする必要があります。そこで，本記事では ASUSTOR NAS のアプリをマニュアルでダウングレードする手順について記述します。

また，以降の章で行っている作業は AS1004T v2 + ADM Ver.3.5.3.RBH1 環境下で行ったものです。そのため，使用しているモデルや ADM のバージョンによって UI が多少異なる場合もあります。その点はご了承下さい。

## 2. APK のダウンロード

まず初めに，[公式リポジトリ](http://appdownload.asustor.com/)から，ダウングレードしたいアプリの APK をダウンロードします。APK ファイルは，32bit 版，64bit 版，ARM 版が存在するため，各々が所持する NAS のアーキテクチャに合ったアプリをダウンロードする必要があります。異なったアーキテクチャの APK をインストールしようとしても，インストール時にエラーを吐いてくれるので，自分が所持している NAS のアーキテクチャがわからない場合は，3 つ全ての APK ファイルをダウンロードしておいても大丈夫です。

![Official Repository](6abb808777ca8fc7be83c42a6f505fec.png)

## 3. APK のインストール

APK のインストールは，管理者権限が必要になるので，管理者権限が付与されたアカウントに切り替えて作業します。管理者権限が付与されたアカウントに切り替えた後，以下の手順で APK をインストールします。

1. 「App Center」を起動します
2. 「管理」をクリックします
3. 「手動インストール」タブをクリックします
4. 事前でダウンロードした APK を参照し，アップロードします
5. 必要なフォルダ・依存アプリに関して確認します
6. 外部 APK ファイルをインストールするリスクに対して同意します
7. APK ファイルをインストールします

![](e09b064ec37977a219bf17915c2fa38c.png)

## 4. おわりに

ここまで，ASUSTOR NAS のアプリをマニュアルでダウングレードする手順について記述してきました。数年前は，ADM のバージョンを行うと高確率でアプリが動作不良を起こしていましたが，最近は安定している印象です。可能であればダウングレード作業は行いたくないですが，トラブルシューティングとして ASUSTOR の NAS を愛用するユーザの参考になれば幸いです。