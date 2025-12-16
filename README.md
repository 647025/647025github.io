澳门天天彩开奖信息网站
<span id="fcd3d"></span>
<script>
function pad(n){return n<10?'0'+n:n;}
function tick(){
  var now=new Date();
  var end=new Date();
  end.setHours(21,15,0,0);
  if(now>end) end.setDate(end.getDate()+1);   // 若已开奖则算次日
  var t=end-now;
  var h=Math.floor(t/36e5);
  var m=Math.floor(t%36e5/6e4);
  var s=Math.floor(t%6e4/1e3);
  document.getElementById('fcd3d').textContent=
    '距福彩3D开奖还有 '+pad(h)+':'+pad(m)+':'+pad(s);
}
tick(); setInterval(tick,1000);
</script>
