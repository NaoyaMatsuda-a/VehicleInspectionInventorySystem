# Cloud Vehicle Maintenance Manager
車検予約 × 部品在庫管理システム  
(Java / Spring Boot / AWS / Terraform / Docker / CI/CD)

---

## 📌 Overview
自動車ディーラーの車検予約と、車検に必要な部品在庫を一元管理するクラウドアプリケーションです。  
前職で経験した「予約管理の煩雑さ」「部品不足による作業遅延」の課題を解決するために開発しました。

---

## 🎯 Purpose
- 車検予約、整備スケジュール、部品在庫をクラウドで統合管理
- 店長・整備士・スタッフ間の情報共有強化
- 在庫不足を事前にアラートし、業務効率を改善
- AWS × Java × Terraform × CI/CD の実務スキルを証明するためのポートフォリオ

---

## 🧩 Features (MVP)
### 🔹 1. ログイン（管理者 / スタッフ）
### 🔹 2. 車検予約管理
- 予約登録（顧客名 / 車種 / 日付 / 整備士）
- 予約一覧表示
- 状態管理（予約 / 完了 / キャンセル）

### 🔹 3. 部品在庫管理
- 部品登録 / 編集 / 削除
- 在庫数、しきい値表示
- 在庫不足アラート（しきい値以下を赤字表示）

### 🔹 4. 入庫・出庫操作
- 使用部品の減算（出庫）
- 仕入れ時の加算（入庫）
- 入出庫履歴の自動作成

### 🔹 5. 車検予約 × 必要部品の連動
- 車検に必要な部品リストを予約画面で表示
- 在庫不足の場合は警告

---

## 🟧 Additional Features (Optional)
- 入出庫履歴の検索・一覧表示
- スケジュールカレンダー表示
- 部品画像アップロード（S3）
- CSVエクスポート
- 管理者/スタッフの権限管理強化

---

## 🏗 Architecture

---

## 🗂 ER Diagram

```mermaid
erDiagram
  CUSTOMER {
    int id
    string name
    string phone
    string address
  }

  VEHICLE {
    int id
    int customer_id
    string model
    string plate_number
    date last_inspection_date
  }

  INSPECTION_RESERVATION {
    int id
    int vehicle_id
    date date
    string status
    string mechanic_name
  }

  PART {
    int id
    string part_number
    string part_name
    int stock_quantity
    int threshold
  }

  PART_USAGE {
    int id
    int reservation_id
    int part_id
    int used_quantity
  }

  CUSTOMER ||--o{ VEHICLE : owns
  VEHICLE ||--o{ INSPECTION_RESERVATION : has
  INSPECTION_RESERVATION ||--o{ PART_USAGE : uses
  PART ||--o{ PART_USAGE : is_used
