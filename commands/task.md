---
description: サブエージェントで直接タスクを実行（building-task-prompts活用）
---

タスク: $ARGUMENTS

**以下の手順で即座に実行してください：**

1. **building-task-prompts Skill** を使用して、上記のタスクから効果的なプロンプトを生成
   - タスクタイプを判定（research-web, research-code, implement, build, test, review）
   - タスクタイプに応じた構造化プロンプトを生成
   - コンテキスト効率化ルールを適用

2. 生成したプロンプトを使って **Task tool** でサブエージェントを起動
   - `run_in_background: true` でバックグラウンド実行
   - 適切な `subagent_type` を選択（Explore, Plan, general-purpose等）

3. **TaskOutput** で結果を取得し、ユーザーに報告

**実行方針：**
- オーケストレーションなし（承認不要、即座に実行）
- サブエージェントに完全に委譲
- 詳細は `.claude/tmp/` に保存し、サマリーのみ報告
