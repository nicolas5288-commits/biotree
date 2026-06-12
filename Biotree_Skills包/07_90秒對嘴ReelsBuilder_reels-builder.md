---
name: reels-90s-builder
description: v11.1 核心 Skill — 真人錄音 + seedance_2_0 自動產 8/15/30/60/90 秒對嘴 Reels。學員只做 2 件事「講主題 + 唸錄音」，Skill 自動切段 + 並行生圖 + 對嘴 + ffmpeg 串接。所有 Reels / 限動對嘴影片都走這個流程。
---

# Reels 90s Builder · v11.1 核心對嘴工作流 ⭐⭐

> 📂 讀取並執行 Skill：`reels-90s-builder`

## 觸發時機

- 學員說「拍 Reels」「做對嘴影片」「對嘴限動」「90 秒影片」「30 秒影片」
- 學員給「主題 + 時長」要做敘事性影片
- 學員丟錄音檔到對話 + 講要做 Reels

## 核心鐵則（v11.1 實測修正）

```
✅ 主路線 = seedance_2_0（對嘴）+ nano_banana（start_image）+ 真人錄音
❌ 不用 Speak 2.0 / 聲音克隆（改真人直錄）

🚨 模型規格（對齊講義）：
- seedance_2_0：吃 start_image + audio 做對嘴 lipsync，單段建議 ≤15s
- start_image：nano_banana（情境人像）；需嵌中文字才改 gpt_image_2
- 想要電影感運鏡的純 B-roll 段落可用 kling3_0（無 audio role＝不能對嘴）

→ 單一指令的對嘴段上限 ~15s
→ 30/60/90 秒 = 切段並行 + ffmpeg 串接
```

## 學員體驗（只做 2 件事）

```
Step 1：講主題 + 時長
       「我要拍 60 秒 Reels，主題 X，類型 Y」
Step 2：手機錄音一次唸完整段，丟回對話
       完成
       
（剩下 Step 3-7 全部 Claude 自動執行，學員看結果）
```

## Claude 自動執行流程（Step 3-7）

### Step 3 · 寫腳本 + 切段

依時長切段：
- 8s → 1 段（單鏡頭）
- 15s → 1 段（單鏡頭）
- 30s → 2 段（每段 15s）
- 60s → 4 段（每段 15s）
- 90s → 6 段（每段 15s）
- 120s+ → 不建議（IG Reels 留人率衰退）

每段標明：
- 時長（秒）
- 台詞（對應錄音時段）
- 場景描述（每段不同場景，但同 Avatar / 同產品 / 同 cardigan）
- 情緒 tone（沉思 / 自信 / 溫柔 / 反差）
- 鏡頭描述（自拍中景 / 微距 / 遠景）

⚠️ 一致性鐵則：每段都用相同 Character / Wardrobe / Avatar reference。場景變、衣服不變。

### Step 4 · 切音檔（ffmpeg 自動）

```bash
# 假設原音檔 voice_v1.m4a 60 秒
ffmpeg -i voice_v1.m4a -ss 00:00 -t 15 -ar 44100 -ac 1 -b:a 128k seg1.mp3
ffmpeg -i voice_v1.m4a -ss 15 -t 15 -ar 44100 -ac 1 -b:a 128k seg2.mp3
ffmpeg -i voice_v1.m4a -ss 30 -t 15 -ar 44100 -ac 1 -b:a 128k seg3.mp3
ffmpeg -i voice_v1.m4a -ss 45 -t 15 -ar 44100 -ac 1 -b:a 128k seg4.mp3
```

⚠️ 切點要在「停頓處」不在「字中間」。Claude 寫腳本時就要對應切點設計。

### Step 5 · 並行產 N 個 start_image

```python
for i in 1..N:
  generate_image({
    model: "nano_banana",
    aspect_ratio: "9:16",
    medias: [
      {role: "image", value: M01_Avatar_job_id},
      {role: "image", value: 真實產品照_media_id}
    ],
    prompt: f"""[該段場景描述] + 50/50 拍攝感
    iPhone selfie aesthetic, FULL DEPTH OF FIELD, natural daylight,
    casual handheld. NOT cinematic, NOT studio.
    CRITICAL: face/cardigan/product IDENTICAL to references."""
  })
```

⚠️ rate limit 8 concurrent — N ≤ 8 才能完全並行；N > 8 分批送。

### Step 6 · 上傳 N 個音檔段 + 並行產 N 個 seedance_2_0 對嘴段

```python
# 上傳每段音檔
for seg_audio in [seg1.mp3, seg2.mp3, ...]:
  media_upload + curl PUT + media_confirm(type="audio")
  → 取得 audio_media_id

# 並行送 seedance_2_0
for i in 1..N:
  generate_video({
    model: "seedance_2_0",
    aspect_ratio: "9:16",
    duration: 15,
    medias: [
      {role: "start_image", value: 對應 start_image_job_id},
      {role: "audio", value: 對應 audio_media_id}
    ],
    prompt: f"""[該段情緒 + 動作描述]
    Lips move naturally in sync with audio.
    Slight handheld iPhone shake.
    CRITICAL: face/cardigan/product IDENTICAL to start_image."""
  })
```

### Step 7 · ffmpeg 串接 N 段 → 成片

```bash
# 建 concat list
echo "file 'seg1.mp4'\nfile 'seg2.mp4'\nfile 'seg3.mp4'\nfile 'seg4.mp4'" > concat.txt

# 串接（同編碼直接 copy 流，不重編碼）
ffmpeg -f concat -safe 0 -i concat.txt -c copy final.mp4

# 如不同解析度需要 re-encode
ffmpeg -f concat -safe 0 -i concat.txt -c:v libx264 -c:a aac final.mp4
```

直接顯示 final.mp4 在對話內。

## 預期成本（每支 Reels）

| 時長 | 段數 | start_image 成本 | seedance_2_0 成本 | 總計 (credit) | NTD |
|---|---|---|---|---|---|
| 8-15s | 1 | 8-12 | 30-45 | 40-60 | 60-100 |
| 30s | 2 | 16-24 | 60-90 | 80-115 | 120-180 |
| 60s | 4 | 32-48 | 120-180 | 150-230 | 230-350 |
| 90s | 6 | 48-72 | 180-270 | 230-340 | 350-510 |

## 限動對嘴版（同流程不同時長）

```
時長：5-8 秒
腳本：純金句（5-12 字）
比例：9:16
其他流程跟 Reels 完全一樣
```

## Bug 排查

| 症狀 | 原因 | 解法 |
|---|---|---|
| 嘴型嘟嘴誇張 | 該段台詞太長太密 | 重切短一點，加停頓 |
| 段間銜接斷裂 | 兩段 start_image 場景跳太遠 | 場景設計要循序漸進（廚房→走廊→梳妝桌） |
| 產品形狀變了 | medias reference 沒鎖好 | 重生該段，加強 CRITICAL 鎖一致 |
| ffmpeg concat fail | 段尺寸不同 | 用 re-encode 版本，不要 -c copy |
| Audio not found | 上傳時 .mp3 副檔名 ≠ 內容 | 真的轉 mp3（用 ffmpeg 不要 m4a 改名） |

## 載入回覆

"✅ Reels 90s Builder 啟動。

請給我：
1️⃣ 主題（例：「3 個月後皮膚有差」）
2️⃣ 時長（8 / 15 / 30 / 60 / 90 秒）
3️⃣ 類型（個人故事 / 客戶見證 / 反向觀點 / 產品教育 / 痛點共鳴）

我先幫你寫腳本 + 切段 + 給你「唸稿提示」。
你錄完音檔丟回對話，我自動跑完剩下 5 步驟。"
