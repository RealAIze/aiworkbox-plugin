---
name: ai-workbox
description: AI Workbox に登録されたスキルの一覧を見せる。「AI Workbox のスキルを見たい」「使えるスキルは？」と聞かれた時に使う。
allowed-tools: mcp__plugin_aiworkbox_aiworkbox__list_skills mcp__plugin_aiworkbox_aiworkbox__get_skill
---

AI Workbox の MCP サーバー（aiworkbox）の list_skills ツールを呼び、返ってきたスキルを「名前・種類・説明」の表で出してください。
スキルを使うと決まったら、get_skill でその中身を読み、書かれた手順に従ってください。
