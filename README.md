# 复盘AI PWA - 部署指南

## 📱 这是什么？

一个可以安装到 iPhone 主屏幕的复盘 AI 应用，具备：
- 🎯 4种复盘框架（KPT/AAR/PDCA/4F）
- 💬 AI 引导式对话
- 📊 智能报告生成
- 📚 本地历史记录
- 📴 离线缓存支持

## 🚀 快速部署

### 方式一：Vercel（推荐，最简单）

1. 注册 [Vercel](https://vercel.com) 账号
2. 安装 Vercel CLI：`npm i -g vercel`
3. 在此目录运行：`vercel`
4. 按提示操作，几秒后获得在线地址

### 方式二：Netlify

1. 注册 [Netlify](https://netlify.com) 账号
2. 拖拽整个 `review-ai-pwa` 文件夹到 Netlify 控制台
3. 立即获得在线地址

### 方式三：GitHub Pages

1. 创建 GitHub 仓库
2. 上传所有文件
3. Settings → Pages → 选择分支 → Save
4. 获得 `https://你的用户名.github.io/仓库名` 地址

## 📲 安装到 iPhone

1. 用 Safari 打开你部署好的网址
2. 点击底部分享按钮 ⬆️
3. 选择「添加到主屏幕」
4. 点击「添加」

完成！现在主屏幕会出现「复盘AI」图标 🎉

## 🖼️ 生成图标

部署前需要将 `icon.svg` 转换为 PNG：

**在线工具（推荐）：**
1. 打开 https://cloudconvert.com/svg-to-png
2. 上传 `icon.svg`
3. 分别导出：
   - 192x192 → 保存为 `icon-192.png`
   - 512x512 → 保存为 `icon-512.png`
   - 180x180 → 保存为 `icon-180.png`

**或使用命令行：**
```bash
# 使用 ImageMagick
convert icon.svg -resize 192x192 icon-192.png
convert icon.svg -resize 512x512 icon-512.png
convert icon.svg -resize 180x180 icon-180.png
```

## 📁 文件结构

```
review-ai-pwa/
├── index.html      # 主应用
├── manifest.json   # PWA 配置
├── sw.js          # Service Worker（离线支持）
├── icon.svg       # 图标源文件
├── icon-192.png   # 图标（需生成）
├── icon-512.png   # 图标（需生成）
├── icon-180.png   # Apple Touch Icon（需生成）
└── README.md      # 本文件
```

## ⚙️ 自定义

### 修改 API Key（可选）

默认使用 Claude.ai 的内置 API。如果你想用自己的 API Key：

在 `index.html` 中找到 `fetch('https://api.anthropic.com/v1/messages'` 部分，添加：

```javascript
headers: { 
  'Content-Type': 'application/json',
  'x-api-key': '你的API_KEY',
  'anthropic-version': '2023-06-01'
},
```

### 修改主题颜色

在 `index.html` 的 `<style>` 中修改 `:root` 变量：

```css
:root {
  --accent: #e94560;        /* 主题色 */
  --accent-light: #ff6b6b;  /* 亮主题色 */
  --bg-primary: #1a1a2e;    /* 背景色 */
}
```

## 🤔 常见问题

**Q: 为什么 AI 响应失败？**
A: 需要网络连接。离线时只能查看历史记录。

**Q: 数据存在哪里？**
A: 本地浏览器存储（localStorage），不会上传到任何服务器。

**Q: 可以导出数据吗？**
A: 点击报告页面的「分享」按钮可以复制或分享报告内容。

---

有问题？随时问我！ 🙋
