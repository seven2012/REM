# REM
#1,  实际页面宽度 == ？ == html {font-size}
#2,  1rem === 实院页面宽度

#举例：假如设计稿是以320px的宽度为原型来设计
#iphone5 
#width = 320px;
#html {
#  font-size:320px;
#}
#body {
#  font-size: 16px;
#}
#div{
# width:64px;  64/320 = 0.2rem
# height:128px; 128/320 = 0.4rem
#}
- p {
    font-size:18px;  18/320=0.05625rem;
- }
#//用js动态写meta与css
#var width = document.documentElement.clientWidth
#var scale = width / 320,
- var css= `
-    html{
#     font-size: ${320 * scale}px; //得到的font-size即为客户端移动手机的屏宽
#   }
#`
#document.write(`<style> ${css} </style>`) // 把动态的css font-size 写入页面

#//由上可知，rem换算后数值太小，运算起来不方便，所以，可以在font-size上先除以100，

#var css= `
#   html{
#     font-size: ${320 * scale / 100 }px; //得到的font-size即为屏宽除以100
#   }

#那么在css里的rem同时全部乘以100，结果是一样的，
#
#// 比较适中的做法，是先除以10，css里的rem再乘以10
  
