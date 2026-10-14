# 2026_ds
test repository for ds

<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ラッキーナンバー抽選</title>
    <style>
        body {
            font-family: 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            background: #ffffff;
            padding: 40px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 400px;
            width: 100%;
        }

        h1 {
            margin-bottom: 24px;
            color: #333;
            font-size: 24px;
        }

        .slot-machine {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
        }

        .slot {
            width: 70px;
            height: 90px;
            background: #f0f4f8;
            border: 3px solid #d1d9e6;
            border-radius: 12px;
            font-size: 48px;
            font-weight: bold;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #333;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
            transition: transform 0.1s ease;
        }

        button {
            background-color: #ff6b6b;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.4);
            transition: background-color 0.2s, transform 0.1s;
        }

        button:hover {
            background-color: #ff5252;
        }

        button:active {
            transform: scale(0.95);
        }

        .message {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
            min-height: 30px;
        }

        /* 当たり演出のアニメーション */
        .win {
            animation: bounce 0.5s ease infinite alternate;
            color: #ff3838 !important;
            border-color: #ff3838 !important;
            background-color: #fff0f0 !important;
        }

        @keyframes bounce {
            0% { transform: translateY(0); }
            100% { transform: translateY(-10px); }
        }

        .jackpot-text {
            color: #e74c3c;
            animation: pulse 0.5s ease infinite alternate;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            100% { transform: scale(1.1); }
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>ラッキーナンバー抽選</h1>
        
        <div class="slot-machine">
            <div class="slot" id="slot1">0</div>
            <div class="slot" id="slot2">0</div>
            <div class="slot" id="slot3">0</div>
        </div>

        <button id="spinButton">まわす</button>
        
        <div class="message" id="message"></div>
    </div>

    <script>
        const spinButton = document.getElementById('spinButton');
        const slots = [
            document.getElementById('slot1'),
            document.getElementById('slot2'),
            document.getElementById('slot3')
        ];
        const message = document.getElementById('message');

        spinButton.addEventListener('click', () => {
            // 当たり演出を一旦リセット
            slots.forEach(slot => slot.classList.remove('win'));
            message.textContent = '';
            message.className = 'message';

            // 演出として、少しの間数字をパタパタと変える（アニメーション風）
            let count = 0;
            const interval = setInterval(() => {
                slots.forEach(slot => {
                    slot.textContent = Math.floor(Math.random() * 10);
                });
                count++;

                // 10回切り替えたら確定
                if (count > 10) {
                    clearInterval(interval);
                    
                    // 最終的なランダムな数字を決定（0〜9）
                    const results = slots.map(slot => {
                        const num = Math.floor(Math.random() * 10);
                        slot.textContent = num;
                        return num;
                    });

                    // ゾロ目判定（3つの数字がすべて同じ）
                    if (results[0] === results[1] && results[1] === results[2]) {
                        // 当たり演出のクラスを付与
                        slots.forEach(slot => slot.classList.add('win'));
                        message.textContent = '🎉 大当たり！おめでとうございます！ 🎉';
                        message.classList.add('jackpot-text');
                    } else {
                        message.textContent = '残念…もう一度挑戦！';
                    }
                }
            }, 50); // 切り替えの間隔（ミリ秒）
        });
    </script>

</body>
</html>
