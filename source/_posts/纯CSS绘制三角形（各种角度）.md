---
title: 纯CSS绘制三角形
date: 2016-03-20 15:28:03
categories: CSS
tags: Triangle
---

相信很多人在处理li图形的时候，都会很纳闷，为什么list-style-type没有三角图案，难度要在网上下个三角图标作为list-style-image?怎么可能呢，所以我整理了网上一些css三角绘制的方法和代码。

##  Triangle-Up

![Triangle-up](http://7xrul1.com1.z0.glb.clouddn.com/triangle-up.jpg "triangle-up")
```css
#triangle-up {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}
```

## Triangle-Down
![Triangle-Down](http://7xrul1.com1.z0.glb.clouddn.com/triangle-down.jpg "triangle-down")
<!--more-->
```css
#triangle-down {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-top: 100px solid red;
}
```

## Triangle-Left
![Triangle-Left](http://7xrul1.com1.z0.glb.clouddn.com/triangle-left.jpg "triangle-left")
```css
#triangle-left {
    width: 0;
    height: 0;
    border-top: 50px solid transparent;
    border-right: 100px solid red;
    border-bottom: 50px solid transparent;
}
```

## Triangle-Right
![Triangle-Right](http://7xrul1.com1.z0.glb.clouddn.com/triangle-right.jpg "triangle-right")
```css
#triangle-right {
    width: 0;
    height: 0;
    border-top: 50px solid transparent;
    border-left: 100px solid red;
    border-bottom: 50px solid transparent;
}
```

## Triangle-Top-Left
![Triangle-Top-Left](http://7xrul1.com1.z0.glb.clouddn.com/triangle-top-left.jpg "triangle-top-left")
```css
#triangle-topleft {
    width: 0;
    height: 0;
    border-top: 100px solid red;
    border-right: 100px solid transparent;
}
```

## Triangle-Top-Right
![Triangle-Top-Right](http://7xrul1.com1.z0.glb.clouddn.com/triangle-top-right.jpg "triangle-top-right")
```css
#triangle-topright {
    width: 0;
    height: 0;
    border-top: 100px solid red;
    border-left: 100px solid transparent;
}
```

## Triangle-Bottom-left
![Triangle-Bottom-left](http://7xrul1.com1.z0.glb.clouddn.com/triangle-bottom-left.jpg "triangle-bottom-left")
```css
#triangle-bottomleft {
    width: 0;
    height: 0;
    border-bottom: 100px solid red;
    border-right: 100px solid transparent;
}
```

## Triangle-Bottom-Right
![Triangle-Bottom-Right](http://7xrul1.com1.z0.glb.clouddn.com/triangle-bottom-right.jpg "triangle-bottom-right")
```css
#triangle-bottomright {
    width: 0;
    height: 0;
    border-bottom: 100px solid red;
    border-left: 100px solid transparent;
}
```
