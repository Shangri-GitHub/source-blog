---
title: html页面的元素
date: 2017-06-08 08:44:06
tags: ['html','css']
---

##### H5的新属性contenteditable="true"

``` html
1 #textarea {
2      width:300px;
3      border:1px solid #ccc;
4      min-height:150px;
5      max-height:300px;
6      overflow: auto;
7      font-size: 14px;
8      outline: none; 
9 }

<div id="textarea" contenteditable="true"></div>
```

##### 清除浮动公共样式
``` css
.clearfix:after {
    content: "";
    height: 0;
    line-height: 0;
    clear: both;
    display: block;
    visibility: hidden
}

.clearfix {
    zoom: 1
}
```

##### 自己手写下拉框
``` html
<!--下拉菜单-->
    /* css */
<style>
    .input {
        text-indent: 4px;
        margin: 10px auto 0;
        width: 98%;
        height: 38px;
        border: solid 1px #505864;
        line-height: 38px;
        font-size: 14px;
        color: #ffffff;

    }

    .arrows {
        width: 11px;
        height: 7px;
        background: url("theme/default/images/collect-data/arrows.png") no-repeat;
        position: relative;
        top: 34px;
        left: 86%;
    }

    #sub {
        width: 155px;
        position: absolute;
        top: 48px;
        left: 0;
        display: none;
        z-index: 2;
    }

    #sub ul {
        width: 100%;
        height: 100%;
        border: solid 1px #0e90d2;
        background: #424a5a;
    }

    #sub ul li {
        color: #ffffff;
        padding: 0 5px;
        line-height: 24px;

    }

    #sub ul li:hover {
        color: #ffffff;
        background: #0e90d2;
    }
</style>
<div id="layout">
    <div class="arrows"></div>
    <div class="input">
        视频源类型
    </div>
    <div id="sub">
        <ul>
            <li>视频源类型1</li>
            <li>视频源类型2</li>
            <li>视频源类型3</li>
        </ul>
    </div>
</div


```

##### 左侧栏多级菜单
``` html
<style>
 /*三级菜单*/
    .collect-data .sidebar .three-conten .mtree > li {
        background: url("theme/default/images/collect-data/split-line.png") 0px 52px no-repeat;
        width: 100%;
        position: relative;
        z-index: 1;
    }

    .collect-data .sidebar .three-conten .mtree > li .allow-down {
        position: absolute;
        top: 21px;
        right: 8%;
        width: 10px;
        height: 6px;
        background: url("theme/default/images/collect-data/allow-down.png") 0px 0px no-repeat;
    }

    .collect-data .sidebar .three-conten .mtree > li .allow-right {
        position: absolute;
        top: 20px;
        right: 8%;
        width: 6px;
        height: 10px;
        background: url("theme/default/images/collect-data/allow-right.png") 0px 0px no-repeat;
    }

    .collect-data .sidebar .three-conten .mtree > li a {
        color: #ffffff;
        font-size: 16px;
        line-height: 54px;
        text-decoration: none;
        margin-left: 4px;
    }

    .collect-data .sidebar .three-conten .mtree > li > ul > li a {
        color: #ffffff;
        font-size: 14px;
        line-height: 36px;
        text-decoration: none;
        margin-left: 10px;
    }

    .collect-data .sidebar .three-conten .mtree > li > ul > li a:hover {
        color: #c4e8f9;
    }

    .collect-data .sidebar .three-conten .mtree > li > ul > li > ul > li a {
        color: #ffffff;
        font-size: 12px;
        line-height: 36px;
        text-decoration: none;
        margin-left: 14px;
    }
    .collect-data .sidebar .three-conten .mtree > li a:hover {
        color: #c4e8f9;
    }
    .collect-data .sidebar .three-conten .mtree .mtree-active {
        color: #e3a76b;
    }
</style>
 <!--三级菜单-->
 <div class="three-conten">
     <!-- This is mtree list -->
     <ul class=mtree>
         <li><a href="#">人防工程</a>
             <span class="allow-right"></span>
             <ul>
                 <li>
                     <a href="#">人防工程1</a>
                     <ul>
                         <li><a href="#">人防工程1-1</a></li>
                     </ul>
                 </li>
                 <li><a href="#">人防工程2</a>
                     <ul>
                         <li><a href="#">人防工程2-1</a></li>
                         <li><a href="#">人防工程2-2</a></li>
                     </ul>
                 </li>
                 <li><a href="#">人防工程3</a>
                 </li>
             </ul>
         </li>
         <li><a href="#">重要经济目标</a>
             <span class="allow-right"></span>
             <ul>
                 <li><a href="#">人防工程1</a>
                     <ul>
                         <li><a href="#">人防工程1-1</a></li>
                     </ul>
                 </li>
             </ul>

         </li>
     </ul>
 </div>
 <script>
  //侧栏的三级菜单
     if ($('ul.mtree').length) {
         var collapsed = true;
         var duration = 400;
         $('.mtree ul').css({
             'overflow': 'hidden',
             'height': collapsed ? 0 : 'auto',
             'display': collapsed ? 'none' : 'block'
         });
         var node = $('.mtree li:has(ul)');
         node.children(':first-child').on('click.mtree', function (e) {
             var el = $(this).parent().children('ul').first();
             var isOpen = $(this).parent().hasClass('mtree-open');
             el.css({'height': 'auto'});
             setNodeClass($(this).parent(), isOpen);
             el.slideToggle(duration);
             e.preventDefault();
         });
         //  选中颜色
         $('.mtree li > *:first-child').on('click.mtree-active', function (e) {
             if ($(this).parent().hasClass('mtree-closed')) {
                 $('.mtree-active').not($(this)).removeClass('mtree-active');
                 $(this).addClass('mtree-active').siblings().removeClass('mtree-active');
             } else if ($(this).parent().hasClass('mtree-open')) {
                 $('.mtree-active').not($(this).parent()).removeClass('mtree-active');
                 $(this).addClass('mtree-active');
             } else {
                 $('.mtree-active').not($(this).parent()).removeClass('mtree-active');
                 $(this).toggleClass('mtree-active');
             }
         });
         function setNodeClass(el, isOpen) {
             if (isOpen) {
                 el.find('span').removeClass('allow-down').addClass('allow-right')
                 el.removeClass('mtree-open').addClass('mtree-closed');
             } else {
                 el.find('span').removeClass('allow-right').addClass('allow-down')
                 el.removeClass('mtree-closed').addClass('mtree-open');
             }
         }
 
 </script>

```