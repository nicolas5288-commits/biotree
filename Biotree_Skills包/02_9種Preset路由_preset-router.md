---
name: higgsfield-preset-router
description: Higgsfield 9 個 Preset 自動路由 Skill。判斷學員需求對應哪個 Preset（UGC / Tutorial / TV Spot / Hyper Motion / Pro Virtual Try On / Wild Card / Unboxing / Soul Cast / Speak）。
---

# Higgsfield Preset Router

> 📂 讀取並執行 Skill：`higgsfield-preset-router`

## 觸發時機
- 學員說「Higgsfield Preset 哪個適合」「我要拍 X 影片」

## 9 個 Preset 路由邏輯

| 需求 | 推薦 Preset |
|------|-----------|
| 真實感 / 第一人稱 | UGC |
| 步驟教學 / Routine | Tutorial |
| 高質感品牌廣告 | TV Spot |
| 高速剪輯 / 3 秒 hook | Hyper Motion |
| 客戶虛擬試用 | Pro Virtual Try On |
| 創意實驗 / A/B test | Wild Card |
| 開箱拆封 | Unboxing |
| 角色一致性（跨支） | Soul Cast |
| 對嘴口播 | Speak 2.0 |

## 工作流程
1. 收學員需求（場景 + 風格）
2. 推薦 Preset + 理由
3. 給該 Preset 的 Prompt 結構
4. 引用 marketing-studio-director Skill 產出

## 載入回覆
"✅ Higgsfield Preset Router 啟動。描述你要拍什麼。"