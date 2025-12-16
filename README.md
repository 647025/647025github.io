        澳门天天彩开奖信息网站
        22:30开奖 距离下次开奖
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>福彩3D 模拟滚动开奖</title>
<style>
body{background:#111;color:#fff;font-family:Arial;text-align:center;padding-top:80px}
#stage{font-size:72px;letter-spacing:20px}
#btn{margin-top:40px;padding:12px 30px;font-size:20px;border:none;background:#c9302c;color:#fff;border-radius:4px;cursor:pointer}
.rolling{animation:flip .08s infinite;}
@keyframes flip{0%{transform:translateY(0)}50%{transform:translateY(-8px)}100%{transform:translateY(0)}}
</style>
</head>
<body>
<div id="stage" class="rolling">000</div>
<button id="btn" onclick="start()">开始开奖</button>

<script>
const $=id=>document.getElementById(id);
let timer=null;
function rand(){return Math.floor(Math.random()*10);}
function start(){
  if(timer)return;                 // 防止重复点击
  $('btn').disabled=true;
  $('stage').classList.add('rolling');
  timer=setInterval(()=>{
      $('stage').textContent=''+rand()+rand()+rand();
  },80);
  setTimeout(()=>{                 // 5 秒后停止
      clearInterval(timer);timer=null;
      $('stage').classList.remove('rolling');
      $('btn').disabled=false;
  },5000);
}
</script>
</body>
</html>
