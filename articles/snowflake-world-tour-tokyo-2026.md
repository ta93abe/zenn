---
title: "Snowflake World Tour Tokyo 2026 に行ってきたよー"
emoji: "🎿"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["snowflake"]
published: true
---

9/12, 9/13 と 2 日間にわたって毎年恒例の Snowflake World Tour Tokyo が開催されました。毎年足を運んでいます。
登録がちょっと遅かったのもあって今年はブレイクアウトセッションを回るのではなく、EXPO の対角線で交互に繰り広げられるシアターセッションを反復横跳びしていました。

というわけでいち参加者のラップアップにお付き合いください。時系列に書き出しているはずです。


## Snowflakeで業務アプリを作ろう。Snowflakeのアプリ機能解説＆実践ガイド

https://x.com/Yamaguchi_aaaaa/status/2097892589139800374

Streamlit in Snowflake, Snowflake App Runtime, Snowpark Container Services と Snowflake 内でアプリを構築するための選択肢は増えていますが、じゃあそのアプリはどれを使って構築するかを選択する必要があります。この意思決定をサポートするための優れたガイドでした。
これからは Snowflake App Runtime で何かを作る機会が増えそうです。Skill に抗って Next.js じゃなくて Tanstack Start や Remix を使っていきましょうかね。

https://www.youtube.com/@DataEngineerCasualRadio

山口さんは同僚でありながら Data Engineer Casual Radio をホストしているのでいちリスナーとして楽しんでいます。

## Adaptive Warehouse を今すぐ導入すべき理由と迷ったときの判断基準

https://x.com/__allllllllez__/status/2098194383334256680

6 月に GA したばかりなので使っていないぞという人もいるでしょうか。サイズどれがいいかなということはせず、ワークロードに最適なものを自動で選択してくれるようになります。管理がなくなるのは嬉しいですね。
手軽に導入できるので、まずは検証してみるというのもできますし、このスライドでどういったワークロードには向いているぞ向いていないぞが書かれているので参考になります。


## dbt CoreとSnowflakeで実現する多層的なデータガバナンス

https://x.com/civitaspo/status/2098270535855870306

Snowflake の Row Access Policy や Column Masking Policy を使ってユーザーロールによってデータを見せないようにすることができますが、それを dbt で付与してくと統制が取りやすいですね。

https://github.com/civitaspo/dbt-authorized-models

その中でも civi さんが公開したこの OSS を使ってみたいと思いました。CI 時に許可していないモデルの依存関係を作れないようにすることができるものでホワイトリスト形式で許可していきます。
source は staging からしか参照されないなどの style guide を強制する使い方がぱっと思いつきました。こんな感じ。

```yaml
sources:
    your_project_name:
      +meta:
        authorize:
          - resource_type: model
            database: analytics
            schema: staging
```

## Snowflakeのコスト最適化を支えるアーキテクチャ設計

https://x.com/cs_dev_engineer/status/2098406802052514161

鮮度などのサービスレベルをそこまで求められないワークロードにおいてカリカリにパフォーマンスチューニングをすることが最適なのかというとそうではないですよね。クエリプロファイルを見てスピルしているとすぐにウェアハウスサイズを上げてしまいがちですが1つ大きくするなら半分以下の実行時間にならないとコストが下がらないということは肝に命じておかないといけないです。課金の大半がコンピュートコストになるので改めてそこでウェアハウスを動かす必要があるのか、サイズを上げる必要があるのかは考えて設計する必要があります。
Iceberg テーブルもそんなに構えないでもどの企業にも使い所はあるのでメリットを理解して導入していくとよいと思いました。



https://x.com/takimiko_gohan/status/2098274897680097685

https://x.com/yuto16s/status/2098244945928925565


こみぃさん
Resharing
デジタル庁さんカレンダーAPIをという話があったが、PODBがあるし、それに対して自社の非営業日などを足してReshareできるじゃん


https://x.com/mmjjaadmm/status/2098317252403908837



コミュニティーブース
行く決定が直前過ぎたので何もできなかった
初日にの最初に九州にシールを貼った。２日目には結構貼られていた。九州でもまたSnowflakeのユーザーイベントやりますよ。
