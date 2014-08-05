api_design-resources
====================

A list of resources to design good API.

- [Heroku HTTP API Design Guide](https://github.com/interagent/http-api-design) - Heroku でまとめられた、API のデザイン指針
- [《REST思想》と《リソース指向》と《Webページ》に関する（主にRailsの）話](http://qiita.com/tkawa/items/9bd50e80cfe354062dfb) - よい URL とは？ REST とリソース指向から読み解くURL
- [アジャイルAPI設計時代の到来！？APIデザインの極意を読みました。](http://kozake.hatenablog.com/entry/2014/08/03/232443) - ヤバい API 本
- [すべてがJSONになる](http://r7kamura.hatenablog.com/entry/2014/06/10/023433) - JSON Schema を利用して、Validation や Doc, API Client を自動的に用意する
- [NetflixのAPIプラットフォーム](http://wazanova.jp/items/1114) - フロントエンドチームが API をカスタマイズできるようにしている
- [モバイルAPIデザインのまとめ](http://wazanova.jp/items/1283) - Etsy での API デザイン。モバイルのために、如何に必要な API コール回数を減らすかを考える。
- [\[その１\] Netflix: APIの改善と継続的デリバリー](http://wazanova.jp/items/678) - Netflix は如何に 800 種のデバイスに利用される API を運用しているのか？
- [Ruby RoguesメンバとiOSエンジニアのAPI議論](http://wazanova.jp/items/1211) - 一貫性、ドキュメント、モバイル

Tools
---

- [Apiary](http://apiary.io/) - API Blueprint というスキーマから、Validation や Doc などを生成
- [Swagger UI](https://github.com/wordnik/swagger-ui) - JSON から「試せる API Doc」を生成
- [prmd](https://github.com/interagent/prmd) - JSON Schema を色々出来るツール by Heroku

全体的に
---

### JSON Schema の台頭

JSON Schema のようなものを使い、API のメタ情報（どんなリクエストからどんなレスポンスが返るかetc..）を記述。これを利用して API に関する諸作業を自動化しようという流れがある。 ([すべてがJSONになる](http://r7kamura.hatenablog.com/entry/2014/06/10/023433))

たとえば、ドキュメントなどはその筆頭。正直決まりきったことを書くのつらい。
JSON Schema のようなものを使い、Swagger UI みたいな試せる系ドキュメントを作るというのはかなり良い。

あと辛いものといえば、API Client がある。これは対応するプラットフォームの数だけ作らなければならなくなり業が深い。
どうせやることは Serialization と URL Mapping くらいのものであり、JSON Schema などで自動化出来る。

手前味噌ですが、iOS, Android 向けのものを自社の業務でも使っています。[API開発自動化と量産](https://speakerdeck.com/kaiinui/apikai-fa-zi-dong-hua-toliang-chan)を参照。（オープンソースにする予定）

このへん、まだまだエコシステムが整っていないけれど、これからどんどん整っていくと思っています。

### フロントエンドに最適化した API

HTTP のネットワーキングのパフォーマンスについて知見の共有が進み、API のデザインも沿ったものにしなければ、という流れがある。

一番大きいのは、コール回数を減らそうという流れ。
リソース指向偏重の API にして何度も API を叩くより、最適化された API を用意して 1 回のコールで全て取れるようにしたい。

モバイルにおいては、一回の HTTP コールだけで 250ms 消費されるという話もあるから、重要な話。

Etsy などは、API をカスタムメイド出来るようにしており、モバイル開発チームで最適な API を自らデザインしている。（[モバイルAPIデザインのまとめ](http://wazanova.jp/items/1283)）

### 一貫性のための規約の確立

API に関する規約がまだあまり確立していません。
広く用いられる規約を適用し、一貫性を保つことで、API を利用するための学習コストを劇的に減らすことが出来ます。
また、規約により形式が定まることで、様々なツールでの連携が容易になります。

どんな認証を使えばいいのか？どんな形式で返すべきか？どんなレベルで子要素をネストすべきか？

Heroku はこの点に関するデザイン指針を公開しています。 ([Heroku HTTP API Design Guide](https://github.com/interagent/http-api-design))
