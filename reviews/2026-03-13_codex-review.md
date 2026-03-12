# Codex Review

- Reviewer: Codex
- Date: 2026-03-13
- Scope: LPサイトのレビュー
- Note: このレビューでは実装変更は行っていない

## 指摘事項

### 1. CTAが実際の問い合わせ先につながっていない

LPの目的は問い合わせ獲得ですが、最終CTAはダミーリンクで、`alert()` を出すだけで終わっています。

- Reference: `index.html:226`
- Impact: LPが本来の目的を達成できない

### 2. 主要コンテンツの表示がJavaScriptに依存しすぎている

`.fade-up` は初期状態で `opacity: 0` になっており、`IntersectionObserver` が動いたときだけ表示されます。JavaScriptが無効、またはエラーで止まると主要セクションが見えないままになる可能性があります。

- Reference: `style.css:130`, `index.html:246`
- Impact: 公開品質としてリスクが高い

### 3. FAQのアクセシビリティが弱い

FAQの質問部分が `div` のクリック実装になっており、`button` や `aria-expanded` などのアクセシビリティ対応がありません。

- Reference: `index.html:187`, `index.html:238`, `style.css:414`
- Impact: キーボード操作や支援技術で扱いづらい

### 4. CTAボタンのコントラストが不足している

主CTAは `#f5a623` の背景に白文字を使っており、視認性が不足しています。

- Reference: `style.css:117`
- Impact: 最重要導線なのに読みづらい

### 5. OGP / Twitterカード設定が壊れている可能性が高い

`og-image.jpg` を参照していますが、その画像はリポジトリ内に存在しません。`og:url` も固定値なので、公開URLが変わると不整合が起きます。

- Reference: `index.html:13`, `index.html:14`, `index.html:19`
- Impact: SNS共有時のプレビュー崩れにつながる

### 6. 訴求内容が現行方針とずれている

現行要件では「AIをアピールしない」方針ですが、実装ではメタ情報とヒーローでAIを前面に出しています。また、要件にある「サービス紹介」の説得力も弱いです。

- Reference: `requirements.md:76`, `docs/要件定義書.md:35`, `index.html:7`, `index.html:38`
- Impact: 信頼感と訴求力を落とす

### 7. 画像運用がリポジトリ内の素材と整合していない

`images/` 配下にローカル素材があるのに、実装では外部のUnsplash画像を直接参照しています。

- Reference: `index.html:43`, `index.html:109`, `design.md:71`
- Impact: 外部依存が増え、表示安定性と見た目の統一感を損ねる

## 要約

このLPは見た目の構成自体は整っていますが、公開用としては次の3点に大きな問題があります。

1. 問い合わせ導線が成立していない
2. JavaScriptが失敗すると主要コンテンツが見えなくなる
3. コピーと実装が最新の方針に揃っていない

## 優先度

1. CTAを実際の問い合わせ先につなぐ
2. JavaScriptなしでも読めるようにする
3. 訴求内容を現行方針に合わせて整理する

## 次点で直すべき項目

- CTAのコントラスト改善
- FAQのアクセシビリティ改善
- OGP画像とURL設定の修正
- 外部画像参照をローカル管理素材に寄せる
