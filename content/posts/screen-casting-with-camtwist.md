---
title: "Google Meetでの画面共有に手書き文字を書く (Mac対象)"
date: 2020-04-21
draft: false
tags: 
  - teacher
  - google meet
  - mac
  - camtwist
---

## Google Meetでの画面共有
[#Google Meet]({{<ref "../tags/google-meet/">}})では自分の画面を共有することができます。デスクトップ全体を共有したり、個別のウインドウを共有したりできます。詳細は[会議中に自分のPCの画面を共有]({{<ref "cast-your-screen.md">}})を参照にしてください。ですが、Google Meetの機能では単純な画面共有で、手書きのメモを記入したりはできません。ここでは、別のソフトを介してこの機能を実現します。今回紹介するのはMac用のソフトですが、Windowsでも同様のソフトはあるかと思います。

## CamTwist
[#CamTwist]({{<ref "../tags/camtwist/">}})は仮想的なカメラとして動作します。インストールすると、Google Meetの動画入力にCamTwistが表示されます。


### インストール
[http://camtwiststudio.com](http://camtwiststudio.com)にアクセスしてインストールしてください。Mac OS 10.10以上が推奨されています。DLしたdmgファイルを実行するとインストールができます。最近のMac OS（Sierra以降）だと「開発元が未確認」というエラーが出ますので、適切に対応してください。（[開発元が未確認のMacアプリケーションを開く](https://support.apple.com/ja-jp/guide/mac-help/mh40616/mac)を参照）


### 動作画面と初期設定
インストールして起動するとこのような画面が出て来ます。
{{<figure src="1.png" title="動作画面" class="center">}}

Step 1では入力する映像ソース（webカメラやデスクトップやアプリケーションの画面など）を選択します。Step 2では様々なエフェクトをかけることができます。手書きなどもここで呼び出します。Step 3では設定の確認と保存・呼び出しなどができます。

Preferencesを開くと、出力解像度やFPSなどが設定できます。初期設定だと解像度が低いので適宜調整してください。ただし、解像度をあげすぎると処理落ちする可能性があるので、PCの能力に合わせて調整してください。
{{<figure src="2.png" title="設定画面" class="center" width="350">}}


### webカメラの映像をそのまま出力する
まずは動作確認のために、webカメラをそのまま出力します。Step 1でWebcamを選択してアプリ下部の「Select」をクリックするとStep 3に「Webcam」が追加されます。
{{<figure src="3.png" title="Webカメラ呼び出し" class="center">}}


Google Meetの設定（[画質などの設定]({{<ref "join-meeting/#画質などの設定">}})を参考）を開いて、動画の設定を開くとカメラのソースを選択できますが、CamTwistインストール前は内臓のwebカメラや外付けのwebカメラが表示されるはずですが、ここにCamTwistという名前の仮想的なカメラが表示されます。CamTwist（2VUY）を選べばよいです。問題があればCamTwistを選択してみてください。

{{<figure src="4.png" title="Google MeetでCamTwistをカメラとして呼び出す" class="center" width="450">}}

これでGoogle Meetで相手に動画がCamTwist経由で配信されます。

### アプリケーションの画面を出力する
Step 1で「Desktop+」を選択するとデスクトップの画面を配信できます。「Full Screen」にチェックが入っているとデスクトップ全体が共有されますが、「Confine to Application Window」を選択するとアプリケーションの画面を共有できます。「Select from existing windows」からアプリケーションを選択してください。

{{<figure src="5.png" title="アプリケーションを選択して出力" class="center">}}

ただ、PowerPointの場合、フルスクリーンにするとアプリケーションとの接続が切れてしまいます。その場合アプリケーション名を正規表現で指定します。例えば「Regex Search」に"PowerPoint"と入力するとPowerPointをフルスクリーン表示にしても捕捉し続ける事が出来ます。他のアプリケーションも正規表現を使って指定すれば対応はできるかと思います。

{{<figure src="6.png" title="アプリケーション名を正規表現で指定" class="center">}}

### 手書き文字を重ねる（推奨: ペンタブ）
webカメラやアプリケーションの画面に手書きを重ねるためにはStep 2で「Telestrator」を選択してください。選択すると、手書き入力画面が出て来ますので、色やペンサイズなどを設定して手書きすれば、その手書きが重なった状態で配信されます。

{{<figure src="7.png" title="手書き入力画面" class="center" width="350">}}
{{<figure src="8.png" title="手書き入力画面" class="center" width="350">}}

Google Meet上では左右が反転して見えていますが、問題はありません。相手には反転してない状態で配信されています。

{{<figure src="9.png" title="Google Meet上では左右反転して見える" class="center" width="450">}}

マウスやトラックパッドでもできますが、ペンタブがあるともっと書きやすくなると思います。ペンタブの使い方や設定はそれぞれの説明を参考にしてください。

webカメラや何らかのアプリケーションの上に手書き文字を重ねることもできますが、Video source (WebcamとかDesktopとか) なしでも手書き入力は出来ます。ただ、その場合背景が黒になってしまいますが、「Color Invert」フィルタをかけると白黒反転するので、ホワイトボード？的に使う事が出来ます。フィルタの順番には注意しましょう。

### クロマキー合成（推奨: グリーンバック）
Google Meetには背景を変える機能はないのですが、CamTwistにはクロマキー合成機能がありますので、webカメラを使いながら背景を変える事も出来ます。背景に風景画像？を使う事も出来ますし、PowerPointのスライドを背景にする事も出来ます。

PIPの設定にはプレビューがあったほうが便利です。CamTwistのメニューバー → 「View」 → 「Preview」でプレビュー画面が表示されます。

Step 1でWebcamを選択して、アプリ下部の「PIP」ボタン（PIPとはPicture in Pictureの意味です）を押します。PIPの設定画面でScaleを変更すると倍率が変わります。Scale2でちょうど画面いっぱいになると思います。

クロマキー合成を使うには、「Chroma Key」にチェックを入れてください。その下で色を選ぶと、選んだ色と同じ色が透過されます。透過されるということは、その下にある画像が透けてみえるということです。下に背景画像があればそれが見えますし、PowerPointのスライドがあればそれが見えます。CamTwistではStep 3で上に配置されている映像ソース・フィルタが最背面になります。背景にしたいものを一番上に配置することになります。



{{<figure src="10.png" title="PIPの設定画面" class="center">}}

クロマキー合成をするといっても光の当たり方や布のシワなどの影響で、全体に綺麗に抜けなかったりするので、色やThresholdを微調整しましょう。また、「Crop Left」などを変更するとwebカメラ映像を切り抜いたり、Positionを変更してwebカメラ映像の配置を変更したり出来ます。

クロマキー合成で背景を抜いた動画の後ろにパワポのスライドを配置して手書きで文字入力した例です。

{{<figure src="11.png" title="クロマキー合成で背景を抜いてパワポに手書き入力" class="center" width="500">}}
