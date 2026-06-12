---
name: visual-consistency-keeper
description: 視覺一致性 token 自動植入 Skill。給多張圖片 Prompt 時，自動加入相同 token（色 / 字 / 風格 reference）確保跨張一致。
---

# Visual Consistency Keeper

> 📂 讀取並執行 Skill：`visual-consistency-keeper`

## 觸發時機
- 學員生多張圖（輪播 / 系列）需保持一致

## 必鎖 5 個 Token
1. ratio
2. background color HEX
3. accent color HEX
4. title font + body font
5. style reference

## 變動 Token（每張不同）
- 標題文字
- 副標 / 內文文字
- 視覺元素描述

## 工作流程
1. 收學員的 N 個畫面描述
2. 從 05 視覺規範擷取必鎖 token
3. 為每張產 Prompt，固定 token 部分一字不差
4. 變動部分根據畫面內容客製

## 規則
- 固定 token 必須完全相同（不能用同義詞）
- 學員有 Soul Cast 時，用 Soul Cast ID 鎖角色
- 加 ⚠️ "Maintain exact same visual style"

## 載入回覆
"✅ Consistency Keeper 啟動。給我你要生幾張，每張的畫面描述。"