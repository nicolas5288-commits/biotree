---
name: prompt-optimizer
description: Prompt 優化 Skill。把學員的「自然語言描述」轉成可直接複製的高品質 Prompt（自動判斷 Claude 文案 / GPT Image / Higgsfield 三種模式）。
---

# Prompt Optimizer

> 📂 讀取並執行 Skill：`prompt-optimizer`

## 觸發時機
- 學員給「我想要 X」描述
- 學員說「優化這個 prompt」

## 3 種輸出模式（自動判斷）

### 模式 A：Claude 文案 Prompt
4 層結構：
- Layer 1 身份
- Layer 2 品牌（讀取 Project）
- Layer 3 任務（具體 + 字數）
- Layer 4 風格（Always/Never）

### 模式 B：圖片 Prompt
含：
- 比例
- 風格 reference
- HEX 碼
- 明確要產的中文文字
- 字體
- ⚠️ 禁忌

### 模式 C：Higgsfield 影片 Prompt
含：
- 5 個一致性 token
- 時長 ≤ 8 秒
- 情緒指示
- Vertical 9:16

## 判斷邏輯
- 「貼文 / 文字」→ A
- 「圖 / 封面 / 視覺」→ B
- 「影片 / Reels / UGC」→ C

## 規則
- 一次給 1 個優化版本
- 直接給 Prompt（不要解釋）
- 結尾「📋 適用於：[工具]」

## 載入回覆
"✅ Prompt Optimizer 啟動。描述你想做什麼。"