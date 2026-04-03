# 本地文件差异对比工具 Local Diff Checker

纯前端浏览器端多格式内容差异对比工具，**所有文件解析、对比逻辑100%本地执行，不上传任何数据到服务器**，关闭页面后所有临时数据自动销毁，保障隐私安全。

## 功能特性

### 核心功能 ✅
- ✅ 支持多种对比精度：行级 / 单词级 / 字符级
- ✅ 支持两种视图模式：拆分视图（左右分栏）/ 统一视图（单栏合并）
- ✅ 实时编辑器，可编辑后立即重新对比
- ✅ 支持一键折叠所有未更改行，提升大文件可读性
- ✅ 支持换行显示控制，可关闭换行保持行号对齐
- ✅ 完整差异导航：转到第一个 / 上一个 / 下一个 / 最后一个差异，支持键盘快捷键 (Ctrl+↑/↓)
- ✅ 支持单行复制 / 全部复制结果
- ✅ 交换左右对比内容一键完成
- ✅ 完整差异统计：新增/删除/修改数量 + 总行数 + 无差异行数
- ✅ 纯本地多种导出格式：TXT报告 / HTML带格式报告
- ✅ 浅色/深色主题切换

### 格式支持
| 格式 | 状态 | 功能说明 |
|------|------|----------|
| 纯文本 | ✅ P0 | 支持三种对比精度，多种忽略规则 |
| JSON | ✅ P0 | 自动格式化、语法校验、支持忽略键顺序、忽略注释、语法高亮 |
| Excel | ✅ P0 | 支持 .xls/.xlsx，按工作表选择对比，单元格级对比 |
| Word | ✅ P1 | 支持 .docx，提取文本后对比 |
| PDF | ✅ P1 | 支持文本型PDF，提取文本后对比 |

### 忽略规则 ✅
- 忽略大小写
- 忽略空格/制表符
- 忽略空行
- 忽略换行符差异
- JSON专属：忽略键顺序差异、忽略JSON注释

## 使用方法

### 直接使用
直接用浏览器打开 `index.html` 文件即可使用，不需要任何服务器、不需要安装依赖。

### 本地部署（静态文件服务）
如果需要通过网络访问，可以使用任意静态文件服务器：

**方法1：Python 简单服务器**
```bash
cd local-diff-checker
python3 -m http.server 8000
```
然后访问 `http://你的服务器IP:8000/index.html`

**方法2：Node.js http-server**
```bash
npm install -g http-server
cd local-diff-checker
http-server -p 8000
```

## 技术栈
- 原生 HTML + CSS + JavaScript（无框架依赖）
- 第三方开源库（通过CDN引入）：
  - [diff](https://github.com/kpdecker/jsdiff) - 多精度文本差异对比
  - [SheetJS (xlsx)](https://sheetjs.com/) - Excel 文件解析
  - [mammoth](https://github.com/mwilliamson/mammoth.js) - Word 文件解析
  - [pdf.js](https://mozilla.github.io/pdf.js/) - PDF 文件解析
  - [JSON5](https://json5.org/) - 支持带注释的JSON解析
  - [highlight.js](https://highlightjs.org/) - 代码语法高亮
  - [file-saver](https://github.com/eligrey/FileSaver.js) - 本地文件保存

## 安全说明
- 无任何接口请求、无数据上报、无埋点
- 不读取本地无关文件，仅解析用户主动上传的文件
- 页面刷新/关闭后，所有解析数据立即释放
- 所有操作都在浏览器本地完成

## 性能说明
- 支持单文件大小最大 50MB
- 10MB 文件解析对比 ≤ 2秒
- 50MB 文件解析对比 ≤ 5秒
- 大文件异步处理，不会阻塞UI

## 已知限制
- ❌ 不支持加密PDF / 加密Office文件
- ❌ 不支持图片型扫描PDF（无OCR能力）
- ❌ 旧版 .doc Word 格式支持有限（优先使用 .docx）
- ❌ Word/PDF 不保留复杂格式，仅提取文本对比

## 快捷键
| 快捷键 | 功能 |
|--------|------|
| Ctrl + ↑ | 上一个差异 |
| Ctrl + ↓ | 下一个差异 |

## 项目部署
本项目为纯静态项目，可以部署到任何静态托管服务：
- GitHub Pages
- Cloudflare Pages
- Vercel
- Netlify
- 阿里云 OSS / 腾讯云 COS
