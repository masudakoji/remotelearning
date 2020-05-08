---
title: "OBSを仮想カメラとして動作させる"
date: 2020-05-07
draft: false
tags: 
  - obs
  - google meet
  - live streaming
  - teacher
---

## OBSとは
YouTubeなどでライブ配信するときなどに使うソフトで、これで動画も作成する事が出来ます。

> 動画作成については[OBSを使って動画を作成・配信する]({{<ref "getting-started-obs">}})を参考にしてください。

> ライブ配信に関しては[YouTubeで動画を共有する（OBSでライブ配信）]({{<ref "live-streaming-with-obs-on-youtube">}})を参考にしてください。

ただ、これだとYouTubeなどの配信には使えますが、Google Meetなどのソフトでは使えません。
しかし、OBSに別のプラグインなどを追加すると仮想的なウェブカメラとして動作させる事が出来ますので、Google Meetなどでカメラとして設定すれば、OBSからGoogle Meetに参加する事ができます。

## 仮想カメラとして動作させる（Windows）
Windowsの場合は、OBSを仮想カメラとして動作させるプラグインが作成されているので、それをインストールすれば、完了します。
[obs-virtual-cam](https://github.com/Fenrirthviti/obs-virtual-cam/releases)にアクセスして、インストーラーをDLして、インストールしてください。
インストール時はOBSを終了しておいたほうが良いかと思います。

インストールが完了すれば、OBSを起動して、「ツール」から「Start Virtual Camera」をクリックすると仮想カメラが立ち上がります。
ブラウザでGoogle Meetなどにアクセスすると、カメラの選択時に「OBS Virtual Camera」が追加されていますので、それを選択してください。
ブラウザは、仮想カメラを立ち上げた後に、再起動する必要があるかもしれません。

> 使い方は[OBS Virtualcam](https://obsproject.com/forum/resources/obs-virtualcam.949/)にも書かれています。


## 仮想カメラとして動作させる（Mac）
Macの場合は少し厄介で、Windowsのようにプラグインを配置したりインストールするだけでは使えないので、自分でビルドする必要があります。
OBSに仮想カメラ機能を追加するソフトウェアに関しては公開されていますので、そこで示されているように実行すれば、仮想カメラ機能が追加さればOBSがビルドされます。

[obs-mac-virtualcam](https://github.com/johnboiles/obs-mac-virtualcam)に記載されている通りです。

    # Clone and build OBS
    git clone --recursive https://github.com/obsproject/obs-studio.git
    cd obs-studio

    # Follow normal OBS build steps
    brew install FFmpeg x264 Qt5 cmake mbedtls swig
    mkdir build
    cd build
    # Note: if you installed homebrew to a custom location, this will be $BREW_INSTALL_PATH/opt/qt
    export QTDIR=/usr/local/opt/qt
    cmake .. && make -j

    # Clone this repo
    cd ../..
    git clone https://github.com/johnboiles/obs-mac-virtualcam.git
    cd obs-mac-virtualcam

    # Set an environment variable that points to the directory for your OBS clone
    export OBS_DIR=$PWD/../obs-studio

    # Build the plugin
    mkdir build
    cd build
    cmake -DLIBOBS_INCLUDE_DIR:STRING=$OBS_DIR/libobs -DLIBOBS_LIB:STRING=$OBS_DIR/build/libobs/libobs.dylib -DOBS_FRONTEND_LIB:STRING=$OBS_DIR/build/UI/obs-frontend-api/libobs-frontend-api.dylib -DQTDIR:STRING=$QTDIR ..
    make -j

    # Copy the OBS plugin to your local OBS build
    cp src/obs-plugin/obs-mac-virtualcam.so $OBS_DIR/build/rundir/RelWithDebInfo/obs-plugins/

    # Remove any existing plugin and copy the DAL plugin to the right place
    sudo rm -rf /Library/CoreMediaIO/Plug-Ins/DAL/obs-mac-virtualcam.plugin && sudo cp -r src/dal-plugin/obs-mac-virtualcam.plugin /Library/CoreMediaIO/Plug-Ins/DAL

    # Run your build of OBS
    cd $OBS_DIR/build/rundir/RelWithDebInfo/bin
    ./obs

ビルドが完了したら、ビルドしたOBSを立ち上げてください。後はWindows版と同様です。


すでにYouTube配信などのために、OBSをインストールされているかもしれませんが、そちらと混同しないようにしましょう。
ビルド済みのobsがどこにあるかがわかりづらいので、下記の様なシェルスクリプトを用意しておいたほうが良いかも知れません。
パスは適宜修正してください。

    cd obs-studio/build/rundir/RelWithDebInfo/bin
    ./obs

