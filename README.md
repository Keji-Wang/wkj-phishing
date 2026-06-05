# Phishing Email Trainer

> 钓鱼邮件识别训练系统 | Interactive Phishing Email Awareness Training Tool

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/wjfthomas318-rgb/phishing-email-trainer?style=social)](https://github.com/wjfthomas318-rgb/phishing-email-trainer)

## 📖 项目简介

**钓鱼邮件找茬训练系统**是一个面向企业和个人的网络安全意识培训工具。通过模拟真实钓鱼邮件场景，让用户主动识别邮件中的风险点，建立对网络钓鱼攻击的敏感度和判断能力。

不同于传统的"听课式"培训，本系统采用"找茬"式互动训练：
- 用户阅读模拟邮件，主动发现可疑之处
- Hover 悬停探索，点击标记风险点
- 提交后查看结构化解读和正确做法
- 覆盖6大常见钓鱼场景，难度渐进

## ✨ 核心特性

- **🎯 互动式训练** - 用户主动探索发现风险点，而非被动观看
- **📧 真实邮件模拟** - 高度还原邮件客户端 UI，沉浸式体验
- **🎨 深色专业界面** - SOC 风格设计，专注培训内容
- **📊 结构化反馈** - 每个风险点配有详细解读和正确处理方式
- **🎓 6大场景覆盖** - 紧急施压、身份伪装、财务诱骗、快递通知、技术支持、数据泄露
- **💻 纯前端实现** - 单文件 HTML，无需后端，易于部署
- **🔧 数据驱动** - JSON 配置题目，轻松扩展内容

## 🚀 快速开始

### 在线使用

访问 [GitHub Pages](https://wjfthomas318-rgb.github.io/phishing-email-trainer/) 即可开始训练。

### 本地运行

```bash
# 克隆仓库
git clone https://github.com/wjfthomas318-rgb/phishing-email-trainer.git
cd phishing-email-trainer

# 使用任意 HTTP 服务器打开
python -m http.server 8000
# 或使用 Node.js
npx serve .

# 浏览器访问 http://localhost:8000
```

### Docker 部署

```bash
docker run -d -p 80:80 \
  -v $(pwd):/usr/share/nginx/html:ro \
  nginx:alpine
```

## 📁 项目结构

```
phishing-email-trainer/
├── index.html          # 单文件应用（HTML + CSS + JS）
├── logo.png            # 品牌 Logo
├── README.md           # 项目说明
├── LICENSE             # MIT 许可证
└── .gitignore          # Git 忽略配置
```

## 🎯 训练场景

| 场景 | 描述 | 难度 |
|------|------|------|
| ⚡ 紧急施压型 | 通过紧迫感迫使你降低警惕，仓促行动 | ⭐⭐⭐ |
| 👤 身份伪装型 | 冒充领导、同事或合作伙伴发送邮件 | ⭐⭐⭐⭐ |
| 💰 财务诱骗型 | 以退款、补贴、奖金等名义诱导提供财务信息 | ⭐⭐⭐ |
| 📦 快递通知型 | 伪装快递、物流通知诱导点击恶意链接 | ⭐⭐ |
| 🔧 技术支持型 | 伪装IT部门要求修改密码或安装软件 | ⭐⭐ |
| 🔐 数据泄露型 | 利用数据泄露恐慌诱导立即操作 | ⭐⭐⭐⭐ |

## 🛠️ 自定义内容

所有训练数据存储在 `index.html` 的 `EMAILS` 数组中。你可以：

1. 添加新邮件场景
2. 修改风险点配置
3. 调整难度评级
4. 扩展解读内容

### 数据结构示例

```javascript
{
  id: 'e001',
  scenario: 'urgency',        // 场景类型
  difficulty: 3,              // 难度 1-5
  title: '紧急密码重置通知',
  email: {
    subject: '邮件主题',
    from: { name: '发件人名', email: 'email@example.com' },
    body: `<p>邮件内容，<span class="risk-point" data-risk-id="r1">风险点文字</span></p>`
  },
  riskPoints: [
    {
      id: 'r1',
      label: '风险点标签',
      severity: 'high',
      explanation: '为什么危险',
      correctAction: '正确处理方式'
    }
  ]
}
```

## 🎨 界面预览

### 训练首页
用户选择训练场景，查看题目统计。

### 邮件练习
模拟真实邮件客户端界面，用户通过 hover 探索发现风险点。

### 结果反馈
展示得分、命中/遗漏风险点，以及每个风险点的详细解读。

## 📝 开发路线

- [ ] 支持用户自定义题库
- [ ] 练习进度本地存储
- [ ] 多语言支持（i18n）
- [ ] 移动端优化
- [ ] 管理后台界面
- [ ] 统计分析功能

## 🤝 贡献

欢迎贡献！你可以：

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

特别欢迎：
- 新的训练场景
- UI/UX 改进
- Bug 修复
- 文档完善

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源。

## 🙏 致谢

- 设计灵感来源于网络安全意识培训实践
- 感谢所有贡献者和使用者

---

⚠️ **免责声明**：本工具仅用于网络安全教育和培训目的。请勿用于任何非法活动。
