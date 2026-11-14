# SUNXC 作业助手

[简体中文](#简体中文) | [English](#english)

---

## 简体中文

SUNXC 作业助手是一个**单文件、纯前端**的 AI 作业问答页面。它不依赖后端服务，所有模型配置保存在浏览器本地，支持 OpenAI Chat Completions、OpenAI Responses API 和 Anthropic Messages 三种接口格式，适合直接打开使用或部署到任意静态托管平台。

> 本项目定位为学习辅助工具：引导解题思路、分步讲解知识点，而不是直接给出可抄写的完整答案。

### 功能特性

- **单文件 HTML**：无构建步骤，下载后即可运行
- **多模型配置**：保存、切换、编辑、删除多个模型配置
- **三种 API 格式**：OpenAI Chat Completions / OpenAI Responses / Anthropic Messages
- **流式输出**：实时显示生成内容，支持中途停止
- **Markdown 渲染**：支持代码块、表格、列表、引用等
- **图片输入**：上传图片或 `Ctrl + V` 粘贴截图，支持多模态模型
- **主题切换**：浅色 / 深色模式，首次访问跟随系统
- **本地存储**：模型配置与主题保存在浏览器 `localStorage`
- **连通测试**：保存前可测试 API 是否可用
- **响应式布局**：适配桌面端与移动端
- **内置使用指南**：右上角 `?` 查看配置与快捷键说明

### 快速开始

1. 将项目 HTML 保存为 `index.html`
2. 可选：在同一目录放置 `logo.png` 作为站点图标；不需要可删除 `<link rel="icon" ...>` 一行
3. 直接用浏览器打开 `index.html`，或部署到静态托管平台
4. 点击右上角 **齿轮按钮**，填写 API 信息并保存
5. 在顶部下拉框选择模型
6. 输入题目，按 `Ctrl + Enter` 发送

### 模型配置说明

| 配置项 | 说明 |
| --- | --- |
| API 格式 | 根据服务商选择：大多数兼容 OpenAI 的服务选 **Chat Completions**；Claude 选 **Anthropic Messages**；使用 OpenAI Responses API 选 **Responses** |
| 请求地址 | API 基础 URL，**不要**带 `/chat/completions` 等接口后缀，系统会自动补全。例如 `https://api.deepseek.com/v1` |
| 模型 ID | 服务商规定的模型标识，例如 `deepseek-chat`、`gpt-4o-mini`、`claude-3-5-sonnet-20241022` |
| 模型展示名称 | 可选，留空则显示模型 ID |
| API 密钥 | 服务商提供的 Key，仅保存在当前浏览器本地 |
| Temperature | 0 更稳定，1 更发散，默认 `0.7` |
| System 提示词 | 决定 AI 的角色定位，默认已针对作业辅导场景优化 |

#### 配置示例

| 服务商 | API 格式 | 请求地址示例 | 模型 ID 示例 |
| --- | --- | --- | --- |
| DeepSeek | Chat Completions | `https://api.deepseek.com/v1` | `deepseek-chat` |
| OpenAI | Chat Completions / Responses | `https://api.openai.com/v1` | `gpt-4o-mini` |
| Anthropic | Anthropic Messages | `https://api.anthropic.com/v1` | `claude-3-5-sonnet-20241022` |

> 以上仅为示例，请以服务商最新文档为准。

### 快捷键

| 快捷键 | 功能 |
| --- | --- |
| `Ctrl + Enter` / `Cmd + Enter` | 发送消息 |
| `Enter` | 输入框内换行 |
| `Ctrl + V` / `Cmd + V` | 粘贴图片 |
| `Esc` | 关闭当前弹窗 |

### 文件结构

```text
.
├── index.html      # 主页面，单文件应用
└── logo.png        # 可选，站点图标
```

### 部署

本项目是纯静态页面，可部署到：

- GitHub Pages
- Cloudflare Pages
- Vercel / Netlify
- 任意 Nginx / Apache 静态目录
- 也可以直接在本地双击 `index.html` 打开

### 隐私与安全

- 本项目**没有后端服务器**，模型配置保存在浏览器 `localStorage` 中：
  - 模型列表：`homework_assistant_model_list`
  - 主题：`homework_assistant_theme`
- API 请求由浏览器**直接发往你配置的 API 服务商**，不会经过本项目服务器
- 请不要在公共设备上保存 API Key
- 建议使用额度受限的 API Key，并在服务商侧设置用量上限
- 页面末尾包含一段 Cloudflare Insights 统计脚本；如不需要，可删除对应的 `<script type="module" src="https://static.cloudflareinsights.com/...">` 标签

### 常见问题

**提示“网络请求失败 / CORS”？**  
浏览器直接请求第三方 API 时可能被跨域策略拦截。请使用支持 CORS 的服务商，或自建反向代理转发请求。

**提示 401 / 403？**  
通常是 API Key 不正确、已过期，或账号没有该模型权限。请检查密钥和额度。

**请求一直转圈？**  
可能是服务商响应较慢，或流式接口被中断。可点击停止按钮后重试，并确认请求地址格式正确。

**图片上传后模型不识别？**  
请确认所选模型支持视觉/多模态输入；不支持视觉的模型可能忽略图片。

**主题或配置没有保存？**  
浏览器可能禁用了 `localStorage`，或处于无痕模式。请使用普通窗口并允许本地存储。

### 定制开发

- 本项目无构建步骤，直接编辑 `index.html` 即可
- 修改默认 System 提示词：搜索 `DEFAULT_SYSTEM`
- 修改存储键名：搜索 `STORAGE_KEY`、`THEME_KEY`
- 修改主题色：编辑 `:root` 与 `html[data-theme="dark"]` 中的 CSS 变量
- 新增 API 格式：需要同步修改 `buildRequest`、`extractDelta` 和 `testConnect`

### 免责声明

AI 生成内容可能不准确或不完整，请自行判断并核对。请遵守所使用 API 服务商的条款，以及学校/机构关于作业与 AI 工具的规定。

### 许可证

- **代码**：建议采用 [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html)
- **文档与非代码内容**：建议采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.zh-hans)
- 如需商业使用授权，请联系作者

> 发布前请根据你的实际情况确认最终许可证，并确保你对项目中全部代码和内容拥有相应权利。

---

## English

SUNXC Homework Assistant is a **single-file, frontend-only** AI homework Q&A page. It requires no backend. All model configurations are stored locally in the browser. It supports three API formats: OpenAI Chat Completions, OpenAI Responses API, and Anthropic Messages. You can open it directly or deploy it to any static hosting platform.

> This project is intended as a learning aid: it guides problem-solving and explains concepts step by step, rather than providing complete answers to copy.

### Features

- **Single HTML file**: no build step, runs after download
- **Multiple model profiles**: save, switch, edit, and delete model configurations
- **Three API formats**: OpenAI Chat Completions / OpenAI Responses / Anthropic Messages
- **Streaming output**: real-time rendering with stop support
- **Markdown rendering**: code blocks, tables, lists, blockquotes, etc.
- **Image input**: upload images or paste screenshots with `Ctrl + V`, for multimodal models
- **Theme switching**: light / dark mode, follows system preference on first visit
- **Local storage**: model profiles and theme are saved in browser `localStorage`
- **Connection test**: test API connectivity before saving
- **Responsive layout**: works on desktop and mobile
- **Built-in guide**: click the `?` button for configuration and shortcut help

### Quick Start

1. Save the project HTML as `index.html`
2. Optional: place `logo.png` in the same directory as the favicon; otherwise remove the `<link rel="icon" ...>` line
3. Open `index.html` directly in a browser, or deploy it to static hosting
4. Click the **gear button** in the top-right corner, fill in the API details, and save
5. Select a model from the top dropdown
6. Enter your question and press `Ctrl + Enter` to send

### Model Configuration

| Field | Description |
| --- | --- |
| API Format | Choose based on your provider: most OpenAI-compatible services use **Chat Completions**; Claude uses **Anthropic Messages**; OpenAI Responses API uses **Responses** |
| Base URL | API base URL. **Do not** append `/chat/completions`; the app adds the endpoint automatically. Example: `https://api.deepseek.com/v1` |
| Model ID | Model identifier from your provider, e.g. `deepseek-chat`, `gpt-4o-mini`, `claude-3-5-sonnet-20241022` |
| Display Name | Optional. If empty, the model ID is shown |
| API Key | Provider key, stored only in the current browser |
| Temperature | `0` is more stable, `1` is more diverse. Default: `0.7` |
| System Prompt | Defines the AI role. The default is optimized for homework tutoring |

#### Configuration Examples

| Provider | API Format | Base URL Example | Model ID Example |
| --- | --- | --- | --- |
| DeepSeek | Chat Completions | `https://api.deepseek.com/v1` | `deepseek-chat` |
| OpenAI | Chat Completions / Responses | `https://api.openai.com/v1` | `gpt-4o-mini` |
| Anthropic | Anthropic Messages | `https://api.anthropic.com/v1` | `claude-3-5-sonnet-20241022` |

> Examples only. Always refer to the latest provider documentation.

### Keyboard Shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl + Enter` / `Cmd + Enter` | Send message |
| `Enter` | New line in the input box |
| `Ctrl + V` / `Cmd + V` | Paste image |
| `Esc` | Close the current modal |

### File Structure

```text
.
├── index.html      # Main page, single-file app
└── logo.png        # Optional favicon
```

### Deployment

This is a pure static page. You can deploy it to:

- GitHub Pages
- Cloudflare Pages
- Vercel / Netlify
- Any Nginx / Apache static directory
- Or simply open `index.html` locally

### Privacy and Security

- This project has **no backend server**. Model profiles are stored in browser `localStorage`:
  - Model list: `homework_assistant_model_list`
  - Theme: `homework_assistant_theme`
- API requests are sent **directly from the browser to the configured API provider**, not through this project's server
- Do not save API keys on public or shared devices
- Use restricted API keys and set usage limits on the provider side
- The page includes a Cloudflare Insights analytics script at the end. If you do not need it, remove the `<script type="module" src="https://static.cloudflareinsights.com/...">` tag

### FAQ

**“Network request failed / CORS”?**  
Browsers may block direct cross-origin requests to third-party APIs. Use a provider that supports CORS, or set up a reverse proxy.

**401 / 403?**  
Usually an invalid or expired API key, or the account lacks permission for the model. Check the key and quota.

**The request keeps loading?**  
The provider may be slow, or the streaming connection was interrupted. Stop and retry, and verify the base URL format.

**The model does not understand uploaded images?**  
Make sure the selected model supports vision/multimodal input. Text-only models may ignore images.

**Theme or configuration is not saved?**  
`localStorage` may be disabled, or you may be in private browsing mode. Use a normal window and allow local storage.

### Customization

- No build step. Edit `index.html` directly
- Change the default system prompt: search for `DEFAULT_SYSTEM`
- Change storage keys: search for `STORAGE_KEY` and `THEME_KEY`
- Change theme colors: edit CSS variables in `:root` and `html[data-theme="dark"]`
- Add a new API format: update `buildRequest`, `extractDelta`, and `testConnect`

### Disclaimer

AI-generated content may be inaccurate or incomplete. Please verify it yourself. Follow the terms of your API provider and your school/institution's policies on homework and AI tools.

### License

- **Code**: recommended [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html)
- **Documentation and non-code content**: recommended [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.en)
- For commercial licensing, please contact the author

> Before publishing, confirm the final license based on your actual situation and ensure you have the necessary rights to all code and content in the project.