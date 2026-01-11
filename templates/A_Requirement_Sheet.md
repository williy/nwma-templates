# A. システム設計 要件定義シート (A-Sheet: Requirement & Policy)

本書は NWMA 2026 準拠の設計憲法であり、インフラストラクチャの自動執行（Enforcement）におけるポリシー識別子（A-No）を定義する。

## 1. 基本情報

システム存立の前提となる境界条件を定義する。

| A-No | 項目名 | 設計上の定義 | 記載例 | 設計判断メモ |
| --- | --- | --- | --- | --- |
| A-001 | システム識別名 | ポリシー適用スコープの特定 | 基幹業務データ基盤 |  |
| A-002 | 執行境界定義 | 制御リソースの物理・論理境界 | Google Cloud プロジェクト A, B |  |
| A-003 | ライフサイクル要件 | 技術選定および償却期間の基準 | 5年以上（LTS選定必須） |  |

## 2. インフラストラクチャ・プロトコル層の定義

**永続資産（Asset）、計算資源（Vessel）、制御平面（Control Plane）を分離し、各層に最適な保護プロトコルを適用する。**

| A-No | 項目名 | 技術定義（Enforcement Policy） | 実装・設定例 | 設計判断メモ |
| --- | --- | --- | --- | --- |
| A-101 | 永続資産（Asset） | 物理削除保護（Deletion Protection）の強制 | Cloud SQL, Cloud Storage |  |
| A-102 | 計算資源（Vessel） | ステートレス化（Stateless）と置換可能性 | GKE Nodes, Compute Engine |  |
| A-103 | 制御平面（Control） | 状態管理（State）および特権アクセスの隔離 | Cloud Storage (State), IAM |  |
|  | **設計者メモ** | **Asset、Vessel、Control Planeの論理境界が未定義のまま実装（B-Sheet）へ移行することを禁ずる。** |  |  |

## 3. サービスレベル目標（SLO）および自動執行要件

**抽象的な可用性要求を、監視・復旧制御が可能な SLI / SLO および自動執行フローへ変換・定義する。**

| A-No | 項目名 | サービスレベル指標（SLI） | 目標数値（SLO） | 自動執行プロトコル（例） |
| --- | --- | --- | --- | --- |
| A-201 | 可用性指標 | 正常レスポンス（HTTP 20x）率 | 99.9% 以上 | MIG / GKE オートヒーリング |
| A-202 | 性能指標 | レスポンス遅延（P95 Latency） | 500ms 以内 | Cloud Monitoring アラート |
| A-203 | 復旧指標 | 目標復旧時間（RTO） | 30分 以内 | 自動フェイルオーバー制御 |
|  | **設計者メモ** | **SLI / SLO が技術的に計測・執行不可能な状態での構築着手を禁ずる。数値なき要件は無効である。** |  |  |

## 4. セキュリティ・ガバナンス方針

ゾーン設計に基づき、アクセス制御および暗号化プロトコルを A-No に紐付け、後続の実装へ貫通させる。

| A-No | 項目名 | セキュリティ執行ポリシー | 実装例 | 設計判断メモ |
| --- | --- | --- | --- | --- |
| A-301 | 境界防御ポリシー | 同一性検証（Identity-Aware）アクセス | Identity-Aware Proxy (IAP) |  |
| A-302 | 暗号化ポリシー | 鍵管理サービス（KMS）による暗号化強制 | CMEK（顧客管理暗号鍵） |  |

> **Enforcement Key Notice**
> A-No は単なる識別子ではなく、B-Sheet における Terraform リソース名、タグ、および C-Sheet における自動検証項目を 1:1 で紐付けるための**ユニバーサル・マッピング・キー**である。

---

### GoLog v2026.01.11.19 (Technical Finalization)

```yaml
version: "2026.01.11.19"
status: "A-SHEET_TECHNICAL_LOCKED"

activity_log:
  - time: "20:30"
    action: "A_Requirement_Sheet.md の最終更新"
    detail: "工学的整合性の確保。抽象的表現を排除し、Asset/Vessel/Control および SLI/SLO 体系へ統一。"
    status: "MASTER_VERSION_LOCKED"

```
