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
  - git clone https://github.com/mganeko/kvs_webrtc_example.git
- kvs_keys.js を編集
  - AWS_CHANNEL_ARN ... シグナリングチャネルのARNを指定
  - AWS_ACCESS_KEY_ID ... ユーザーのアクセスキーIDを指定
  - AWS_SECRET_ACCESS_KEY ... シークレットアクセスキーを指定
- ローカルのWebサーバーにhtml, jsファイルを配置

## ブラウザでアクセス



# License / ライセンス

* This sample is under the MIT license
* このレポジトリはMITランセンスで提供されます


