<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>专属告白</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft Yahei", sans-serif;
        }

        body {
            width: 100vw;
            height: 100vh;
            background: linear-gradient(160deg, #120420, #381028, #5a1f3b);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #fff;
            position: relative;
        }

        /* 中心跳动大爱心 */
        .big-heart {
            font-size: 120px;
            color: #ff5c8a;
            animation: beat 1s infinite ease-in-out;
            text-shadow: 0 0 40px #ff3366;
            margin-bottom: 30px;
        }

        @keyframes beat {
            0%, 100% {transform: scale(1);}
            50% {transform: scale(1.18);}
        }

        .title-text {
            font-size: 24px;
            margin-bottom: 40px;
            letter-spacing: 2px;
        }

        .btn-box {
            display: flex;
            gap: 30px;
        }

        button {
            width: 130px;
            height: 50px;
            border: none;
            border-radius: 30px;
            font-size: 18px;
            cursor: pointer;
            transition: 0.2s;
        }

        #yesBtn {
            background-color: #ff477e;
            color: #fff;
        }

        #noBtn {
            background-color: #eee;
            color: #333;
            position: relative;
        }

        /* 漂浮小爱心 */
        .float-heart {
            position: absolute;
            color: #ffb6c1;
            opacity: 0.7;
            animation: floatUp 8s linear infinite;
        }

        @keyframes floatUp {
            0% {transform: translateY(100vh) rotate(0deg); opacity: 0;}
            10% {opacity: 0.8;}
            90% {opacity: 0.7;}
            100% {transform: translateY(-15vh) rotate(360deg); opacity: 0;}
        }

        /* 成功告白全屏文字 */
        .success-box {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.85);
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 999;
            text-align: center;
            padding: 20px;
        }
        .success-box h1{
            font-size: 36px;
            color: #ff7799;
            margin-bottom: 20px;
        }
        .success-box p{
            font-size: 20px;
            line-height: 2;
        }
    </style>
</head>
<body>
    <div class="big-heart">♥</div>
    <div class="title-text">我喜欢你，做我的女朋友好吗？</div>
    <div class="btn-box">
        <button id="yesBtn">我愿意</button>
        <button id="noBtn">再考虑下</button>
    </div>

    <!-- 答应之后弹出的告白页面 -->
    <div class="success-box" id="success">
        <h1>太好了！🥰</h1>
        <p>往后四季三餐</p>
        <p>朝朝暮暮都想陪着你</p>
        <p>我的女孩，余生多多指教</p>
    </div>

    <script>
        // 持续生成漂浮爱心
        function createFloatHeart(){
            const heart = document.createElement('div');
            heart.classList.add('float-heart');
            heart.innerText = '♥';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.fontSize = 10 + Math.random() * 25 + 'px';
            heart.style.animationDuration = 5 + Math.random() * 6 + 's';
            document.body.appendChild(heart);
            setTimeout(()=>heart.remove(), 12000);
        }
        setInterval(createFloatHeart, 600);

        // 拒绝按钮自动躲避
        const noBtn = document.getElementById('noBtn');
        noBtn.addEventListener('mouseover', moveBtn);
        noBtn.addEventListener('touchstart', moveBtn);
        function moveBtn(){
            const maxX = window.innerWidth - noBtn.offsetWidth;
            const maxY = window.innerHeight - noBtn.offsetHeight;
            noBtn.style.left = Math.random() * maxX + 'px';
            noBtn.style.top = Math.random() * maxY + 'px';
        }

        // 点击同意触发告白弹窗
        document.getElementById('yesBtn').onclick = function(){
            document.getElementById('success').style.display = 'flex';
            createFireworks();
        }

        // 简易礼花效果
        function createFireworks(){
            for(let i=0;i<80;i++){
                let dot = document.createElement('div');
                dot.style.position = 'fixed';
                dot.style.width = '6px';
                dot.style.height = '6px';
                dot.style.borderRadius = '50%';
                dot.style.backgroundColor = ['#ff477e','#ffdd00','#4cd964','#5ac8fa','#fff'][Math.floor(Math.random()*5)];
                dot.style.left = '50%';
                dot.style.top = '50%';
                document.body.appendChild(dot);
                let tx = (Math.random()-0.5)*600;
                let ty = (Math.random()-0.5)*600;
                dot.animate([
                    {transform:'translate(0,0)', opacity:1},
                    {transform:`translate(${tx}px,${ty}px)`, opacity:0}
                ], {duration: 1200});
                setTimeout(()=>dot.remove(), 1200);
            }
        }
    </script>
</body>
</html>
