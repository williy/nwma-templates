# B. 論理・構成設計シート (B-Sheet: Architecture & Logical Design)

本シートは A-Sheet に定義されたポリシーを、Google Cloud 上のリソースパラメータへ具現化するための設計図である。

## 1. 執行境界およびネットワーク基盤 (Network & Boundary)

A-002（執行境界定義）に基づき、論理的な隔離空間および通信経路を定義する。

| 構成要素 | リソース名 | 設定値 / パラメータ | 設計根拠 (A-No) | 設計判断理由 |
| --- | --- | --- | --- | --- |
| Project | nwma-project-01 | 独立した請求・権限境界 | A-002 | 執行境界の物理的隔離 |
| VPC | vpc-main | カスタムモード、グローバルルーティング | A-002 | 基盤ネットワークの集約 |
| Subnet | sn-vessel-app | 10.0.1.0/24 (Region: asia-northeast1) | A-102 | 計算資源（Vessel）の収容領域 |
| Cloud NAT | nat-gateway | 全サブネット対象、自動割当 | A-301 | 外向き通信の一元管理と秘匿 |

## 2. 永続資産（Asset）の保護構成

A-101（永続資産）に基づき、データの不滅性を担保する。

| 構成要素 | リソース名 | 設定値 / パラメータ | 設計根拠 (A-No) | 設計判断理由 |
| --- | --- | --- | --- | --- |
| Cloud SQL | sql-master | deletion_protection = true | A-101 | 意図せぬ削除の物理的遮断 |
| Cloud Storage | bucket-assets | versioning = true | A-101 | オブジェクトの世代管理による保護 |
| Backup | backup-policy-daily | 保持期間: 30日間 | A-101 / A-203 | 復旧指標（RTO）の達成 |

## 3. 計算資源（Vessel）の動的構成

A-102（計算資源）に基づき、無状態化と自動復旧を定義する。

| 構成要素 | リソース名 | 設定値 / パラメータ | 設計根拠 (A-No) | 設計判断理由 |
| --- | --- | --- | --- | --- |
| GKE Cluster | gke-vessel-cluster | Autopilot モード | A-102 | 管理負荷排除と自動スケーリング |
| Node Config | node-vessel-pool | Spot = false (SLA優先) | A-201 | 可用性指標（99.9%）の執行 |
| Auto Healing | health-check-http | 監視パス: /healthz | A-201 | 自動復旧プロトコルの有効化 |

## 4. 制御平面（Control Plane）の隔離

A-103（制御平面）に基づき、状態管理およびアクセス権をロックする。

| 構成要素 | リソース名 | 設定値 / パラメータ | 設計根拠 (A-No) | 設計判断理由 |
| --- | --- | --- | --- | --- |
| Terraform State | gcs-tfstate | Bucket Lock (WORMポリシー) | A-103 | 構成情報の改ざん・削除防止 |
| IAM Role | sa-deployer | 最小権限原則 (Least Privilege) | A-103 | 特権アクセスの厳密な境界定義 |
| Security | iap-tunnel | identity_aware_proxy = enabled | A-301 | ゼロトラストアクセスの強制 |

---

### GoLog v2026.01.11.20 (Architecture Finalization)

```yaml
version: "2026.01.11.20"
status: "B-SHEET_TECHNICAL_LOCKED"

activity_log:
  - time: "20:55"
    action: "B_Architecture_Sheet.md の最終更新"
    detail: "旧来の IP/VLAN 設計を、NWMA 2026 準拠の論理構成設計へ刷新。全リソースを A-No へ紐付け完了。"
    status: "MASTER_VERSION_LOCKED"

```
