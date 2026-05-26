# 🕵️‍♂️ WeChat Article Scraper

> 微信公众号文章抓取工具 - 提取完整文章内容和懒加载图片

## 📖 简介

**WeChat Article Scraper** 是一款专门用于抓取微信公众号文章全文的 TRAE Skill。解决微信文章无法直接复制、带图片文章难以保存的痛点。

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 📰 全文提取 | 提取公众号文章的完整正文内容 |
| 🖼️ 图片处理 | 自动识别并提取 `data-src` 懒加载图片 |
| 📄 Markdown 输出 | 输出干净的 Markdown 格式 |
| 🔄 批量处理 | 支持多个文章链接批量抓取 |

## 🎯 使用场景

- **内容采集**：批量采集竞品公众号文章，做内容分析
- **离线阅读**：将文章保存为 Markdown，随时离线阅读
- **素材收集**：内容创作者收集素材和参考资料
- **文章摘要**：抓取后配合 AI 生成摘要和分析

## 🚀 快速开始

### 方式一：直接对话（推荐）

```
用户：帮我抓取这个微信公众号文章
      https://mp.weixin.qq.com/s/xxxxx

SOLO：自动调用 wechat_article_scraper skill
      生成 Python 脚本并执行
```

### 方式二：Python 脚本调用

```python
import requests
import re

def fetch_wechat(url):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
    }
    
    response = requests.get(url, headers=headers)
    html = response.text
    
    # 提取标题
    title = re.search(r'property="og:title" content="([^"]+)"', html)
    title = title.group(1) if title else "WeChat_Article"
    
    # 提取正文内容
    content = re.search(r'<div.*?id="js_content".*?>(.*?)</div>', html, re.DOTALL)
    if not content:
        return "Error: 无法提取内容"
    
    # 处理图片
    def replace_img(match):
        src = re.search(r'data-src=["\'](.*?)["\']', match.group(0))
        return f'\n\n![image]({src.group(1)})\n\n' if src else ''
    
    text = re.sub(r'<img[^>]+>', replace_img, content.group(1))
    text = re.sub(r'<br\s*/?>', '\n', text)
    text = re.sub(r'</p>', '\n\n', text)
    text = re.sub(r'<[^>]+>', '', text)
    
    lines = [l.strip() for l in text.split('\n') if l.strip()]
    return f"# {title}\n\n" + "\n\n".join(lines)

# 使用
result = fetch_wechat("https://mp.weixin.qq.com/s/xxxxx")
print(result)
```

## 📊 输出示例

**输入**：微信公众号文章链接

**输出**：
```markdown
# 文章标题

这是文章正文内容第一段...

![image](https://mmbiz.qpic.cn/mmbiz_png/...)

这是文章正文内容第二段...

![image](https://mmbiz.qpic.cn/mmbiz_png/...)
```

## ⚠️ 限制说明

| 限制 | 说明 |
|------|------|
| 🔒 认证文章 | 部分文章可能需要登录认证 |
| ⏰ 图片时效 | 图片可能有有效期限制 |
| 💰 付费内容 | 付费文章无法抓取 |

## 🔧 技术实现

```
提取流程：
┌─────────────┐
│  请求页面   │  User-Agent 伪装
└──────┬──────┘
       ▼
┌─────────────┐
│  解析 HTML  │  正则提取 js_content
└──────┬──────┘
       ▼
┌─────────────┐
│  处理图片   │  data-src → ![image](url)
└──────┬──────┘
       ▼
┌─────────────┐
│  清理标签   │  去除 HTML 标签
└──────┬──────┘
       ▼
┌─────────────┐
│  输出 MD    │  标准 Markdown 格式
└─────────────┘
```

## 🔗 Skill 链接

**GitHub 完整地址**：
- Skill 源码：https://github.com/fupengyu1/trae-skills-submission/blob/main/.trae/skills/wechat_article_scraper/SKILL.md
- 本地路径：`.trae/skills/wechat_article_scraper/SKILL.md`

## 📁 文件结构

```
wechat_article_scraper/
├── README.md      # 本文件
└── SKILL.md      # Skill 核心定义
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📜 许可证

MIT License

---

*使用 SOLO + TRAE 创作于 2025-05-26*
