# notes

野球の投球改善ログと技術調査メモ。GitHub Pages で公開する Jekyll サイト。

- 公開URL: https://hosoyama0909.github.io/notes/
  - 野球 ステータス: https://hosoyama0909.github.io/notes/baseball/status/
  - 野球 練習メニュー: https://hosoyama0909.github.io/notes/baseball/training/
  - AI技術: https://hosoyama0909.github.io/notes/ai/

## 構成

```
_config.yml         サイト設定（theme: null で GitHub Pages のデフォルトテーマを無効化）
_data/categories.yml カテゴリスラッグ（英語）→ 表示ラベル（日本語）の対応表
_layouts/
  default.html      共通レイアウト（ヘッダー・ナビ・フッター、assets/style.css を使用）
  post.html         通常の記事用（default を継承）
  dashboard.html    ビジュアル重視の記事用（共通スタイルを継承せず、記事側のCSSをそのまま使う）
_includes/post-list.html  記事一覧の共通マークアップ（index.html とセクションページで共用）
index.html          全記事一覧（site.posts をループ）
baseball/status.html    野球 - ステータス（/baseball/status/）
baseball/training.html  野球 - 練習メニュー（/baseball/training/）
ai/index.html            AI技術（/ai/）
assets/style.css    共通スタイル（ライト/ダーク自動切替）
_posts/             記事本体
```

## 記事の書き方

`_posts/YYYY-MM-DD-タイトル.md`（または `.html`）を追加し、front matter で指定する。

```yaml
---
layout: post        # 通常の記事は post、ビジュアル重視の記事は dashboard
title: "記事タイトル"
date: 2026-08-10
categories: [baseball, status]   # baseball/status, baseball/training, ai のいずれか
---
```

カテゴリスラッグと記事一覧ページの対応:

| categories                  | 表示先ページ                |
|------------------------------|------------------------------|
| `[baseball, status]`         | `/baseball/status/`（野球 ステータス） |
| `[baseball, training]`       | `/baseball/training/`（野球 練習メニュー） |
| `[ai]`                       | `/ai/`（AI技術） |

新しいカテゴリを追加する場合は `_data/categories.yml` にスラッグ→日本語ラベルを1行足す。

`layout: dashboard` の記事は、記事本文に `<style>` を書けば独自デザインをそのまま反映できる
（共通の `assets/style.css` は読み込まれない）。

## ローカルプレビュー

GitHub Pages は `github-pages` gem 経由で**やや古い Jekyll/Liquid**（Jekyll 3.10 系）を使ってビルドする。
最新の `jekyll` gem では通ってしまうが本番では構文エラーになる書き方があるため、
検証は必ず `Gemfile` 経由で行う。

```bash
bundle install
bundle exec jekyll serve
```

## GitHub Pages の有効化手順

1. リポジトリの **Settings → Pages** を開く
2. **Source** を `Deploy from a branch` にする
3. Branch を `main` / `/(root)` に設定して **Save**
4. 数分後に `https://hosoyama0909.github.io/notes/` で公開される
5. 反映確認は **Actions** タブの `pages build and deployment` が成功しているかを見る
