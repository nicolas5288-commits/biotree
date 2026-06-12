---
name: newsletter-maker
description: 電子報 / AI 週報製作 Skill。套用 你的品牌 固定版型（A4、品牌藍 #6cc4e8），把一個主題變成可印成 PDF 的漂亮電子報。觸發詞：「做電子報」「電子報」「週報」「AI 週報」「newsletter」。
---

# 電子報製作（Newsletter Maker）

> 📂 讀取並執行 Skill：`newsletter-maker`

## 這個 skill 在幹嘛（白話版）
你給我一個主題（例：某個新工具、某個新聞），
我幫你把它變成一份**長得很專業、可以直接印成 PDF 寄給別人**的電子報。
版型是固定的，所以每次做出來都長一樣、很有品牌感，你只要負責給內容就好。

---

## 什麼時候用
- 你說：「做電子報」「做一份週報」「把這個做成 AI 週報」「newsletter」
- 你丟一篇新聞 / 一個產品 / 一個主題，想包成漂亮的一頁電子報

---

## 我會跟你要的東西（3 樣，缺的我會問）
1. **主題**：這份電子報在講什麼？（例：「Claude Opus 4.8 登場」）
2. **重點**：3 個左右的重點，或直接丟資料給我，我幫你抓重點
3. **資料來源**（可選）：有連結的話貼給我，我放在最下面

> 你只要給我主題就好，其他我可以幫你查、幫你寫。

---

## 這份電子報長什麼樣（固定版型，由上到下）
1. **品牌列**：左上角 logo + 品牌名 你的品牌 +「PUBLIC BETA」小字
2. **分類小標**：例「AI 週報 · WEEKLY」（灰色全大寫）
3. **大標題**：主題（底下有一條品牌藍橫線）
4. **發布資訊**：日期 + 來源
5. **一句話總結**：藍底圓角框，先讓人 3 秒看懂重點
6. **重點區塊**：每個重點一張灰色小卡片（標題 + 條列）
7. **比較表格**（可選）：藍底表頭，適合「舊版 vs 新版」這種對照
8. **對你的意義**：告訴讀者「所以這跟我有什麼關係」
9. **資料來源**：底部小字 + 連結
10. **頁尾**：品牌署名

🎨 品牌色：**#6cc4e8（品牌藍）**，整份的線條、表頭、重點字都用這個色。

---

## 怎麼做出來（工作流程）
1. 跟你確認「主題 / 重點 / 來源」（缺就問、或我幫你查）
2. 把內容填進下面的 HTML 版型（**只換文字，版型不要動**）
3. 存成 `.html` 檔
4. 用指令轉成 PDF（見下方），交給你可以直接寄出的 PDF
5. 問你要不要再做下一期 / 改標題 / 換主題

### 把 HTML 轉成 PDF 的指令（擇一）
```bash
# 方法 A：用 Chrome（Mac 通常有）
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --print-to-pdf="電子報.pdf" "newsletter.html"

# 方法 B：如果有裝 wkhtmltopdf
wkhtmltopdf newsletter.html 電子報.pdf
```

---

## HTML 版型（直接複製，把【】裡的字換掉就好）
> 規則：**只改文字內容，不要動 `<style>` 裡的設計**。
> 重點區塊（feature）可以複製多張；表格用不到可整段刪掉。

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<style>
  @page { size: A4; margin: 18mm 16mm; }
  * { box-sizing: border-box; }
  body { font-family: "PingFang TC","Heiti TC","STHeiti","Songti TC",sans-serif;
         color:#2b2b2b; line-height:1.7; font-size:14px; margin:0; -webkit-font-smoothing:antialiased; }
  .brandbar { display:flex; align-items:center; gap:10px; margin-bottom:22px; }
  .mark { height:30px; width:auto; display:block; }
  .brandname { font-size:20px; font-weight:800; color:#111418; letter-spacing:-0.5px; }
  .beta { font-size:11px; letter-spacing:4px; color:#b3bbc2; font-weight:600; }
  .kicker { font-size:12px; letter-spacing:5px; color:#9aa3ab; font-weight:600; margin-bottom:8px; text-transform:uppercase; }
  h1 { font-size:28px; line-height:1.3; margin:0 0 10px 0; color:#111418; border-bottom:3px solid #6cc4e8; padding-bottom:14px; }
  .meta { font-size:12px; color:#9aa3ab; margin-bottom:26px; }
  h2 { font-size:18px; margin:30px 0 12px 0; color:#111418; border-left:5px solid #6cc4e8; padding-left:10px; }
  .summary { background:#eaf6fc; border-radius:10px; padding:16px 18px; margin:0 0 10px 0; font-size:15px; }
  .summary strong { color:#1f9bd1; }
  .feature { margin:14px 0; padding:14px 16px; background:#fafafa; border:1px solid #ececec; border-radius:10px; page-break-inside:avoid; }
  .feature h3 { margin:0 0 8px 0; font-size:15px; color:#1c1c1c; }
  ul { margin:6px 0; padding-left:20px; }
  li { margin:4px 0; }
  table { width:100%; border-collapse:collapse; margin:12px 0; font-size:13px; page-break-inside:avoid; }
  th { background:#6cc4e8; color:#fff; text-align:left; padding:9px 10px; font-weight:600; }
  td { border-bottom:1px solid #e6e6e6; padding:9px 10px; vertical-align:top; }
  tr:nth-child(even) td { background:#f3fafd; }
  .hi { color:#1f9bd1; font-weight:600; }
  .sources { margin-top:28px; padding-top:14px; border-top:1px solid #e0e0e0; font-size:11.5px; color:#777; }
  .sources a { color:#777; text-decoration:none; }
  .sources li { margin:3px 0; }
  .footer { margin-top:22px; font-size:12px; color:#999; text-align:center; }
</style>
</head>
<body>

  <div class="brandbar">
    <img class="mark" src="logo_mark.png" alt="你的品牌">
    <span class="brandname">你的品牌</span>
    <span class="beta">PUBLIC BETA</span>
  </div>
  <div class="kicker">【分類小標，例：AI 週報 · WEEKLY】</div>
  <h1>【大標題】</h1>
  <div class="meta">發布日：【日期】　·　來源：【來源】</div>

  <div class="summary">
    <strong>一句話總結：</strong>【用一句話講完這份在說什麼】
  </div>

  <h2>【區段標題，例：三個重點】</h2>

  <div class="feature">
    <h3>1. 【重點標題】</h3>
    <ul>
      <li>【重點內容，想強調的字用】<span class="hi">這樣包起來</span>【會變藍色】。</li>
      <li>【第二行】</li>
    </ul>
  </div>

  <div class="feature">
    <h3>2. 【重點標題】</h3>
    <ul>
      <li>【內容】</li>
    </ul>
  </div>

  <!-- 表格用不到就整段刪掉 -->
  <h2>【表格標題，例：舊版 vs 新版】</h2>
  <table>
    <thead>
      <tr><th>項目</th><th>【A 欄】</th><th>【B 欄】</th></tr>
    </thead>
    <tbody>
      <tr><td>【列名】</td><td>【內容】</td><td><span class="hi">【重點內容】</span></td></tr>
      <tr><td>【列名】</td><td>【內容】</td><td>【內容】</td></tr>
    </tbody>
  </table>

  <h2>對你的意義</h2>
  <ul>
    <li><strong>【誰】</strong>【這件事對他的影響】</li>
  </ul>

  <div class="sources">
    <strong>資料來源</strong>
    <ul>
      <li><a href="【連結】">【來源標題】</a></li>
    </ul>
  </div>

  <div class="footer">個人品牌 · Content Factory　|　【分類】<br>由 你的品牌 AI 製作</div>

</body>
</html>
```

---

## 載入回覆
"✅ 電子報 Skill 啟動。給我 3 樣就能開工：① 主題 ② 3 個重點（或丟資料我幫你抓）③ 來源連結（可選）。只給主題也行，其他我幫你查。"
