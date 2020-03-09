# Browser MCU with KVS WebRTC example

# Descriptiopn / 説明

- This repo is an example for Browser MCU and Amazon Kinesis Video Streams with WebRTC
  - Realize multi-party video chat with Browser MCU seriese
  - based of https://github.com/awslabs/amazon-kinesis-video-streams-webrtc-sdk-js
- これは Amazon Kinesis Video Streams with WebRTC のサンプルです
  - ブラウザMCUを利用して、複数人のビデオチャットを実現します

## Browser MCU Seriese について

- Browser MCU Series is WebRTC MCU using a browser for video/audio processing 
- Browser MCU シリーズは、ブラウザの映像/音声処理を活用した、WebRTC用MCUです 
  - https://github.com/mganeko/browser_mcu

## KVS WebRTC について

- KVS WebRTC には、ルームに相当するシグナリングチャネル、ルームのオーナーに相当する Master、参加者に相当する Viewer がある
- 通信形態は2種をサポート
  - Master が1つ、Viewerが1つの1対1
  - Master が1つ、ViewerがNの1対N
  - いずれもViewerがOffer、MasterがAnswer
- Master-Viewer間の通信方向も双方向、片方向の両方が可能


# 使い方

## 準備

- AWS console の Kinesis Video Streams で 「シグナリングチャネル」を作成
  - シグナリングチャネル名を指定
  - 生成された ARN を確認
- AWS console の IAM でユーザーを作成
  - ユーザー名を指定
  - プログラムによるアクセスを許可（選択）
  - ユーザーグループを作り、AmazonKinesisVideoStreamsFullAccessポリシーを付与
  - 作成したユーザを、そのグループに追加
  - 生成されたアクセスキーID、シークレットアクセスキーを確認
- レポジトリをクローン
  - git clone  --recursive https://github.com/mganeko/kvs_webrtc_example.git
- kvs_keys.js を編集
  - AWS_CHANNEL_ARN ... シグナリングチャネルのARNを指定
  - AWS_ACCESS_KEY_ID ... ユーザーのアクセスキーIDを指定
  - AWS_SECRET_ACCESS_KEY ... シークレットアクセスキーを指定


## ローカルで動かす

- ローカルのWebサーバーにhtml, jsファイルを配置
- ブラウザでMaster(MCU)を開く
  - mcu_master.html
  - ボタンの横に" setup KVS done."と表示されれば初期化完了
- Master(MCU)のウィンドウ/タブで、[Connect]ボタンをクリック
  - "-- signaling client open --" と表示されれば、KVS シグナリングチャネルに接続成功
  - ※Masterのウィンドウ/タブは、完全に隠れてしまわないよう、別ウィンドウにしてどこかに表示しておく必要あり
  - ※完全に隠れてしまうと、画面更新（動画の描画）がポーズしてしまうため
- ブラウザでViewerを開く
  - mcu_master.html
- Viewerのウィンドウ/タブで、[start MCU member(offer)]ボタンをクリック
  - カメラ/マイクへのアクセス許可を求められたら、許可
  - 自分の映像と、MCU masterが合成した映像（最初は1人）が映ったら接続成功
- 2つ目以降のViewerを起動
  - 1つ目と同様、合成した映像の人数が増えていく
- 切断
  - Viewerの切断 ... [stop MCU member]ボタンをクリック
  - Masterの切断 ... [Disconnet]ボタンをクリック

## GitHub Pages　で試す

- ブラウザでラウンチャーページ を開く
  - https://mganeko.github.io/browser_mcu_kvs/
- パラメータを指定する
  - Region ... シグナリングチャネルを作成したリージョン
  - ARN ... 作成したシグナリングチャネルのARN
  - AccessKeyId ... 割り当てたIAMのアクセスキーID
  - AccessSecretKey ... 割り当てたIAMのシークレットアクセスキー
- Masterを起動
  - [open MCU master]ボタンをクリック
    - 開いたウィンドウ/タブが開き、ボタンの横に" setup KVS done."と表示されれば初期化完了
  - 開いたウィンドウ/タブで、[Connect]ボタンをクリック
    - "-- signaling client open --" と表示されれば、KVS シグナリングチャネルに接続成功
  - ※Masterのウィンドウ/タブは、完全に隠れてしまわないよう、別ウィンドウにしてどこかに表示しておく必要あり
    - 完全に隠れてしまうと、画面更新（動画の描画）がポーズしてしまうため
- 最初のViewerを起動
  - [open MCU member(viewer)]ボタンをクリック
    - ※その時のURLを別マシンで開いてもOK
  - 開いたウィンドウ/タブで、[start MCU member(offer)]ボタンをクリック
    - カメラ/マイクへのアクセス許可を求められたら、許可
    - 自分の映像と、MCU masterが合成した映像（最初は1人）が映ったら接続成功
- 2つ目以降のViewerを起動
  - 1つ目と同様、合成した映像の人数が増えていく


# License / ライセンス

* This sample is under the MIT license
* このレポジトリはMITランセンスで提供されます


