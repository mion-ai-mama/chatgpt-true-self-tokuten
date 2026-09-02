# ChatGPTで「本当の自分」を深掘りする5つの質問

Instagramリールのコメント特典として配布する、スマートフォン向けの自己分析ガイドページです。
コードやHTMLの知識がなくても、`js/content.js` というファイル1つを書き換えるだけで、
文章やリンクを変更できます。

---

## 目次

1. [このページの目的](#1-このページの目的)
2. [ファイル構成](#2-ファイル構成)
3. [ローカルでの確認方法](#3-ローカルでの確認方法)
4. [GitHub Pagesでの公開方法](#4-github-pagesでの公開方法)
5. [Vercelでの公開方法](#5-vercelでの公開方法)
6. [タイトルや文章の変更箇所](#6-タイトルや文章の変更箇所)
7. [OGP画像とfaviconの差し替え方法](#7-ogp画像とfaviconの差し替え方法)
8. [動作確認項目](#8-動作確認項目)

---

## 1. このページの目的

Instagramリールを見てコメントしてくれた方に、リール内で紹介した「ChatGPTで本当の自分を
深掘りする5つの質問」を、コピペしてすぐ使える形で届けるための特典ページです。

ChatGPT初心者の方でも迷わないように、

- 始める前の準備（同じチャット内で聞く、自己紹介テンプレートを送る）
- 5つの質問（個別コピー・まとめてコピーの両対応）
- 回答が浅かったときの深掘り質問
- 結果を行動プランにつなげる追加プロンプト
- 使ううえでの注意点

を順番に案内する構成にしています。

---

## 2. ファイル構成

| ファイル・フォルダ | 説明 | 編集頻度 |
|---|---|---|
| `index.html` | ページのHTML本体（文章はJavaScript無効時のフォールバック表示） | 通常は編集不要 |
| `css/style.css` | 色やレイアウトなどの見た目 | 編集不要 |
| `js/content.js` | ページの文章・プロンプト・リンク・表示ON/OFFをまとめた設定ファイル | **文章を変えたいときはここ** |
| `js/script.js` | ページの動き（コピー機能・表示の組み立て・アニメーション） | 編集不要 |
| `assets/favicon/` | favicon（ブラウザタブのアイコン） | 差し替えるときのみ |
| `assets/images/` | CTAバナー画像などの置き場所 | 差し替えるときのみ |
| `docs/requirements.md` | このページの要件定義 | 参考資料 |
| `docs/SCOPE_PROGRESS.md` | 制作の進捗管理 | 参考資料 |

**文章やリンクを変えたいときは、基本的に `js/content.js` の中身だけを書き換えれば反映されます。**

---

## 3. ローカルでの確認方法

このページはビルド不要の静的サイトです。次のどちらかの方法で確認できます。

**方法A：ファイルを直接開く**

`index.html` をダブルクリックしてブラウザで開くだけで確認できます。

**方法B：簡易サーバーを使う（コピー機能まで正しく確認したい場合におすすめ）**

```bash
cd chatgpt-true-self-tokuten
python3 -m http.server 8080
```

ブラウザで `http://localhost:8080` を開いてください。

> 💡 コピーボタンの動作は、ブラウザによっては `file://` で開いた場合に制限されることがあります。
> 気になる場合は方法Bを使ってください。

---

## 4. GitHub Pagesでの公開方法

1. GitHubのリポジトリページを開く
2. `Settings` → `Pages` を開く
3. `Source` を `Deploy from a branch` にし、ブランチを `main`、フォルダを `/ (root)` に設定して保存
4. 数分後、`https://<アカウント名>.github.io/<リポジトリ名>/` で公開されます

公開URLは `js/content.js` の `meta.siteUrl` にも設定しておくと、SNSシェア時の情報が正しくなります。

---

## 5. Vercelでの公開方法

1. [Vercel](https://vercel.com/) にログインし、「Add New...」→「Project」を選ぶ
2. このリポジトリを選択してインポートする
3. Framework Preset は **Other（フレームワークなし）** のままでOK
4. Build Command・Output Directory は空欄のまま「Deploy」をクリック
   （静的ファイルのみのため、ビルド設定は不要です）
5. 発行されたURL（例: `https://chatgpt-true-self-tokuten.vercel.app`）で公開されます

---

## 6. タイトルや文章の変更箇所

すべて `js/content.js` の中の項目に対応しています。

| 変更したい内容 | `content.js` の場所 |
|---|---|
| ページタイトル・SEO説明文 | `meta.pageTitle` / `meta.description` |
| ファーストビューの見出し・キャッチコピー | `hero` |
| 「この資料でできること」カード3つ | `tips.cards` |
| 準備セクションの説明・持ち物リスト | `prep` |
| 自己紹介テンプレートの文面 | `introTemplate.promptText` |
| 5つの質問（見出し・質問文・分かること） | `mainQuestions.items` |
| まとめてコピーの案内文・ボタン文言 | `mainQuestions.bulk` |
| 深掘り質問4つ | `extraQuestions.questions` |
| 30日間の行動プランのプロンプト | `actionPlan.promptText` |
| 注意点の文章 | `caution.paragraphs` |
| まとめ・締めのメッセージ | `summary` |
| CTA（AIマネタイズの教科書への案内文） | `cta.paragraphs`（バナー・リンク先は変更不要） |

セクションを一時的に非表示にしたい場合は、`sections` の中の該当項目を `false` にしてください
（文章は消えないので、`true` に戻せば元通り表示されます）。

---

## 7. OGP画像とfaviconの差し替え方法

- **OGP画像**：このページでは方針として設定していません（`meta.ogpImage` は `null`、
  `index.html` にも `og:image` タグを置いていません）。設定したい場合は、画像を
  `assets/images/` に追加し、`meta.ogpImage` に絶対URL（`https://`から始まるURL）を指定した上で、
  `index.html` の `<head>` 内にも `<meta property="og:image" content="...">` を追加してください。
- **favicon**：`assets/favicon/favicon.svg` を差し替えてください。SVG以外の形式を使う場合は、
  `index.html` の `<link rel="icon">` と `content.js` の `meta.faviconPath` のパスも
  あわせて書き換えてください。

---

## 8. 動作確認項目

公開前に、以下を確認してください。

- [ ] iPhoneサイズでレイアウトが崩れない
- [ ] Androidサイズでレイアウトが崩れない
- [ ] PCでも読みやすい（最大幅720px程度で中央表示）
- [ ] すべてのコピーボタンが正しい文章をコピーする
- [ ] 「5つの質問をまとめてコピー」ボタンが、質問番号付きで正しくコピーされる
- [ ] コピー成功時にボタンがチェックマーク表示に変わり、2〜3秒で元に戻る
- [ ] 横スクロールが発生しない
- [ ] ブラウザのコンソールにJavaScriptエラーが出ていない
- [ ] ページ内のリンク（目次ボタン等）が正常に動く
- [ ] 質問文・テンプレート文がこのページの設計内容と一致している
- [ ] 外部へ個人情報を送信する処理がない（このページはユーザーの入力内容を保存・送信しません）

---

このページは `mion-ai-mama/instagram-tokuten-template` から複製して作成しています。
元テンプレートの汎用的な仕組み（セクションON/OFF・content.js編集方式）についての詳しい説明は、
[元テンプレートのREADME](https://github.com/mion-ai-mama/instagram-tokuten-template#readme) を参照してください。
