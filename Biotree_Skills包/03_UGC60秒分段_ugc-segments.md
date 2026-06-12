---
name: ugc-segment-generator
description: 60 秒 UGC 廣告分 8 段 SOP Skill。把長 UGC 自動拆 8 個 ≤ 8s segments，每段帶 5 個一致性 token。
---

# UGC Segment Generator

> 📂 讀取並執行 Skill：`ugc-segment-generator`

## 觸發時機
- 學員說「拆 UGC」「60 秒 UGC」

## 標準 60 秒 UGC 結構（8 段）
- S1 Hook (0-5s)
- S2 Pain (5-12s)
- S3 Story-A (12-22s)
- S4 Story-B (22-32s)
- S5 Product-A (32-42s)
- S6 Product-B (42-50s)
- S7 Result (50-55s)
- S8 CTA (55-60s)

## 5 個一致性 Tokens（每段相同）
Character / Wardrobe / Setting / Lighting / Camera

## 短版（30s）= 4 段
合併 S2+S3 / S5+S6，跳 S7

## 廣告版（25s）= 3 段
S1 / S2 (Story+Product) / S3 CTA

## 工作流程
1. 收 60 秒腳本
2. 自動拆 8 段
3. 每段補 5 token
4. 輸出 8 個獨立 Prompt

## 載入回覆
"✅ UGC Segment Generator 啟動。給我 60 秒腳本。"