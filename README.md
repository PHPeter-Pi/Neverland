# PHPeter-Pi

[PHPeter-Pi](https://github.com/PHPeter-Pi/) は 5〜10 人規模の店舗を支援するためのオープンソースの Docker コンテナ・ライブラリです。

主に Raspberry Pi ZeroW および RasPi 3 の Docker 上で動かすことを前提としています。

<details><summary>共通仕様</summary><div><br>

<p>いずれのライブラリも Docker コンテナ上で動き、別のコンテナから Web API（HTTP アクセス）で利用します。</p>

<p>基本的に PHP で開発されていますが、Web API を実装していればいいので Python などのコンテナもありえます。</p>

<h3>利用時の注意</h3>

<ul>
<li><b>特定少数向け</b>です。<br>一般ユーザー（不特定多数）向けのライブラリではありません。例えば、店舗のスタッフなどが操作する端末のバックエンド用のライブラリとして利用します。</li>
</ul>

</div></details>

## 動作保証

全てのライブラリ（コンテナ）は以下の環境で動作確認しています。

- ハードウェア:
  - RaspberryPi Zero W(ARMv6l)
  - RaspberryPi 3(ARMv7l)
- OS: Raspbian Stretch Lite (v9), Buster Lite (v10)
- Docker: Docker version 19.03.4
- Docker Compose: 1.25.0dev

## ライブラリ/コンテナ一覧

### Peterpan

- [https://github.com/PHPeter-Pi/peterpan](https://github.com/PHPeter-Pi/peterpan)

Markdown で書かれたページを HTML で表示するためのサンプルです。ライブラリというよりは HTML テンプレートです。

GitHub Pages など、静的サイトに `index.html` と `index.md` を公開すると `index.html` 内の Javascript が同じ階層にある `index.md` を読み込み HTML にパース（変換）して表示します。

SEO には向きませんが、更新頻度の多いページを Markdown で公開できます。詳しくはリポジトリを参照。

### Tinker-Bell

- [https://github.com/PHPeter-Pi/Tinker-Bell](https://github.com/PHPeter-Pi/Tinker-Bell)

来客数のカウントを行うだけの Web API コンテナです。現在の来客数管理に利用します。

このコンテナの 8080 ポートに HTTP リクエスト（`GET`）すると、現在の来客数を JSON 形式で返します。

リクエスト・クエリによって、人数のカウント・アップ／ダウンを行ったり、開店／閉店などの設定も行えます。

将来的には、ラズパイ・カメラで人体検知した人数の更新に使われます。

### JAN

- [https://github.com/PHPeter-Pi/JAN](https://github.com/PHPeter-Pi/JAN)

JAN コードから商品情報を返すだけの Web API コンテナです。仕入れ管理にバーコードを使う場合の商品情報取得に使います。

このコンテナの 8080 ポートに `jan=` クエリ付きで HTTP リクエスト（`GET`）すると商品情報を JSON 形式で返します。

### Jolly Roger

- [https://github.com/PHPeter-Pi/JollyRoger](https://github.com/PHPeter-Pi/JollyRoger)

同じ Docker ネットワーク内にある Web API（もしくは HTTP 接続）を、外部に一般公開するためのコンテナです。

お店のルーターや Docker ネットワークなどでポートの解放設定をしなくても安全に外部公開できます。

大量アクセスには向きません。来店中のお客様向け（数人向け）のサイト公開などに使われます。

### Nana

- [https://github.com/PHPeter-Pi/Nana](https://github.com/PHPeter-Pi/Nana)

コンテナの Web API の動作確認を行うためのテスト用コンテナです。単独では利用しません。

docker-compose で、テスト対象のコンテナと Nana のコンテナを起動させるとテストが実行されます。

テストファイルを Nana にマウントして起動すると、テスト対象のコンテナに Nana のコンテナから HTTP アクセス（Web API へリクエスト）を行いテストを実行します。
