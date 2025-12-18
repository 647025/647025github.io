<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>开奖结果展示</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh;
            color: white;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .countdown-section {
            background: rgba(255,255,255,0.1);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 40px;
            backdrop-filter: blur(10px);
            text-align: center;
        }

        .countdown-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
        }

        .countdown-timer {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        .time-unit {
            background: rgba(255,255,255,0.2);
            border-radius: 15px;
            padding: 20px;
            min-width: 100px;
            text-align: center;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255,255,255,0.3);
        }

        .time-number {
            font-size: 3rem;
            font-weight: bold;
            display: block;
            line-height: 1;
        }

        .time-label {
            font-size: 0.9rem;
            opacity: 0.8;
            margin-top: 5px;
        }

        .results-section {
            background: rgba(255,255,255,0.1);
            border-radius: 20px;
            padding: 30px;
            backdrop-filter: blur(10px);
        }

        .result-card {
            background: rgba(255,255,255,0.15);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255,255,255,0.2);
            animation: fadeInUp 0.6s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .result-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .lottery-type {
            font-size: 1.5rem;
            font-weight: bold;
        }

        .issue-info {
            font-size: 1rem;
            opacity: 0.8;
        }

        .numbers-display {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .number-ball {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff6b6b, #ee5a52);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            animation: bounceIn 0.6s ease-out;
            transition: transform 0.3s ease;
        }

        .number-ball:hover {
            transform: scale(1.1);
        }

        .number-ball.special {
            background: linear-gradient(135deg, #4ecdc4, #44a08d);
        }

        @keyframes bounceIn {
            0% {
                opacity: 0;
                transform: scale(0.3);
            }
            50% {
                transform: scale(1.05);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }

        .no-results {
            text-align: center;
            padding: 60px 20px;
            opacity: 0.8;
        }

        .no-results h3 {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }

        .loading {
            text-align: center;
            padding: 40px;
        }

        .spinner {
            border: 4px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top: 4px solid white;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .countdown-timer {
                gap: 10px;
            }
            
            .time-unit {
                min-width: 80px;
                padding: 15px;
            }
            
            .time-number {
                font-size: 2rem;
            }
            
            .numbers-display {
                gap: 10px;
            }
            
            .number-ball {
                width: 50px;
                height: 50px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎰 开奖结果展示</h1>
            <p>实时开奖信息，精彩不容错过</p>
        </div>

        <div class="countdown-section">
            <h2 class="countdown-title">⏰ 下次开奖倒计时</h2>
            <div class="countdown-timer" id="countdownTimer">
                <div class="time-unit">
                    <span class="time-number" id="days">00</span>
                    <span class="time-label">天</span>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="hours">00</span>
                    <span class="time-label">时</span>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="minutes">00</span>
                    <span class="time-label">分</span>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="seconds">00</span>
                    <span class="time-label">秒</span>
                </div>
            </div>
        </div>

        <div class="results-section">
            <div id="resultsContainer">
                <div class="loading">
                    <div class="spinner"></div>
                    <p>正在加载最新开奖结果...</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        class LotteryDisplay {
            constructor() {
                this.resultsContainer = document.getElementById('resultsContainer');
                this.countdownTimer = document.getElementById('countdownTimer');
                this.countdownInterval = null;
                
                this.init();
            }

            init() {
                this.loadResults();
                this.startCountdown();
                
                // 每30秒刷新一次结果
                setInterval(() => this.loadResults(), 30000);
            }

            loadResults() {
                try {
                    const results = JSON.parse(localStorage.getItem('lotteryResults') || '[]');
                    const sortedResults = results.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
                    
                    if (sortedResults.length === 0) {
                        this.showNoResults();
                    } else {
                        this.displayResults(sortedResults.slice(0, 5)); // 显示最近5条
                    }
                } catch (error) {
                    this.showError();
                }
            }

            displayResults(results) {
                const html = results.map(result => this.createResultCard(result)).join('');
                this.resultsContainer.innerHTML = html;
            }

            createResultCard(result) {
                const typeNames = {
                    'ssq': '双色球',
                    'dlt': '大乐透',
                    '3d': '福彩3D',
                    'pl3': '排列三'
                };

                const typeConfig = {
                    'ssq': { main: 6, special: 1 },
                    'dlt': { main: 5, special: 2 },
                    '3d': { main: 3, special: 0 },
                    'pl3': { main: 3, special: 0 }
                };

                const config = typeConfig[result.type];
                const mainNumbers = result.numbers.slice(0, config.main);
                const specialNumbers = result.numbers.slice(config.main);

                const mainBalls = mainNumbers.map(num => 
                    `<div class="number-ball">${num.padStart(2, '0')}</div>`
                ).join('');

                const specialBalls = specialNumbers.map(num => 
                    `<div class="number-ball special">${num.padStart(2, '0')}</div>`
                ).join('');

                return `
                    <div class="result-card">
                        <div class="result-header">
                            <div class="lottery-type">${typeNames[result.type]}</div>
                            <div class="issue-info">第 ${result.issue} 期 | ${result.date}</div>
                        </div>
                        <div class="numbers-display">
                            ${mainBalls}
                            ${specialBalls}
                        </div>
                    </div>
                `;
            }

            showNoResults() {
                this.resultsContainer.innerHTML = `
                    <div class="no-results">
                        <h3>🎲 暂无开奖结果</h3>
                        <p>请等待管理员发布最新开奖信息</p>
                    </div>
                `;
            }

            showError() {
                this.resultsContainer.innerHTML = `
                    <div class="no-results">
                        <h3>❌ 加载失败</h3>
                        <p>请刷新页面重试</p>
                    </div>
                `;
            }

            startCountdown() {
                // 设置下次开奖时间为今天晚上9点
                const now = new Date();
                const nextDraw = new Date();
                nextDraw.setHours(21, 0, 0, 0);
                
                if (now > nextDraw) {
                    nextDraw.setDate(nextDraw.getDate() + 1);
                }

                this.updateCountdown(nextDraw);
                this.countdownInterval = setInterval(() => this.updateCountdown(nextDraw), 1000);
            }

            updateCountdown(targetDate) {
                const now = new Date().getTime();
                const distance = targetDate.getTime() - now;

                if (distance < 0) {
                    clearInterval(this.countdownInterval);
                    this.startCountdown(); // 重新开始下一个倒计时
                    return;
                }

                const days = Math.floor(distance / (1000 * 60 * 60 * 24));
                const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((distance % (1000 * 60)) / 1000);

                document.getElementById('days').textContent = days.toString().padStart(2, '0');
                document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
                document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
                document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
            }
        }

        // 初始化展示界面
        new LotteryDisplay();
    </script>
</body>
</html>


