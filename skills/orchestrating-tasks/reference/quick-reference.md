# クイックリファレンス

## タスクタイプ一覧

| タイプ | 説明 | 並列化 |
|--------|------|--------|
| `research-web` | Web事例調査、ドキュメント検索 | 可能 |
| `research-code` | 既存コードベースの調査 | 可能 |
| `root-cause-analysis` | エラーや問題の原因分析 | 可能 |
| `implement` | コード実装 | 依存関係による |
| `build` | プロジェクトビルド | 実装後 |
| `test` | テスト実行 | 実装後 |
| `review` | コードレビュー | 実装後 |

## 依存関係図

```
research-web        ──┐
research-code       ──┼──> implement ──> build ──> test
root-cause-analysis ──┘                    │
                                           └──> review
```

## タスクタイプ判定表

| ユーザー指示 | タスクタイプ | 備考 |
|--------------|--------------|------|
| 「〇〇を調べて」 | research-web または research-code | コンテキストで判断 |
| 「事例を調査して」 | research-web | 外部情報の検索 |
| 「既存実装を確認して」 | research-code | コードベース調査 |
| 「原因を調べて」 | root-cause-analysis | エラー分析 |
| 「〇〇を実装して」 | implement | コード生成 |
| 「ビルドして」 | build | ビルド実行 |
| 「テストして」 | test | テスト実行 |
| 「レビューして」 | review | コードレビュー |
| 「調査して実装して」 | research-* + implement | 複合（順次） |
| 「実装してテストまで」 | implement + test | 複合（順次） |

## 並列化判断フローチャート

```
作業指示を受けた
      ↓
複数タスクか？
      ├─ No → 単一タスクとして実行
      └─ Yes
           ↓
      依存関係チェック
           ├─ データ依存あり → フェーズ分割（順次）
           ├─ 同一ファイル変更 → フェーズ分割（順次）
           └─ 依存なし → 並列実行
```

## プロンプトテンプレート索引

詳細は `building-task-prompts/templates/` を参照：

- `research-web.md` - Web調査用
- `research-code.md` - コードベース調査用
- `root-cause-analysis.md` - 原因分析用
- `implement.md` - 実装用
- `build.md` - ビルド用
- `test.md` - テスト用
- `review.md` - レビュー用
