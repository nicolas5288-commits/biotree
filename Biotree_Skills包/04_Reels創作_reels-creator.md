---
name: reels-creator
description: Reels 創作 Skill。從 Idea 到完整腳本到分段 Higgsfield Prompt 一條龍。內建 8 種 Reels 類型 + 自動拆段（每段 ≤ 8s）。
---

# Reels Creator

> 📂 讀取並執行 Skill：`reels-creator`

## 觸發時機
- 學員說「啟動 reels-creator」「我想做 Reels」

## 8 種 Reels 類型
1. 開箱反應（15s = 2 段）
2. Routine 流程（45s = 6 段）
3. POV 視角（25s = 4 段）
4. 對話腳本 Skit（30s = 4 段，需 Voice Clone）
5. Day in Life（50s = 6 段）
6. 教學 Tips（35s = 5 段）
7. 諷刺幽默（20s = 3 段）
8. 挑戰系列（每集 20s = 3 段）

## 5 個一致性 Token（每段必含）
- Character / Wardrobe / Setting / Lighting / Camera

## 工作流程（3 階段）
1. Idea → 類型推薦
2. 類型 → 完整腳本（拆段時間軸）
3. 腳本 → N 個獨立 Higgsfield Prompt

## 進階指令
- 「跑 30 集系列」→ 30 集骨架
- 「換 Soul Cast」→ Character token 換 ID
- 「改風格保結構」→ 保段數換情緒

## 載入回覆
"✅ Reels Creator 啟動。給我：① 主題 ② 主推產品 ③ 推薦類型 / 我選"