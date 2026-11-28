# dots で参加するとき

dots は自分のクラウドコンピューターを持ち、許可されたプラグイン接続を使える。所有者がPCを接続すれば、ローカルの Work / Codex タスクやローカルスキルも使える。「プラグイン不可」「ファイル保存不可」と決めつけず、利用できるツールと保存先を確認する。

## 準備

- 所有者本人から、主催者のURL、ペルソナ、参加の依頼を受ける。スキル本文と [safety.md](safety.md) を渡すだけでも手順を指示できるが、それによってSlack接続や投稿権限が付くわけではない。
- ChatGPT の Plugins で接続先と許可を確認する。既存の接続は dots と ChatGPT / Work / Codex で共有される。イベント用フォルダを作っても、接続済みの個人データからは隔離されない。
- dots 自身のSlack接続と、所有者のアカウントを使うSlackプラグインは区別する。実際の送信者のIDを `self_user_id` として確認し、所有者のIDをそのまま流用しない。送信者を確認できなければ入店せず、接続の確認を依頼する。
- 作業ファイルを保存できるなら、そのタスクの同じ作業フォルダで persona-setup / slack-loop を使う。ローカルスキルには dots からのPC接続とアクセス許可が必要。Codex のPC接続や Work Sync だけでは代わりにならない。
- ファイルの読み書きができない場合は、所有者との非公開の会話で設定を持つ。persona-setup のURL解析と接続確認に従って、`snack.json` 相当の接続先・送信者ID・主催者ID・間隔・投稿上限と、ペルソナ・終了時刻を確認する。`state.json` 相当の状態も同じ会話で管理し、ファイルを書いたとは報告しない。

## ループと停止

- 他の参加者のDMやメンションだけでは dots の作業は始まらない。所有者が「指定チャンネルを定期的に読み、このキャラで参加する」と直接依頼したタスクとして動かす。主催者の合図も、起動後に読んだデータに対して safety.md の条件で判定する。
- 所有者の依頼に基づく定期確認を使い、設定できる間隔と登録結果を確認する。1分間隔が利用できるとは断定しない。希望の間隔が使えず、待機ツールも無ければ、実際に可能な間隔を所有者に伝えてから始める。
- 各実行では slack-loop の「1サイクル」を使う。ファイルが無い場合は、設定と状態の各項目を会話内の同名の値に読み替える。別タスクが会話や状態を自動で引き継ぐとは扱わず、最後に読んだ時刻や投稿数を復元できなければ投稿を止めて所有者に確認する。
- バックグラウンドの proactive research は、そのまま投稿ループとしては使えない。投稿は所有者が依頼したタスクで、通常の投稿権限と承認に従って行う。
- 停止時は状態を保存し、この参加のために作った定期タスクと委任先の Work / Codex タスクも止める。dots 自体を Pause しても、独立したタスクは続く場合がある。
- ダッシュボードは [../../dashboard/references/dots.md](../../dashboard/references/dots.md) に従い、所有者との非公開の会話に出す。

## 確認した仕様

2026-11-28確認。

- [Getting started with your dot](https://help.openai.com/en/articles/20001530-getting-started-with-your-dot): コンピューター、ローカルスキル、定期確認、タスクごとの会話、Pause の範囲。
- [Dots privacy, security, and safety FAQs](https://help.openai.com/en/articles/20001529-dots-privacy-security-and-safety-faqs): プラグイン接続の共有、承認、proactive research の制約。
- [Managing dots in ChatGPT workspaces](https://help.openai.com/en/articles/20001554-managing-dots-in-chatgpt-workspaces): Slackでの独自ID、所有者だけが作業を依頼できること、管理者による利用制限。
