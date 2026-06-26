# slop-nuki

服のシミ抜きと同じ。AIが残した slop（シミ）だけを抜き、生地（敬語や、場面に応じた丁寧さ）は傷つけない。

日本語の文章から、生成AIが量産しがちな **slop**（中身が薄い・機械的・水増しされた定型表現）を取り除くための Claude スキル。[hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) の日本語・汎用ビジネス文章版。

> *A Claude Skill for stripping AI "slop" from Japanese business writing — the Japanese, general-purpose adaptation of [stop-slop](https://github.com/hardikpandya/stop-slop).*

## 何をするか

メール、お詫び・クレーム対応、社内Slack、お知らせ、依頼文、提案書などを書く・推敲する・レビューするときに、AIっぽい定型表現・冗長・空虚な強調・過剰敬語を取り除き、自然で誠実な日本語に直す。テックライティング専用ではなく、ビジネス文章全般が対象。

### 設計の核心：register（場面）を壊さない

英語版 stop-slop の「とにかく直接的に・簡潔に」をそのまま日本語に当てると、敬語やクッション言葉まで削って無礼で不自然な文になる。このスキルが削るのは **slop（過剰・空虚・機械的な部分）だけ**で、場面にふさわしい丁寧さ・敬語・配慮は **残す**。

- 社外フォーマルメールと社内Slackでは、正解の方向が逆（丁寧め ⇆ 簡潔・カジュアル）。
- お詫び・クレーム対応では、謝意は保ったまま「事実 → 原因 → 対応 → 再発防止」を具体化する。
- 「簡潔にしすぎてぶっきらぼう・無礼になる」のも別種の slop として点検する。

## 構成

```
slop-nuki/
├── SKILL.md                  コア原則・場面別の使い分け・クイックチェック・スコアリング
├── references/
│   ├── phrases.md            削るべき語句（空虚な形容・動詞・強調・前置き・締め・対句・決意・安心）
│   ├── structures.md         構造・論理・整形（受け身・対比・反復・三点リスト・結論先出し・長文・煽り・中黒・ダッシュ・太字・半角全角）
│   ├── keigo.md              敬語の slop と、残すべき敬語の線引き
│   ├── registers.md          場面別ガイド（社外メール／お詫び・クレーム／社内Slack／お知らせ・依頼）
│   └── examples.md           before/after の総合例（メッセージ単位）
├── README.md
└── LICENSE
```

## 使い方

### Claude Code / Claude.ai でスキルとして使う

`SKILL.md` を含むこのディレクトリを、Claude のスキル置き場に配置する。

```bash
# 例：ユーザー単位の Claude Code スキルとして
mkdir -p ~/.claude/skills/slop-nuki
cp -r SKILL.md references ~/.claude/skills/slop-nuki/
```

プロジェクト単位で使うなら `.claude/skills/slop-nuki/` に置く。

### 呼び出しの例

- 「このメールの文章、AIっぽさを取って自然にして」
- 「取引先へのお詫びメールをレビューして」
- 「この Slack のメッセージ、もっと簡潔にして（でも失礼にならないように）」
- 「このお知らせ文の冗長なところを削って」

宛先や媒体が不明なとき、スキルは推測せず確認する。

## クレジット

- 原案：[stop-slop](https://github.com/hardikpandya/stop-slop)（Hardik Pandya, MIT License）の構成と思想を翻案。
- 日本語の文章規範：[k16shikano / japanese-tech-writing](https://gist.github.com/k16shikano/fd287c3133457c4fd8f5601d34aa817d) を参考（テックライティング固有の規則は除外し、ビジネス文章全般に汎用化）。

## ライセンス

MIT License（`LICENSE` 参照）。
