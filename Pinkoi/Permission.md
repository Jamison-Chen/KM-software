# ER Diagram

```mermaid
erDiagram
    User }o--o{ Role: is_a
    Role }o--o{ Operation: has_permission_to
    User }o--o{ Operation: has_permission_to
    User |o--o| Role: supervise
    User |o--o| User: supervise
```

# 新增權限

### 法一：使用 Admin Tool

這是正規管道，適用於「符合規則」的授權，所謂的符合規則就是「User 只能為其下轄的 Users 或 Roles 加減權限」。

```mermaid
flowchart LR
id1(Admin Tool 側邊欄)
id2(Permission)
id3(User/Role)
id1 --> id2
id2 --> id3
```

### 法二：直接改資料庫

**Step1: 到 `rbac_permission` 加上一筆資料**

**Step2: 刷新 Cache**

執行 `/scripts/ruby/permission/refresh_permission.py`，記得後面要加上 `-u <uid>` option。