<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>开奖展示 - 2025350期</title>
<meta name="viewport" content="width=device-width,initial-scale=1">
<style>
    *{margin:0;padding:0;box-sizing:border-box;font-family:-apple-system,"Helvetica Neue","PingFang SC",sans-serif}
    body{background:#0d1425;display:flex;justify-content:center;align-items:center;min-height:100vh;color:#fff}
    .box{width:94%;max-width:420px;background:#1a1f2e;border-radius:16px;padding:25px 20px 30px;box-shadow:0 8px 30px rgba(0,0,0,.4)}
    .tit{text-align:center;font-size:18px;margin-bottom:20px;letter-spacing:1px}
    .num-wrap{display:flex;justify-content:center;gap:10px;margin-bottom:25px}
    .ball{width:46px;height:46px;border-radius:50%;background:linear-gradient(135deg,#ff7b00,#ffaa00);color:#0d1425;font-size:22px;font-weight:700;line-height:46px;text-align:center;box-shadow:0 2px 6px rgba(255,123,0,.35)}
    .sx-wrap{display:flex;justify-content:center;gap:10px;flex-wrap:wrap}
    .sx{padding:6px 12px;border-radius:20px;background:rgba(255,255,255,.08);font-size:14px;color:#ffd66b}
    .cd{margin-top:25px;text-align:center;font-size:13px;color:#aaa}
    .cd span{color:#ffd66b;font-weight:700;font-size:16px}
</style>
</head>
<body>
<div class="box">
    <div class="tit">第 <span id="q">2025350</span> 期 开奖结果</div>

    <!-- 数字球 -->
    <div class="num-wrap" id="numWrap"></div>

    <!-- 生肖 -->
    <div class="sx-wrap" id="sxWrap"></div>

    <!-- 倒计时 -->
    <div class="cd">距下一期开奖还剩 <span id="cd">--:--</span></div>
</div>

<script>
/* ===== 模拟后台返回数据 ===== */
const data = {
    qihao: "2025350",
    numbers: ["07","22","42","35","16","47","49"],
    shengxiao: ["猪","猴","鼠","羊","虎","羊","蛇"],
    nextOpenTime: new Date("2025-12-20 21:30:00").getTime()
};

/* ===== 渲染 ===== */
document.getElementById('q').textContent = data.qihao;
data.numbers.forEach(n=>{
    const b=document.createElement('div');b.className='ball';b.textContent=n;
    document.getElementById('numWrap').appendChild(b);
});
data.shengxiao.forEach(s=>{
    const d=document.createElement('div');d.className='sx';d.textContent=s;
    document.getElementById('sxWrap').appendChild(d);
});

/* ===== 倒计时 ===== */
const cd=document.getElementById('cd');
function tick(){
    const left=Math.max(0,data.nextOpenTime-Date.now());
    const m=String(Math.floor(left/6e4)).padStart(2,'0');
    const s=String(Math.floor(left%6e4/1e3)).padStart(2,'0');
    cd.textContent=`${m}:${s}`;
    if(left<=0)location.reload();
}
tick();setInterval(tick,1000);
</script>
</body>
</html>

