---
title: "Cloudflare Workers + GitHub Actions + Fuwariで技術ブログを構築してみた"

published: 2026-08-02

description: "Cloudflare WorkersとGitHub Actionsを利用してFuwari製ブログを構築した記録"

tags:
  - Astro
  - Fuwari
  - Cloudflare
  - GitHub Actions

category: Web開発

draft: false
---

# はじめに

はい、どうもcrabです。
以前から個人のサイトを作成したいと思っていて始めました。  
これからWeb開発をメインに発信できたなあと思います。  
まずは手始めに今回のブログを作成した経緯について簡単にまとめたいと思います。  
ちなみにこの記事はchatgptでほぼすべて書いてもらいました。なので間違っていることがあるかもしれないのでダブルチェックをお願いします。。。

今回は

- Astro
- Fuwari
- Cloudflare Workers
- Github Actions

を利用して構築しました。以下それぞれ選んだ理由を記載します。
chatgptと相談して選んだので、理由は後付けですが・・・

## Cloudflare Workersを選んだ理由

ブログを公開する方法はいくつかあります。

- GitHub Pages
- Vercel
- Netlify
- Cloudflare Workers

今回はCloudflare Workersを選びました。

理由は以下の3つです。

- GitHubとの連携が簡単
- CDN込みで高速
- 将来的にWorkersやKVなどCloudflareのサービスも使ってみたい

## Astroを選んだ理由

今回はAstroを採用しました。

理由は

- 静的サイト生成が高速
- SEOに強い
- Markdownで記事を書ける
- ReactやSvelteなども組み込める

という点です。

拡張性の高さも結構ありますね。もともと自作で作成していたアプリとかも埋め込みたいですね。

## Fuwariを選んだ理由

テーマはいくつか比較しました。

- AstroPaper
- AstroWind
- Yukina
- Fuwari

最終的にFuwariを選びました。

決め手は

- シンプルで見やすい
- デザインの完成度が高い
- ダークモード対応
- タグや検索機能が充実している
- カスタマイズしやすい

という点です。

プロフィール画像との雰囲気も合っていたので採用しました

---

# 構築手順

## GitHubリポジトリを作成

まずGitHubで新しいRepositoryを作成します。

今回はPublic Repositoryで作成しました。

---

## Cloudflare Workersを作成

Cloudflareへログインし、

Workers & Pages

から新しいWorkerを作成します。

最初に

```

workers.dev

```

のサブドメイン登録を求められます。

これは初回のみ必要です。

---

## GitHub Actionsを設定

GitHub Secretsへ

- CLOUDFLARE_API_TOKEN
- CLOUDFLARE_ACCOUNT_ID

を登録します。

その後、

```

.github/workflows/deploy.yml

```

を作成し、

Push時にCloudflare Workersへ自動デプロイするよう設定しました。

---

## Fuwariを導入

Fuwariをインストールします。

```bash
pnpm create fuwari@latest
```

インストール後

```bash
pnpm install
```

で依存関係を取得します。

---

## ハマったポイント

### workers.devの登録

Cloudflare Workersでは最初にworkers.devのサブドメイン登録が必要でした。

### Astroのバージョン

Astro 7へアップデートすると
@astrojs/svelteとのバージョンが合わずビルドエラーになりました。

最終的には

Astro 5
@astrojs/svelte 7.2.3

へ戻すことで解決しました。

### GitHub Actions

Biomeのフォーマットチェックで失敗したため、
コード整形を実施してからPushしました。

## 今後

このブログでは今のところ

- Web開発
- 米国株投資

について発信していく予定です。
お楽しみに。

## まとめ

Cloudflare WorkersとFuwariを利用することで、
無料かつ高速なブログを構築できました。

今後も実際に試した内容や、
開発中にハマったポイントを中心に記録していこうと思います。
