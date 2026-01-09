# NWMA Implementation Templates (A/B/C Sheets)

## 1. Overview
本リポジトリは、設計思想 **NWMA (Next-gen Worth Management Architecture)** を具体化し、インフラ設計における「価値の保存」と「責任境界の分離」を証明するための実装テンプレート群です。

従来の「作業指示」としての設計書を廃し、要件(A)・構造(B)・試験(C)を一本の論理（Why）で繋ぐことで、IaC（Terraform / Ansible）による自動執行の正当性を担保します。

---

## 2. NWMA Architecture Model
インフラ全体の自律性を高めるため、以下の3つのサブ概念で構成を管理します。

* **NWMA (Next-gen Worth Management Architecture)**: 全体の統治思想。要件(A)・構造(B)・試験(C)の論理整合性を担保。
* **IWMA (Infrastructure Worth Management Architecture)**: 基盤層の管理。クラウドはTerraform、オンプレは手順書で「器」を定義。
* **PWMA (Platform Worth Management Architecture)**: プラットフォーム層の管理。SSH接続可能な全リソースをAnsibleで一元管理。

---

## 3. The Core Architecture: A/B/C Sheets
設計を3つの階層で管理し、ドキュメント間での完全なトレーサビリティを実現します。

| Sheet | Role | Key Output / Target KPI |
| :--- | :--- | :--- |
| **A-Sheet (Requirement)** | 設計判断の根拠 (Why) の定義 | 投資対効果、リスク許容度の合意 |
| **B-Sheet (Architecture)** | 構造と責任境界 (Who/Where) の設計 | 可用性SLA、Google Cloud マネージド活用率 |
| **C-Sheet (Verification)** | 設計の正当性 (Proof) の証明 | 構成逸脱率の抑制、復旧時間(MTTR)の短縮 |

---

## 4. Directory Structure
管理手法（Terraform / Ansible / 手順書）によって場所を分けることで、実務における迷いを排除します。

```text
nwma-templates/
├── docs/                 # NWMA共通の思想・ガイドライン
├── IWMA/                 # 基盤構成（Infrastructure）
│   ├── cloud/            # Terraformによる管理
│   └── on-premise/       # 手順書ベースの管理（VMware等）
└── PWMA/                 # 構成管理（Platform）
    └── ansible/          # SSH接続によるOS・ミドルウェア設定
```

---

## 5. Implementation Stack
NWMAは特定の技術に依存しませんが、以下のスタックとの併用で最大の効果を発揮します。

* **Public Cloud**: Google Cloud (GKE Autopilot, Cloud Run, Cloud Spanner) / Microsoft Azure
* **Infrastructure as Code**:
    * **Terraform (IWMA)**: 基盤の「器」の固定化。クラウドベンダー責務と利用者責務の境界定義。
    * **Ansible (PWMA)**: OS・ミドルウェアの状態維持。SSH接続可能な全リソースの構成ドリフト抑制。
* **Virtualization**: VMware vSphere / vSAN / NSX-T (HCI基盤)

---

## 6. Why NWMA?
* **From "Hours" to "Value"**: 単なる構築時間ではなく、設計によってどれだけの将来リスクを吸収したかをA-Sheetで可視化します。
* **Responsibility Isolation**: B-Sheetで責任の所在（ベンダー/自社/チーム）を明確にし、不透明な責任追及を排除する「設計の盾」となります。
* **AI-Ready Traceability**: 要件No（A-No）が試験項目まで紐付くため、生成AIによる設計監査や、自動ドキュメント生成との親和性が極めて高い構造です。

---

## 7. Getting Started
1. **ガイドラインの確認**: `docs/` 内のドキュメントでNWMAの基本思想を理解します。
2. **シートの活用**: 
   - 基盤構築（クラウド/オンプレ）なら `IWMA/` 内のテンプレートを選択。
   - OS・ミドルウェア設定なら `PWMA/` 内のテンプレートを選択。
3. **事例の参照**: `examples/` 内にある「K3s on Ubuntu」の実装事例を参考に、要件から試験までの繋がりを確認してください。

---

## 8. Links & Resources
* **連載記事**: [「NWMAの地図」- Zenn](https://zenn.dev/asurawill/articles/your-index-article-link)
* **Author**: Hitoshi K. (Platform Architect)
