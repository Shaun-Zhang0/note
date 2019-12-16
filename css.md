## 盒子模型

属性:
1. margin
2. padding
3. border
4. content

分类:
1. IE怪异盒子模型
2. 标准盒子模型

## 隐藏元素

1. display: none;
2. opacity: 0;
3. visbility: hidden;
4. position: absolute;
   top: -9999px;
   left:-9999px;

## link 和 @import 的区别

1. 加载顺序 link会和页面加载的同时一起加载, @import 会等页面资源加载完后再进行加载
2. link 可以通过js操作dom 直接插入link标签

## 水平 垂直居中

水平居中 

1. 行内元素: text-align: center;
2. 块级元素: 
  
   2.1 设置宽度  margin: 0 auto;

   2.2 父级元素 设置display: flex; justify-content:center;

   2.3 父元素:position:relative; 子元素:position:absolute; left: 50%; transfrom: translateX(-50%) || margin-left:-宽度/2px;

垂直居中

1. 行内元素: 父级元素设置line-height与height相同 
2. 块级元素: 
   
   2.1 position: absolute; top:50%; transfrom: translateY(-50%) || margin-top: -宽度/2px;

   2.2 父级元素设置 display: flex; align-item: center;

   2.3 父级元素设置display: table; 子元素设置display:table-cell; vertical-align: middle;

## 什么是flexbox以及适用场景

1. 弹性布局 用来为盒状模型提供最大的灵活性 , 任何一个容器都可以成为flex 布局
2. 容器内部同样也可以适用flex布局 , display: inline-flex

* 设置flex布局后 , 子元素的float clear vertical-align 属性值均会失效
* 提供了一种更高效的方式来对容器的条目进行布局 , 对齐 , 和 分配空间 弹性布局没有这样内在的限制 操作比较自由

浮动元素引起的问题和解决办法

* 浮动脱离文档流 父级元素高度无法撑开 影响与父级元素同级的元素
清除浮动的方式  

1. 父级元素添加overflow:hidden;
2. 给父级元素添加::after伪类 
```
    .parent:after{
        content: '';
        height: 0;
        clear: both;
        display: block;
    }         

```

## 块级元素 内联元素 的 特点

1. 块级元素

    1.1 独占一行

    1.2 可以设定宽高 宽度默认100%

    1.3 块级元素可以嵌套块级元素 或者 内联元素

2. 内联元素

    2.1 在一行内显示

    2.2 不能设置宽度和高度

    2.3 内联元素可以嵌套内联元素 但不能嵌套块级元素 容易导致布局混乱


## 实现两栏布局 

1. 左边固定 右边自适应

    ```
        .left{
            float: left;
            width: 200px;
        }
        .right{
            margin-left: 200px;
        }


    ```
2. 通过定位实现

    ```
        .parent{
            position:relative;
        }
        .left{
            position: absolute;
            left: 0;
            width: 200px;
        }
        .right{
            position: absolute;
            right: 0;
            left: 200px;
        }

    ```

## dom元素中的 attribute 和 property 的区别

1. property 是指dom元素本身存在的属性 class , id , value
2. attribute 存在于html本身 , 而不是在Dom中 


## css实现三列布局怎么做？如果中间是自适应又怎么做？

1. 使用浮动布局来实现

```
    .left{
        float: left;
        width: 200px;
    }
    .right{
        float: right;
        width: 200px;
    }
    .center{
        margin: 0 200px;
    }

```
2. BFC

```
    .left{
        float: left;
        width: 200px;

    }
    .right{
        float: right;
        width: 200px;
    }
    .center{
        overflow:hidden;
        width: 500px;

    }
```
3. 绝对定位

```
    .left{
        position: absolute;
        top: 0;
        left: 0;
        width: 300px;
    }
    .right{
        position: absolute;
        top: 0;
        right: 0;
        width: 300px;
    }
    .center{
        margin: 0 300px;
        width: 500px;
    }

```

4. 双飞翼布局

```
    .center{
        float:left;
        margin: 0 500px;
    }
    .left{
        float: left;
        width: 500px;
        margin-left: -100%;
    }
    .right{
        float: right;
        width: 500px;
        margin-left: -500px;
    }
   
```

## overflow: hidden


1. 防止溢出
2. 实现BFC
   
   2.1 垂直相邻的子元素外边距合并
   
   ```
    .top{
        width:200px;
        margin-bottom: 10px;
    }

    . bottom{
        width: 200px;
        margin-top: 10px;
    }

    /********************************/

    原因: 两个盒子都处于同一个BFC中 
    解决方案: 让他们处于不用的BFC中

    给top盒子添加一个父元素 , 同时添加overflow: hidden

    .parent{
        overflow: hidden;
    }

   ```
   2.2 清除浮动

   2.3 不能裁剪 position:absolute 的元素


## css 长度单位

* 分为 绝对长度 和 相对长度
1. 绝对长度
    
    1.1 px 像素 

    1.2 cm 厘米 1cm = 37.8px

    1.3 mm 毫米 1mm = 3.78px

    1.4 in 英尺 1in = 2.54cm = 96px;

    1.5 pt 点 1pt = 1.33px

    1.6 pc 派卡 1pc = 16px

2. 相对长度

    2.1 em 一个字符大小 默认为16px;

    2.2 rem 相对于根元素HTML的字体大小

    2.3 % 百分比是一个相对长度单位 , 相对于包含块 的高宽或字体大小

    2.4 vh 视口高度

    2.5 vw 视口宽度

    2.6 vmin 取视口高度和视口宽度最小的值

    2.7 vmax 取视口高度和视口宽度最大的值

## ::before 和 :before

1. 伪类
   
    伪类是给页面中已经存在的元素添加一个类名

2. 伪元素

   伪元素只是在页面中添加了一个元素 并没有在dom树上添加  

## css选择器优先级

内联样式 > id > class > 通配符

## margin padding 百分比

* 相对父级元素的宽度



