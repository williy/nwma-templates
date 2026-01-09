# NWMA Implementation Templates (A/B/C Sheets)

## 1. Overview
本リポジトリは、設計思想 **NWMA (Net Worth Management Architecture)** を具体化し、インフラ設計における「価値の保存」と「責任境界の分離」を証明するための実装テンプレート群です。

従来の「作業指示」としての設計書を廃し、要件(A)・構造(B)・試験(C)を一本の論理（Why）で繋ぐことで、IaC（Terraform / Ansible）による自動執行の正当性を担保します。



---

## 2. The Core Architecture: A/B/C Sheets
NWMAでは、設計を以下の3つの階層（Layer）で管理し、ドキュメント間での完全なトレーサビリティを実現します。

| Sheet | Role | Key Output / Target KPI |
| :--- | :--- | :--- |
| **A-Sheet (Requirement)** | 設計判断の根拠 (Why) の定義 | 投資対効果、リスク許容度の合意 |
| **B-Sheet (Architecture)** | 構造と責任境界 (Who/Where) の設計 | 可用性SLA、Google Cloud マネージド活用率 |
| **C-Sheet (Verification)** | 設計の正当性 (Proof) の証明 | 構成逸脱率の抑制、復旧時間(MTTR)の短縮 |

---

## 3. Implementation Stack
本テンプレートは、以下の技術スタックとの併用を前提に最適化されています。

* **Public Cloud**: Google Cloud (GKE Autopilot, Cloud Run, Cloud Spanner)
* **Infrastructure as Code**:
    * **Terraform**: 構造の固定化、および「クラウドベンダー責務」と「利用者責務」の境界線定義。
    * **Ansible**: 構成の状態維持（冪等性）および時間経過によるドリフト（状態逸脱）の抑制。

---

## 4. Why use NWMA Templates?
* **From "Hours" to "Value"**: 稼働時間ではなく、設計によってどれだけの「将来リスク（コスト）」を吸収したかをA-Sheetで可視化します。
* **Responsibility Isolation**: B-Sheetで責任の所在を明確に分離し、不条理な責任追及を排除する「設計の盾」として機能します。
* **Traceability**: 要件No（A-No）が各設計値・試験項目に紐付くため、AIによる自動レビューや監査への耐性が飛躍的に向上します。

---

## 5. Getting Started
1. `templates/` ディレクトリ内の各シート（Markdown/Excel形式）をダウンロードします。
2. インデックス記事 [「NWMAの地図」](https://zenn.dev/asurawill/articles/your-index-article-link) を参照し、設計思想の全体像を把握してください。
