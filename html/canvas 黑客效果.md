> 利用 canvas，定时创建新的图层达到效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        html,body {
            overflow: hidden;
        }
    </style>
</head>

<body>
    <canvas id="canvas"></canvas>
    <script>
        const q = document.getElementById('canvas');

        const s = window.screen;
        const w = (q.width = s.width);
        const h = (q.height = s.height);
        const ctx = q.getContext("2d");

        const p = Array(Math.floor(w / 10) + 1).fill(0);

        
        // 乱序数组
        const random = (items) => items[Math.floor(Math.random() * items.length)];

        console.log(p)

        const hex = "0123456789ABCDEF".split("");

        // 通过不断建立层，达到模糊的效果
        setInterval(() => {
            ctx.fillStyle = "rgba(0,0,0,.05)";
            ctx.fillRect(0, 0, w, h);
            ctx.fillStyle = "#0f0";
            p.map((v, i) => {
                ctx.fillText(random(hex), i * 10, v);
                // 当超过屏幕或者  很大的时候，则需要重新设置，否则纵坐标自动+10
                p[i] = v >= h || v > 50 + 10000 * Math.random() ? 0 : v + 10;
            });
        }, 1000/30);
    </script>
</body>

</html>
```