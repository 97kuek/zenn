---
title: "Expressive CodeとGiscussで魅せる記事をつくる"
emoji: "📚"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["astro", "github", "frontend"]
published: true
---

## はじめに
最近、Astroを使って個人ポートフォリオ兼技術ブログを作成したので、**Expressive Code**と**Giscuss**の紹介記事を書いてみました。

## Expressive Codeでコードブロックを魅せる

技術ブログの主役はコードです。Astro標準のシンタックスハイライトも悪くありませんが、**ファイル名の表示**や**行ハイライト**などを手軽に実装したかったため、Expressive Codeを採用しました。

Expressive Codeを導入すると、こんな感じの見た目になります。

![Expressive Code](/images/expressive-code.png)

### 導入手順
まずはプロジェクトにパッケージを追加します。Astroには便利な`astro add`コマンドが用意されているので、これを使うのが一番早いです。ターミナルを開き、以下のコマンドを実行してください。

```bash
npx astro add astro-expressive-code
```

これだけでおしまいです。インストールが完了したら、念のため`astro.config.mjs`を確認してみましょう。このファイルは、Astroプロジェクトの設定ファイルで、**拡張機能の管理**や**サイト全体の基本情報**などを記述する場所です。
以下のように、`expressiveCode()`がインポートされ、`integrations`配列に追加されていればOKです。

```js
import { defineConfig } from 'astro/config';
import expressiveCode from 'astro-expressive-code';

export default defineConfig({
  integrations: [expressiveCode()],
});
```

## Giscussでコメント機能を魅せる

![giscuss](/images/giscuss.png)

Astroのようにデータベースを持たない**静的サイト**では、コメント機能の実装は少しハードルが高いです。
そこで便利なのが **Giscuss** です。 これは GitHub Discussions の仕組みを利用して、コメント欄を「埋め込む」ことができるツールです。 データベースの管理が一切不要で、しかも**完全無料**です。

### 導入手順
Giscussを利用するには、以下の3条件を満たす必要があります。

1. リポジトリがPublicであること
    - Privateリポジトリは対応していません
2. Discussion機能が有効であること
    - GitHubのSettings > General > Features にあるDiscussionを有効にしてください
3. Giscussアプリがインストールされていること
    - [Giscussアプリのページ](https://github.com/apps/giscus)から、自分のリポジトリに対してアクセス権を許可してください

[Giscussの公式サイト](https://giscus.app/ja)にアクセスし、画面に従って設定を入力していきます。正しく入力すると、サイト下部に`<script>`タグが表示されます。

生成された`<script>`タグをそのまま貼っても動きますが、使いまわせるようにコンポーネント化しましょう。`src/components/Giscuss.astro`を作成します。

```astro
<div class="giscuss-container">
  <script src="https://giscus.app/client.js"
    data-repo="[ここに data-repo の値]"
    data-repo-id="[ここに data-repo-id の値]"
    data-category="Announcements"
    data-category-id="[ここに data-category-id の値]"
    data-mapping="pathname"
    data-strict="0"
    data-reactions-enabled="1"
    data-emit-metadata="0"
    data-input-position="bottom"
    data-theme="preferred_color_scheme"
    data-lang="ja"
    data-loading="lazy"
    crossorigin="anonymous"
    async>
  </script>
</div>

<style>
  .giscuss-container {
    margin-top: 4rem;
    padding-top: 2rem;
    border-top: 1px solid var(--gray-light, #e0e0e0); /* サイトの変数があれば使う */
    width: 100%;
  }
</style>
```

> [!NOTE]
> `data-repo` や `data-repo-id` などの値は、Giscuss公式サイトで設定を入力した際に自動生成されるスクリプトタグ内に記載されています。それらをコピーして貼り付けてください。

最後に、ブログ記事のレイアウトファイルにこのコンポーネントを配置します。例えば`src/layouts/BlogPost.astro`を編集します。

```astro
---
import Giscuss from '../components/Giscuss.astro';
// ... その他のimport
---

<article>
  <!-- 記事の本文 -->
  <slot />

  <!-- 記事の下にコメント欄を配置 -->
  <Giscuss />
</article>
```

### 動作確認
ローカル環境でもGiscussは表示されますが、実際に投稿テストをする場合は、本番環境またはlocalhostの設定許可を確認してください。

記事ページの下部にコメント欄が表示され、GitHubアカウントでログインして書き込み出来れば成功です。

## まとめ

今回は、Astroでブログを作成する際に役立つ**Expressive Code**と**Giscuss**の導入方法について紹介しました。
どちらも簡単に導入でき、技術ブログを作るにはうってつけのツールなので、ぜひ使ってみてください。
