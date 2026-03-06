# 无用软件100系列 - 技术规范

## 一、核心约束

### 1. 运行环境
- **目标**: 微信/Telegram 内置浏览器
- **限制**: 不支持 JavaScript 或支持极差
- **方案**: 纯 HTML + CSS 实现交互

### 2. 交互方式
- ✅ 可用: radio button + label 跳转
- ✅ 可用: CSS :checked 伪类控制显示/隐藏
- ❌ 不可用: JavaScript onclick/addEventListener
- ❌ 不可用: fetch/XMLHttpRequest

---

## 二、计分方案

### 纯CSS计分（当前方案）

**原理**: 用 radio 记录每道题的选择，最后几道题的组合决定结果

**实现方式**:
```
Q1 → Q2 → Q3 → Q4 → Q5 → Q6(结果)
```

每道题的选项跳转到下一题，最后一题的选项直接跳转到不同结果卡片。

**优点**: 不需要JS，完全兼容  
**缺点**: 只能综合最后2-3题，更早的题目无法精确计入

### 示例结构
```html
<!-- 题目radio -->
<input type="radio" name="q1" id="q1a">
<input type="radio" name="q1" id="q1b">

<!-- 结果radio -->
<input type="radio" name="result" id="r-s">
<input type="radio" name="result" id="r-a">

<!-- CSS控制显示 -->
#q4a:checked ~ #q5a:checked ~ #q6a:checked ~ .container #r-s { display: block; }
```

---

## 三、页面结构

### 1. 首页 (index.html)
- 展示所有App卡片
- 2列网格布局
- 点击卡片进入具体测试

### 2. 测试页 (apps/xxx.html)
- 返回链接
- 进度条 (6个点)
- 题目卡片 (每次显示1个)
- 结果卡片 (根据选择显示)

### 3. 题目设计
- 6道题最佳 (太多CSS写不完)
- 每题4个选项 (A/B/C/D)
- 选项带分值提示 (+3/+2/+1/0)

---

## 四、部署

### GitHub Pages 结构
```
Bobby-Bot-00/bobby-bot-00.github.io (首页)
  └── index.html → 入口页

Bobby-Bot-00/useless-apps (App列表)
  └── index.html → App卡片列表
  └── apps/dan-nan.html → 脱单测试
  └── apps/xxx.html → 下一个测试
```

### 访问地址
- 首页: https://bobby-bot-00.github.io/
- App列表: https://bobby-bot-00.github.io/useless-apps/
- 具体App: https://bobby-bot-00.github.io/useless-apps/apps/xxx.html

---

## 五、开发流程

1. **本地开发**: 在 Mac 上写 HTML
2. **推送**: git push 到 GitHub
3. **等待**: 1-2分钟构建
4. **测试**: 手机打开链接测试

---

## 六、注意事项

1. **先在手机测试** - Telegram/微信浏览器兼容性最差
2. **CSS选择器** - 用 ~ 相邻兄弟选择器
3. **结果组合** - 只需写高频组合，不用覆盖所有
4. **文件命名** - 英文/拼音，不用中文

---

## 七、后续优化方向（可选）

如果需要精确计分:
- 方案A: 部署 Zeabur 后端 + MiniMax API
- 方案B: 用 Cloudflare Workers (免费)
- 方案C: 预生成所有组合 (适合题目少的测试)

---

*最后更新: 2026-03-06*
