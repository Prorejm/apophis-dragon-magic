# 阿波菲斯·龙之魔法 全面审计修复计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 修复所有41个HTML文件的导航一致性、汉堡菜单、Tab切换、内容完整性问题

**Architecture:** 使用Python脚本批量处理41个文件，确保导航链接一致性（40个链接+qimen-chart），为所有文件添加汉堡菜单HTML按钮，修复6个文件的switchTab和null check问题

**Tech Stack:** Python (文件批量处理), HTML/CSS/JS

---

## 审计发现汇总

### Critical (3项)
1. **全部41个文件缺少汉堡菜单按钮HTML** - CSS和JS存在但HTML中无 `<button class="hamburger" id="hamburger">` 元素
2. **qimen-chart.html 导航缺少16个链接** - 仅23/39个nav-link
3. **40个文件未链接到qimen-chart.html** - 该页面完全孤立

### High (6项)
4. **kabbalah.html** - switchTab使用onclick字符串解析 + hamburger无null check
5. **rune-alphabet.html** - hamburger无null check
6. **golden-bough.html** - hamburger无null check
7. **ogham-alphabet.html** - hamburger无null check
8. **hebrew-alphabet.html** - Tab使用onclick内联方式
9. **necromancy.html** - Tab使用onclick内联方式

---

## Task 1: 为所有41个文件添加汉堡菜单HTML按钮

**Files:** 全部41个HTML文件

- [ ] **Step 1: 创建Python脚本 `add_hamburger.py`**

脚本逻辑：
1. 扫描目录下所有.html文件
2. 对每个文件，在 `<nav class="nav-bar" id="navBar">` 之后、第一个 `<a class="nav-link"` 之前，插入汉堡菜单按钮HTML
3. 按钮HTML: `<button class="hamburger" id="hamburger"><span></span><span></span><span></span></button>`
4. 同时在 `</nav>` 之后添加移动端菜单容器: `<div class="mobile-menu" id="mobileMenu"></div>`（如果不存在的话）
5. 跳过已经有该按钮的文件

```python
import os, re, glob

DIR = r'g:\新建文件夹 (18)\apophis-dragon-magic'
HAMBURGER_BTN = '<button class="hamburger" id="hamburger"><span></span><span></span><span></span></button>'

for f in glob.glob(os.path.join(DIR, '*.html')):
    with open(f, 'r', encoding='utf-8') as fh:
        content = fh.read()
    if 'id="hamburger"' in content:
        print(f'SKIP (already has hamburger): {os.path.basename(f)}')
        continue
    # Insert hamburger button after <nav class="nav-bar" id="navBar">
    content = content.replace(
        '<nav class="nav-bar" id="navBar">',
        '<nav class="nav-bar" id="navBar">\n' + HAMBURGER_BTN
    )
    # Add mobile menu div after </nav> if not present
    if 'id="mobileMenu"' not in content:
        content = content.replace('</nav>', '</nav>\n<div class="mobile-menu" id="mobileMenu"></div>', 1)
    with open(f, 'w', encoding='utf-8') as fh:
        fh.write(content)
    print(f'OK: {os.path.basename(f)}')
```

- [ ] **Step 2: 运行脚本**

Run: `python add_hamburger.py`
Expected: 41 files processed, all get hamburger button

- [ ] **Step 3: 验证**

Run: `grep -c 'id="hamburger"' *.html | grep -v ':0$'`
Expected: 41 files with count >= 1

---

## Task 2: 修复qimen-chart.html导航 + 将qimen-chart添加到所有文件

**Files:**
- Modify: `qimen-chart.html` (补充16个缺失的nav-link)
- Modify: 其余40个HTML文件 (各添加1个qimen-chart链接)

- [ ] **Step 1: 创建Python脚本 `fix_nav_qimen.py`**

脚本逻辑：
1. 读取一个参考文件（如index.html）的完整nav-link列表
2. 用参考列表替换qimen-chart.html中不完整的nav-link部分
3. 对其他40个文件，在导航栏中适当位置添加 `qimen-chart.html` 链接

```python
import os, re, glob

DIR = r'g:\新建文件夹 (18)\apophis-dragon-magic'

# Read reference nav from index.html
with open(os.path.join(DIR, 'index.html'), 'r', encoding='utf-8') as f:
    ref = f.read()

# Extract all nav links from reference
links = re.findall(r'<a class="nav-link" href="([^"]+)">([^<]+)</a>', ref)
print(f'Reference has {len(links)} nav-links')

# Process qimen-chart.html - replace entire nav content
qimen_file = os.path.join(DIR, 'qimen-chart.html')
with open(qimen_file, 'r', encoding='utf-8') as f:
    content = f.read()

# Extract nav bar section
nav_match = re.search(r'(<nav class="nav-bar" id="navBar">.*?</nav>)', content, re.DOTALL)
if nav_match:
    old_nav = nav_match.group(1)
    # Build new nav with hamburger + all links
    hamburger = '<button class="hamburger" id="hamburger"><span></span><span></span><span></span></button>'
    new_links = '\n'.join(f'<a class="nav-link" href="{href}">{text}</a>' for href, text in links)
    new_nav = f'<nav class="nav-bar" id="navBar">\n{hamburger}\n<span class="nav-brand">阿波菲斯</span>\n{new_links}\n</nav>'
    content = content.replace(old_nav, new_nav)
    with open(qimen_file, 'w', encoding='utf-8') as f:
        f.write(content)
    print(f'Fixed qimen-chart.html nav: {len(links)} links')

# Process other files - add qimen-chart link if missing
qimen_link = '<a class="nav-link" href="qimen-chart.html">奇门遁甲</a>'
for f in glob.glob(os.path.join(DIR, '*.html')):
    if os.path.basename(f) == 'qimen-chart.html':
        continue
    with open(f, 'r', encoding='utf-8') as fh:
        c = fh.read()
    if 'qimen-chart.html' not in c:
        # Insert after qimen-dunjia link
        c = c.replace(
            '<a class="nav-link" href="qimen-dunjia.html">奇门遁甲</a>',
            '<a class="nav-link" href="qimen-dunjia.html">奇门遁甲</a>\n' + qimen_link
        )
        with open(f, 'w', encoding='utf-8') as fh:
            fh.write(c)
        print(f'Added qimen-chart link to: {os.path.basename(f)}')
```

- [ ] **Step 2: 运行脚本**

- [ ] **Step 3: 验证所有文件都有40个nav-link**

---

## Task 3: 修复kabbalah.html的switchTab和null check

**Files:**
- Modify: `kabbalah.html`

- [ ] **Step 1: 读取kabbalah.html的switchTab函数和tab按钮**

用Grep搜索 `switchTab` 和 `onclick` 确认当前实现

- [ ] **Step 2: 将tab按钮从onclick改为data-tab**

将所有 `<div class="tab-btn" onclick="switchTab('tabN')">` 改为 `<div class="tab-btn" data-tab="tabN">`

- [ ] **Step 3: 重写switchTab函数使用data-tab**

替换为标准版本：
```javascript
function switchTab(tabId){
  var panels=document.querySelectorAll('.tab-panel');
  for(var i=0;i<panels.length;i++){panels[i].classList.remove('active');}
  var btns=document.querySelectorAll('.tab-btn');
  for(var i=0;i<btns.length;i++){btns[i].classList.remove('active');}
  var target=document.getElementById(tabId);
  if(target)target.classList.add('active');
  var btn=document.querySelector('[data-tab="'+tabId+'"]');
  if(btn)btn.classList.add('active');
}
```

- [ ] **Step 4: 添加hamburger null check**

确保hamburger相关代码有 `if(hamburgerBtn)` 包裹

---

## Task 4: 修复rune-alphabet.html, golden-bough.html, ogham-alphabet.html的null check

**Files:**
- Modify: `rune-alphabet.html`
- Modify: `golden-bough.html`
- Modify: `ogham-alphabet.html`

- [ ] **Step 1: 对每个文件，找到 `getElementById('hamburger').addEventListener` 行**

- [ ] **Step 2: 在前面添加null check**

将:
```javascript
document.getElementById('hamburger').addEventListener('click',function(){
```
改为:
```javascript
var hamburgerBtn=document.getElementById('hamburger');
if(hamburgerBtn){
hamburgerBtn.addEventListener('click',function(){
```

---

## Task 5: 修复hebrew-alphabet.html的Tab切换

**Files:**
- Modify: `hebrew-alphabet.html`

- [ ] **Step 1: 读取当前switchTab和tab按钮实现**

- [ ] **Step 2: 将onclick改为data-tab属性**

- [ ] **Step 3: 重写switchTab使用data-tab**

---

## Task 6: 修复necromancy.html的Tab切换

**Files:**
- Modify: `necromancy.html`

- [ ] **Step 1: 读取当前switchTab和tab按钮实现**

- [ ] **Step 2: 将onclick改为data-tab属性**

- [ ] **Step 3: 重写switchTab使用data-tab**

---

## Task 7: 为所有缺少汉堡菜单CSS/JS的文件添加样式和脚本

**Files:** 33个没有汉堡菜单功能的HTML文件

- [ ] **Step 1: 创建Python脚本 `add_hamburger_css_js.py`**

对每个缺少汉堡菜单CSS的文件，在 `<style>` 标签内追加标准汉堡菜单CSS：
```css
.hamburger{display:none;cursor:pointer;padding:5px;background:none;border:none}
.hamburger span{display:block;width:25px;height:3px;background:#d4a843;margin:5px 0;transition:all .3s}
.hamburger.active span:nth-child(1){transform:rotate(45deg) translate(5px,5px)}
.hamburger.active span:nth-child(2){opacity:0}
.hamburger.active span:nth-child(3){transform:rotate(-45deg) translate(5px,-5px)}
.mobile-menu{display:none;position:fixed;top:60px;left:0;width:100%;background:rgba(10,10,10,.95);padding:20px;z-index:998}
.mobile-menu.show{display:flex;flex-direction:column;gap:10px}
.mobile-menu a{color:#d4a843;text-decoration:none;padding:10px;border-bottom:1px solid rgba(212,168,67,.2)}
@media(max-width:768px){.hamburger{display:block}.nav-bar.open .nav-link{display:none}}
```

对每个缺少汉堡菜单JS的文件，在 `<script>` 标签内追加：
```javascript
var hamburgerBtn=document.getElementById('hamburger');
var navBar=document.getElementById('navBar');
var mobileMenu=document.getElementById('mobileMenu');
if(hamburgerBtn){
hamburgerBtn.addEventListener('click',function(){
  hamburgerBtn.classList.toggle('active');
  if(mobileMenu)mobileMenu.classList.toggle('show');
  if(navBar)navBar.classList.toggle('open');
});
}
// Populate mobile menu
if(mobileMenu){
var navLinks=document.querySelectorAll('.nav-link');
navLinks.forEach(function(link){
  var clone=link.cloneNode(true);
  clone.className='nav-link';
  mobileMenu.appendChild(clone);
});
}
```

---

## Task 8: 最终验证和部署

- [ ] **Step 1: 运行JS验证**

Run: `python validate_all_js.py`
Expected: 41/41 passed

- [ ] **Step 2: 验证汉堡菜单**

Run: `grep -c 'id="hamburger"' *.html`
Expected: 41 files, all >= 1

- [ ] **Step 3: 验证导航链接数**

Run: `grep -c 'nav-link' *.html`
Expected: all files have 40 links (qimen-chart now included)

- [ ] **Step 4: Git commit and push**

Run: `git add -A && git commit -m "fix: 全面审计修复 - 汉堡菜单/导航一致性/Tab切换" && git push`
