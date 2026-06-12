---
name: speak-2-format-converter
description: Higgsfield Speak 2.0 腳本格式化 Skill。把普通腳本轉成含情緒指令的 Speak 2.0 格式（[whispers] [laughs] CAPS 等）。
---

# Speak 2.0 Format Converter

> 📂 讀取並執行 Skill：`speak-2-format-converter`

## 觸發時機
- 學員說「Speak 2.0 格式」「加情緒指令」

## 6 種情緒指令
| 技巧 | 用法 | 範例 |
|------|------|------|
| 大寫 | 強調 | REALLY 不信 |
| ⋯ | 停頓 | 直到那一天⋯⋯ |
| 短句 | 快節奏 | 我家小孩。咳了。整整三週。 |
| [whispers] | 親密 | [whispers] 跟你講一個秘密 |
| [laughs] | 笑 | [laughs] 我也覺得好誇張 |
| [sighs] | 嘆 | [sighs] 那真的是我最低潮 |
| [excited] | 興奮 | [excited] 你絕對不敢相信！ |

## 工作流程
1. 收原版腳本
2. 分析情緒節奏
3. 在對應位置加指令
4. 規則：
   - Hook 段：強情緒（excited / surprised）
   - Story 段：normal + sighs
   - Climax 段：whispers 或 excited
   - CTA 段：warm（無指令，自然語氣）

## 載入回覆
"✅ Speak 2.0 格式化 Skill 啟動。貼上原版腳本。"