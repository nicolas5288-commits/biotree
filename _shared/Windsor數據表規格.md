# Windsor.ai → Google Sheets 標準欄位規格（資料合約）

> 這是「Windsor 端怎麼設」與「skill 端怎麼讀」的共同合約。
> 客戶在 Windsor.ai 建立連接器時，**照這張表勾選欄位 + 命名分頁**，②⑥ skill 才抓得到。
> Windsor 設定路徑：Google Sheets → Extensions → Windsor.ai → Get Data into Sheet → 選 metrics/dimensions。

---

## 通用設定
- 一個 Google Sheets 檔案，內含 **2 個分頁（tab）**，名稱固定如下。
- 每天自動刷新（Windsor 排程），抓「過去 90 天」滾動區間。
- 第 1 列必須是欄位英文名（skill 靠欄名抓，不靠欄位順序）。

---

## 分頁 1：`ig_posts`（Reels / 貼文 — IG Insights 連接器，organic）

> ⭐ **全部選「每篇貼文 `media_` 層級」**（同一報表粒度 → 每列＝一篇貼文，標題與數字鎖死對齊，`media_reach` 是真‧每篇觸及）。欄名以 Windsor 官方 Instagram Insights 欄位字典為準。

| Windsor 欄位名 | 說明 | 用途 |
|---|---|---|
| `media_caption` | 文案 | hook / 主題分群（主力）|
| `media_type` | REEL / IMAGE / CAROUSEL_ALBUM | 分格式比較 |
| `timestamp` | 發佈時間 | 趨勢/時段 |
| `media_permalink` | 貼文連結 | 回查 |
| `media_reach` | 每篇觸及（私有★） | outlier 基準、互動率分母 |
| `media_views` | 觀看/播放（取代舊 `media_plays`）| 量能 |
| `media_like_count` | 讚 | 互動 |
| `media_comments_count` | 留言 | 互動 |
| `media_saved` | 儲存數（私有★） | 高權重訊號 |
| `media_shares` | 分享 | 互動 |
| `media_engagement` | 互動總和（讚+留言+儲存+分享）| 互動率分子 |
| `media_reel_total_interactions` | Reel 互動總數 | Reels 表現 |
| `media_reel_avg_watch_time` | Reel 平均觀看（毫秒）| Reels 完看訊號 |

> ⛔ **不要選**（會害資料亂掉 / 整欄空白）：`reach`、`likes`、`saves`、`shares`、`comments`（屬「帳號每日總和」，跟貼文對不齊）；`media_impressions`、`media_plays`、`story_impressions`、`carousel_album_impressions`、`clicks`（IG 已**棄用**）。觀看一律改用 `media_views`。
> 🔑 **逐則排行**：上面的 `media_` 欄位本身就是每篇層級，已可逐則排行；需要外接其他資料時再加 `media_id` 當鑰匙。

## 分頁 2：`meta_ads`（投放成效 — Facebook/Meta Ads 連接器）

> 欄位分四組，對齊 Windsor 官方 Meta Ads 分析 prompt + ⑥ 投放品質診斷。欄位名以 Windsor「Facebook/Meta Ads」清單為準，找不到挑語意最接近的。

**維度（拆解用）**
| 欄位名 | 說明 |
|---|---|
| `date` | 日期（趨勢/環比）|
| `campaign` / `adset_name` / `ad_name` | 三層歸戶（活動名是 `campaign`，不是 `campaign_name`）|
| `publisher_platform` | 平台（Facebook / Instagram）|
| `platform_position` | 版位（限動/動態/Reels…；舊寫 `placement` 不存在）|
| `age` / `gender` / `country` | 受眾拆解 |

**成效（核心）** — ⚠️ Facebook 把購買/轉換依事件拆名，泛稱（`purchases`/`purchase_roas`/`conversion_value`…）**都不存在**，要用下面 `*_omni_purchase` 這組（omni＝網站+App+線下合計，品牌投網站轉換的安全預設）
| 欄位名 | 說明 |
|---|---|
| `spend` | 花費（Amount Spent）|
| `purchase_roas_omni_purchase` | ROAS 廣告投報率 ★核心（舊寫 `purchase_roas` 不存在）|
| `actions_omni_purchase` | 購買數（舊寫 `purchases`/`conversions` 不存在）|
| `cost_per_action_type_omni_purchase` | 單次購買成本 CPP（舊寫 `cost_per_purchase` 不存在）|
| `action_values_omni_purchase` | 轉換金額（算營收；舊寫 `conversion_value` 不存在）|
| 轉換率 CVR | **自己算**＝購買÷點擊（無此單一欄位；`conversion_rate_ranking` 是高/中/低排名不是 %）|

**投放品質（Meta 官方三排名 → ⑥ 投放品質診斷主用）**
| 欄位名 | 說明 |
|---|---|
| `quality_ranking` | 品質排名（vs 同受眾競品）|
| `engagement_rate_ranking` | 互動率排名 |
| `conversion_rate_ranking` | 轉換率排名 |
> 三個都是 Above/Average/Below average 分級，**不是數字、不要硬算比率**，直接讀分級判素材好壞。

**效率**
| `impressions` / `reach` / `frequency` | 曝光 / 觸及 / 頻次（>3 疲勞）|
| `clicks` / `ctr` / `cpc` / `cpm` | 點擊 / 點擊率 / 單次點擊 / 千次曝光成本 |

**素材力**
| `video_thruplay_watched_actions_video_view` | 影片 ThruPlay（舊寫 `video_thruplay` 不存在）|
| `video_avg_time_watched_actions_video_view` | 平均觀看秒數（舊寫 `video_avg_play_time` 不存在）|
| `video_p100_watched_actions_video_view` | 看到 100%（完看，算疲勞曲線）|

★ = 只存在於後台、爬蟲抓不到的私有數據，這正是用 Windsor 的理由。
> 進階：要算素材疲勞曲線,就讓 `meta_ads` 帶 `ad_name` + `date`,看 top 素材的 CTR/CVR 隨時間衰退。

---

## skill 怎麼讀
1. 用 Google Drive MCP `search_files` 找到這個 Sheets 檔（檔名建議：`[客戶]_Windsor_數據`）。
2. `read_file_content` 讀對應分頁。
3. 依「欄位名」抓值（缺欄就跳過該指標，並提示客戶去 Windsor 補勾）。

## 🧨 踩坑筆記（2026/6/7 實戰）
1. **預設不用 `media id`**：為了讓客戶設定更順，預設走「主題分群 + 趨勢」模式。想要逐則數字才加 `media id`（進階）。
2. **口徑不一致要擋**：帳號級 reach 與互動混了 Reels/探索流量，會出現「shares > reach」這種物理不可能值。skill 偵測到 `互動 > 觸及` 或空值 → 標記異常、**不硬算比率**。
3. **混合列**：同一張表可能同時有「帳號每日彙總列（有數字無貼文資訊）」與「貼文列（有文案無數字）」。讀取時依「該列有沒有 caption/permalink」區分兩種列。
4. **主題分群勝過單則數字**：把 caption 依主題分群（情緒/畢業 vs 日常 vlog vs 乾貨）對照流量爆發期，就能得出可用結論——這是預設主力分析法。
