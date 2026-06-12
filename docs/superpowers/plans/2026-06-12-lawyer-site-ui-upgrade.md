# 律师网站UI升级实现计划

> **面向 AI 代理的工作者：** 必需子技能：使用 superpowers:subagent-driven-development（推荐）或 superpowers:executing-plans 逐任务实现此计划。步骤使用复选框（`- [ ]`）语法来跟踪进度。

**目标：** 将律师个人宣传网站从深海军蓝配色升级为黑白+金色现代简约风格，添加视差滚动、微交互动画和文字动画效果

**架构：** 单文件HTML结构保持不变，修改内嵌CSS变量和样式，添加JavaScript动画逻辑

**技术栈：** HTML5, CSS3 (CSS Variables, Transitions, Animations), Vanilla JavaScript (IntersectionObserver, requestAnimationFrame)

---

## 文件结构

- 修改：`lawyer-site/index.html` - 唯一需要修改的文件，包含所有样式和脚本

---

### 任务 1：更新CSS变量和基础配色

**文件：**
- 修改：`lawyer-site/index.html:11-14` (CSS变量定义)

- [ ] **步骤 1：更新CSS变量**

将 `:root` 中的配色变量从深海军蓝改为黑白+金色方案：

```css
:root{
    --black:#000000;
    --dark:#1a1a1a;
    --white:#ffffff;
    --light:#f8f8f8;
    --gold:#c9a96e;
    --gold2:#dbb978;
    --text:#333333;
    --gray:#666666;
}
```

- [ ] **步骤 2：验证变量已更新**

在浏览器中打开 `lawyer-site/index.html`，检查页面配色已变为黑白基调。

- [ ] **步骤 3：Commit**

```bash
cd lawyer-site
git add index.html
git commit -m "style: update color scheme to black-white-gold"
```

---

### 任务 2：更新导航栏样式

**文件：**
- 修改：`lawyer-site/index.html:33-46` (导航栏CSS)

- [ ] **步骤 1：更新导航栏样式**

```css
nav{
    position:fixed;
    top:0;
    width:100%;
    z-index:100;
    transition:all .4s;
    padding:0 8%;
    height:68px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}
nav.scrolled{
    background:rgba(0,0,0,.97);
    backdrop-filter:blur(12px);
    box-shadow:0 1px 30px rgba(0,0,0,.15);
    height:60px;
}
.logo-text{
    font-family:'Noto Serif SC',serif;
    font-size:18px;
    font-weight:700;
    color:#fff;
    letter-spacing:3px;
}
.logo-text span{
    color:var(--gold);
}
nav ul li a{
    color:rgba(255,255,255,.75);
    text-decoration:none;
    font-size:13px;
    font-weight:400;
    letter-spacing:1px;
    transition:.3s;
    position:relative;
}
nav ul li a::after{
    content:"";
    position:absolute;
    bottom:-4px;
    left:0;
    width:0;
    height:1.5px;
    background:linear-gradient(to right, var(--gold), var(--gold2));
    transition:.3s;
}
nav ul li a:hover{
    color:#fff;
}
nav ul li a:hover::after{
    width:100%;
}
```

- [ ] **步骤 2：验证导航栏效果**

刷新页面，滚动页面检查导航栏背景变为纯黑半透明，悬停链接时有金色渐变下划线动画。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "style: update navbar with black background and gold hover effect"
```

---

### 任务 3：更新Hero区域样式

**文件：**
- 修改：`lawyer-site/index.html:49-73` (Hero区域CSS)

- [ ] **步骤 1：更新Hero区域基础样式**

```css
.hero{
    min-height:100vh;
    position:relative;
    display:flex;
    align-items:center;
    justify-content:center;
    overflow:hidden;
    background:var(--black);
}
.hero-bg{
    position:absolute;
    inset:0;
}
.hero-bg img{
    width:100%;
    height:100%;
    object-fit:cover;
    opacity:.15;
    filter:blur(1px);
    will-change:transform;
}
.hero-overlay{
    position:absolute;
    inset:0;
    background:linear-gradient(180deg,rgba(0,0,0,.85) 0%,rgba(0,0,0,.95) 60%,var(--black) 100%);
}
```

- [ ] **步骤 2：更新Hero内容样式**

```css
.hero-content{
    position:relative;
    z-index:2;
    text-align:center;
    max-width:760px;
    padding:0 20px;
}
.hero-badge{
    display:inline-flex;
    align-items:center;
    gap:8px;
    padding:8px 24px;
    border:1px solid rgba(201,169,110,.3);
    border-radius:100px;
    margin-bottom:32px;
    background:rgba(201,169,110,.08);
}
.hero-badge span{
    font-size:12px;
    color:var(--gold);
    letter-spacing:4px;
    font-weight:500;
}
.hero h1{
    font-family:'Noto Serif SC',serif;
    font-size:clamp(42px,7vw,68px);
    font-weight:900;
    color:#fff;
    letter-spacing:8px;
    margin-bottom:20px;
    line-height:1.2;
}
.hero h1 em{
    font-style:normal;
    color:var(--gold);
}
.hero .sub{
    font-size:clamp(15px,2.2vw,18px);
    color:rgba(255,255,255,.55);
    font-weight:300;
    letter-spacing:3px;
    margin-bottom:16px;
}
.hero .desc{
    font-size:clamp(13px,1.6vw,15px);
    color:rgba(255,255,255,.35);
    max-width:520px;
    margin:0 auto 48px;
    line-height:1.9;
}
```

- [ ] **步骤 3：更新按钮样式**

```css
.btn{
    display:inline-flex;
    align-items:center;
    gap:8px;
    padding:14px 40px;
    font-size:14px;
    font-weight:600;
    letter-spacing:2px;
    text-decoration:none;
    border-radius:4px;
    transition:.3s;
    border:none;
    cursor:pointer;
    font-family:inherit;
    position:relative;
    overflow:hidden;
}
.btn-gold{
    background:linear-gradient(135deg, var(--gold), var(--gold2));
    color:var(--black);
}
.btn-gold:hover{
    background:linear-gradient(135deg, var(--gold2), var(--gold));
    transform:translateY(-2px);
    box-shadow:0 8px 30px rgba(201,169,110,.25);
}
.btn-ghost{
    background:transparent;
    color:#fff;
    border:1px solid rgba(255,255,255,.2);
}
.btn-ghost:hover{
    border-color:var(--gold);
    color:var(--gold);
}
```

- [ ] **步骤 4：验证Hero区域效果**

刷新页面，检查Hero区域背景为纯黑，按钮有金色渐变效果。

- [ ] **步骤 5：Commit**

```bash
git add index.html
git commit -m "style: update hero section with black background and gold gradient buttons"
```

---

### 任务 4：更新关于我区域样式

**文件：**
- 修改：`lawyer-site/index.html:84-99` (关于我区域CSS)

- [ ] **步骤 1：更新关于我区域样式**

```css
.about{
    background:var(--light);
    padding:140px 8%;
}
.about-grid{
    max-width:1100px;
    margin:0 auto;
    display:grid;
    grid-template-columns:420px 1fr;
    gap:80px;
    align-items:center;
}
.about-photo-wrap{
    position:relative;
}
.about-photo{
    width:100%;
    aspect-ratio:3/4;
    background:linear-gradient(160deg,var(--dark),var(--black));
    border-radius:6px;
    overflow:hidden;
    position:relative;
    box-shadow:0 20px 60px rgba(0,0,0,.15);
}
.about-photo img{
    width:100%;
    height:100%;
    object-fit:cover;
}
.about-photo-overlay{
    position:absolute;
    inset:0;
    background:linear-gradient(to top,rgba(0,0,0,.6),transparent 40%);
}
.about-deco{
    position:absolute;
    top:-16px;
    right:-16px;
    bottom:16px;
    left:16px;
    border:2px solid var(--gold);
    border-radius:6px;
    z-index:-1;
    opacity:.3;
}
.about-info h3{
    font-family:'Noto Serif SC',serif;
    font-size:24px;
    color:var(--black);
    margin-bottom:24px;
    letter-spacing:2px;
}
.about-info p{
    margin-bottom:18px;
    color:#555;
    font-size:16px;
    line-height:1.9;
}
.about-info p.intro{
    font-size:17px;
    color:#333;
    font-weight:500;
    border-left:3px solid var(--gold);
    padding-left:16px;
}
.about-stats{
    display:flex;
    gap:48px;
    margin-top:36px;
    padding-top:36px;
    border-top:1px solid #e5e3df;
}
.stat-item .num{
    font-family:'Noto Serif SC',serif;
    font-size:42px;
    font-weight:900;
    background:linear-gradient(135deg, var(--gold), var(--gold2));
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    display:block;
    line-height:1;
}
.stat-item .label{
    font-size:13px;
    color:var(--gray);
    margin-top:6px;
}
```

- [ ] **步骤 2：验证关于我区域效果**

刷新页面，检查统计数字有金色渐变效果，照片区域有精致阴影。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "style: update about section with gold gradient stats and photo shadow"
```

---

### 任务 5：更新专业领域卡片样式

**文件：**
- 修改：`lawyer-site/index.html:102-110` (专业领域卡片CSS)

- [ ] **步骤 1：更新卡片样式**

```css
.areas-grid{
    max-width:1100px;
    margin:0 auto;
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:24px;
}
.area-card{
    background:#fff;
    border:1px solid #eee;
    border-radius:8px;
    padding:44px 32px;
    transition:.4s;
    position:relative;
    overflow:hidden;
}
.area-card::before{
    content:"";
    position:absolute;
    top:0;
    left:0;
    right:0;
    height:3px;
    background:linear-gradient(to right, var(--gold), var(--gold2));
    transform:scaleX(0);
    transform-origin:left;
    transition:.4s;
}
.area-card:hover{
    border-color:transparent;
    transform:translateY(-6px);
    box-shadow:0 20px 60px rgba(0,0,0,.08);
}
.area-card:hover::before{
    transform:scaleX(1);
}
.area-icon{
    width:56px;
    height:56px;
    background:linear-gradient(135deg,var(--black),var(--dark));
    border-radius:12px;
    display:flex;
    align-items:center;
    justify-content:center;
    margin-bottom:24px;
}
.area-icon svg{
    width:28px;
    height:28px;
}
.area-card h4{
    font-size:18px;
    color:var(--black);
    margin-bottom:12px;
    font-weight:700;
}
.area-card p{
    font-size:14px;
    color:var(--gray);
    line-height:1.8;
}
```

- [ ] **步骤 2：验证卡片效果**

刷新页面，悬停卡片检查有金色渐变边框和阴影提升效果。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "style: update practice area cards with gold gradient hover effect"
```

---

### 任务 6：更新Why Choose Me区域样式

**文件：**
- 修改：`lawyer-site/index.html:113-123` (Why Choose Me区域CSS)

- [ ] **步骤 1：更新区域样式**

```css
.why{
    background:var(--black);
    position:relative;
    overflow:hidden;
    padding:140px 8%;
}
.why::before{
    content:"";
    position:absolute;
    inset:0;
    background:url("data:image/svg+xml,%3Csvg width='80' height='80' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M40 0L80 40L40 80L0 40Z' fill='none' stroke='rgba(201,169,110,0.04)' stroke-width='1'/%3E%3C/svg%3E");
}
.why .sec-title h2{
    color:#fff;
}
.why .sec-title .label{
    color:var(--gold);
}
.why .sec-title p{
    color:rgba(255,255,255,.4);
}
.why-grid{
    max-width:1000px;
    margin:0 auto;
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:32px;
    position:relative;
    z-index:1;
}
.why-item{
    text-align:center;
    padding:40px 20px;
    border-radius:8px;
    transition:.3s;
}
.why-item:hover{
    background:rgba(255,255,255,.03);
}
.why-num{
    font-family:'Noto Serif SC',serif;
    font-size:56px;
    font-weight:900;
    color:transparent;
    -webkit-text-stroke:1px var(--gold);
    display:block;
    margin-bottom:16px;
    line-height:1;
}
.why-item h4{
    font-size:16px;
    color:#fff;
    margin-bottom:12px;
    font-weight:600;
    letter-spacing:1px;
}
.why-item p{
    font-size:13px;
    color:rgba(255,255,255,.45);
    line-height:1.8;
}
```

- [ ] **步骤 2：验证效果**

刷新页面，检查区域背景为纯黑，数字有金色描边效果。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "style: update why section with black background and gold stroke numbers"
```

---

### 任务 7：更新案例和服务流程样式

**文件：**
- 修改：`lawyer-site/index.html:126-146` (案例和服务流程CSS)

- [ ] **步骤 1：更新案例卡片样式**

```css
.cases{
    background:var(--light);
    padding:140px 8%;
}
.cases-grid{
    max-width:1100px;
    margin:0 auto;
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:24px;
}
.case-card{
    background:#fff;
    border-radius:8px;
    overflow:hidden;
    border:1px solid #eee;
    transition:.4s;
}
.case-card:hover{
    transform:translateY(-4px);
    box-shadow:0 16px 48px rgba(0,0,0,.08);
}
.case-top{
    background:linear-gradient(135deg,var(--black),var(--dark));
    padding:28px;
    color:#fff;
    position:relative;
}
.case-top .tag{
    display:inline-block;
    background:linear-gradient(135deg, var(--gold), var(--gold2));
    color:var(--black);
    padding:3px 14px;
    border-radius:3px;
    font-size:11px;
    font-weight:700;
    margin-bottom:12px;
    letter-spacing:1px;
}
.case-top h4{
    font-size:16px;
    font-weight:600;
}
.case-body{
    padding:28px;
}
.case-body p{
    font-size:14px;
    color:#555;
    margin-bottom:16px;
    line-height:1.8;
}
.case-result{
    display:flex;
    align-items:flex-start;
    gap:8px;
    font-size:13px;
    color:var(--black);
    font-weight:600;
    background:var(--light);
    padding:12px 16px;
    border-radius:6px;
    border-left:3px solid var(--gold);
}
.case-result svg{
    width:16px;
    height:16px;
    flex-shrink:0;
    margin-top:2px;
}
```

- [ ] **步骤 2：更新服务流程样式**

```css
.process{
    padding:140px 8%;
}
.process-wrap{
    max-width:900px;
    margin:0 auto;
}
.process-steps{
    display:flex;
    justify-content:space-between;
    position:relative;
}
.process-steps::before{
    content:"";
    position:absolute;
    top:32px;
    left:8%;
    right:8%;
    height:1px;
    background:linear-gradient(to right,transparent,var(--gold),var(--gold),transparent);
}
.step{
    text-align:center;
    position:relative;
    z-index:1;
    flex:1;
}
.step-circle{
    width:64px;
    height:64px;
    border-radius:50%;
    background:var(--black);
    display:flex;
    align-items:center;
    justify-content:center;
    margin:0 auto 20px;
    border:3px solid var(--gold);
    position:relative;
}
.step-circle svg{
    width:24px;
    height:24px;
}
.step h4{
    font-size:15px;
    color:var(--black);
    margin-bottom:6px;
    font-weight:700;
    letter-spacing:1px;
}
.step p{
    font-size:12px;
    color:var(--gray);
    padding:0 8px;
}
```

- [ ] **步骤 3：验证效果**

刷新页面，检查案例卡片和服务流程使用新配色。

- [ ] **步骤 4：Commit**

```bash
git add index.html
git commit -m "style: update cases and process sections with new color scheme"
```

---

### 任务 8：更新客户评价和联系区域样式

**文件：**
- 修改：`lawyer-site/index.html:149-175` (客户评价和联系区域CSS)

- [ ] **步骤 1：更新客户评价样式**

```css
.testimonials{
    background:var(--light);
    padding:140px 8%;
}
.testi-grid{
    max-width:1000px;
    margin:0 auto;
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:24px;
}
.testi-card{
    background:#fff;
    padding:36px 28px;
    border-radius:8px;
    border:1px solid #eee;
    transition:.3s;
}
.testi-card:hover{
    box-shadow:0 12px 40px rgba(0,0,0,.06);
}
.testi-stars{
    background:linear-gradient(135deg, var(--gold), var(--gold2));
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    font-size:14px;
    margin-bottom:16px;
    letter-spacing:2px;
}
.testi-card blockquote{
    font-size:14px;
    color:#555;
    line-height:1.9;
    margin-bottom:20px;
    font-style:italic;
}
.testi-author{
    display:flex;
    align-items:center;
    gap:12px;
}
.testi-avatar{
    width:40px;
    height:40px;
    border-radius:50%;
    background:linear-gradient(135deg,var(--black),var(--dark));
    display:flex;
    align-items:center;
    justify-content:center;
    color:#fff;
    font-size:14px;
    font-weight:700;
}
.testi-author-info span{
    display:block;
}
.testi-author-info .name{
    font-size:14px;
    font-weight:600;
    color:var(--black);
}
.testi-author-info .case-type{
    font-size:12px;
    color:var(--gray);
}
```

- [ ] **步骤 2：更新联系区域样式**

```css
.contact{
    padding:140px 8%;
}
.contact-wrap{
    max-width:1000px;
    margin:0 auto;
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:60px;
}
.contact-left h3{
    font-family:'Noto Serif SC',serif;
    font-size:22px;
    color:var(--black);
    margin-bottom:32px;
    letter-spacing:2px;
}
.c-info{
    display:flex;
    gap:16px;
    margin-bottom:28px;
    align-items:flex-start;
}
.c-icon{
    width:48px;
    height:48px;
    background:var(--light);
    border-radius:12px;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-shrink:0;
}
.c-icon svg{
    width:22px;
    height:22px;
}
.c-info h4{
    font-size:14px;
    color:var(--black);
    margin-bottom:4px;
    font-weight:600;
}
.c-info p{
    font-size:14px;
    color:var(--gray);
}
.contact-form input,
.contact-form textarea,
.contact-form select{
    width:100%;
    padding:14px 18px;
    border:1px solid #e0ddd8;
    border-radius:6px;
    font-size:14px;
    margin-bottom:16px;
    font-family:inherit;
    transition:.3s;
    background:#fff;
}
.contact-form input:focus,
.contact-form textarea:focus,
.contact-form select:focus{
    outline:none;
    border-color:var(--gold);
    box-shadow:0 0 0 3px rgba(201,169,110,.1);
}
.contact-form textarea{
    height:120px;
    resize:vertical;
}
.contact-form .btn{
    width:100%;
    justify-content:center;
    padding:16px;
    font-size:15px;
}
```

- [ ] **步骤 3：验证效果**

刷新页面，检查客户评价星级有金色渐变，联系表单输入框聚焦时有金色边框。

- [ ] **步骤 4：Commit**

```bash
git add index.html
git commit -m "style: update testimonials and contact sections with new styling"
```

---

### 任务 9：更新页脚和通用样式

**文件：**
- 修改：`lawyer-site/index.html:178-185` (页脚CSS)
- 修改：`lawyer-site/index.html:76-81` (通用section样式)

- [ ] **步骤 1：更新通用section样式**

```css
section{
    padding:140px 8%;
}
.sec-title{
    text-align:center;
    margin-bottom:72px;
}
.sec-title .label{
    font-size:12px;
    color:var(--gold);
    letter-spacing:6px;
    font-weight:500;
    text-transform:uppercase;
    margin-bottom:12px;
    display:block;
}
.sec-title h2{
    font-family:'Noto Serif SC',serif;
    font-size:clamp(26px,4vw,36px);
    color:var(--black);
    letter-spacing:3px;
    margin-bottom:12px;
}
.sec-title .line{
    width:40px;
    height:2px;
    background:linear-gradient(to right, var(--gold), var(--gold2));
    margin:20px auto 0;
}
.sec-title p{
    color:var(--gray);
    font-size:14px;
    max-width:480px;
    margin:16px auto 0;
}
```

- [ ] **步骤 2：更新页脚样式**

```css
footer{
    background:var(--black);
    color:rgba(255,255,255,.4);
    padding:60px 8% 40px;
}
.footer-top{
    display:flex;
    justify-content:space-between;
    align-items:flex-start;
    flex-wrap:wrap;
    gap:40px;
    padding-bottom:40px;
    border-bottom:1px solid rgba(255,255,255,.06);
}
.footer-brand .logo-text{
    font-size:20px;
    margin-bottom:12px;
}
.footer-brand p{
    font-size:13px;
    max-width:300px;
    line-height:1.8;
}
.footer-links h5{
    color:#fff;
    font-size:14px;
    margin-bottom:16px;
    font-weight:600;
    letter-spacing:1px;
}
.footer-links a{
    display:block;
    font-size:13px;
    color:rgba(255,255,255,.4);
    text-decoration:none;
    margin-bottom:10px;
    transition:.3s;
}
.footer-links a:hover{
    color:var(--gold);
}
.footer-bottom{
    text-align:center;
    padding-top:32px;
    font-size:12px;
}
```

- [ ] **步骤 3：更新返回顶部按钮**

```css
.totop{
    position:fixed;
    bottom:32px;
    right:32px;
    width:44px;
    height:44px;
    background:var(--black);
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
    cursor:pointer;
    opacity:0;
    transform:translateY(20px);
    transition:.3s;
    z-index:90;
    border:1px solid var(--gold);
}
.totop.show{
    opacity:1;
    transform:translateY(0);
}
.totop svg{
    width:18px;
    height:18px;
}
```

- [ ] **步骤 4：验证效果**

刷新页面，检查页脚为纯黑背景，分割线为金色渐变。

- [ ] **步骤 5：Commit**

```bash
git add index.html
git commit -m "style: update footer and common section styles"
```

---

### 任务 10：添加视差滚动效果

**文件：**
- 修改：`lawyer-site/index.html:666-734` (JavaScript部分)

- [ ] **步骤 1：添加视差滚动JavaScript代码**

在 `<script>` 标签中添加视差滚动逻辑：

```javascript
// ── parallax effect ──
(function(){
    const heroBg = document.querySelector('.hero-bg img');
    if (!heroBg) return;

    let ticking = false;
    window.addEventListener('scroll', () => {
        if (!ticking) {
            requestAnimationFrame(() => {
                const scrolled = window.pageYOffset;
                const rate = scrolled * 0.5;
                heroBg.style.transform = `translate3d(0, ${rate}px, 0)`;
                ticking = false;
            });
            ticking = true;
        }
    });
})();
```

- [ ] **步骤 2：验证视差效果**

刷新页面，滚动页面检查Hero背景图片有视差滚动效果。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "feat: add parallax scrolling effect to hero section"
```

---

### 任务 11：添加按钮波纹效果

**文件：**
- 修改：`lawyer-site/index.html` (CSS和JavaScript部分)

- [ ] **步骤 1：添加波纹效果CSS**

在 `<style>` 标签中添加：

```css
/* ripple effect */
.btn .ripple {
    position: absolute;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.3);
    transform: scale(0);
    animation: ripple-anim 0.6s ease-out;
    pointer-events: none;
}
@keyframes ripple-anim {
    to {
        transform: scale(4);
        opacity: 0;
    }
}
```

- [ ] **步骤 2：添加波纹效果JavaScript**

在 `<script>` 标签中添加：

```javascript
// ── button ripple effect ──
document.querySelectorAll('.btn').forEach(btn => {
    btn.addEventListener('click', function(e) {
        const rect = this.getBoundingClientRect();
        const ripple = document.createElement('span');
        ripple.className = 'ripple';
        ripple.style.left = `${e.clientX - rect.left}px`;
        ripple.style.top = `${e.clientY - rect.top}px`;
        this.appendChild(ripple);
        setTimeout(() => ripple.remove(), 600);
    });
});
```

- [ ] **步骤 3：验证波纹效果**

刷新页面，点击按钮检查有波纹扩散效果。

- [ ] **步骤 4：Commit**

```bash
git add index.html
git commit -m "feat: add ripple effect to buttons"
```

---

### 任务 12：添加文字动画效果

**文件：**
- 修改：`lawyer-site/index.html` (CSS和JavaScript部分)

- [ ] **步骤 1：添加文字动画CSS**

在 `<style>` 标签中添加：

```css
/* text animation */
.fade-up {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
}
.fade-up.visible {
    opacity: 1;
    transform: translateY(0);
}
.fade-left {
    opacity: 0;
    transform: translateX(-40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
}
.fade-left.visible {
    opacity: 1;
    transform: translateX(0);
}
/* stagger children */
.stagger-children > * {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease, transform 0.5s ease;
}
.stagger-children.visible > *:nth-child(1) { transition-delay: 0.1s; }
.stagger-children.visible > *:nth-child(2) { transition-delay: 0.2s; }
.stagger-children.visible > *:nth-child(3) { transition-delay: 0.3s; }
.stagger-children.visible > *:nth-child(4) { transition-delay: 0.4s; }
.stagger-children.visible > *:nth-child(5) { transition-delay: 0.5s; }
.stagger-children.visible > *:nth-child(6) { transition-delay: 0.6s; }
.stagger-children.visible > * {
    opacity: 1;
    transform: translateY(0);
}
```

- [ ] **步骤 2：更新IntersectionObserver**

确保现有的IntersectionObserver代码正常工作：

```javascript
// ── scroll animation ──
const obs = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
        if (e.isIntersecting) {
            setTimeout(() => e.target.classList.add('visible'), i * 80);
            obs.unobserve(e.target);
        }
    });
}, { threshold: 0.12 });
document.querySelectorAll('.fade-up, .fade-left, .stagger-children').forEach(el => obs.observe(el));
```

- [ ] **步骤 3：验证动画效果**

刷新页面，滚动页面检查各元素有淡入上移动画效果。

- [ ] **步骤 4：Commit**

```bash
git add index.html
git commit -m "feat: add text reveal animations with stagger effect"
```

---

### 任务 13：优化响应式设计

**文件：**
- 修改：`lawyer-site/index.html:193-210` (响应式CSS)

- [ ] **步骤 1：更新响应式样式**

```css
/* ═══ responsive ═══ */
@media(max-width:1024px){
    .areas-grid, .cases-grid, .testi-grid {
        grid-template-columns: repeat(2, 1fr);
    }
    .why-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}
@media(max-width:768px){
    nav ul {
        display: none;
    }
    .hamburger {
        display: flex;
    }
    nav ul.active {
        display: flex;
        flex-direction: column;
        position: absolute;
        top: 60px;
        left: 0;
        right: 0;
        background: var(--black);
        padding: 24px;
        gap: 18px;
        box-shadow: 0 8px 30px rgba(0,0,0,.2);
    }
    .about-grid {
        grid-template-columns: 1fr;
        gap: 40px;
    }
    .about-photo {
        max-width: 300px;
        margin: 0 auto;
    }
    .about-deco {
        display: none;
    }
    .areas-grid, .cases-grid, .testi-grid {
        grid-template-columns: 1fr;
    }
    .why-grid {
        grid-template-columns: 1fr 1fr;
    }
    .contact-wrap {
        grid-template-columns: 1fr;
    }
    .process-steps {
        flex-direction: column;
        gap: 24px;
    }
    .process-steps::before {
        display: none;
    }
    section {
        padding: 80px 5%;
    }
    /* disable parallax on mobile for performance */
    .hero-bg img {
        transform: none !important;
    }
}
```

- [ ] **步骤 2：验证移动端效果**

使用浏览器开发者工具模拟移动端，检查布局正常，视差效果已禁用。

- [ ] **步骤 3：Commit**

```bash
git add index.html
git commit -m "style: optimize responsive design and disable parallax on mobile"
```

---

### 任务 14：最终测试和提交

**文件：**
- 无新增文件

- [ ] **步骤 1：完整功能测试**

在浏览器中打开 `lawyer-site/index.html`，检查：
1. 配色方案为黑白+金色
2. 视差滚动效果正常
3. 按钮波纹效果正常
4. 文字动画效果正常
5. 所有原有功能正常（导航、表单等）
6. 移动端布局正常

- [ ] **步骤 2：性能检查**

检查页面加载速度没有明显下降，动画流畅。

- [ ] **步骤 3：最终提交**

```bash
cd lawyer-site
git add -A
git commit -m "feat: complete UI upgrade with modern black-white-gold design

- Update color scheme from navy to black-white-gold
- Add parallax scrolling effect to hero section
- Add button ripple click effect
- Add text reveal animations with stagger
- Optimize responsive design
- Disable parallax on mobile for performance"
```

- [ ] **步骤 4：推送到Gitee**

```bash
git push gitee master
```

---

## 验收检查清单

- [ ] 配色方案为黑白+金色
- [ ] Hero区域有视差滚动效果
- [ ] 按钮点击有波纹效果
- [ ] 滚动时文字有淡入动画
- [ ] 卡片悬停有精致阴影效果
- [ ] 统计数字有金色渐变
- [ ] 移动端布局正常
- [ ] 页面加载性能正常
- [ ] 所有原有功能正常
- [ ] 已推送到Gitee
