<!doctype html>
<html lang="zh-CN">
<head>
<meta charset="utf-8">
<title>六合彩开奖板（无服务器版）</title>
<meta name="viewport" content="width=device-width,initial-scale=1">
<style>
:root{
  --red:#ff3b30; --blue:#007aff; --gap:10px;
}
body{margin:0;font-family:-apple-system,BlinkMacSystemFont,"Helvetica Neue",Arial;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);min-height:100vh;display:flex;justify-content:center;align-items:center;padding:20px}
.box{background:#fff;border-radius:20px;padding:30px 40px;box-shadow:0 15px 35px rgba(0,0,0,.2);text-align:center;max-width:600px;width:100%}
h1{margin:0 0 20px;font-size:28px}
.balls{display:flex;justify-content:center;gap:var(--gap);flex-wrap:wrap;margin:20px 0}
.ball{width:56px;height:56px;border-radius:50%;background:var(--red);color:#fff;font-size:22px;font-weight:bold;line-height:56px;box-shadow:0 4px 8px rgba(0,0,0,.2)}
.ball.special{background:var(--blue)}
#date{color:#666;margin-top:10px}
button{padding:10px 24px;border:none;border-radius:20px;background:#34c759;color:#fff;font-size:16px;cursor:pointer}
/* 后台面板 */
#adminPanel{display:none;background:#f8f9fa;border-radius:15px;padding:20px;margin-top:25px;text-align:left}
.row{margin-bottom:12px}label{display:inline-block;width:70px;font-weight:600}input{width:60px;padding:6px;border:1px solid #ccc;border-radius:6px;text-align:center}
</style>
</head>
<body>
<div class="box">
  <h1>六合彩开奖结果</h1>
  <div class="balls" id="balls"></div>
  <div id="date"></div>

  <!-- 控制区 -->
  <button onclick="location.hash='admin'">进入后台</button>
  <button onclick="clearDraw()">清空记录</button>

  <!-- 隐藏的后台录入面板 -->
  <div id="adminPanel">
    <h3 style="margin-top:0">后台录入</h3>
    <div class="row"><label>正选①</label><input id="n1" type="number" min="1" max="49"></div>
    <div class="row"><label>正选②</label><input id="n2" type="number" min="1" max="49"></div>
    <div class="row"><label>正选③</label><input id="n3" type="number" min="1" max="49"></div>
    <div class="row"><label>正选④</label><input id="n4" type="number" min="1" max="49"></div>
    <div class="row"><label>正选⑤</label><input id="n5" type="number" min="1" max="49"></div>
    <div class="row"><label>正选⑥</label><input id="n6" type="number" min="1" max="49"></div>
    <div class="row"><label>特别号</label><input id="sp" type="number" min="1" max="49"></div>
    <button onclick="saveDraw()">保存并公布</button>
    <button onclick="location.hash=''">关闭后台</button>
  </div>
</div>

<script>
/* ===== 工具函数 ===== */
const LS_KEY = 'lottery_draw';          // localStorage 键名
const $   = id => document.getElementById(id);
const randColor = () => `hsl(${Math.random()*360},70%,55%)`;

/* 读取本地开奖数据 */
function loadDraw(){
  const raw = localStorage.getItem(LS_KEY);
  if(!raw) return {numbers:[],special:null,date:null};
  return JSON.parse(raw);
}
/* 保存到本地 */
function saveDraw(){
  const nums = ['n1','n2','n3','n4','n5','n6'].map(id => parseInt($(id).value));
  const sp   = parseInt($('sp').value);
  if(nums.some(isNaN) || isNaN(sp)) return alert('请完整输入号码！');
  const set = new Set([...nums,sp]);
  if(set.size !== 7) return alert('号码重复或超出范围！');
  const data = {numbers:nums, special:sp, date:new Date().toLocaleString('zh-CN')};
  localStorage.setItem(LS_KEY, JSON.stringify(data));
  renderDraw(data);
  location.hash='';          // 保存后自动回到前台
}
/* 清空记录 */
function clearDraw(){
  if(confirm('确定清空当前记录？')){
    localStorage.removeItem(LS_KEY);
    renderDraw({numbers:[],special:null,date:null});
  }
}
/* 渲染号码球 */
function renderDraw(data){
  const box = $('balls');
  const dateBox = $('date');
  box.innerHTML = '';
  if(!data.numbers.length){
    box.innerHTML = '<p style="color:#999">等待开奖</p>';
    dateBox.textContent = '';
    return;
  }
  data.numbers.forEach(n => {
    const b = document.createElement('div');
    b.className = 'ball'; b.textContent = n.pad(2); box.appendChild(b);
  });
  const spBall = document.createElement('div');
  spBall.className = 'ball special'; spBall.textContent = data.special.pad(2);
  box.appendChild(spBall);
  dateBox.textContent = '开奖时间：' + data.date;
}
/* 补零 */
Number.prototype.pad = function(d){ return this<10?'0'+this:this; };

/* ===== 路由控制（hash = admin 则显示后台） ===== */
function route(){
  const isAdmin = location.hash === '#admin';
  $('adminPanel').style.display = isAdmin ? 'block' : 'none';
  if(isAdmin){          // 自动填上一次的数据，方便修改
    const d = loadDraw();
    ['n1','n2','n3','n4','n5','n6'].forEach((id,i)=> $(id).value = d.numbers[i]||'');
    $('sp').value = d.special||'';
  }
}
window.addEventListener('hashchange', route);
window.addEventListener('load', ()=>{ route(); renderDraw(loadDraw()); });

/* 每 5 秒自动刷新（支持多标签同时打开） */
setInterval(()=> renderDraw(loadDraw()), 5000);
</script>
</body>
</html>

