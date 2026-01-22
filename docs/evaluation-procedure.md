# Coro Cybersecurity v3.7/v3.8 評価手順書

## 文書情報

| 項目 | 内容 |
|------|------|
| **文書名** | Coro Cybersecurity v3.7/v3.8 評価手順書 |
| **作成日** | 2026年1月22日 |
| **バージョン** | 1.0 |
| **対象** | 評価担当者、Claude Code |
| **関連Issue** | [GitHub Issue #1](https://github.com/takaos/coro-net/issues/1) |

---

## 0. コンテキスト復元ガイド（Claude Code向け）

> **重要**: このセクションは、Claude Codeがコンテキストを補完する際に参照するためのものです。

### 0.1 必読ドキュメント一覧

作業を再開する前に、以下のドキュメントを**必ず**読み込んでください：

| 優先度 | ドキュメント | パス | 内容 |
|--------|--------------|------|------|
| **必須** | 評価計画書 | `docs/evaluation-plan.md` | 評価項目、制約条件、スケジュール |
| **必須** | 本手順書 | `docs/evaluation-procedure.md` | 実行手順、チェックリスト |
| 推奨 | リリースノート分析 | `docs/analysis/release-notes-analysis.md` | v3.7/v3.8機能詳細 |
| 参考 | サービス概要 | `docs/analysis/coro-service-overview.md` | Coroプラットフォーム概要 |

### 0.2 評価環境の制約条件（最重要）

```
┌─────────────────────────────────────────────────────────────────┐
│                      評価環境の制約                              │
├─────────────────────────────────────────────────────────────────┤
│  ✅ 利用可能                    │  ❌ 利用不可                   │
├─────────────────────────────────┼────────────────────────────────┤
│  Google Workspace               │  Microsoft 365                 │
│  macOS                          │  Windows                       │
│  Linux                          │                                │
│  英語・日本語                   │  フランス語・その他           │
│  英語圏・日本の機密データ       │  UAE・ブラジルの機密データ    │
└─────────────────────────────────┴────────────────────────────────┘
```

### 0.3 評価ID体系

評価項目は以下のID体系で管理されています：

| プレフィックス | カテゴリ | 例 |
|----------------|----------|-----|
| `SEC-AI-xxx` | セキュリティ/AI関連 | SEC-AI-001: Prompt Injection Detection |
| `SEC-AUTH-xxx` | セキュリティ/認証 | SEC-AUTH-001: MFA Status Detection |
| `MGT-CON-xxx` | 管理/コンソール | MGT-CON-001: Actionboard Redesign |
| `MGT-DEV-xxx` | 管理/デバイス | MGT-DEV-002: Remote Shell |
| `CMP-DATA-xxx` | コンプライアンス/データ | CMP-DATA-002: 日本機密データ検出 |
| `INT-CLOUD-xxx` | 統合/クラウド | INT-CLOUD-001: Google Workspace MFA |
| `INT-AGT-xxx` | 統合/エージェント | INT-AGT-001: macOS Agent 3.7 |

### 0.4 現在の進捗確認方法

GitHub Issueで進捗を確認してください：

```bash
gh issue view 1 --comments
```

---

## 1. 評価手順概要

### 1.1 評価フロー全体図

```
┌─────────────────────────────────────────────────────────────────┐
│                        評価実行フロー                            │
└─────────────────────────────────────────────────────────────────┘

Phase 1: 環境準備 ─────────────────────────────────────────────────
    │
    ├── 1.1 Coroワークスペース設定
    ├── 1.2 Google Workspace連携
    ├── 1.3 macOS Agent設定
    ├── 1.4 Linux Agent設定
    └── 1.5 テストデータ準備
    │
    ▼ チェックポイント: 環境確認完了
    │
Phase 2: セキュリティ機能評価 ─────────────────────────────────────
    │
    ├── 2.1 Prompt Injection Detection [SEC-AI-001]【最高優先】
    ├── 2.2 MFA Status Detection [SEC-AUTH-001]【最高優先】
    ├── 2.3 Shadow AI Blocklist [SEC-AI-002]
    ├── 2.4 Threat Detection Policies [SEC-AUTH-002]
    └── 2.5 Coro AI Summary [SEC-AI-003]
    │
    ▼ チェックポイント: セキュリティ評価完了
    │
Phase 3: 管理機能評価 ─────────────────────────────────────────────
    │
    ├── 3.1 Actionboard Redesign [MGT-CON-001]
    ├── 3.2 Ticket Structure [MGT-CON-002]
    ├── 3.3 Bulk Ticket Actions [MGT-CON-003]
    ├── 3.4 Setup Hub [MGT-CON-004]
    ├── 3.5 Security Gaps [MGT-CON-006]
    ├── 3.6 Remote Shell - Linux [MGT-DEV-002]
    └── 3.7 Scheduled Scan - macOS [MGT-DEV-003]
    │
    ▼ チェックポイント: 管理機能評価完了
    │
Phase 4: コンプライアンス・統合評価 ───────────────────────────────
    │
    ├── 4.1 英語圏機密データ検出 [CMP-DATA-001]
    ├── 4.2 日本機密データ検出 [CMP-DATA-002]
    ├── 4.3 Google Workspace連携 [INT-CLOUD-001～004]
    ├── 4.4 macOS Agent 3.7 [INT-AGT-001]
    └── 4.5 Linux Agent 3.7 [INT-AGT-002]
    │
    ▼ チェックポイント: 全評価完了
    │
Phase 5: 総合評価・報告書作成 ─────────────────────────────────────
    │
    ├── 5.1 評価結果集計
    ├── 5.2 スコアリング
    ├── 5.3 課題・改善点整理
    └── 5.4 最終報告書作成
    │
    ▼ 完了
```

### 1.2 評価スコアリング基準

| スコア | 評価 | 判断基準 |
|--------|------|----------|
| **5** | 優秀 | 期待以上の機能・性能。追加の価値を提供 |
| **4** | 良好 | 期待通りの機能・性能。問題なく使用可能 |
| **3** | 許容 | 軽微な問題があるが、業務使用は可能 |
| **2** | 要改善 | 重要な問題があり、改善が必要 |
| **1** | 不可 | 機能せず、使用不可 |

### 1.3 評価記録テンプレート

各評価項目について、以下の形式で記録してください：

```markdown
## [評価ID] 評価項目名

### 基本情報
- **対象バージョン**: v3.7 / v3.8
- **評価日**: YYYY-MM-DD
- **評価者**:

### テスト環境
- **OS/デバイス**:
- **Coroバージョン**:
- **関連設定**:

### テスト結果

| テストケース | 期待結果 | 実際の結果 | Pass/Fail |
|--------------|----------|------------|-----------|
| TC-001: xxx | xxx | xxx | Pass/Fail |

### スクリーンショット
- [ ] 設定画面
- [ ] 実行結果
- [ ] エラー（発生した場合）

### 評価スコア: X/5

### 所見・課題
-
-

### 改善提案
-
```

---

## 2. Phase 1: 環境準備手順

### 2.1 Coroワークスペース設定

**目的**: 評価用のCoroワークスペースを準備する

**手順**:

```
Step 1: Coroコンソールにログイン
    │
    ├── URL: https://console.coro.net/
    └── 管理者アカウントでログイン
    │
Step 2: ワークスペース確認/作成
    │
    ├── 評価用ワークスペースの存在確認
    ├── なければ新規作成
    └── 全モジュールが有効化されていることを確認
    │
Step 3: モジュール有効化確認
    │
    ├── Email Security: ✅
    ├── Cloud Security: ✅
    ├── Endpoint Security: ✅
    ├── EDR: ✅
    ├── Network/SWG: ✅
    ├── Data Governance: ✅
    └── Coro AI: ✅
    │
Step 4: 基本設定
    │
    ├── 言語設定: English
    ├── タイムゾーン: 適切に設定
    └── 通知設定: 有効化
```

**確認チェックリスト**:

- [ ] Coroコンソールにログイン可能
- [ ] 評価用ワークスペースが利用可能
- [ ] 全モジュールが有効化
- [ ] 管理者権限を持っている

### 2.2 Google Workspace連携設定

**目的**: Google WorkspaceをCoroに連携する

**参照**: `docs/evaluation-plan.md` - セクション 3.4.1

**前提条件**:
- Google Workspace管理者権限
- Coro Cloud Security連携権限

**手順**:

```
Step 1: Google Workspace管理コンソールでの準備
    │
    ├── admin.google.com にログイン
    ├── セキュリティ > API制御
    └── サードパーティアプリのアクセス設定確認
    │
Step 2: Coroでの連携設定
    │
    ├── Control Panel > Cloud Security
    ├── "Add Cloud Application" をクリック
    ├── Google Workspace を選択
    └── OAuth認証を完了
    │
Step 3: 権限確認
    │
    ├── メールアクセス権限
    ├── Driveアクセス権限
    └── ユーザー情報アクセス権限
    │
Step 4: 連携テスト
    │
    ├── Protected Usersにユーザーが表示されることを確認
    └── Cloud Securityダッシュボードで接続状態を確認
```

**トラブルシューティング**:

| 問題 | 原因 | 対処法 |
|------|------|--------|
| 連携が完了しない | 権限不足 | Google Workspace管理者に追加権限を依頼 |
| ユーザーが表示されない | 同期遅延 | 15-30分待機後に再確認 |
| "Disconnected"表示 | トークン期限切れ | 再連携を実行 |

**確認チェックリスト**:

- [ ] Google Workspace連携完了
- [ ] Protected Usersにユーザー表示
- [ ] 接続状態が"Connected"

### 2.3 macOS Agent設定

**目的**: macOSデバイスにCoro Agent 3.7をインストール・設定

**参照**: `docs/evaluation-plan.md` - セクション 3.4.2, INT-AGT-001

**前提条件**:
- macOS 最新版（推奨）
- 管理者権限

**手順**:

```
Step 1: Agentダウンロード
    │
    ├── Coroコンソール > Devices > "Add Device"
    ├── macOSを選択
    └── インストーラーをダウンロード
    │
Step 2: インストール
    │
    ├── .pkgファイルを実行
    ├── システム環境設定でフルディスクアクセスを許可
    └── ネットワーク拡張機能を許可（必要に応じて）
    │
Step 3: 登録確認
    │
    ├── Coroコンソール > Devices
    ├── デバイスが表示されることを確認
    └── Agent バージョン 3.7以降であることを確認
    │
Step 4: 保護設定
    │
    ├── Endpoint Security有効化確認
    ├── EDR有効化確認
    └── スケジュールスキャン設定（評価用）
```

**確認チェックリスト**:

- [ ] macOS Agent 3.7インストール完了
- [ ] Coroコンソールにデバイス表示
- [ ] Endpoint Security有効
- [ ] EDR有効

### 2.4 Linux Agent設定

**目的**: LinuxデバイスにCoro Agent 3.7をインストール・設定

**参照**: `docs/evaluation-plan.md` - セクション 3.4.2, INT-AGT-002

**前提条件**:
- Ubuntu 22.04 LTS または RHEL 9
- root/sudo権限

**手順**:

```
Step 1: Agentダウンロード
    │
    ├── Coroコンソール > Devices > "Add Device"
    ├── Linuxを選択
    └── インストールコマンドをコピー
    │
Step 2: インストール（Ubuntu例）
    │
    ├── curl -sL <download-url> | sudo bash
    └── インストール完了を待機
    │
Step 3: 登録確認
    │
    ├── Coroコンソール > Devices
    ├── デバイスが表示されることを確認
    └── Agent バージョン 3.7以降であることを確認
    │
Step 4: 保護設定
    │
    ├── Endpoint Security有効化確認
    └── リモートシェル権限確認
```

**確認チェックリスト**:

- [ ] Linux Agent 3.7インストール完了
- [ ] Coroコンソールにデバイス表示
- [ ] Endpoint Security有効
- [ ] リモートシェルアクセス可能

### 2.5 テストデータ準備

**目的**: 評価用のテストデータを準備する

**参照**: `docs/evaluation-plan.md` - セクション 5.3

#### 2.5.1 プロンプトインジェクションテストメール

以下のテストメールを準備：

| テストID | 件名 | 本文パターン | 期待結果 |
|----------|------|--------------|----------|
| PI-001 | "Ignore previous instructions" | 明示的なプロンプトインジェクション | 検知 |
| PI-002 | "Meeting Request" | エンコードされたプロンプト（Base64） | 検知確認 |
| PI-003 | "AI Conference Invitation" | AI関連の正当なビジネスメール | 正常通過 |
| PI-004 | "System prompt override" | 複数パターンの組み合わせ | 検知 |

#### 2.5.2 機密データテストファイル

**日本向けテストデータ**:

```
# test-sensitive-jp.txt
マイナンバー: 123456789012
運転免許証番号: 012345678901
パスポート番号: AB1234567
健康保険証番号: 12345678
```

**英語圏向けテストデータ**:

```
# test-sensitive-en.txt
Social Security Number: 123-45-6789
Credit Card: 4111-1111-1111-1111
Bank Account: 123456789012
Passport: A12345678
```

**確認チェックリスト**:

- [ ] プロンプトインジェクションテストメール準備完了
- [ ] 日本機密データテストファイル準備完了
- [ ] 英語圏機密データテストファイル準備完了

### 2.6 Phase 1 完了チェック

以下のすべてが完了していることを確認してください：

```
Phase 1 完了チェックリスト
├── [ ] Coroワークスペース設定完了
├── [ ] Google Workspace連携完了
├── [ ] macOS Agent 3.7設定完了
├── [ ] Linux Agent 3.7設定完了
├── [ ] テストデータ準備完了
└── [ ] GitHub Issueに進捗報告
```

**GitHub Issue更新コマンド**:

```bash
gh issue comment 1 --body "## Phase 1: 環境準備 完了

### 完了項目
- [x] Coroワークスペース設定
- [x] Google Workspace連携
- [x] macOS Agent 3.7設定
- [x] Linux Agent 3.7設定
- [x] テストデータ準備

### 備考
（問題点や注意事項があれば記載）

---
*次のステップ: Phase 2 セキュリティ機能評価*"
```

---

## 3. Phase 2: セキュリティ機能評価手順

### 3.1 SEC-AI-001: Prompt Injection Detection【最高優先】

**参照**: `docs/evaluation-plan.md` - セクション 3.1.1

**評価目的**: メール本文・件名内のAIプロンプトインジェクション検知精度を評価

**前提条件**:
- Google Workspace連携済み
- Email Security有効

**テスト手順**:

```
Step 1: 検知ポリシー確認
    │
    ├── Control Panel > Email Security
    ├── Threat Detection設定を確認
    └── Prompt Injection検知が有効であることを確認
    │
Step 2: テストケース実行
    │
    ├── TC-001: 明示的プロンプトインジェクション
    │   ├── テストメール送信（PI-001）
    │   ├── 検知までの時間を計測
    │   └── チケット作成を確認
    │
    ├── TC-002: エンコードされたプロンプト
    │   ├── テストメール送信（PI-002）
    │   └── 検知可否を確認
    │
    └── TC-003: 正常メール誤検知確認
        ├── テストメール送信（PI-003）
        └── 正常に配信されることを確認
    │
Step 3: 結果記録
    │
    ├── 検知率（True Positive Rate）
    ├── 誤検知率（False Positive Rate）
    ├── 検知までの時間
    └── チケット情報の正確性
```

**評価観点**:

| 観点 | 評価基準 | 重み |
|------|----------|------|
| 検知率 | 悪意あるプロンプトの検知率 | 40% |
| 誤検知率 | 正常メールの誤検知率 | 30% |
| 検知速度 | 検知までの時間 | 15% |
| アラート品質 | チケット情報の正確性 | 15% |

**結果記録テンプレート**:

```markdown
## SEC-AI-001: Prompt Injection Detection 評価結果

### テスト結果サマリー

| テストケース | 期待結果 | 実際の結果 | 検知時間 | Pass/Fail |
|--------------|----------|------------|----------|-----------|
| TC-001 | 検知 | | | |
| TC-002 | 検知確認 | | | |
| TC-003 | 正常通過 | | | |

### スコア: X/5

### 所見
-

### スクリーンショット
- [ ] 検知設定画面
- [ ] チケット詳細
- [ ] 誤検知確認
```

### 3.2 SEC-AUTH-001: MFA Status Detection (Google Workspace)【最高優先】

**参照**: `docs/evaluation-plan.md` - セクション 3.1.2

**評価目的**: Google WorkspaceのMFA状態検出精度を評価

**前提条件**:
- Google Workspace連携済み
- MFA有効ユーザー3名以上
- MFA無効ユーザー2名以上

**テスト手順**:

```
Step 1: 現在のMFA状態確認
    │
    ├── Google Workspace管理コンソールでMFA状態を確認
    └── 各ユーザーのMFA設定をメモ
    │
Step 2: Coroでの検出確認
    │
    ├── Control Panel > Protected Users
    ├── MFA状態ラベルの表示を確認
    │   ├── "MFA enabled" ラベル
    │   └── "MFA not enabled" ラベル
    └── フィルター機能でMFA状態別にフィルタリング
    │
Step 3: テストケース実行
    │
    ├── TC-001: MFA有効ユーザーの検出
    │   └── "MFA enabled"ラベルが正しく表示されることを確認
    │
    ├── TC-002: MFA無効ユーザーの検出
    │   └── "MFA not enabled"ラベルが正しく表示されることを確認
    │
    ├── TC-003: MFA状態変更の反映
    │   ├── Google Workspace上でMFA状態を変更
    │   └── Coro側への反映時間を計測
    │
    └── TC-004: フィルタリング機能
        ├── MFA enabled でフィルタリング
        └── MFA not enabled でフィルタリング
```

**評価観点**:

| 観点 | 評価基準 | 重み |
|------|----------|------|
| 検出精度 | MFA状態の正確な検出 | 40% |
| 更新速度 | 状態変更の反映時間 | 25% |
| UI表示 | ラベル表示の正確性 | 20% |
| フィルター機能 | フィルタリングの正常動作 | 15% |

### 3.3 SEC-AI-002: Shadow AI Blocklist

**参照**: `docs/evaluation-plan.md` - セクション 3.1.1

**評価目的**: AIチャットボットへのアクセスブロック機能を評価

**テスト手順**:

```
Step 1: Shadow AI Blocklist確認
    │
    ├── Control Panel > SWG > DNS Filtering
    ├── "Shadow AI" カテゴリのデフォルトリストを確認
    └── ブロック対象サイト一覧を確認
    │
Step 2: ブロックテスト
    │
    ├── テストデバイスでSWG有効化
    ├── ブロックリスト内のAIサービスにアクセス
    └── ブロックされることを確認
    │
Step 3: 許可リスト設定
    │
    ├── 特定のAIサービスを許可リストに追加
    └── アクセス可能になることを確認
```

### 3.4 SEC-AUTH-002: Threat Detection Policies

**参照**: `docs/evaluation-plan.md` - セクション 3.1.3

**評価目的**: 新しい脅威検知タイプの動作確認

**テスト対象の検知タイプ**:

| 検知タイプ | テスト方法 | 期待結果 |
|------------|------------|----------|
| Abnormal Admin Activity | 通常時間外の管理操作 | 検知・チケット作成 |
| Mass Data Deletion | 大量ファイル削除 | 検知・チケット作成 |
| Mass Data Download | 大量ファイルダウンロード | 検知・チケット作成 |
| Suspected Bot Attack | 自動化パターンのアクセス | 検知・チケット作成 |
| Suspected Identity Compromise | 異常ログインパターン | 検知・チケット作成 |

**注意**: テストは本番環境に影響を与えない範囲で実施すること

### 3.5 Phase 2 完了チェック

```
Phase 2 完了チェックリスト
├── [ ] SEC-AI-001: Prompt Injection Detection 完了
├── [ ] SEC-AUTH-001: MFA Status Detection 完了
├── [ ] SEC-AI-002: Shadow AI Blocklist 完了
├── [ ] SEC-AUTH-002: Threat Detection Policies 完了
├── [ ] SEC-AI-003: Coro AI Summary 完了
└── [ ] GitHub Issueに進捗報告
```

---

## 4. Phase 3: 管理機能評価手順

### 4.1 MGT-CON-001～006: コンソール機能評価

**参照**: `docs/evaluation-plan.md` - セクション 3.2.1

#### 4.1.1 Actionboard Redesign (MGT-CON-001)

**評価ポイント**:
- オープンチケットサマリーの表示
- 保護デバイス/ユーザーへのリンク
- ワークスペースヘルススコア

**テスト手順**:

```
Step 1: Actionboard表示確認
    │
    ├── ダッシュボードにアクセス
    ├── 各セクションの表示を確認
    └── リンクの動作確認
    │
Step 2: ヘルススコア確認
    │
    ├── スコアの計算ロジック理解
    └── 表示の正確性確認
```

#### 4.1.2 Bulk Ticket Actions (MGT-CON-003)

**評価ポイント**:
- 複数チケット選択
- 一括アクション実行
- 処理の完了確認

**テスト手順**:

```
Step 1: 同一タイプのチケット一括操作
    │
    ├── 複数のマルウェア検知チケットを選択
    ├── 一括でQuarantineアクション実行
    └── 全チケットに適用されることを確認
    │
Step 2: 大量チケットの一括操作
    │
    ├── 50件以上のチケット選択
    └── パフォーマンス・完了確認
```

#### 4.1.3 Security Gaps (MGT-CON-006)

**評価ポイント**:
- セキュリティギャップの検出
- 推奨アクションの表示
- 改善後の更新

**検出対象ギャップ**:

| カテゴリ | ギャップ |
|----------|----------|
| Cloud Security | No Cloud Application Connected |
| Cloud Security | No Access Permission Rules Configured |
| Devices | Agent Protection Limited by Security Software Conflict |
| Data Governance | Privacy Sensitive Data Types Not Configured |

### 4.2 MGT-DEV-002: Remote Shell (Linux)

**参照**: `docs/evaluation-plan.md` - セクション 3.2.2

**評価目的**: Linuxリモートシェルアクセスの動作確認

**前提条件**:
- Linux Agent 3.7以降インストール済み
- デバイスがオンライン状態
- リモートシェル権限が付与済み

**テスト手順**:

```
Step 1: 正常なリモートシェル接続
    │
    ├── Coroコンソール > Devices > 対象デバイス
    ├── "Remote Shell" をクリック
    ├── 接続完了を待機
    └── 基本コマンド実行確認
        ├── ls
        ├── pwd
        ├── cat /etc/os-release
        └── uname -a
    │
Step 2: セッション管理
    │
    ├── セッションタイムアウト確認
    ├── 複数セッションの挙動確認
    └── セッション終了確認
    │
Step 3: 権限制御
    │
    ├── 実行可能なコマンドの確認
    └── 危険なコマンドのブロック確認
```

**評価観点**:

| 観点 | 評価基準 |
|------|----------|
| 接続安定性 | 接続の成功率、切断頻度 |
| レスポンス | コマンド実行のレスポンス時間 |
| セキュリティ | 権限制御の適切性 |
| 監査ログ | 操作ログの記録 |

### 4.3 MGT-DEV-003: Scheduled Malware Scan (macOS)

**参照**: `docs/evaluation-plan.md` - セクション 3.2.2

**評価目的**: macOSスケジュールスキャンの動作確認

**テスト手順**:

```
Step 1: スケジュール設定
    │
    ├── Control Panel > Endpoint Security
    ├── スケジュールスキャン設定を開く
    └── 日次スキャンを設定（テスト用に近い時刻）
    │
Step 2: スキャン実行確認
    │
    ├── スケジュールされた時刻にスキャン開始を確認
    ├── スキャン完了を確認
    └── スキャン結果をログで確認
    │
Step 3: 検出テスト
    │
    ├── EICAR テストファイルを配置
    ├── スキャン実行
    └── チケット作成を確認
```

### 4.4 Phase 3 完了チェック

```
Phase 3 完了チェックリスト
├── [ ] MGT-CON-001: Actionboard Redesign 完了
├── [ ] MGT-CON-002: Updated Ticket Structure 完了
├── [ ] MGT-CON-003: Bulk Ticket Actions 完了
├── [ ] MGT-CON-004: Setup Hub 完了
├── [ ] MGT-CON-005: Hierarchy Tree 完了
├── [ ] MGT-CON-006: Security Gaps 完了
├── [ ] MGT-DEV-001: Agent Health Filter 完了
├── [ ] MGT-DEV-002: Remote Shell (Linux) 完了
├── [ ] MGT-DEV-003: Scheduled Malware Scan (macOS) 完了
├── [ ] MGT-DEV-004: Disable Protection (Linux) 完了
└── [ ] GitHub Issueに進捗報告
```

---

## 5. Phase 4: コンプライアンス・統合評価手順

### 5.1 CMP-DATA-001: 英語圏機密データ検出

**参照**: `docs/evaluation-plan.md` - セクション 3.3.1

**評価目的**: SSN、クレジットカード等の検出精度を評価

**テスト手順**:

```
Step 1: Data Governance設定確認
    │
    ├── Control Panel > Data Governance
    ├── 有効化されているデータタイプを確認
    │   ├── Social Security Number (SSN)
    │   ├── Credit Card Number
    │   ├── Bank Account Number
    │   └── Passport Number
    └── 検出ポリシーを確認
    │
Step 2: テストファイル配置
    │
    ├── Google Driveに test-sensitive-en.txt をアップロード
    └── 検出を待機（スキャン間隔に依存）
    │
Step 3: 検出確認
    │
    ├── Data Governanceダッシュボードで検出結果確認
    ├── チケット作成を確認
    └── 検出されたデータタイプの正確性確認
    │
Step 4: 誤検知確認
    │
    ├── 類似パターンの非機密データ（電話番号等）を含むファイル配置
    └── 誤検知されないことを確認
```

### 5.2 CMP-DATA-002: 日本機密データ検出

**参照**: `docs/evaluation-plan.md` - セクション 3.3.1

**評価目的**: マイナンバー、運転免許証番号等の検出精度を評価

**テスト手順**:

```
Step 1: 日本機密データタイプ有効化確認
    │
    ├── Control Panel > Data Governance
    └── 日本固有のデータタイプが利用可能か確認
    │
Step 2: テストファイル配置
    │
    ├── Google Driveに test-sensitive-jp.txt をアップロード
    └── 検出を待機
    │
Step 3: 検出確認
    │
    ├── 各データタイプの検出を確認
    │   ├── マイナンバー（12桁）
    │   ├── 運転免許証番号
    │   ├── パスポート番号
    │   └── 健康保険証番号
    └── チケット情報の正確性確認
```

**注意**: 日本機密データ検出がCoroでサポートされているか事前確認が必要。サポートされていない場合は「機能なし」として記録。

### 5.3 INT-CLOUD-001～004: Google Workspace連携評価

**参照**: `docs/evaluation-plan.md` - セクション 3.4.1

**評価項目**:

| 評価ID | 項目 | 評価内容 |
|--------|------|----------|
| INT-CLOUD-001 | MFA Integration | MFA状態の取得・表示 |
| INT-CLOUD-002 | Connection Status | 権限不足時の状態表示 |
| INT-CLOUD-003 | Drive DLP | ファイル内機密データ検出 |
| INT-CLOUD-004 | Gmail Protection | メールセキュリティ機能 |

### 5.4 INT-AGT-001: macOS Agent 3.7

**参照**: `docs/evaluation-plan.md` - セクション 3.4.2

**評価項目**:
- スケジュールマルウェアスキャン
- EDRパフォーマンス最適化
- オンアクセススキャン

**テスト手順**:

```
Step 1: スケジュールマルウェアスキャン
    │
    ├── スケジュール設定・実行確認
    └── スキャン結果の確認
    │
Step 2: EDRパフォーマンス
    │
    ├── EDR有効時のシステム負荷測定
    │   ├── CPU使用率
    │   ├── メモリ使用量
    │   └── ディスクI/O
    └── 通常操作への影響確認
    │
Step 3: オンアクセススキャン
    │
    ├── ファイル操作時のスキャン動作確認
    └── EICAR テストファイルでの検出確認
```

### 5.5 INT-AGT-002: Linux Agent 3.7

**参照**: `docs/evaluation-plan.md` - セクション 3.4.2

**評価項目**:
- 保護無効化機能
- リモートシェル機能

**テスト手順**:

```
Step 1: 保護無効化機能
    │
    ├── Coroコンソールから保護無効化を実行
    ├── デバイス上で無効化状態を確認
    │   └── coro-agent status コマンドで確認
    ├── 再有効化を実行
    └── 再有効化状態を確認
    │
Step 2: リモートシェル機能
    │
    ├── （MGT-DEV-002で評価済みの場合はスキップ可）
    └── 追加のテストケースがあれば実行
```

### 5.6 Phase 4 完了チェック

```
Phase 4 完了チェックリスト
├── [ ] CMP-DATA-001: 英語圏機密データ検出 完了
├── [ ] CMP-DATA-002: 日本機密データ検出 完了
├── [ ] CMP-DATA-003: Unified Ticket Consolidation 完了
├── [ ] CMP-LOC-001: 英語UI 完了
├── [ ] CMP-LOC-002: 日本語対応確認 完了
├── [ ] INT-CLOUD-001～004: Google Workspace連携 完了
├── [ ] INT-AGT-001: macOS Agent 3.7 完了
├── [ ] INT-AGT-002: Linux Agent 3.7 完了
└── [ ] GitHub Issueに進捗報告
```

---

## 6. Phase 5: 総合評価・報告書作成手順

### 6.1 評価結果集計

**手順**:

```
Step 1: 全評価項目の結果収集
    │
    ├── 各評価記録ファイルを確認
    └── スコアを集計表に転記
    │
Step 2: カテゴリ別集計
    │
    ├── セキュリティ機能評価の平均スコア
    ├── 管理機能評価の平均スコア
    ├── コンプライアンス機能評価の平均スコア
    └── 統合・連携機能評価の平均スコア
    │
Step 3: 総合スコア算出
    │
    ├── 最高優先度項目の確認
    │   ├── SEC-AI-001: Prompt Injection Detection
    │   └── SEC-AUTH-001: MFA Status Detection
    └── 全体平均スコアの算出
```

**集計テンプレート**:

```markdown
## 評価結果集計表

### セキュリティ機能評価

| 評価ID | 項目 | スコア | 備考 |
|--------|------|--------|------|
| SEC-AI-001 | Prompt Injection Detection | /5 | |
| SEC-AI-002 | Shadow AI Blocklist | /5 | |
| SEC-AI-003 | Coro AI Summary | /5 | |
| SEC-AUTH-001 | MFA Status Detection | /5 | |
| SEC-AUTH-002 | Threat Detection Policies | /5 | |
| **平均** | | **/5** | |

### 管理機能評価
...

### 総合評価

| 項目 | 値 |
|------|-----|
| 最高優先度項目最低スコア | /5 |
| 全体平均スコア | /5 |
| **総合評価** | 推奨 / 条件付き推奨 / 保留 / 非推奨 |
```

### 6.2 総合評価判定

**判定基準**:

| 評価 | 条件 |
|------|------|
| **推奨** | 最高優先度項目が全て4以上、かつ平均スコア3.5以上 |
| **条件付き推奨** | 最高優先度項目に3があるが、重大な問題なし |
| **保留** | 最高優先度項目に2以下があり、改善待ち |
| **非推奨** | 複数の重大な問題があり、導入リスクが高い |

### 6.3 報告書作成

**成果物**:

| 成果物 | ファイル名 | 内容 |
|--------|------------|------|
| 評価結果報告書 | `docs/reports/evaluation-report.md` | 全評価項目の結果と分析 |
| 機能別評価シート | `docs/reports/evaluation-details.md` | 各機能の詳細評価結果 |
| 課題・改善提案書 | `docs/reports/issues-and-recommendations.md` | 発見された問題と改善提案 |

**報告書テンプレート**:

```markdown
# Coro Cybersecurity v3.7/v3.8 評価結果報告書

## 1. エグゼクティブサマリー

### 総合評価: [推奨 / 条件付き推奨 / 保留 / 非推奨]

### 主要所見
1.
2.
3.

### 推奨事項
1.
2.
3.

## 2. 評価結果詳細
...

## 3. 課題と改善提案
...

## 4. 付録
- スクリーンショット
- テスト証跡
```

### 6.4 Phase 5 完了チェック

```
Phase 5 完了チェックリスト
├── [ ] 全評価結果の集計完了
├── [ ] 総合評価判定完了
├── [ ] 評価結果報告書作成完了
├── [ ] 機能別評価シート作成完了
├── [ ] 課題・改善提案書作成完了
├── [ ] スクリーンショット整理完了
└── [ ] GitHub Issueに最終報告
```

---

## 7. トラブルシューティング

### 7.1 よくある問題と対処法

#### 環境関連

| 問題 | 原因 | 対処法 |
|------|------|--------|
| Google Workspace連携失敗 | 権限不足 | Google Workspace管理者に追加権限を依頼 |
| Agent接続不可 | ネットワーク問題 | ファイアウォール設定確認、プロキシ設定確認 |
| MFA状態が表示されない | 同期遅延 | 15-30分待機、手動同期実行 |

#### 評価関連

| 問題 | 原因 | 対処法 |
|------|------|--------|
| 機密データが検出されない | スキャン未実行 | スキャンスケジュール確認、手動スキャン実行 |
| チケットが作成されない | ポリシー設定不備 | 検知ポリシーの設定確認 |
| リモートシェルが接続できない | 権限不足 | 権限設定確認、Agent再起動 |

### 7.2 サポート連絡先

問題が解決しない場合は、以下に連絡：

- Coroサポート: support@coro.net
- ドキュメント: https://docs.coro.net/

---

## 8. 過去の教訓・注意事項

### 8.1 一般的な注意事項

| 項目 | 注意事項 |
|------|----------|
| **テスト環境** | 本番環境でのテストは避け、評価専用ワークスペースを使用 |
| **機密データ** | テスト用の機密データは架空のものを使用（実際の個人情報は使用しない） |
| **スクリーンショット** | 評価証跡として全ての主要画面をキャプチャ |
| **進捗報告** | 各Phase完了時にGitHub Issueに進捗を報告 |

### 8.2 コンテキスト管理（Claude Code向け）

| 項目 | 注意事項 |
|------|----------|
| **ドキュメント参照** | 作業再開時は必ず「0. コンテキスト復元ガイド」を参照 |
| **進捗確認** | `gh issue view 1 --comments` で最新の進捗を確認 |
| **評価ID確認** | 評価項目は評価IDで管理し、混乱を避ける |
| **制約条件** | 評価環境の制約条件を常に意識する |

### 8.3 過去の失敗パターン（将来のために記録）

> **注意**: このセクションは評価実施後に更新してください。

| 日付 | 問題 | 原因 | 対処 | 教訓 |
|------|------|------|------|------|
| - | - | - | - | - |

---

## 9. 付録

### 9.1 評価チェックリスト（全体）

```
Coro Cybersecurity v3.7/v3.8 評価チェックリスト

Phase 1: 環境準備
├── [ ] Coroワークスペース設定
├── [ ] Google Workspace連携
├── [ ] macOS Agent 3.7設定
├── [ ] Linux Agent 3.7設定
└── [ ] テストデータ準備

Phase 2: セキュリティ機能評価
├── [ ] SEC-AI-001: Prompt Injection Detection【最高】
├── [ ] SEC-AI-002: Shadow AI Blocklist
├── [ ] SEC-AI-003: Coro AI Summary
├── [ ] SEC-AUTH-001: MFA Status Detection【最高】
└── [ ] SEC-AUTH-002: Threat Detection Policies

Phase 3: 管理機能評価
├── [ ] MGT-CON-001: Actionboard Redesign
├── [ ] MGT-CON-002: Updated Ticket Structure
├── [ ] MGT-CON-003: Bulk Ticket Actions
├── [ ] MGT-CON-004: Setup Hub
├── [ ] MGT-CON-005: Hierarchy Tree
├── [ ] MGT-CON-006: Security Gaps
├── [ ] MGT-DEV-001: Agent Health Filter
├── [ ] MGT-DEV-002: Remote Shell (Linux)
├── [ ] MGT-DEV-003: Scheduled Malware Scan (macOS)
└── [ ] MGT-DEV-004: Disable Protection (Linux)

Phase 4: コンプライアンス・統合評価
├── [ ] CMP-DATA-001: 英語圏機密データ検出
├── [ ] CMP-DATA-002: 日本機密データ検出
├── [ ] CMP-DATA-003: Unified Ticket Consolidation
├── [ ] CMP-LOC-001: 英語UI
├── [ ] CMP-LOC-002: 日本語対応確認
├── [ ] INT-CLOUD-001: Google Workspace MFA Integration
├── [ ] INT-CLOUD-002: Google Workspace Connection
├── [ ] INT-CLOUD-003: Google Drive DLP
├── [ ] INT-CLOUD-004: Gmail Protection
├── [ ] INT-AGT-001: macOS Agent 3.7
└── [ ] INT-AGT-002: Linux Agent 3.7

Phase 5: 総合評価・報告書作成
├── [ ] 評価結果集計
├── [ ] 総合評価判定
├── [ ] 評価結果報告書作成
├── [ ] 機能別評価シート作成
├── [ ] 課題・改善提案書作成
└── [ ] GitHub Issue最終報告
```

### 9.2 関連ドキュメントリンク

| ドキュメント | パス | 用途 |
|--------------|------|------|
| 評価計画書 | `docs/evaluation-plan.md` | 評価項目・基準の詳細 |
| 評価計画書（英語版） | `docs/evaluation-plan-en.md` | English version |
| リリースノート分析 | `docs/analysis/release-notes-analysis.md` | v3.7/v3.8機能詳細 |
| サービス概要 | `docs/analysis/coro-service-overview.md` | Coroプラットフォーム概要 |
| **スクリーンショット索引** | `docs/screenshots-index.md` | 取得済みスクリーンショット一覧 |
| Coro公式ドキュメント | https://docs.coro.net/ | 公式リファレンス |
| v3.7リリースノート | https://docs.coro.net/rn/major-3.7 | 公式リリースノート |
| v3.8リリースノート | https://docs.coro.net/rn/major-3.8 | 公式リリースノート |

### 9.3 取得済みスクリーンショット

| ファイル | 内容 | 関連評価項目 |
|----------|------|--------------|
| `img/actionboard-dashboard.png` | Actionboardダッシュボード | MGT-CON-001, MGT-CON-006 |
| `img/user-profile-settings.png` | ユーザープロファイル設定 | CMP-LOC-001 |
| `img/notification-settings-threat-types.png` | 通知設定（脅威タイプ一覧） | SEC-AI-001, SEC-AUTH-002 |

### 9.4 コマンドリファレンス

**GitHub Issue操作**:

```bash
# Issue一覧表示
gh issue list

# Issue詳細表示（コメント含む）
gh issue view 1 --comments

# コメント追加
gh issue comment 1 --body "コメント内容"

# 新規Issue作成
gh issue create --title "タイトル" --body "本文"
```

**進捗報告テンプレート**:

```bash
gh issue comment 1 --body "## Phase X: [Phase名] 完了

### 完了項目
- [x] 項目1
- [x] 項目2

### 評価結果サマリー
| 評価ID | スコア |
|--------|--------|
| XXX-001 | X/5 |

### 課題・所見
-

---
*次のステップ: Phase Y [Phase名]*"
```

---

## 文書履歴

| 版 | 日付 | 変更内容 | 作成者 |
|----|------|----------|--------|
| 1.0 | 2026-01-22 | 初版作成 | - |

---

*本評価手順書は、Coro Cybersecurity v3.7およびv3.8の新機能評価を実行するための詳細手順を提供します。*
*評価実施時には、最新のドキュメントおよび製品仕様を確認してください。*
