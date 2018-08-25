# REM
 - 1,  实际页面宽度 == ？ == html {font-size}
 - 2,  1rem === 实院页面宽度

 - 举例：假如设计稿是以320px的宽度为原型来设计
 - iphone5 
 - width = 320px;
 - html {
 -  font-size:320px;
 - }
 - body {
 -   font-size: 16px;
 - }
 - div{
 -  width:64px;  64/320 = 0.2rem
 -  height:128px; 128/320 = 0.4rem
 - }
 - p {
  -   font-size:18px;  18/320=0.05625rem;
 - }
 - //用js动态写meta与css
 - var width = document.documentElement.clientWidth
 - var scale = width / 320,
 - var css= `
 -    html{
 -      font-size: ${320 * scale}px; //得到的font-size即为客户端移动手机的屏宽
 -    }
 - `
 - document.write(`<style> ${css} </style>`) // 把动态的css font-size 写入页面

 - //由上可知，rem换算后数值太小，运算起来不方便，所以，可以在font-size上先除以100，

 - var css= `
 -    html{
 -      font-size: ${320 * scale / 100 }px; //得到的font-size即为屏宽除以100
 -    }

 -  但是浏览器一般字体不能小于12px,如果小于12px,就会被浏器的默认值覆盖}
 
 -  // 比较适中的做法，是先除以10，css里的rem再乘以10

 - 总结：
 - 要点1,浏览器禁止980像素的缩放
 - 设置html { font-size: 设备的页面宽度 / 10 px;}
 - 10rem == 设备页面宽度
 - 所有单位都用rem == 所有长度都以页面宽度为基准
 - 最后页面可以兼容任何移动端屏宽

  - 完整的meta例子：
 ```<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0;minimum-scale=1.0">```
 
 
 ```
     <!-- 方案1 -->
<script>
        //精确的rem方案，包括border:1px的解决方案
            var scale = 1 / window.devicePixelRatio  //整体缩放到这个比例，比如iphone5，dpr是2，scale结果是0.5，所以下面动态添加的meta整体缩放了50%,此操作是为了解决1像素问题，如在retina屏上，物理像素1px事实上是css里的0.5px,但0.5px是不能被识别的
            //所以只能让整个屏幕先缩放50%，那样写的border:1px,就是物理上的1px,实现了设计师的需求
            //所以最后，
            // `html {
            //    font-size : width / 10 * (window.devicePixelRati（1 or 2 or 3）)px;
            // }`
            //css里 元素rem = (元素px / 屏宽px) * 10 
            console.log('scale '+scale)
            document.write(`<meta name="viewport" content="initial-scale=${scale}, user-scalable=no, maximum-scale=${scale}, minimum-scale=${scale}">`)
    
            var width = document.documentElement.clientWidth / window.devicePixelRatio
            console.log('document.documentElement.clientWidth '+document.documentElement.clientWidth)
            console.log('window.devicePixelRatio '+window.devicePixelRatio)
            console.log('width '+width)
            var css = `
            html{
            font-size: ${(width / 10) * window.devicePixelRatio}px;
            }    
            `
            document.write(`<style>${css}</style>`)
    </script>
    <!-- 方案2 -->
    <script>
        //简单的动态rem方案
        // 让html font-size = 屏幕宽度/10;  //10rem = 页面宽度 计算方法：元素width(px)/屏幕width = X rem,因数值过小，所以在html 设置font-size时除以10，所以换算元素rem需乘以10;
        // `html {
        //    font-size : width / 10;
        // }`
        //meta的设置是固定的，不缩放：<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0;minimum-scale=1.0">
        //最终rem = (元素px / 屏宽px) * 10;
    </script>
    <!-- 方案3 -->
    <!-- 
        新建一个scss文件style.scss:
        输入计算公式：
        @function rem($px){
            $remSize: $px / width * 10;
            @return #{$remSize}rem;
        }
    
        body{
            font-size: rem(16);
        }
        对应设计稿基础上写的样式文件style.css：
        body{
            font-size:16px;
        }
    
        注：需在html页面引用这个css文件:
        <link rel="stylesheet" href="./style.css">
     -->
    
    
 ```
