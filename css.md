# CSS Coding Style

## 編碼

首行定義編碼。

```css
@charset "utf-8";
```

## 分類

```css
/* --- Base --- */
  /* Normailize or Myerweb */
  /* Customer Reset CSS */

/* --- Layout --- */
  /* Header */
  /* Nav */
  /* Content */
  /* Siderbar */
  /* Footer */

/* --- Module --- */
  /* Animation */
  /* Dropdown */
  /* Alert */
  /* Button */

/* --- Utility --- */
  /* Helper */
  /* State */

/* --- Vendors --- */
  /* Fontawesome */
  /* jQuery UI */
```

## 檔案分配

除了有共用的 CSS 文件，每一個 HTML 文件也需對應一個 CSS 文件，例如：有一個 HTML 文件檔名為 about.html，就須對應一個 about.css 文件。手機版也需獨立一個 CSS 文件，以便維護與效能優化管理。如下:

```text
├── style
|   ├── about.css
|   ├── all.css
|   ├── index.css
|   ├── mobile.css
├── about.html
├── index.html
```

## 選取器撰寫

對於通用元素務必使用 class ，這樣有利於模組延伸的優化增加複用性。

### 避免使用屬性選取器

對於經常出現的元素，避免使用屬性選取器。瀏覽器的效率會受到這些因素的影響。

```css
/* Bad */
.img-resp[alt] { ... }

/* Good */
.img-resp { ... }
```

### 選取器組成個數不要超過 3 個，特殊情況則不在此限

選取器要儘可能短，並且儘量限制組成選取器的元素個數。

```css
/* Bad */
body.home div.header .list { ... }

/* Good */
.list { ... }
```

### 避免使用涵蓋範圍太大的選取器

```css
/* Bad */
.foo * { ... }
```

### 只有在必要的時候才將 class 限制在最近的父元素內（後代選取器）

```css
.post__date { ... }
.post__head .post__date { ... }
.post__body .post__date { ... }
.post__foot .post__date { ... }
```

### 避免使用 id 選取器

```css
/* Bad */
#Header { ... }

/* Good */
.header { ... }
```

### 避免隨意加重選取器的優先權

```css
/* Bad */
div.post { ... }

/* Good */
.post { ... }
```

### 減少對 HTML 的依賴

HTML:

```html
/* Bad */
<div class="form">
  <p> ... </p>
  <span> ... </span>
</div>

/* Good */
<div class="form">
  <p class="form__desc"> ... </p>
  <span class="form__name"> ... </span>
</div>
```

CSS:

```css
/* Bad */
.form p { ... }
.form span { ... }

/* Good */
.form__desc { ... }
.form__name { ... }
```

## class 命名方式

### 區塊 (Block)

- 命名應當儘可能短，並使用有組織或目的明確的名稱，不要使用表現形式的名稱，例如: .red。
- class 名稱中只能出現英文字元、破折號（dashe）、底線（underline）、數字。
- 避免過度任意的簡寫。.btn 代表 button，但是 .s 不能表達任何意思。
- 一個破折號應當用於相關 class 的命名，也就是模組化的延伸，類似於命名空間。

HTML:

```html
<article class="post"> ... </article>
<article class="post post-reverse"> ... </article>
<article class="post post-hover"> ... </article>
```

CSS:

```css
.product { ... }
.product-reverse { ... }
.product-hover { ... }
```

### 元素 (Element)

繼承最近的父層 class 或基本 class 作為新 class 的首碼。同一個 class 模組中，子層元件的命名方式都用「模組名 + 兩個底線 + 組織名」。

- 沒有辦法獨立於區塊之外生存，換句話說區塊可以沒有元素，但元素不可以沒有區塊。
- 表達的是目的，而不是狀態。

HTML:

```html
<article class="product">
  <header class="product__head">
    <h1 class="product__name"> ... </h1>
  </header>
  <div class="product__body">
    <p class="product__desc"> ... </p>
    <p class="product__desc"> ... </p>
  </div>
</article>
```

CSS:

```css
.product { ... }
.product__head { ... }
.product__name { ... }
.product__body { ... }
.product__desc { ... }
```

### 修飾符 (Modifier)

#### 框架開發或靜態套用

修飾子層元件目前狀態的命名方式以「模組名 + 兩個底線 + 組織名 + 兩個破折號 + 目的名」。

- 不能脱離區塊或元素使用。
- 應該改變的是實體的外觀，行為或狀態，而不是替換它。
- 不能同時使用兩個相同屬性卻不同值的修飾符。

HTML:

```html
<article class="product">
  <header class="product__head">
    <h1 class="product__name"> ... </h1>
  </header>
  <div class="product__body">
    <p class="product__price"> ... </p>
    <p class="product__price product__price--onsale"> ... </p>
  </div>
</article>
```

CSS:

```css
.product__price { ... }
.product__price--onsale { ... }
```

#### 非框架開發

使用 .js-* 的 class 方式來標示行為，也就是供 Javascript 控制的 class。

HTML:

```html
<article class="product">
  <header class="product__head">
    <h1 class="product__name"> ... </h1>
  </header>
  <div class="product__body">
    <p class="product__price"> ... </p>
    <p class="product__price js-product__price"> ... </p>
  </div>
</article>
```

CSS:

```css
.product__price { ... }
.js-product__price { ... }
```

## 語法

- 為選取器分組時，將單獨的選取器單獨放在一行。
- 用 2 個空白進行縮排。(tabSize: 2)
- 為了 CSS 的易讀性，在每個註解區域內，前後各添加一個空格。
- 在每個屬性後的冒號（:）後應該插入一個空格。
- 所有 Value 應當以分號結尾。最後 Value 的分號是可不加，但是，如果省略這個分號，你的 CSS 可能更易出錯。
- 對於以逗號分隔的屬性值，每個逗號後面都應該插入一個空格易於辨識。
- 對於屬性值或顏色參數，省略小於 1 的小數前面的 0 ，例如：.5 代替 0.5。
- 十六進位值應該全部小寫，例如：#fff。在解讀 CSS 文件時，小寫字元易於分辨，因為他們的形式更易於區分。
- 儘量使用縮寫形式的十六進位值，例如：用 #fff 代替 #ffffff。
- 為選取器中的屬性添加雙引號，例如：<code>input[type="text"]</code>。
- 避免為 0 值指定單位，例如：用 <code>margin: 0</code> 代替 <code>margin: 0px</code>。
- 為字體加粗時，請以 <code>font-weight: 900</code> 代替 <code>font-weight: bold</code>。
- 除了修飾符 (Modifier) 以外，其他 class 禁用 <code>!important</code>。

```css
/* 註解區域 */
.selector,
.selector-secondary,
.selector__input--text {
  padding: 15px;
  margin: 0 0 15px;
  background-color: rgba(0, 0, 0, .5);
  font-weight: 900;
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}

.js-tab__item {
  background-color: #fff!important;
}

.tab__item--active {
  background-color: #fff!important;
}
```
## 屬性類型的順序

相關的屬性應當歸為一組，並按照下面的順序排列:

1. Positioning（定位）。
1. Box Model（區塊模型）。
1. Typographic（排字）。
1. Visual（視覺）。
1. Other（其他）。

由於定位（Positioning）可以從正常的模型中移動、移除元素，並且還能覆蓋區塊模型（Box Model）相關的樣式，因此排在首位。區塊模型排在第二順位，因為它決定了元件的尺寸和位置。其他屬性只是影響元件的內部（inside）或者是不影響前兩組屬性，因此排在後面。

```css
.store {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
  display: block;
  float: right;
    
  /* Box Model */
  width: 100px;
  height: 100px;
  padding: 10px;
  margin: 10px;
    
  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
    
  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  box-shadow: 10px 0 5px rgba(0, 0, 0, .5);

  /* Other */
  opacity: 1;
  cursor: pointer;
  transition: width .3s;
}
```

## 避免使用 @import 引入 CSS

- 必須等主要的樣式檔載入完成，才會開始載入 @import 的樣式檔。
- 額外多增加請求次數。

## 如有必要才使用縮寫

但並非所有情況下都必須縮寫，因為當一個屬性的值縮寫時，會將所有項目都設定一遍，所以，會導致不需設定的屬性被強行寫入了。

```css
/* Bad */
.something {
  margin: 0 auto;
  background: pink;
}

/* Good */
.something {
  margin-left: auto;
  margin-right: auto;
  bagkground-color: pink;
}
```
