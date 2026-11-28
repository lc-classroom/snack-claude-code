# Grok でダッシュボードを見せる

Grok（Grok Build、Grok Bot）での見せ方。Grok Bot と Grok Build で見せ方が違う。

## Grok Bot

Grok Bot の作業フォルダはエージェント側のコンピューターにあるので、`dashboard.html` のパスを伝えても参加者のブラウザでは開けない。代わりに、チャットの横に開くページ（Canvas）で見せる。

### 手順

1. **初回（`open`）**: `dashboard.json` の中身で Canvas を1枚作り、そのリンクを参加者に伝える。作る前に Cursor 管理の `canvas` スキルを読む
   - タイトルは「スナック作戦ボード」。SKILL.md の6つの欄（いまの状況、次の発言の作戦、話題の移り変わり、会話の流れ、自分の過去の発言、判断の記録）をそのまま並べる
   - 会話の流れは、自分・エージェント・人間を色で分ける。表示の色や並びは `assets/dashboard.html` のひな形に合わせる
   - Canvas の識別子を `dashboard.json` の `canvas_id` に残す（次から同じページを書き直すため）
2. **毎サイクル（`update`）**: `dashboard.json` だけを更新する。Canvas は毎分書き直さない（1分のループのリズムが崩れるため）
3. **5分ごと**: slack-loop の references/Grok.md の「5分ごとくらいの節目」の途中報告に合わせて、`canvas_id` の Canvas を最新の `dashboard.json` で書き直す。新しい Canvas は作らない。途中報告には、SKILL.md のテキスト版の「次の作戦」の行を1行添える
4. **止まったとき**: 最後にもう一度 Canvas を書き直して「止まっている」の状態にし、お別れの報告にリンクを添える
5. Canvas の書き直しに失敗しても、ループは止めない。次の5分の節目で書き直す

### 守ること

- Canvas は参加者本人の Library に置き、Slack にリンクを貼らない
- Canvas にも個人情報を書かない（SKILL.md の `（略）` のルールに従う）

## Grok Build

1. SKILL.md の「使える材料」の HTML のひな形で、作業フォルダに `dashboard.html` を作る（2回目以降は、データの部分だけ書き換える）
2. 初回だけ、ブラウザで開ける `dashboard.html` のパスを参加者に伝える
3. 2回目以降は書き換えるだけ。ページが60秒ごとに読み直すので、参加者への報告はしない
