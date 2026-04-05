# OMC (oh-my-claudecode) エージェントカタログ

> Claude Code 用マルチエージェントオーケストレーションシステム
> バージョン: v4.9.3 | 更新日: 2026-04-05

---

## 概要

OMC（oh-my-claudecode）は、Claude Code上で動作するマルチエージェントオーケストレーション層です。
専門化されたエージェントに作業を委譲し、品質と効率を両立させます。

---

## エージェント一覧

### コア開発エージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **executor** | Sonnet | 実装タスクの実行。コード生成・編集の中心 |
| **architect** | Opus (READ-ONLY) | 戦略的アーキテクチャ設計・デバッグ助言 |
| **planner** | Opus | 戦略的計画立案。インタビュー形式で要件整理 |
| **analyst** | Opus | 要件分析・事前計画コンサルタント |
| **designer** | Sonnet | UI/UXデザイン・開発。美しいインターフェース構築 |

### コード品質エージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **code-reviewer** | — | 重大度評価付きコードレビュー。ロジック欠陥・SOLID原則・セキュリティチェック |
| **code-simplifier** | — | コードの簡素化・リファクタリング。可読性と保守性の向上 |
| **security-reviewer** | — (READ-ONLY) | セキュリティ脆弱性検出（OWASP Top 10、シークレット、安全でないパターン） |
| **critic** | Opus (READ-ONLY) | 作業計画・コードの多角的レビュー |

### テスト・検証エージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **test-engineer** | — | テスト戦略、統合/E2Eカバレッジ、フレイキーテスト対策、TDDワークフロー |
| **qa-tester** | — | tmuxを使ったインタラクティブCLIテスト |
| **verifier** | — | 検証戦略、エビデンスベースの完了チェック、テスト妥当性評価 |

### デバッグ・分析エージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **debugger** | — | 根本原因分析、リグレッション分離、スタックトレース解析、ビルドエラー解決 |
| **tracer** | — | 証拠駆動の因果トレース。競合仮説・不確実性追跡・次の調査提案 |
| **scientist** | — (READ-ONLY) | データ分析・研究実行 |

### リサーチ・ドキュメントエージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **explore** | — (READ-ONLY) | コードベース検索。ファイル・コードパターンの発見 |
| **document-specialist** | — (READ-ONLY) | 外部ドキュメント・リファレンス調査 |
| **writer** | Haiku | 技術ドキュメント作成（README、APIドキュメント、コメント） |

### Git・運用エージェント

| エージェント | モデル | 用途 |
|---|---|---|
| **git-master** | — | Gitエキスパート。アトミックコミット、リベース、履歴管理、スタイル検出 |

---

## 組み込みエージェント（Claude Code標準）

| エージェント | 用途 |
|---|---|
| **general-purpose** | 汎用。複雑な質問の調査、コード検索、マルチステップタスク |
| **Explore** | コードベースの高速探索。ファイルパターン・キーワード検索 |
| **Plan** | ソフトウェアアーキテクト。実装計画の設計 |
| **feature-dev:code-explorer** | 既存機能の深掘り分析。実行パス・アーキテクチャ層のトレース |
| **feature-dev:code-architect** | 機能アーキテクチャ設計。実装ブループリント提供 |
| **feature-dev:code-reviewer** | コードレビュー。バグ・セキュリティ・品質チェック |

---

## Tier-0 ワークフロー（スキル）

| スキル | トリガー | 用途 |
|---|---|---|
| **autopilot** | `autopilot` | 自律実行モード |
| **ultrawork** | `ulw` | 高負荷作業モード |
| **ralph** | `ralph` | 反復改善ワークフロー |
| **ralplan** | `ralplan` | 計画 + 実行の統合ワークフロー |
| **team** | `/team` | チームオーケストレーション |

---

## モデルルーティング

| モデル | 用途 |
|---|---|
| **Haiku** | 軽量ルックアップ、簡易タスク |
| **Sonnet** | 標準的な実装・分析 |
| **Opus** | アーキテクチャ設計、深い分析、セキュリティ |

---

## セットアップ手順（ゼロから構築）

### 前提条件
- Node.js 18以上
- Claude Code CLI（Anthropic公式）がインストール済み
- Claude Pro または Max サブスクリプション

### Step 1: Claude Code のインストール
```bash
# macOS
brew install claude-code

# npm（全OS共通）
npm install -g @anthropic-ai/claude-code
```

### Step 2: OMC のインストール
```bash
npm install -g oh-my-claudecode
```

### Step 3: OMC の初期化
```bash
# Claude Code を起動して初期化
claude
# Claude Code 内で以下を実行
omc setup
```

これで全エージェント・スキルが利用可能になります。

### Step 4: 動作確認
```bash
# Claude Code 内で以下を試す
omc version
```

---

## 使い方

### エージェントの呼び出し（Claude Code内）
```
Agent tool → subagent_type: "oh-my-claudecode:code-reviewer"
```

### スキルの呼び出し
```
/oh-my-claudecode:<skill-name>
```

### 主要コマンド例
```bash
# コードレビュー
# → Claude Code 内で「このファイルをレビューして」と依頼するとcode-reviewerが起動

# 自律実行モード
# → 「autopilot」と入力

# チームオーケストレーション
# → /team で複数エージェント並列実行
```

---

## 参考リンク

- [oh-my-claudecode GitHub](https://github.com/nicekid1/oh-my-claudecode)
- [Claude Code 公式ドキュメント](https://docs.anthropic.com/en/docs/claude-code)
- [Claude Code インストールガイド](https://docs.anthropic.com/en/docs/claude-code/getting-started)
