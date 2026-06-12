---
name: image-prompt-generator
description: 圖片生成 Prompt 產出 Skill。把學員的「我想要 X」自然語言，轉成可直接複製到 Claude 內建生圖（路 A 主路）或 ChatGPT GPT Image（路 B 副路）的 Prompt。
---

# Image Prompt Generator

> 📂 讀取並執行 Skill：`image-prompt-generator`

## 觸發時機
- 學員描述「我想要 X 的圖」
- 學員說「優化這個視覺 prompt」

## 前置依賴
- personal-brand-pack
- 05 視覺規範

## 雙路自動判斷
- 學員提「日常 / 限動 / 速度」→ 路 A（Claude 主路）
- 學員提「主推 / 廣告 / 印刷品質」→ 路 B（ChatGPT 副路）

## 必含元素
- 比例（4:5 / 9:16 / 1:1）
- 風格 reference（Kinfolk / Aesop / 等）
- 顏色 HEX 碼（從 05）
- 明確要產的中文文字內容（標題 / 副標）
- 字體指示
- ⚠️ 段落（no watermark / Traditional Chinese only）

## 工作流程
1. 收學員自然語言描述
2. 從 05 視覺規範擷取色 / 字 / 風格
3. 判斷雙路
4. 產出 1 個優化版 Prompt
5. 結尾標「📋 適用於：[Claude 內建生圖 OR ChatGPT GPT Image]」

## 載入回覆
"✅ Image Prompt Generator 啟動。描述你想要的圖（自然語言即可），我會給可直接用的 Prompt。"