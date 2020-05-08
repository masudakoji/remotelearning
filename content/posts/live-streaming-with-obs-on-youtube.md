---
title: "YouTubeで動画を共有する（OBSでライブ配信）"
date: 2020-05-05
draft: false
tags: 
  - teacher
  - youtube
  - live streaming
  - google classroom
  - obs
---

## OBSを使ってYouTubeライブ配信
ライブ配信の基本的な流れはWebカメラを使った時と同様です。

> webカメラを使ったYouTubeライブ配信は[YouTubeで動画を共有する（Webカメラでライブ配信）]({{<ref "live-streaming-on-youtube">}})を参考にしてください。


#### YouTube Studioでの設定
https://studio.youtube.com/
にアクセスします。ライブ配信ボタンを押すとライブ配信管理画面が出ますので、「エンコーダ配信」を選択して下さい。
{{<figure src="1.png" title="エンコーダ配信開始" class="center">}}

「ウェブカメラ配信」の時と同様に、タイトルなどを設定します。
{{<figure src="2.png" title="タイトルなど設定" class="center">}}

配信の準備が完了しました。ただ、まだ配信ソフト（OBS）からの映像が届いていないので、プレビュー画面には何も映像が表示されていません。「ストリーミングソフトウェアに接続してプレビューを開始します。」とだけ表示されています。

ここで、ストリームキー（エンコーダに貼り付け）という項目があります。このストリームキーが配信のためのパスワードのようなものです。このストリームキーがあると、他の人がなりすまして配信することが出来てしまいますので、知られないようにしてください。このストリームキーをコピーしておきます。
{{<figure src="3.png" title="配信準備完了" class="center">}}

#### OBSでの設定
OBSを開いて、設定ボタンを押すと、設定画面が出てきますので、「配信」メニューを開いてください。
- サービスとして「YouTube / YouTube Gaming」
- サーバーとして「Primary YouTube ingest server」

を選択して、先ほどコピーしたストリームキーをペーストします。
{{<figure src="4.png" title="YouTube Studioで生成したストリームキーを貼り付け" class="center">}}

これでOBSの設定が完了しました。OBSの「配信開始」ボタンを押すと、OBSからYouTubeにデータが送信されます。YouTube Studioのライブ配信管理画面に戻るとOBSからの映像が届いているはずですので、確認ができたら「ライブ配信を開始」ボタンを押すと、ライブ配信がはじまります。
{{<figure src="3.png" title="配信準備完了" class="center">}}


#### 同じ設定を使って配信
一度エンコーダ配信をすると、今度も同じ設定を呼び出して配信することが出来ます。むしろ、同じ設定を呼び出して配信を作成しないと、毎回ストリームキーがリセット（再生成）されるので、その度にOBSの設定を行う必要がありますので、「前回の設定を使用して配信」するのがベターだとは思います。

{{<figure src="6.png" title="前回の設定を使用して配信" class="center">}}
