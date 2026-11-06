# AI Workbox プラグイン

Claude Code と Codex を AI Workbox につなぐプラグインです。入れると、AI Workbox の会社の管理者が管理画面に書いたルール・メモリ・止める操作・答えのチェックが、質問のたびに AI に届きます。

管理者が中身を書き換えても、このプラグインを入れ直す必要はありません。中身は AI Workbox のサーバーにあり、プラグインにはサーバーの住所と hooks の呼び方だけが入っています。社員の PC で命令を動かす hooks（`type: "command"`）は使っていません。秘密の値も入っていません。

## 入れ方

接続の手順は、AI Workbox の管理画面の「AIの設定方法」に出ているコマンドを使ってください。

### Claude Code（2.1.318以降）

```sh
claude mcp remove aiworkbox --scope user
claude plugin marketplace add RealAIze/aiworkbox-plugin
claude plugin install aiworkbox@aiworkbox
claude mcp login plugin:aiworkbox:aiworkbox
```

1行目は、前の手順でつないだ接続を外します。「見つかりません」と出ても、そのまま進めてください。

### Codex CLI（0.164.0以降）

```sh
codex plugin marketplace add RealAIze/aiworkbox-plugin
codex plugin add aiworkbox@aiworkbox
codex mcp login aiworkbox --scopes skills:read,skills:run
```

初めて `codex` を開いた時に「Hooks need review」と出たら、「2. Trust all and continue」を選んでください。

## 中身

| ファイル | 役割 |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code のマーケットプレイスの目印 |
| `.agents/plugins/marketplace.json` | Codex のマーケットプレイスの目印 |
| `plugins/aiworkbox/.mcp.json` | AI Workbox の MCP の住所（Claude Code と Codex が読む） |
| `plugins/aiworkbox/hooks/hooks.json` | Claude Code の hooks。質問・コマンド・答えの前に AI Workbox の `harness` を呼ぶ |
| `plugins/aiworkbox/hooks/codex-hooks.json` | Codex の hooks（`.codex-plugin/plugin.json` から読む） |

`main` は本番（`https://mcp.ai-workbox.com/mcp`）、`dev` は開発環境を指します。

hooks のファイルは中身を変えません。Codex は hooks が変わると、社員にもう一度信用を求めます。
