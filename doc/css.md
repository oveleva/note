# css笔记

### 文本截断

1. 单行截断

```css
div {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

2. 多行截断

  - 谷歌css属性 `适合场景：谷歌内核可用`
  ```css
  div {
    display: -webkit-box;
    overflow: hidden;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }
  ```

  - 伪元素方案 `适合场景：文字内容较多，确定文字内容一定会超过容器的，那么选择这种方式不错。`
  ```
  p {
      position: relative;
      line-height: 18px;
      height: 36px;
      word-break: break-all;
      overflow: hidden;
  }
  p::after {
      content:"...";
      font-weight:bold;
      position:absolute;
      bottom:0;
      right:0;
      padding:0 20px 1px 45px;
      
      /* 为了展示效果更好 */
      background: -webkit-gradient(linear, left top, right top, from(rgba(255, 255, 255, 0)), to(white), color-stop(50%, white));
      background: -moz-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
      background: -o-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
      background: -ms-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
      background: linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
  }

  ```

  - float 方案
  
  ```html
  <div class="wrap">
    <div class="text">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dignissimos labore sit vel itaque delectus atque quos magnam assumenda quod architecto perspiciatis animi.</div>
  </div>
  ```
  ```css
  .wrap {
    height: 40px;
    line-height: 20px;
    word-break: break-all;
    overflow: hidden;
  }
  .wrap .text {
    float: right;
    margin-left: -5px;
    width: 100%;
    word-break: break-all;
  }
  .wrap::before {
    float: left;
    width: 5px;
    content: '';
    height: 40px;
  }
  .wrap::after {
    float: right;
    content: "...";
    height: 20px;
    line-height: 20px;
    /* 为三个省略号的宽度 */
    width: 3em;
    /* 使盒子不占位置 */
    margin-left: -3em;
    /* 移动省略号位置 */
    position: relative;
    left: 100%;
    top: -20px;
    padding-right: 5px;
  }
  ```

- 图片错误样式优化

img {
  text-align: center;
  position: relative;
  /* overflow: hidden; */
}

img:before {  
  content: " ";
  display: block;
  position: absolute;
  top: -2px;
  left: -2px;
  height: 100%;
  width: 100%;
  background-color: #eee;
  border: 2px dotted #ddd;
  border-radius: 5px;
}

img:after {
  content: attr(alt);
  font-size: 1em;
  color: #666;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  z-index: 2;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #eee;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
