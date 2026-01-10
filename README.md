# NWMA Templates: IT資産価値管理方式 (Net Worth Management Architecture)

> **「SLAを自動執行しない設計は未完成である」**

NWMAは、効率化の代償として失われた設計の「判断」と「意味」を取り戻し、ITシステムを負債ではなく「資産」として維持するための設計憲法です。

## 1. 原典（Manifesto）

最新の思想定義とSLA自動執行の理論については、公式サイトを参照してください。

👉 [NWMA公式サイト：SLA自動執行による設計の主権回復](https://juicyltd.biz/nwma-manifesto/)

---

## 2. 統治構造と階層定義

NWMAは、以下の 3 つのレイヤーによってシステムの健全性を自律的に維持します。

* **NWMA (The Constitution / 憲法)**

  全体を貫く設計基準。要件（A）・構造（B）・試験（C）をセットで記録し、10年先でも「なぜこの形なのか」を誰もが理解できる資産価値を確立します。

* **IWMA (The Vessel / 器)**

  インフラ基盤。Terraform 等を用い、製品の寿命やクラウドベンダーの変遷に左右されない「器」の境界と責任を定義します。

* **PWMA (The State / 状態)**

  プラットフォーム。Ansible 等を用い、設計時の意志を 24 時間強制執行。構成ドリフトを根絶し、何度でも「正しい状態」を再現します。

---

## 3. 永続化の原則：データの聖域化

NWMAは「器（OS/MW）」と「資産（データ）」を物理的・論理的に切り離す「**論理的ブレードサーバ革命**」を推進します。

* **器は使い捨て:** 

  異常検知時には自動的に再デプロイされ、常に新品の状態へ回帰します。

* **データは聖域:** 

  データベースやストレージは執行対象外として保護。器が何度壊れても、資産は一瞬たりとも失われません。

これにより、バックアップ対象を「純粋なデータ層」のみに絞り込み、SLA（復旧時間）の数学的保証を実現します。

---

## 4. The Triplets: A/B/C Sheets

設計を 3 つの階層で管理し、完全なトレーサビリティを実現します。

| Sheet | Role | Output / Target |
| --- | --- | --- |
| **A-Sheet (Requirement)** | 設計判断の根拠 (Why) | 投資対効果、SLA/SLOの定義 |
| **B-Sheet (Structure)** | 構造の正本 (How) | IaC (Terraform / Ansible), 責任境界 |
| **C-Sheet (Verification)** | 設計の正当性 (Proof) | 自動検証スクリプト, 構成逸脱率の抑制 |

---

## 5. Directory Structure

管理手法によって場所を分けることで、実務における迷いを排除します。

```text
nwma-templates/
├── manifesto/              # NWMAの神様定義ファイル（core_philosophy.yaml）
├── A-Sheets/               # 要件定義テンプレート（Whyの保存）
├── B-Sheets/               # 構造の正本（Howの自動執行）
│   ├── IWMA/               # インフラ基盤（Terraform / 手順書）
│   └── PWMA/               # プラットフォーム（Ansible / K8s）
├── C-Sheets/               # 検証スクリプト（Proofの自動証明）
├── examples/               # 構築事例（K3s on Ubuntu 等）
└── templates/              # 各種設計書の雛形資産

```

---

## 6. Why NWMA?

* **Responsibility Isolation:** B-Sheetで責任の所在を明確にし、不条理な責任追及を排除する「設計の盾」となります。
* **SLA Auto-Execution:** 監視メトリクスと連動し、異常時に「PWMAリロード → IWMA再構築」を自動執行します。
* **AI-Ready:** 全ての設計判断が構造化（YAML）されているため、AIによる設計監査や保守との親和性が極めて高い構造です。

---

## 7. Links & Resources

* **解説記事**: [「NWMAの地図」- Zenn](https://zenn.dev/asurawill/articles/d17d9407671e41)
* **Author**: Hitoshi K. (Platform Architect)
