# Skein

**A single-file, local-first knowledge graph for a folder of Markdown notes.**

*[繁體中文說明見下方](#skein-繁體中文)*

Skein is one HTML file. Open it in a Chromium browser, point it at a folder, and it renders your `notes/*.md` — YAML frontmatter, `[[wikilinks]]` and all — as an interactive force-directed graph with faceted filtering, full-text search, inline editing, and a lint report for broken links. No install, no server, no account, no network.

The name is the metaphor: a skein is a loosely coiled length of yarn — many threads wound into one connected whole, which is what a linked set of notes becomes.

## Quick start

1. Download `skein.html`.
2. Open it in **Chrome or Edge** (see [Browser support](#browser-support)).
3. Click **Open folder** and pick a folder that contains a `notes/` subfolder of `.md` files.
4. Give the workspace a display name when prompted. Next time, one click on **Resume last** brings it straight back.

## Expected folder structure

```
my-wiki/
├── notes/
│   ├── some-note.md
│   ├── another-note.md
│   └── ...
├── index.md      (optional — any .md in the root shows under "Workspace files")
└── log.md        (optional)
```

Each note is Markdown with optional YAML frontmatter:

```markdown
---
id: some-note
title: A readable title
type: concept        # e.g. concept / project / meeting / reference
status: draft        # e.g. draft / review / final
domain: personal
tags: [example, getting-started]
related: [another-note]
revision: 3          # optional — nudges the node size on the graph
---

Body text. Link to other notes with [[another-note]].
Supports # headings, **bold**, `inline code`, and - lists.
```

Edges on the graph come from two sources: the `related:` list and any `[[wikilink]]` in the body. The `type` field drives node color; the facet panel filters by `type`, `status`, `domain`, and `tags`.

## Features

- **Workspaces** — save any number of folders under custom names; switch, rename, or forget them from the Workspaces menu. Resuming your last workspace is always one click.
- **Graph** — pan, wheel-zoom, drag nodes, click to highlight a note and its neighbors. The physics simulation cools down and stops when the layout settles (and pauses in background tabs), so it doesn't burn CPU.
- **View / Edit / Lint** — read a rendered note with its backlinks, edit the raw Markdown in place (with an unsaved-changes guard), and run a lint report: filename/id mismatches, broken wikilinks, duplicate ids, orphan notes, missing fields.
- **Persistent preferences** — theme, panel widths, and collapsed panels survive restarts.
- Keyboard: `/` focuses search, `Esc` clears the selection.

## Security model

Read this before trusting the tool with anything sensitive.

- **Local only.** There is no server and no telemetry. The page makes zero network requests, and a Content-Security-Policy with `connect-src 'none'` is baked in — so even injected code could not send data anywhere.
- **Read-only by default.** Folders open with read permission. Write permission is requested only the first time you save or create a note, via the browser's own permission prompt.
- **Escaped rendering.** All note content is HTML-escaped (including quotes) before display; no `eval`, no dynamic script loading, no third-party code.
- **Honest limits.** The code is short enough to audit yourself, but it has not been through a formal penetration test. Don't use it as the sole container for highly sensitive data.

Workspace shortcuts (folder handles) are stored in your browser profile via IndexedDB. Anyone with access to your browser profile could re-request access to those folders — the browser will still show a permission prompt, but keep this in mind on shared machines.

## Browser support

Skein uses the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API), which is available in Chromium-based browsers (Chrome, Edge, Brave, Arc). **Firefox and Safari are not supported.** The first open of any folder always requires a manual pick — browsers intentionally never let a page scan your disk without a prompt.

## Known limitations

- The YAML parser is minimal by design: scalars, `[a, b]` arrays, `- item` arrays, and one level of inline `{key: value}` objects. Nested mappings and multiline strings are not supported.
- Markdown rendering covers headings, bold, inline code, lists, and wikilinks — it is a viewer, not a full CommonMark engine.
- Notes are read from `notes/` only (not recursively).
- Interface language is currently **English**.

## License

[MIT](LICENSE)

---

<a name="skein-繁體中文"></a>

# Skein（繁體中文）

**單一檔案、本機優先的 Markdown 筆記知識圖譜工具。**

Skein 就是一個 HTML 檔案。用 Chromium 系瀏覽器開啟後，指向一個資料夾，它會讀取其中的 `notes/*.md`，解析 YAML frontmatter 與 `[[wikilink]]` 關聯，把整個筆記庫畫成一張可互動的力導向圖，並附帶分面篩選、全文搜尋、就地編輯，以及檢查斷連結的 Lint 報告。不需安裝、沒有伺服器、不用註冊帳號、完全不連網。

名稱取自比喻：skein 是一綹鬆繞的紗線——許多條線纏繞成一個相連的整體，這正是一組彼此連結的筆記所形成的樣子。

## 快速開始

1. 下載 `skein.html`。
2. 用 **Chrome 或 Edge** 開啟（見下方[瀏覽器支援](#瀏覽器支援)）。
3. 按「**Open folder**」選一個內含 `notes/` 子資料夾（放 `.md` 檔）的資料夾。
4. 系統會請你為這個工作區取一個顯示名稱。之後只要按一下「**Resume last**」就能直接回到上次的工作區。

## 預期的資料夾結構

```
my-wiki/
├── notes/
│   ├── some-note.md
│   ├── another-note.md
│   └── ...
├── index.md      （選用——根目錄下任何 .md 會列在「Workspace files」）
└── log.md        （選用）
```

每則筆記是 Markdown，YAML frontmatter 為選用：

```markdown
---
id: some-note
title: 可讀的標題
type: concept        # 例如 concept / project / meeting / reference
status: draft        # 例如 draft / review / final
domain: personal
tags: [example, getting-started]
related: [another-note]
revision: 3          # 選用——會微調節點在圖上的大小
---

正文。用 [[another-note]] 連結到其他筆記。
支援 # 標題、**粗體**、`行內程式碼`，以及 - 清單。
```

圖上的連線來自兩個來源：`related:` 清單，以及正文中的任何 `[[wikilink]]`。`type` 欄位決定節點顏色；左側分面面板可依 `type`、`status`、`domain`、`tags` 篩選。

## 功能

- **工作區（Workspaces）**——可用自訂名稱儲存任意多個資料夾；從 Workspaces 選單切換、重新命名或移除。回到上次的工作區永遠只要一次點擊。
- **圖譜**——可平移、滾輪縮放、拖曳節點、點擊以高亮某筆記及其鄰居。物理模擬會在版面穩定後自動冷卻停止（背景分頁時暫停），不會持續佔用 CPU。
- **檢視 / 編輯 / Lint**——閱讀渲染後的筆記與其反向連結、就地編輯原始 Markdown（有未存檔警告），並執行 Lint 報告：檔名與 id 不符、斷掉的 wikilink、重複 id、孤兒筆記、缺漏欄位。
- **偏好持久化**——主題、面板寬度、面板收合狀態關掉再開都會記得。
- 鍵盤：`/` 聚焦搜尋框，`Esc` 清除選取。

## 安全模型

在把重要資料交給這個工具之前，請先讀這一段。

- **純本機。** 沒有伺服器、沒有遙測。頁面不發出任何網路請求，並內建了含 `connect-src 'none'` 的 Content-Security-Policy——所以即使發生程式碼注入，也無法把資料傳送到任何地方。
- **預設唯讀。** 開啟資料夾時只請求讀取權限。只有在你第一次存檔或新增筆記時，才會透過瀏覽器本身的權限提示請求寫入權限。
- **轉義渲染。** 所有筆記內容在顯示前都經過 HTML 轉義（含引號）；不使用 `eval`、不動態載入腳本、不含任何第三方程式碼。
- **誠實的限制。** 程式碼短到你可以自行審查，但它未經過正式的滲透測試。請勿把它當作高度敏感資料的唯一存放容器。

工作區捷徑（資料夾 handle）透過 IndexedDB 存在你的瀏覽器 profile 中。任何能操作你瀏覽器的人都可能重新請求存取這些資料夾——瀏覽器仍會顯示權限提示，但在共用電腦上請留意這一點。

## 瀏覽器支援

Skein 使用 [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API)，僅 Chromium 系瀏覽器支援（Chrome、Edge、Brave、Arc）。**不支援 Firefox 與 Safari。** 每次首度開啟資料夾都必須手動選取——瀏覽器刻意不允許網頁在沒有提示的情況下掃描你的磁碟。

## 已知限制

- YAML 解析器刻意保持精簡：純量、`[a, b]` 陣列、`- item` 陣列，以及一層行內 `{key: value}` 物件。不支援巢狀對應與多行字串。
- Markdown 渲染涵蓋標題、粗體、行內程式碼、清單與 wikilink——它是檢視器，不是完整的 CommonMark 引擎。
- 只讀取 `notes/` 下的筆記（不遞迴子資料夾）。
- 介面語言目前為**英文**。

## 授權

[MIT](LICENSE)
