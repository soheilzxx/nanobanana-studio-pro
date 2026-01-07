# 🍌 NanoBanana Studio Pro

<div align="center">

![Version](https://img.shields.io/badge/version-3.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Cloudflare](https://img.shields.io/badge/cloudflare-workers-orange.svg)

**專業級 AI 圖像創作工作室 | 一鍵部署到 Cloudflare Workers**

[🚀 立即部署](#-快速部署) · [✨ 功能特性](#-核心功能) · [📖 使用文檔](#-使用指南) · [🎨 演示](#-功能演示)

</div>

---

## 🌟 項目簡介

NanoBanana Studio Pro 是一個基於 Cloudflare Workers 的專業 AI 圖像生成平台，提供多種創作模式和風格選擇，讓 AI 藝術創作變得簡單而強大。

### 💡 為什麼選擇 NanoBanana Studio Pro？

- 🎨 **14+ 藝術風格** - 從吉卜力到賽博朋克，應有盡有
- 🖼️ **多創作模式** - 文生圖、圖生圖、圖生手辦、吉卜力專屬
- 📐 **靈活比例** - 支持 6 種常用圖像比例
- 🔢 **批量生成** - 一次生成最多 4 張圖片
- 🚀 **零成本部署** - Cloudflare Workers 免費額度完全夠用
- 🎯 **IP 偽裝技術** - 內置智能重試機制，突破限制
- 💾 **智能歷史** - 自動保存創作記錄，支持批量下載
- 🌐 **OpenAI 兼容** - 完全兼容 OpenAI API 格式

---

## ✨ 核心功能

### 🎭 創作模式

| 模式 | 說明 | 適用場景 |
|------|------|----------|
| 📝 **文生圖** | 純文字描述生成圖像 | 從零開始創作 |
| 🌸 **吉卜力專屬** | 宮崎駿風格一鍵生成 | 動畫風格插畫 |
| 🖼️ **圖生圖** | 保持構圖轉換風格 | 風格遷移、重繪 |
| 🎎 **圖生手辦** | 角色圖轉 3D 手辦 | 模型收藏品設計 |

### 🎨 風格庫（14種）

<table>
<tr>
<td><strong>動漫系</strong></td>
<td>🌸 吉卜力 · ⭐ 動漫 · 😊 表情包</td>
</tr>
<tr>
<td><strong>3D 系</strong></td>
<td>🧸 3D可愛 · 🎬 皮克斯</td>
</tr>
<tr>
<td><strong>卡通系</strong></td>
<td>🏰 迪士尼</td>
</tr>
<tr>
<td><strong>藝術系</strong></td>
<td>🖼️ 油畫 · 🎨 水彩</td>
</tr>
<tr>
<td><strong>數字系</strong></td>
<td>🎮 像素風 · 🤖 賽博朋克 · 🌈 蒸汽波</td>
</tr>
<tr>
<td><strong>攝影系</strong></td>
<td>📷 寫實 · 📸 拍立得</td>
</tr>
</table>

### 📐 圖像比例

- ⬜ **1:1** 正方形（社交媒體）
- 🖥️ **16:9** 橫屏（桌面壁紙）
- 📱 **9:16** 豎屏（手機壁紙）
- 📺 **4:3** 標準（演示文稿）
- 📄 **3:4** 豎版（海報設計）
- 🎬 **21:9** 超寬（電影感）

---

## 🚀 快速部署

### 方法一：一鍵部署（推薦）

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/kinai9661/nanobanana-studio-pro)

**步驟：**

1. 點擊上方按鈕
2. 登入 Cloudflare 賬戶
3. 授權 GitHub 訪問
4. 等待自動部署完成
5. 獲取你的專屬域名 🎉

### 方法二：手動部署

```bash
# 1. 克隆倉庫
git clone https://github.com/kinai9661/nanobanana-studio-pro.git
cd nanobanana-studio-pro

# 2. 安裝 Wrangler CLI
npm install -g wrangler

# 3. 登入 Cloudflare
wrangler login

# 4. 部署
wrangler deploy
```

### 配置 API 密鑰（可選）

部署後，建議在 Cloudflare Workers 控制台設置環境變量：

```
變量名: API_MASTER_KEY
變量值: your-custom-secret-key
```

---

## 📖 使用指南

### Web UI 使用

1. **訪問你的 Worker 域名**，打開工作室界面
2. **選擇創作模式**：文生圖 / 吉卜力 / 圖生圖 / 圖生手辦
3. **輸入提示詞**，描述你想要的圖像
4. **選擇風格和比例**
5. **設置生成數量**（1-4張）
6. **點擊生成**，等待 AI 創作完成
7. **查看結果**，下載或複用提示詞

### API 調用

#### 文生圖 API

```bash
curl -X POST https://your-worker.workers.dev/v1/images/generations \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer YOUR_API_KEY" \\
  -d '{
    "prompt": "a cute cat sitting on the moon",
    "n": 2,
    "size": "1024x1024",
    "style": 9,
    "mode": "text-to-image"
  }'
```

#### Chat Completions API（兼容 OpenAI）

```bash
curl -X POST https://your-worker.workers.dev/v1/chat/completions \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer YOUR_API_KEY" \\
  -d '{
    "model": "nano-banana-v1",
    "messages": [
      {"role": "user", "content": "Generate an image of a sunset over the ocean"}
    ],
    "stream": false
  }'
```

#### 圖生圖 API

```bash
curl -X POST https://your-worker.workers.dev/v1/images/generations \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer YOUR_API_KEY" \\
  -d '{
    "prompt": "convert to Studio Ghibli style",
    "image": "data:image/jpeg;base64,/9j/4AAQSkZJRg...",
    "mode": "image-to-image",
    "style": 9
  }'
```

### 參數說明

| 參數 | 類型 | 說明 | 可選值 |
|------|------|------|--------|
| `prompt` | string | 提示詞描述 | 任意文字 |
| `n` | number | 生成數量 | 1-4 |
| `size` | string | 圖像尺寸 | `1024x1024`, `1792x1024`, `1024x1792`, `1536x1152`, `1152x1536`, `2048x878` |
| `style` | number | 風格 ID | 0-19（見風格列表）|
| `mode` | string | 創作模式 | `text-to-image`, `image-to-image`, `image-to-figure`, `ghibli-special` |
| `image` | string | 源圖像（Base64）| 僅圖生圖模式需要 |

---

## 🎨 功能演示

### 吉卜力風格生成

**提示詞：** `一個小女孩騎著掃帚飛過城市上空`

**效果：** 自動應用宮崎駿手繪動畫風格

### 圖生手辦

**輸入：** 動漫角色立繪

**輸出：** 3D 手辦效果圖

### 批量生成

一次性生成 4 張不同角度或變體，輕鬆選擇最佳結果

---

## 🛠️ 技術特性

### 🔐 IP 偽裝與突破

- **隨機 IP 生成**：每次請求生成隨機住宅 IP
- **多頭注入**：`X-Forwarded-For`, `X-Real-IP`, `Client-IP` 等
- **32位指紋**：模擬真實瀏覽器特徵
- **智能重試**：遇到限制自動切換身份（最多3次）

### 📦 項目結構

```
nanobanana-studio-pro/
├── worker.js          # 主程序（包含 UI 和 API）
├── wrangler.toml      # Cloudflare 配置
├── README.md          # 說明文檔
├── README_CN.md       # 簡體中文文檔
├── README_EN.md       # 英文文檔
└── LICENSE            # MIT 協議
```

### 🌐 API 兼容性

完全兼容 OpenAI API 格式，可直接替換：

```javascript
// 原 OpenAI 調用
const openai = new OpenAI({
  apiKey: "your-key",
  baseURL: "https://api.openai.com/v1"
});

// 替換為 NanoBanana
const openai = new OpenAI({
  apiKey: "your-worker-key",
  baseURL: "https://your-worker.workers.dev/v1"
});
```

---

## 📊 性能與限制

### Cloudflare Workers 免費額度

- **請求數**：每天 100,000 次
- **CPU 時間**：每請求 10ms（通常只用 2-3ms）
- **內存**：128MB
- **存儲**：無限（通過 KV）

### 生成速度

- **首次請求**：~15-30 秒
- **後續請求**：~10-20 秒
- **批量生成**：每張額外 +3-5 秒

---

## 🤝 貢獻指南

歡迎提交 Issue 和 Pull Request！

### 開發環境

```bash
# 安裝依賴
npm install

# 本地開發
wrangler dev

# 運行測試
npm test
```

### 提交規範

- `feat`: 新功能
- `fix`: 修復 Bug
- `docs`: 文檔更新
- `style`: UI/樣式改進
- `refactor`: 代碼重構

---

## 📝 更新日誌

### v3.0.0 (2025-12-01)

#### 🎉 重大更新

- ✨ 新增吉卜力風格專屬生成器
- 🎎 新增圖生手辦功能
- 🖼️ 新增圖生圖功能
- ✏️ 新增圖像編輯功能
- 🔢 支持批量生成（1-4張）
- 🎨 擴展至 14 種風格
- 📐 新增 6 種圖像比例
- 💾 智能歷史記錄系統
- 🎯 全新現代化 UI 設計

### v2.0.0 (2025-11-30)

- 🎨 現代化 UI 設計
- 📱 響應式佈局
- 💾 歷史記錄功能

### v1.0.0 (2025-11-26)

- 🚀 初始版本發布
- 🔐 IP 偽裝機制
- 🔁 智能重試系統

---

## 📄 開源協議

本項目採用 [MIT License](./LICENSE) 開源協議。

---

## 🙏 致謝

- [Cloudflare Workers](https://workers.cloudflare.com/) - 提供強大的邊緣計算平台
- [NanoBanana AI](https://nanobananaai.org/) - 上游 AI 圖像生成服務
- 所有貢獻者和用戶的支持 ❤️

---

## 📞 聯繫方式

- **GitHub Issues**: [提交問題](https://github.com/kinai9661/nanobanana-studio-pro/issues)
- **GitHub Discussions**: [參與討論](https://github.com/kinai9661/nanobanana-studio-pro/discussions)
- **作者**: [@kinai9661](https://github.com/kinai9661)

---

<div align="center">

**如果這個項目對你有幫助，請給個 ⭐ Star 支持一下！**

Made with ❤️ by [kinai9661](https://github.com/kinai9661)

</div>