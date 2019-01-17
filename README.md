# hano-
一、效果：


image.png

二、操作步骤：
1.输入框输入汉诺塔的层数
2.点击start
3.生成汉诺塔
4.chrome F12 点击执行代码块（如下图），可看到汉诺塔每一块的移动过程


image.png

三、分析
1.获取输入值
```
 // 获取输入值
        function getNumber() {
            return document.getElementById('number').value;
        }
```
2.生成随机颜色
```
// 生成随机颜色
        function randomColor() {
            var colors = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'];
            var color = '#';
            for (var i = 0; i < 6; i++) {
                color += colors[Math.floor(Math.random() * 16)]
            }
            return color;
        }
```
3.渲染汉诺塔
```
 // 渲染汉诺塔初始化
        function init() {
            // 生成三个柱子
            var number = getNumber();
            var A = document.getElementById('A');
            var B = document.getElementById('B');
            var C = document.getElementById('C');
            // 清空柱子C
            C.innerHTML = "";
            var htmlA = "";
            // 渲染柱子A
            for (var i = 0; i < number; i++) {
                htmlA += "<div style='width:" + 100 * ((i + 1) / number) + "%;background:" + randomColor() + "'></div>";
            }
            A.innerHTML = htmlA;
            hano(number, A, B, C);
        }
```
4.汉诺塔递归
```
// 执行汉诺塔递归函数
        function hano(n, A, B, C) {
            if (n == 1) {
                //汉诺塔移动代码
                moveHano(A,C);
            } else {
                hano(n - 1, A, C, B);
                hano(1, A, B, C);
                hano(n - 1, B, A, C);
            }
        }
```
5.汉诺塔移动

function moveHano(A, C) {
            // objA 内部第一个元素 objA.childNodes[0]
            debugger;
            if(C.childNodes[0]){
                C.insertBefore(A.childNodes[0],C.childNodes[0]);
            }else{
                C.appendChild(A.childNodes[0]);
            }
        }
四、完整代码
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>hano</title>
    <style>
        html,
        body {
            margin: 0;
            padding: 0;
            height: 100%;
        }
        .header > #number{
            display: inline-block;
            width: 80%;
            height: 28px;
            box-sizing: border-box;
            position: absolute;
            left: 0;
        }
        .header > #sure{
            display: inline-block;
            width: 20%;
            height: 28px;
            box-sizing: border-box;
            position: absolute;
            right: 0;
        }
        #contain{
            width: 100%;
            background: skyblue;
            padding: 10px;
            text-align: center;
            position: absolute;
            top: 28px;
            user-select: none;
        }
        .item{
            display: inline-block;
            box-sizing: border-box;
            background: #ffffff;
            border: 1px solid #ffffff;
            border-radius: 10px;
            width: 33%;
        }
        .item p{
            font-size: 20px;
            font-weight: bolder;
            border-top: 1px solid #ffffff;
            border-bottom: 1px solid #ffffff;
        }
        .item > .area div{
            margin: 0 auto; 
            height: 20px;
        }
    </style>
</head>

<body>
    <div class="header">
        <input id="number" type="text" placeholder="please input number...">
        <button id="sure">start</button>
    </div>
    <div id="contain">
        <p>there will be showing result for you.</p>
        <div>
            <div class="item">
                <p>A</p>
                <div class="area" id="A">
                </div>
            </div>
            <div class="item">
                <p>B</p>
                <div class="area" id="B">
                </div>
            </div>
            <div class="item">
                <p>C</p>
                <div class="area" id="C">
                </div>
            </div>
        </div>
    </div>
    <script>
        // 点击开始按钮事件
        var sure = document.getElementById('sure');
        sure.addEventListener('click', function () {
            init();
        })

        // 获取输入值
        function getNumber() {
            return document.getElementById('number').value;
        }

        // 渲染汉诺塔初始化
        function init() {
            // 生成三个柱子
            var number = getNumber();
            var A = document.getElementById('A');
            var B = document.getElementById('B');
            var C = document.getElementById('C');
            // 清空柱子C
            C.innerHTML = "";
            var htmlA = "";
            // 渲染柱子A
            for (var i = 0; i < number; i++) {
                htmlA += "<div style='width:" + 100 * ((i + 1) / number) + "%;background:" + randomColor() + "'></div>";
            }
            A.innerHTML = htmlA;
            hano(number, A, B, C);
        }

        // 生成随机颜色
        function randomColor() {
            var colors = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'];
            var color = '#';
            for (var i = 0; i < 6; i++) {
                color += colors[Math.floor(Math.random() * 16)]
            }
            return color;
        }

        // 执行汉诺塔
        function hano(n, A, B, C) {
            if (n == 1) {
                //汉诺塔移动代码
                moveHano(A,C);
            } else {
                hano(n - 1, A, C, B);
                hano(1, A, B, C);
                hano(n - 1, B, A, C);
            }
        }

        function moveHano(A, C) {
            // objA 内部第一个元素 objA.childNodes[0]
            debugger;
            if(C.childNodes[0]){
                C.insertBefore(A.childNodes[0],C.childNodes[0]);
            }else{
                C.appendChild(A.childNodes[0]);
            }
        }
    </script>
</body>

</html>          
```        