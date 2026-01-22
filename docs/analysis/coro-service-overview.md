# Coro Cybersecurity プラットフォーム 分析レポート

## 1. サービス概要

### 1.1 基本情報

| 項目 | 内容 |
|------|------|
| **サービス名** | Coro Cybersecurity |
| **公式サイト** | https://www.coro.net/ |
| **ドキュメント** | https://docs.coro.net/ |
| **API** | https://developers.coro.net |
| **スローガン** | "A Modern approach to Cybersecurity" |
| **メインメッセージ** | "Cybersecurity Made Easy For Lean IT Teams" |

### 1.2 対象ユーザー

- **主要ターゲット**: リソースが限られたIT運用チーム（Lean IT Teams）
- **ユースケース**: 複雑なセキュリティ運用を簡素化したい企業・組織

### 1.3 グローバル展開

- シカゴ（米国）
- ニューヨーク（米国）
- ロンドン（英国）
- イスラエル
- スペイン
- イタリア

---

## 2. 製品アーキテクチャ

### 2.1 保護対象領域（Protection Domains）

```
┌─────────────────────────────────────────────────────────────────┐
│                    Coro Cybersecurity Platform                  │
├─────────────┬─────────────┬─────────────┬───────────┬───────────┤
│   Email     │    Cloud    │  Endpoint   │  Network  │   User    │
│  Security   │  Security   │  Security   │   & SWG   │  Security │
├─────────────┼─────────────┼─────────────┼───────────┼───────────┤
│ ・脅威検知  │ ・クラウド  │ ・マルウェア│ ・VPN/ZTNA│ ・ユーザー│
│ ・フィッシ  │   アプリ    │   対策      │ ・DNS     │   保護    │
│   ング対策  │   保護      │ ・EDR       │   フィル  │ ・MFA     │
│ ・スパム    │ ・DLP       │ ・デバイス  │   タリング│   状態    │
│   フィルタ  │             │   管理      │           │   監視    │
└─────────────┴─────────────┴─────────────┴───────────┴───────────┘
```

### 2.2 主要モジュール構成

| モジュール | 説明 | 主要機能 |
|------------|------|----------|
| **Email Security** | メールセキュリティ | 脅威検知、フィッシング対策、プロンプトインジェクション検知 |
| **Cloud Security** | クラウドアプリ保護 | アクセス制御、脅威検知ポリシー、MFA状態監視 |
| **Endpoint Security** | エンドポイント保護 | マルウェア対策、USB制御、リモート管理 |
| **EDR** | 高度な脅威検知 | 振る舞い検知、許可/ブロックリスト |
| **Network** | ネットワーク保護 | VPN、ZTNA、サイト間トンネル |
| **SWG** | Secure Web Gateway | DNSフィルタリング、Shadow AIブロック |
| **Data Governance** | データガバナンス | 機密データ検出、DLP |
| **MDM** | モバイルデバイス管理 | デバイスポリシー、リモート管理 |
| **SAT** | セキュリティ意識向上トレーニング | フィッシングシミュレーション、教育 |
| **Coro AI** | AI支援機能 | セキュリティギャップ分析、推奨事項 |

### 2.3 エージェント対応プラットフォーム

| OS | エージェント | 主要機能 |
|----|--------------|----------|
| **Windows** | Windows Agent | フル機能（EDR、マルウェアスキャン、リモートアンインストール） |
| **macOS** | macOS Agent | スケジュールスキャン、EDR、オンアクセススキャン |
| **Linux** | Linux Agent | 保護無効化、リモートシェル、基本保護 |

---

## 3. 管理コンソール構造

### 3.1 Actionboardダッシュボード

以下はCoroコンソールのActionboardダッシュボードの画面です：

![Actionboard Dashboard](../../img/actionboard-dashboard.png)

**画面の主要要素**:
- **Open Tickets**: オープンチケット数とカテゴリ別内訳
- **Workspace Health Score**: ワークスペースの健全性スコア（0-100）
- **Security Gaps**: セキュリティギャップの検出状況
- **Subscription Overview**: 各モジュールの有効/無効状態
- **モジュール別ステータス**: Cloud Security、Email Security、EDR等の状態

### 3.2 ビュー階層

```
┌─────────────────────────────────────────┐
│            Global View (MSP)            │
│  ・複数ワークスペース一元管理           │
│  ・階層ツリー表示                       │
│  ・グローバルポリシー                   │
├─────────────────────────────────────────┤
│         Workspace View (Customer)        │
│  ・個別組織の管理                       │
│  ・Actionboard                          │
│  ・チケットログ                         │
└─────────────────────────────────────────┘
```

### 3.3 主要UI要素

| 要素 | 説明 |
|------|------|
| **Actionboard** | ダッシュボード（オープンチケット、保護状況、ヘルススコア） |
| **Ticket Log** | セキュリティイベントの管理（4タブ構成：Overview, Full details, Activity logs, Comments） |
| **Protected Users** | 保護対象ユーザー一覧 |
| **Devices** | 保護対象デバイス一覧 |
| **Setup Hub** | 新規ワークスペースのオンボーディング |
| **Coro Insights** | 分析・レポート機能 |

### 3.4 通知設定と脅威タイプ

以下は通知設定画面で確認できる脅威タイプの一覧です：

![Notification Settings - Threat Types](../../img/notification-settings-threat-types.png)

**モジュール別の検知可能な脅威タイプ**:

| モジュール | 脅威タイプ |
|------------|------------|
| **Cloud Security** | Abnormal Admin Activity, Access Permissions Violation, Impossible Traveler, Malware in Cloud Drive, Mass Data Deletion, Mass Data Download, Suspected Bot Attacks, Suspected Identity Compromise |
| **Email Security** | Blocklisted Sender, Brand Impersonation, Domain Spoofing, Malware in Email Attachment, **Prompt Injection**, Spam, Suspicious Content, User Impersonation 他 |
| **Endpoint Security** | Endpoint Vulnerability, Forbidden Wi-Fi Connection, Malware on Endpoint, WiFi Phishing |
| **Data Governance** | Cloud Share Containing Sensitive Data, Email Containing Sensitive Data, Endpoint Drive Containing Sensitive Data |
| **EDR** | Command and Control, Credential Access, Defense Evasion, Discovery, Execution, Initial Access, Persistence, Privilege Escalation |

---

## 4. 対応クラウドアプリケーション

### 4.1 主要統合

| アプリケーション | 機能 | 備考 |
|------------------|------|------|
| **Microsoft 365** | メール保護、クラウドセキュリティ、MFA状態検出 | 追加権限が必要な場合あり |
| **Google Workspace** | メール保護、クラウドセキュリティ、MFA状態検出 | |

### 4.2 検出可能な脅威タイプ

- Abnormal Admin Activity（異常な管理者アクティビティ）
- Mass Data Deletion（大量データ削除）
- Mass Data Download（大量データダウンロード）
- Suspected Bot Attack（ボット攻撃の疑い）
- Suspected Identity Compromise（ID侵害の疑い）
- Impossible Traveler（物理的に不可能な移動）

---

## 5. コンプライアンス・データ保護

### 5.1 対応地域の機密データ検出

| 地域 | 検出可能なデータタイプ |
|------|------------------------|
| **UAE** | ID番号、UID番号、ビザファイル番号、パスポート番号、運転免許証番号 |
| **ブラジル** | CPF（個人納税者番号）、パスポート番号、銀行カード番号、CNH（運転免許証）、CNPJ（法人番号） |
| **その他** | 各種国際標準（クレジットカード、SSNなど） |

---

## 6. 言語サポート

### 6.1 Coroコンソール

- English
- French (Canada) ← v3.7で追加

### 6.2 セキュリティ意識向上トレーニング（SAT）

- English (US) - 米国リージョンのみ
- English (UK)
- English (AUS) - 米国リージョンのみ
- Italian
- Spanish
- French (France)

---

## 7. 技術的特徴

### 7.1 アーキテクチャ

- **クラウドネイティブ**: SaaS型セキュリティプラットフォーム
- **マルチテナント**: MSP対応のワークスペース分離
- **API対応**: パブリックAPI提供（developers.coro.net）

### 7.2 統合機能

- **リモートシェル**: Windows、macOS、Linux対応
- **リモートアンインストール**: Windows Agent
- **自動ポリシー適用**: グループ、ラベルベース

---

*作成日: 2026-01-22*
*対象バージョン: v3.7, v3.8*
