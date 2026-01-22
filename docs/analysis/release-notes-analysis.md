# Coro リリースノート詳細分析

## 評価対象バージョン

| バージョン | リリース日 | タイプ |
|------------|------------|--------|
| v3.7 | 2025年11月16日 | メジャーリリース |
| v3.8 | 2025年12月14日 | メジャーリリース |

---

# Part 1: v3.7 リリースノート分析

## 1. 新機能一覧

### 1.1 Coro Console（管理コンソール）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 1.1 | Actionboard redesign | ダッシュボードの再設計（オープンチケットサマリー、保護デバイス/ユーザーへのリンク、ワークスペースヘルススコア） | UI/UX |
| 1.2 | Updated ticket structure | チケット詳細ペインの再設計（4タブ構成：Overview, Full details, Activity logs, Comments） | チケット管理 |
| 1.3 | Updated ticket closure policies | 10日後の自動クローズポリシー（Cloud/Email/Endpoint Security, Data Governance） | 運用フロー |
| 1.4 | Bulk ticket actions | 複数チケットへの一括アクション | 運用効率 |
| 1.5 | Global allowlists and blocklists | MSP管理者向けグローバル許可/ブロックリスト（EDR, Email, Endpoint Security） | MSP管理 |

### 1.2 Cloud Security（クラウドセキュリティ）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 2.1 | Threat detection policies | 新しい脅威検知ポリシー（Abnormal Admin Activity, Mass Data Deletion/Download, Bot Attack, Identity Compromise） | セキュリティポリシー |

### 1.3 Endpoint Security（エンドポイントセキュリティ）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 3.1 | Remote Agent uninstallation | WindowsデバイスのリモートAgentアンインストール | デバイス管理 |
| 3.2 | USB Lockdown allowlisting | シリアル番号によるUSBデバイス許可リスト | デバイスポリシー |

### 1.4 Network and SWG（ネットワーク/SWG）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 4.0 | Module split | NetworkモジュールをNetwork（VPN/ZTNA）とSWG（DNSフィルタリング）に分割 | アーキテクチャ |
| 4.1 | DNS filtering allowlists/blocklists | デバイスラベルによるDNSフィルタリングリスト適用 | ネットワークポリシー |
| 4.2 | Shadow AI blocklist | AIチャットボットブロック用デフォルトリスト | AIセキュリティ |
| 4.3 | Improved DNS summary report | DNSサマリーレポートのレイアウト改善 | レポート |
| 4.4 | Virtual office Brazil server | ブラジルリージョンのVPNサーバー追加 | インフラ |

### 1.5 Email Security（メールセキュリティ）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 5.1 | Prompt injection detection | メール内のAIプロンプトインジェクション検知 | **重要** AIセキュリティ |
| 5.2 | User reports of quarantined emails | 検疫メールのユーザー通知レポート | ユーザー通知 |
| 5.3 | Delete auto-forwarding rules | 自動転送ルールの削除機能 | データ漏洩防止 |

### 1.6 Data Governance（データガバナンス）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 6.1 | Unified ticket - Cloud/Email | クラウド共有・メールの機密データチケット統合 | チケット管理 |
| 6.2 | Unified ticket - Endpoint | エンドポイントドライブスキャンの機密データチケット統合 | チケット管理 |
| 6.3 | UAE sensitive data detection | UAE固有の機密データ検出（ID、パスポート等5種類） | コンプライアンス |

### 1.7 MDM（モバイルデバイス管理）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 7.1 | Demo mode | MDMサービスのデモデータ提供 | デモ/評価 |

### 1.8 Coro AI

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 8.1 | Global view AI summary | グローバルビューへのAIサマリー追加 | AI機能 |

## 2. 機能強化（Enhancements）

### 2.1 Cloud Security

| 項目 | 内容 |
|------|------|
| Impossible Traveler ticket | イベント説明、都市/州詳細、距離（km）、イベント数の表示改善 |

### 2.2 Coro Console

| 項目 | 内容 |
|------|------|
| French (Canada) support | フランス語（カナダ）のUI対応追加 |

### 2.3 EDR

| 項目 | 内容 |
|------|------|
| EDR settings | EDR保護の有効化/無効化設定 |
| Additional ticket info | Privilege Escalation/Credential Access/Persistenceチケットへの詳細追加 |
| Allowlist/blocklist UI | UIの簡素化 |

### 2.4 Endpoint Security

| 項目 | 内容 |
|------|------|
| Allowlist/blocklist UI | UIの簡素化 |
| Container hash | マルウェア検出時のコンテナハッシュ表示 |
| Self-update setting | 自動更新の有効化/無効化設定 |

### 2.5 Email Security

| 項目 | 内容 |
|------|------|
| Inbound Gateway test | 事前DNS変更テスト、エンドツーエンドテスト |
| Localized warning banner | 警告バナーのワークスペース言語対応 |
| Disconnected status | 権限不足時の接続状態表示改善 |

## 3. 修正された問題（Fixed Issues）

| 問題 | 修正内容 |
|------|----------|
| Activity Log Undo action | デバイス保護無効化時のUndoアクション追加 |
| User aliases sync | Microsoft 365/Google Workspaceのエイリアス同期 |
| Reported by User tickets | 保護ユーザー状態の正しい表示 |

## 4. エージェント更新

### 4.1 Linux Agent 3.7

| 機能 | 説明 |
|------|------|
| Disable protection | Linux保護の無効化サポート |
| Remote shell | リモートシェルアクセス |
| Bug fixes | 一般的なバグ修正 |

### 4.2 macOS Agent 3.7

| 機能 | 説明 |
|------|------|
| Scheduled malware scan | スケジュールマルウェアスキャン |
| Optimized performance | EDR/オンアクセススキャンの性能最適化 |
| Bug fixes | 一般的なバグ修正 |

### 4.3 Windows Agent 3.7

| 機能 | 説明 |
|------|------|
| Remote uninstallation | リモートアンインストールサポート |
| Optimized scan | 起動時スキャン性能改善 |
| Enhanced malware reporting | コンテナファイル内マルウェアの親コンテナ報告 |
| Bug fixes | 一般的なバグ修正 |

---

# Part 2: v3.8 リリースノート分析

## 1. 新機能一覧

### 1.1 Coro Console（管理コンソール）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 1.1 | Onboarding for new workspaces | Setup Hubによるオンボーディングチェックリスト | 初期設定 |
| 1.2 | Hierarchy tree for Workspaces | ワークスペース階層ツリー表示（MSP向け） | MSP管理 |
| 1.3 | Security gaps | 新しいセキュリティギャップ検出（Cloud/Devices/Data Governance） | セキュリティ監査 |
| 1.4 | Workspace filter for Actionboard | 全ワークスペース/サブスクリプションのみフィルター | MSP管理 |
| 1.5 | Date range filter for Insights | Coro Insightsの日付範囲フィルター | レポート |
| 1.6 | Agent health filter | デバイスページのエージェント健全性フィルター | デバイス管理 |
| 1.7 | Remote shell for Linux | Linuxデバイスのリモートシェルサポート | リモート管理 |

### 1.2 Cloud Security（クラウドセキュリティ）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 2.1 | MFA status detection | Microsoft 365/Google WorkspaceのMFA状態検出・表示 | **重要** セキュリティ監視 |

### 1.3 Email Security（メールセキュリティ）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 3.1 | Auto-forwarding rules UI | 外部自動転送ルール削除ポリシー対象ユーザーのUI表示 | ユーザー管理 |

### 1.4 Data Governance（データガバナンス）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 4.1 | Brazil sensitive data detection | ブラジル固有の機密データ検出（CPF、パスポート等5種類） | コンプライアンス |

### 1.5 Security Awareness Training（セキュリティ意識向上トレーニング）

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 5.1 | Multi-language support | シミュレーション/トレーニングの多言語対応（6言語） | 国際対応 |
| 5.2 | Selection by user label | ユーザーラベルによるSAT対象選択 | ユーザー管理 |

### 1.6 Coro AI

| 機能ID | 機能名 | 説明 | 影響範囲 |
|--------|--------|------|----------|
| 6.1 | Security gap summary report | AIによるセキュリティギャップサマリーと推奨事項 | AI機能 |

## 2. 機能強化（Enhancements）

### 2.1 Cloud Security

| 項目 | 内容 |
|------|------|
| IP address exclusion | VPN Exclusions → IP Address Exclusionsに名称変更・説明改善 |

### 2.2 SWG

| 項目 | 内容 |
|------|------|
| DNS filtering while disabled | 無効時もDNSフィルタリング設定変更可能 |

---

# Part 3: 機能カテゴリ別サマリー

## 1. セキュリティ機能カテゴリ

### 1.1 AI/ML関連セキュリティ

| バージョン | 機能 | 重要度 |
|------------|------|--------|
| v3.7 | Prompt injection detection（メール） | **高** |
| v3.7 | Shadow AI blocklist（SWG） | 中 |
| v3.7/3.8 | Coro AI サマリー機能 | 中 |

### 1.2 認証・アクセス制御

| バージョン | 機能 | 重要度 |
|------------|------|--------|
| v3.8 | MFA状態検出（Microsoft 365/Google Workspace） | **高** |
| v3.7 | Threat detection policies | 高 |

### 1.3 データ保護・コンプライアンス

| バージョン | 機能 | 重要度 |
|------------|------|--------|
| v3.7 | UAE機密データ検出 | 中 |
| v3.8 | ブラジル機密データ検出 | 中 |
| v3.7 | 統合チケット（機密データ） | 中 |

### 1.4 デバイス管理

| バージョン | 機能 | 重要度 |
|------------|------|--------|
| v3.7 | Remote Agent uninstallation（Windows） | 中 |
| v3.7 | USB Lockdown allowlisting | 中 |
| v3.8 | Agent health filter | 低 |

### 1.5 ネットワークセキュリティ

| バージョン | 機能 | 重要度 |
|------------|------|--------|
| v3.7 | Network/SWGモジュール分割 | 中 |
| v3.7 | DNS filtering allowlists/blocklists | 中 |

## 2. 運用効率化カテゴリ

### 2.1 UI/UX改善

| バージョン | 機能 |
|------------|------|
| v3.7 | Actionboard redesign |
| v3.7 | Updated ticket structure |
| v3.8 | Hierarchy tree for Workspaces |
| v3.8 | Setup Hub onboarding |

### 2.2 一括操作・自動化

| バージョン | 機能 |
|------------|------|
| v3.7 | Bulk ticket actions |
| v3.7 | Auto ticket closure (10 days) |
| v3.7 | Delete auto-forwarding rules |

### 2.3 フィルタリング・検索

| バージョン | 機能 |
|------------|------|
| v3.8 | Workspace filter for Actionboard |
| v3.8 | Date range filter for Insights |
| v3.8 | Agent health filter |

---

# Part 4: 評価観点整理

## 1. 機能評価観点

### 1.1 セキュリティ効果

- [ ] 新しい脅威タイプへの対応力
- [ ] 検知精度（False Positive/Negative）
- [ ] 対応の自動化レベル

### 1.2 運用性

- [ ] UI/UXの使いやすさ
- [ ] 設定の柔軟性
- [ ] 一括操作の効率性

### 1.3 統合性

- [ ] クラウドアプリケーション連携
- [ ] エージェント機能の一貫性
- [ ] API機能

### 1.4 コンプライアンス

- [ ] 地域別データ検出の網羅性
- [ ] レポート機能
- [ ] 監査証跡

## 2. 重点評価項目（v3.7/v3.8）

### 最高優先度

1. **Prompt injection detection** - AIセキュリティの新しい脅威
2. **MFA status detection** - 基本的なセキュリティ姿勢の可視化

### 高優先度

3. **Threat detection policies** - 新しい検知タイプ
4. **Shadow AI blocklist** - 生成AI利用制御
5. **Security gaps detection** - セキュリティ姿勢の改善

### 中優先度

6. **Unified ticket consolidation** - 運用効率化
7. **Remote Agent uninstallation** - デバイス管理
8. **Setup Hub onboarding** - 初期導入

---

*作成日: 2026-01-22*
*分析対象: v3.7 (2025-11-16), v3.8 (2025-12-14)*
