# Hello, CSS!

* [Cascading Style Sheets](https://www.w3.org/Style/CSS/Overview.en.html)
* [CSS Tutorial](https://www.w3schools.com/css/)

## Normalize.css

* [Normalize.css](https://necolas.github.io/normalize.css/)

**Normalize.css** makes browsers render all elements more consistently and in line with modern standards. It precisely targets only the styles that need normalizing.

## Examples

**文本两端对齐**

Example 1:

```html
<div class="example">
    <p>归去来兮，田园将芜胡不归！既目以心为形役，奚惆怅而独悲？悟已往之不谏，知来者之可追。实迷途其未远，觉今是而昨非。舟遥遥以轻飏，风飘飘而吹衣。问征夫以前路，恨晨光之熹微。</p>
    <p>乃瞻衡宇，载欣载奔。僮仆欢迎，稚子候门。三径就荒，松菊犹存。携幼入室，有酒盈樽。引壶觞以自酌，眄庭柯以怡颜。倚南窗以寄傲，审容膝之易安。园日涉以成趣，门虽设而常关。策扶老以流憩，时矫首而遐观。云无心以出岫，鸟倦飞而知还。景翳翳以将入，抚孤松而盘桓。</p>
    <p>归去来兮，请息交以绝遊。世与我而相违，复驾言兮焉求？悦亲戚之情话，乐琴书以消忧。农人告余以春及，将有事于西畴。或命巾车，或棹孤舟。既窈窕以寻壑，亦崎岖而经邱。木欣欣以向荣，泉涓涓而始流。善万物之得时，感吾生之行休。</p>
    <p>已矣乎！寓形宇内复几时！曷不委心任去留？胡为乎遑遑欲何之？富贵非吾愿，帝乡不可期。怀良辰以孤往，或植杖而耘耔。登东皋以舒啸，临清流而赋诗。聊乘化以归尽，乐天天命复奚疑！</p>
</div>
```

```css
.example {
    text-indent: 30px;
    text-align: justify;
}
```

Example 2:

```html
<div class="example-item">
    <span class="label">姓名</span>：
    <span class="value">王小明</span>
</div>
<div class="example-item">
    <span class="label">出生年月</span>：
    <span class="value">1998-02</span>
</div>
<div class="example-item">
    <span class="label">性别</span>：
    <span class="value">男</span>
</div>
```

```css
.example-item {
    margin-bottom: 5px;
    height: 32px;
    line-height: 32px;
}
.example-item .label {
    display: inline-block;
    width: 100px;
    height: 100%;
    text-align: justify;
    vertical-align: top;
}
.example-item .label:after {
    display: inline-block;
    width: 100%;
    height: 0;
    content: '';
}
```

**文本溢出显示省略号（…）**

单行：

```html
<div class="example">
    人生是一场旅程。我们经历了几次轮回，才换来这个旅程。而这个旅程很短，因此不妨大胆一些，不妨大胆一些去爱一个人，去攀一座山，去追一个梦......有很多事我都不明白。但我相信一件事。上天让我们来到这个世上，就是为了让我们创造奇迹。
</div>
```

```css
.example {
    height: 32px;
    line-height: 32px;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
}
```
