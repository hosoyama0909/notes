# notes

野球の投球改善ログと技術調査メモ。GitHub Pages で公開する Jekyll サイト。

- 公開URL: https://hosoyama0909.github.io/notes/

## 構成

```
_config.yml       サイト設定
_layouts/
  default.html    共通レイアウト（ヘッダー・フッター、assets/style.css を使用）
  post.html       通常の記事用（default を継承）
  dashboard.html  ビジュアル重視の記事用（共通スタイルを継承せず、記事側のCSSをそのまま使う）
index.html        記事一覧（site.posts をループ）
assets/style.css  共通スタイル（ライト/ダーク自動切替）
_posts/           記事本体
```

## 記事の書き方

`_posts/YYYY-MM-DD-タイトル.md`（または `.html`）を追加し、front matter で指定する。

```yaml
---
layout: post        # 通常の記事は post、ビジュアル重視の記事は dashboard
title: "記事タイトル"
date: 2026-08-10
categories: [野球]
---
```

`layout: dashboard` の記事は、記事本文に `<style>` を書けば独自デザインをそのまま反映できる
（共通の `assets/style.css` は読み込まれない）。

## ローカルプレビュー

```bash
bundle exec jekyll serve
```

## GitHub Pages の有効化手順

1. リポジトリの **Settings → Pages** を開く
2. **Source** を `Deploy from a branch` にする
3. Branch を `main` / `/(root)` に設定して **Save**
4. 数分後に `https://hosoyama0909.github.io/notes/` で公開される
