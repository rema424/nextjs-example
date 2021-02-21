# Next.js

## コンポーネントの種類

コンポーネントは次の 2 領域に分類される。
なお、以下は一般的な名称ではなく、この文書内における定義とする。

- SSR コンポーネント
- CSR コンポーネント

### SSR コンポーネント

- サーバーサイドで HTML の生成を **許可する** 箇所
- Next.js においてはデフォルトでこのコンポーネントになる
- SSG する際は HTML ファイルに静的にビルドされる（ハードコードされる）

### CSR コンポーネント

- サーバーサイドでの HTML の生成を **許可しない** 箇所
- コンポーネントを [Dynamic Import](https://nextjs.org/docs/advanced-features/dynamic-import#with-no-ssr) する際に `ssr: false` のパラメータを付与するとこのコンポーネントになる
- SSG する際も HTML ファイルにハードコードはされず、ブラウザで読み込まれた際に JavaScript でレンダリングされる
- 例えばログイン状態に応じてヘッダーにログインボタン・ログアウトボタンを出し分けたい場合 HTML に静的にビルドする訳にはいかないのでヘッダーを CSR コンポーネントにする

## SSR と SSG

Next.js は各 URL ごと (テンプレートごと) に SSR と SSG のどちらを採用するか選択することができる。選択は使用する API によって判断される。

### SSR

- リクエストが届いてから HTML を生成する
- リクエストの際にデータフェッチを行うので遅い
- ビルドの際にデータフェッチを行わないので速い
- URL アクセス時の 404 はリクエストのタイミングで確定
- API は `getServerSideProps()` ( or `getInitialProps()`)

### SSG

- ビルド時に HTML を生成する
- リクエストの際にデータフェッチを行わないので速い
- ビルドの際にデータフェッチを行うので遅い
- URL アクセス時の 404 はビルドのタイミングで確定
- API は `getStaticProps()` ( + `getStaticPaths()`)

## ルーティングの種類

以下の 2 つに分類される。

- 静的ルーティング
- 動的ルーティング

|                      |    静的ルーティング    |            動的ルーティング             |
| :------------------- | :--------------------: | :-------------------------------------: |
| URL の例             |       /articles        |          /articles/:articleID           |
| パスパラメータの有無 |          なし          |                  あり                   |
| SSR の API           | `getServerSideProps()` |         `getServerSideProps()`          |
| SSG の API           |   `getStaticProps()`   | `getStaticProps()` + `getStaticPaths()` |
