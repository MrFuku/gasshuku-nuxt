# ツイッタークローンアプリ
- [サイトURL](http://3.112.193.79:3000/comments)
- [Go側のコード](https://github.com/MrFuku/gasshuku)

## アプリ構成図

![https___qiita-image-store s3 ap-northeast-1 amazonaws com_0_307395_94cb3540-7ebb-ce9e-ab90-b697c496be52](https://user-images.githubusercontent.com/47295890/76173882-d577ec00-61e6-11ea-9b49-a006e574185d.jpeg)

## アプリ概要
- テキスト記事の投稿・編集・削除ができるだけのアプリです
- Nuxt.js / Go を使ったWebアプリ構築の練習のために作りました

## 主な機能
- テキスト記事投稿
  - 記事作成
  - 記事編集
  - 記事削除

## 今回挑戦したこと
- Goを使ったapiサーバー構築
  - WAFを使うこと（Echo）
  - ORM を使ったCRUD処理（Gorm）
- Nuxt.jsでフロントを書くこと
- Docker / ECS 上でのアプリ構築
  - Docker / docker-compose を使った開発環境
  - ECS を使ったデプロイ
- CircleCi を使った CI/CD 環境
  - masterブランチへのマージをトリガーに自動デプロイ

## 今回のやり残したこと（今後やる予定のこと）
- 自動テストを書く
  - Nuxt.js / Go
- GoをDDDで書き直す
- Nuxt をbuildファイルにコンパイルしS3にホスティングする

## 使用した技術
- フロント
  - Nuxt.js
- apiサーバー
  - Go
    - Echo
    - Gorm
- DB
  - RDS(MySQL)
- デプロイ
  - ECS
