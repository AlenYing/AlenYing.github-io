---
title: TODoAPP Note (1)
categories: 
- web前端
---
# ToDoAPP 源码阅读
 ## **主页逻辑:**
   1. ### 主页四组件:
      1. app-bar： 顶部导航，在后续中有复用
      2. avatar： 用户详情页，使用flex布局
      3. gradient: 背景容器，渐变色切换
      4. todo-list: 卡片列表
   2. ### 主页主要切换逻辑：
      1. 点击todo卡片的icon时，app-bar不改变，avatar通过透明度与3d切换完成向下隐去的效果（在主页中，click逻辑不生效，复用在detail组件时，触发父组件实现回退效果）
      2. todo-list的切换：div>ul>li的元素结构，使用flex布局，使得li横向排列，元素切换是3d的横坐标变换。question: li的元素宽度受到最外层div影响的问题。
      3. 卡片切换与颜色，使用mounted钩子函数在this.$el上挂载touch事件监听:
         1. 触摸开始，evt.touches[0],client*(相对区域的上/左边沿的*)取鼠标坐标
         2. 触摸结束，取鼠标坐标
         3. 如果没取到结束时坐标，或移动距离小于10，不触发切换 else 检验正负，前往仓库中触发nextodo或prevtodo
         4. 在以上两个函数中变更currentIndex,在Gradient组件中变更颜色。


 ## **点击卡片切换逻辑:**
   1. 先看布局:
      1. 在li中挂载两个div，todo_head,todo_body,todo_body通过3d定位落在li元素


##### ......to be continue....
#### From
[https://github.com/lizzz0523/limni]