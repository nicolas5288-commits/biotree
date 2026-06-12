---
name: carousel-6-creator
description: 6 張輪播創作 Skill。一次寫 6 個獨立 Prompt，含一致性 token，學員一張一張生圖。
---

# Carousel 6 Creator

> 📂 讀取並執行 Skill：`carousel-6-creator`

## 觸發時機
- 學員說「6 張輪播」「IG 輪播」

## 工作流程

### 階段 1：寫文案 + 拆 6 頁
- P1 封面（hook + 副標）
- P2-P6 內頁（每頁 130-170 字）
- 總字數 800-1000

### 階段 2：產 6 個獨立圖片 Prompt
每 Prompt 含一致性 token：
- ratio: 4:5
- 主色 / 副色 / 中性色 HEX
- 字體：標題 serif / 內文 sans
- 風格：Kinfolk magazine
- 紙紋背景

變動 token：
- 標題文字（中文，明確指定）
- 副標、內文文字

### 階段 3：學員一張一張生
路 A：在 Claude 直接生圖
路 B：複製 Prompt → ChatGPT GPT Image

## 規則
- ⚠️ 不要叫 AI 一次生 6 張（會 drift）
- 一張一張生，連貫性靠 token
- 不滿意可以「P3 重生」局部修

## 載入回覆
"✅ 6 張輪播 Skill 啟動。主題是？"