# the-memory-pool
一个背单词网站.......只是作业，仅个人使用
<!doctype html>
<html lang="zh"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>THE MEMORY POOL</title>
<style>
:root{--ink:#eafaf6;--glass:rgba(22,62,68,.58);--line:rgba(205,248,242,.38);--acc:#a6ebdf;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--glass:rgba(8,26,32,.66)}}
:root[data-theme="dark"]{--glass:rgba(8,26,32,.66)}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
html,body{height:100%;margin:0;background:#0f2a2f;color:var(--ink);font:15px/1.7 "Noto Serif SC","Songti SC","STSong",Georgia,serif;overflow:hidden}
canvas{display:block;position:fixed;inset:0;width:100%;height:100%;touch-action:none;cursor:pointer}
#vig{position:fixed;inset:0;pointer-events:none;background:radial-gradient(ellipse at 50% 55%,transparent 45%,rgba(4,10,12,.55) 100%);z-index:1}
#hud{position:fixed;top:calc(env(safe-area-inset-top,0px) + 14px);left:16px;right:16px;display:flex;justify-content:space-between;align-items:flex-start;pointer-events:none;text-shadow:0 1px 12px rgba(10,50,56,.7)}
#hud h1{margin:0;font-size:19px;font-weight:400;letter-spacing:.32em}
#hud small{display:block;opacity:.85;letter-spacing:.08em;font-style:italic}
#chip{text-align:right;font-size:13px}
nav{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(env(safe-area-inset-bottom,0px) + 14px);display:flex;gap:2px;background:var(--glass);border:1px solid var(--line);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);padding:4px;border-radius:30px;max-width:calc(100vw - 20px);overflow-x:auto}
button,select,input,textarea{font:inherit;color:inherit}
nav button{background:none;border:0;padding:7px 13px;border-radius:24px;cursor:pointer;white-space:nowrap;font-size:14px}
nav button.a{background:rgba(255,255,255,.24)}
#hint{position:fixed;bottom:calc(env(safe-area-inset-bottom,0px) + 70px);width:100%;text-align:center;font-size:13px;opacity:.9;pointer-events:none;text-shadow:0 1px 10px rgba(10,50,56,.8);transition:opacity .6s}
#snd{position:fixed;top:calc(env(safe-area-inset-top,0px) + 56px);right:14px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:3px 11px;cursor:pointer;font-size:13px}
#lt{position:fixed;top:calc(env(safe-area-inset-top,0px) + 224px);right:14px;display:flex;align-items:center;gap:8px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:3px 11px;font-size:13px}#lt input{width:84px;margin:0;padding:0;accent-color:#a6ebdf}#lt button{background:none;border:0;cursor:pointer;padding:0}
#wv{position:fixed;top:calc(env(safe-area-inset-top,0px) + 92px);right:14px;display:flex;align-items:center;gap:8px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:3px 11px;font-size:13px}#wv input{width:84px;margin:0;padding:0;accent-color:#a6ebdf}
#av{position:fixed;top:calc(env(safe-area-inset-top,0px) + 136px);right:14px;display:flex;align-items:center;gap:8px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:3px 11px;font-size:13px}#av input{width:84px;margin:0;padding:0;accent-color:#a6ebdf}
#mv{position:fixed;top:calc(env(safe-area-inset-top,0px) + 180px);right:14px;display:flex;align-items:center;gap:8px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:3px 11px;font-size:13px}#mv input{width:84px;margin:0;padding:0;accent-color:#a6ebdf}
#mv select{background:rgba(0,0,0,.25);color:var(--ink);border:1px solid var(--line);border-radius:10px;font-size:12px;max-width:120px;padding:2px 4px}
#mv button{background:none;border:1px solid var(--line);border-radius:50%;width:20px;height:20px;line-height:1;color:var(--ink);cursor:pointer;padding:0}
#uiT{position:fixed;top:calc(env(safe-area-inset-top,0px) + 268px);right:14px;background:var(--glass);border:1px solid var(--line);border-radius:20px;padding:5px 13px;font-size:13px;cursor:pointer;z-index:50}
body.hu nav,body.hu #snd,body.hu #wv,body.hu #av,body.hu #mv,body.hu #lt,body.hu #hint,body.hu #panel,body.hu #card,body.hu #chip,body.hu #moodAdd{display:none!important}
#moodAdd{position:fixed;top:calc(env(safe-area-inset-top,0px) + 122px);left:16px;display:flex;gap:8px;z-index:20}
#moodAdd button{width:38px;height:38px;border-radius:50%;border:1px solid var(--line);cursor:pointer;display:flex;align-items:center;justify-content:center;background:var(--glass);color:var(--ink);-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px)}
#moodAdd svg{width:19px;height:19px}
#clk{position:fixed;top:calc(env(safe-area-inset-top,0px) + 62px);left:16px;display:flex;flex-direction:column;align-items:flex-start;gap:6px;font-size:13px;opacity:.9;text-shadow:0 1px 10px rgba(10,50,56,.7)}
#clk .row{display:flex;align-items:center;gap:10px}
#clk button{background:none;border:1px solid var(--line);border-radius:14px;color:inherit;font-size:12px;padding:2px 10px;cursor:pointer}
.box{position:fixed;left:50%;top:50%;width:min(560px,calc(100vw - 28px));max-height:70vh;overflow-y:auto;transform:translate(-50%,-48%);background:var(--glass);border:1px solid var(--line);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);padding:22px 26px;border-radius:6px;opacity:0;visibility:hidden;transition:opacity .7s,transform .7s,visibility .7s;box-sizing:border-box}
.box.on{opacity:1;visibility:visible;transform:translate(-50%,-50%)}
.box h2{margin:0 0 8px;font-weight:400;font-size:24px;letter-spacing:.12em}
.box h3{font-weight:400;font-size:20px;margin:12px 0}
.dim{opacity:.75}.ex{font-style:italic;opacity:.9}
.x{position:absolute;right:12px;top:6px;background:none;border:0;font-size:22px;cursor:pointer}
.box button{border:1px solid var(--line);background:rgba(255,255,255,.12);padding:8px 16px;border-radius:3px;cursor:pointer;margin:4px 6px 4px 0}
.box button.x{border:0;background:none;padding:0 6px}
.box button.pri{background:rgba(166,235,223,.28)}
.box button.opt{display:block;width:100%;text-align:left}
.box button.ok{background:rgba(150,240,190,.35)}.box button.bad{background:rgba(255,150,130,.35)}
input[type=text],textarea,select{width:100%;box-sizing:border-box;background:rgba(0,0,0,.18);border:1px solid var(--line);padding:8px;border-radius:3px;margin:6px 0}
.bar{display:flex;align-items:center;gap:8px;margin:4px 0;font-size:13px}.bar i{display:block;height:10px;background:var(--acc);opacity:.8;border-radius:2px}
.tag{font-size:12px;border:1px solid var(--line);padding:0 6px;border-radius:9px;margin-left:6px}
@media(prefers-reduced-motion:reduce){.box{transition:none}}
</style></head><body>
<canvas id="cv"></canvas>
<div id="vig"></div>
<div id="hud"><div><h1>THE MEMORY POOL</h1><small>Every word leaves a trace.</small></div><div id="chip"></div></div>
<div id="clk"><div class="row"><span id="clkTime">--:--</span><span id="clkTimer">00:00:00</span></div><div class="row"><button id="tmrBtn">开始计时</button><button id="tmrReset">归零</button></div></div>
<button id="snd">♪ 环境音 关</button>
<div id="wv"><span>水声</span><input type="range" id="wvs" min="0" max="150" value="100" aria-label="水声音量"></div>
<div id="av"><span>环境音</span><input type="range" id="avs" min="0" max="150" value="100" aria-label="环境音音量"></div>
<div id="mv"><span>音乐</span><input type="range" id="mvs" min="0" max="100" value="45" aria-label="背景音乐音量">
<select id="trkSel" aria-label="选择曲目"></select>
<button id="trkAdd" title="添加本地音乐">+</button>
<input type="file" id="trkFile" accept="audio/*" style="display:none">
</div>
<button id="uiT">收起界面</button>
<audio id="bgm" loop preload="none"></audio>
<div id="lt"><span>窗光</span><input type="range" id="ls" min="0" max="100" value="70" aria-label="窗光亮度"><button id="la">跟随时间：关</button></div>
<div id="hint">点击水面的物件查看单词档案 · 点击水面泛起涟漪 · 沉在水底的词正等待复习</div>
<div class="box" id="panel"></div><div class="box" id="card"></div>
<nav><button data-r="pool" class="a">记忆泳池</button><button data-r="study">学习室</button><button data-r="review">复习回廊</button><button data-r="archive">水下档案室</button><button data-r="obs">观测室</button></nav>
<div id="moodAdd"><button id="moodHappy" title="记录今天的好心情"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="12" r="9.3"/><circle cx="8.7" cy="10" r="1" fill="currentColor" stroke="none"/><circle cx="15.3" cy="10" r="1" fill="currentColor" stroke="none"/><path d="M8 14.5c1 1.3 2.4 2 4 2s3-.7 4-2"/></svg></button><button id="moodSad" title="记录今天的不开心"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="12" r="9.3"/><circle cx="8.7" cy="10" r="1" fill="currentColor" stroke="none"/><circle cx="15.3" cy="10" r="1" fill="currentColor" stroke="none"/><path d="M8 16c1-1.3 2.4-2 4-2s3 .7 4 2"/></svg></button></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
const $=s=>document.querySelector(s),DAY=864e5,K="mp_v1",now=()=>Date.now();
const esc=s=>String(s==null?"":s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
const shuf=a=>a.map(x=>[Math.random(),x]).sort((p,q)=>p[0]-q[0]).map(p=>p[1]);
const iso=d=>d.toLocaleDateString("sv");
/* ---------- data: word info and learning progress live in one local store, edited fields never reset progress ---------- */
const SEED=`ubiquitous|juːˈbɪkwɪtəs|adj|无处不在的|present everywhere at the same time|Smartphones are ubiquitous in modern life.|IELTS
mitigate|ˈmɪtɪɡeɪt|v|减轻，缓和|to make something less severe|Planting trees can mitigate the heat of cities.|IELTS
ambiguous|æmˈbɪɡjuəs|adj|模棱两可的|open to more than one interpretation|The question was deliberately ambiguous.|IELTS
scarce|skeəs|adj|稀缺的|not enough to meet a demand|Fresh water is scarce in the region.|IELTS
mitochondria|ˌmaɪtəˈkɒndriə|n|线粒体|organelles that release energy for the cell as ATP|Mitochondria are called the powerhouse of the cell.|Biology
ribosome|ˈraɪbəsəʊm|n|核糖体|a cell structure where proteins are made|The ribosome translates mRNA into protein.|Biology
photosynthesis|ˌfəʊtəʊˈsɪnθəsɪs|n|光合作用|the process by which plants make food using light|Photosynthesis takes place in the chloroplasts.|Biology
momentum|məˈmentəm|n|动量|the product of mass and velocity|The momentum of the car doubled as it accelerated.|Physics
wavelength|ˈweɪvleŋθ|n|波长|the distance between two successive wave peaks|Red light has a longer wavelength than blue light.|Physics
refraction|rɪˈfrækʃn|n|折射|the bending of light as it passes between media|Refraction makes a straw look bent in water.|Physics
covalent|kəʊˈveɪlənt|adj|共价的|relating to a bond formed by shared electrons|Water contains covalent bonds.|Chemistry
catalyst|ˈkætəlɪst|n|催化剂|a substance that speeds up a reaction without being used up|Platinum acts as a catalyst in the reaction.|Chemistry
tessellate|ˈtesəleɪt|v|镶嵌，铺砌|to cover a surface with repeated shapes|The floor tiles tessellate perfectly.|Mathematics`;
function seed(){const t=now(),I=[[25,0,1],[8,0,1],[3,0,-1],[1,0,-0.2],[0,2,-10],[3,0,2],[0,0,0.5]];
 const words=SEED.split("\n").map((l,i)=>{const p=l.split("|"),s=I[i];return{w:p[0],ph:p[1],pos:p[2],zh:p[3],def:p[4],ex:p[5],cat:p[6],learned:!!s,ease:s&&s[1]?1.9:2.5,int:s?s[0]:0,lapses:s?s[1]:0,due:s?t+s[2]*DAY:0}});
 return{words,st:{tot:0,ok:0,act:{},nw:{}}}}
let S;try{S=JSON.parse(localStorage.getItem(K))}catch(e){}
if(!S||!S.words)S=seed();
if(!S.moods)S.moods=[];
const save=()=>{try{localStorage.setItem(K,JSON.stringify(S))}catch(e){}};
const MN=["未学习","已学习","尚不熟悉","基本掌握","熟练掌握"];
function mast(x){if(!x.learned)return 0;if(x.int>=21)return 4;if(x.int>=6)return 3;if(x.lapses>0&&x.int<3||x.ease<2.2)return 2;return 1}
const isDue=x=>x.learned&&x.due<=now(),isSunk=x=>x.learned&&now()-x.due>7*DAY;
function grade(w,ok){const t=now(),d=iso(new Date()),st=S.st;st.tot++;if(ok)st.ok++;st.act[d]=(st.act[d]||0)+1;
 if(!w.learned){w.learned=true;st.nw[d]=(st.nw[d]||0)+1}
 if(ok){w.ease=Math.min(3,w.ease+.05);w.int=w.int<1?1:w.int<2?3:Math.round(w.int*w.ease);w.due=t+w.int*DAY}
 else{w.lapses++;w.ease=Math.max(1.3,w.ease-.2);w.int=0;w.due=t+6e5}save();hud()}
function speak(t,l){try{speechSynthesis.cancel();const u=new SpeechSynthesisUtterance(t);u.lang=l;u.rate=.85;speechSynthesis.speak(u)}catch(e){}}
function hud(){const h=S.moods.filter(m=>m.type==="happy").length,sd=S.moods.filter(m=>m.type==="sad").length;$("#chip").innerHTML=`心情记录 ${S.moods.length}<br>😊 ${h} · 🙁 ${sd}`}

/* ---------- three.js scene ---------- */
const cv=$("#cv"),bgm=$("#bgm"),R=new THREE.WebGLRenderer({canvas:cv,antialias:true});R.setPixelRatio(Math.min(devicePixelRatio,2));R.outputEncoding=THREE.sRGBEncoding;R.toneMapping=THREE.ACESFilmicToneMapping;R.toneMappingExposure=1.15;
const scene=new THREE.Scene(),bg=new THREE.Color(0x404f58);scene.background=bg;scene.fog=new THREE.FogExp2(0x404f58,.02);
const camera=new THREE.PerspectiveCamera(60,1,.1,200);
function rs(){R.setSize(innerWidth,innerHeight,false);camera.aspect=innerWidth/innerHeight;camera.updateProjectionMatrix()}addEventListener("resize",rs);rs();
const HL=new THREE.HemisphereLight(0xaebcc4,0x232d33,.42);scene.add(HL);
let LT,AUTO=false,LV=.7,LVc=.7;{const wm=new THREE.MeshBasicMaterial({color:0xeef3f5,fog:false}),fm=new THREE.MeshBasicMaterial({color:0x232d33});
 const win=new THREE.Mesh(new THREE.PlaneGeometry(7,7),wm);win.rotation.x=Math.PI/2;win.position.set(0,14.9,-5);scene.add(win);
 [[.3,7],[7,.3]].forEach(s=>{const b=new THREE.Mesh(new THREE.BoxGeometry(s[0],.25,s[1]),fm);b.position.set(0,14.75,-5);scene.add(b)});
 const sp=new THREE.SpotLight(0xeaf2f2,1.7,90,.85,1,1);sp.position.set(0,14.85,-5);sp.target.position.set(0,-2,-5);scene.add(sp);scene.add(sp.target);
 const pl=new THREE.PointLight(0xdbeaec,.7,34);pl.position.set(0,13.5,-5);scene.add(pl);
 const shaft=new THREE.Mesh(new THREE.CylinderGeometry(3.2,6.5,16,24,1,true),new THREE.MeshBasicMaterial({color:0xeaf5f5,transparent:true,opacity:.05,blending:THREE.AdditiveBlending,side:THREE.DoubleSide,depthWrite:false}));shaft.position.set(0,6,-5);scene.add(shaft);LT={wm,sp,pl,shaft}}
function makeMarble(base,vein,rx,ry){const c=document.createElement("canvas");c.width=c.height=256;const g=c.getContext("2d");
 g.fillStyle=base;g.fillRect(0,0,256,256);
 for(let i=0;i<9;i++){g.strokeStyle=vein;g.globalAlpha=.07+Math.random()*.09;g.lineWidth=1+Math.random()*2;
  g.beginPath();let x=Math.random()*256,y=Math.random()*256;g.moveTo(x,y);
  for(let j=0;j<5;j++){x+=(Math.random()-.5)*130;y+=(Math.random()-.5)*130;g.lineTo(x,y)}
  g.stroke()}
 g.globalAlpha=1;const tex=new THREE.CanvasTexture(c);tex.wrapS=tex.wrapT=THREE.RepeatWrapping;tex.repeat.set(rx,ry);return tex}
const wallTex=makeMarble("#8d99a0","#5f6e76",7,3.2),colTex=makeMarble("#8e9aa1","#616f77",1,5);
const std=(c,o={})=>new THREE.MeshStandardMaterial(Object.assign({color:o.map?0xffffff:c,roughness:.8,metalness:.05},o));
const hall=new THREE.Mesh(new THREE.BoxGeometry(44,18,44),std(0x8d99a0,{side:THREE.BackSide,map:wallTex}));hall.position.y=6;scene.add(hall);
const cvs=document.createElement("canvas");cvs.width=cvs.height=128;{const g=cvs.getContext("2d");const grd=g.createLinearGradient(0,0,128,128);grd.addColorStop(0,"#5b6d74");grd.addColorStop(1,"#4a5a60");g.fillStyle=grd;g.fillRect(0,0,128,128);
 for(let i=0;i<40;i++){g.fillStyle=`rgba(255,255,255,${Math.random()*.035})`;g.fillRect(Math.random()*128,Math.random()*128,Math.random()*28,Math.random()*28)}
 g.strokeStyle="#7c9298";g.lineWidth=5;g.strokeRect(0,0,128,128);g.strokeStyle="rgba(255,255,255,.12)";g.lineWidth=2;g.strokeRect(4,4,120,120)}
const tt=new THREE.CanvasTexture(cvs);tt.wrapS=tt.wrapT=THREE.RepeatWrapping;tt.repeat.set(44,44);
const fl=new THREE.Mesh(new THREE.PlaneGeometry(44,44),new THREE.MeshStandardMaterial({map:tt,roughness:.4}));fl.rotation.x=-Math.PI/2;fl.position.y=-2.95;scene.add(fl);
[[-16,-8],[16,-8],[-16,6],[16,6]].forEach(p=>{const c=new THREE.Mesh(new THREE.CylinderGeometry(1.1,1.1,15,28),std(0x8e9aa1,{map:colTex}));c.position.set(p[0],4.5,p[1]);scene.add(c)});
[[-22,-8,0],[-22,8,0],[22,-8,Math.PI],[22,8,Math.PI]].forEach(p=>{[[7,1.4,0x98a4aa,7],[7.25,.45,0x707e85,6.7]].forEach(q=>{const b=new THREE.Mesh(new THREE.CylinderGeometry(q[0],q[0],q[1],40,1,false,0,Math.PI),std(q[2],{map:wallTex}));b.position.set(p[0],q[3],p[1]);b.rotation.y=p[2];scene.add(b)})});
const br=new THREE.Mesh(new THREE.BoxGeometry(40,.8,3),std(0xeee3c8));br.visible=false;br.position.set(0,6.4,-17);scene.add(br);
for(let i=0;i<0;i++){const d=new THREE.Mesh(new THREE.BoxGeometry(1.6,3.4,.3),std(0x28484d));d.position.set(i*5.5,1.7,21.9);scene.add(d)}
[].forEach(p=>{const s=new THREE.Mesh(new THREE.PlaneGeometry(7,7),new THREE.MeshBasicMaterial({color:0xffffff,fog:false}));s.rotation.x=Math.PI/2;s.position.set(p[0],14.9,p[1]);scene.add(s);
 const pl=new THREE.PointLight(0xf4fffb,.55,38);pl.position.set(p[0],12,p[1]);scene.add(pl);
 const sh=new THREE.Mesh(new THREE.CylinderGeometry(3,5.5,15,24,1,true),new THREE.MeshBasicMaterial({color:0xffffff,transparent:true,opacity:.06,blending:THREE.AdditiveBlending,side:THREE.DoubleSide,depthWrite:false}));sh.position.set(p[0],7.4,p[1]);scene.add(sh)});

/* ---------- WebGL water: wave-equation heightfield -> texture -> shader normals + fresnel reflection ---------- */
const N=128,SZ=44;let A=new Float32Array(N*N),B=new Float32Array(N*N),waterE=0;const tex=new Uint8Array(N*N*4).fill(128);
const ht=new THREE.DataTexture(tex,N,N,THREE.RGBAFormat);ht.magFilter=ht.minFilter=THREE.LinearFilter;ht.needsUpdate=true;
const WU={h:{value:ht},t:{value:0},L:{value:1},sun:{value:new THREE.Vector3(0,1,-.12)}};
const water=new THREE.Mesh(new THREE.PlaneGeometry(SZ,SZ),new THREE.ShaderMaterial({uniforms:WU,transparent:true,side:THREE.DoubleSide,
vertexShader:"varying vec2 vUv;varying vec3 vW;void main(){vUv=uv;vW=(modelMatrix*vec4(position,1.)).xyz;gl_Position=projectionMatrix*viewMatrix*vec4(vW,1.);}",
fragmentShader:`uniform sampler2D h;uniform float t;uniform float L;uniform vec3 sun;varying vec2 vUv;varying vec3 vW;
void main(){float e=1./128.;
float hl=texture2D(h,vUv-vec2(e,0.)).r,hr=texture2D(h,vUv+vec2(e,0.)).r,hd=texture2D(h,vUv-vec2(0.,e)).r,hu=texture2D(h,vUv+vec2(0.,e)).r;
vec3 n=normalize(vec3((hl-hr)*8.,1.,(hu-hd)*8.));vec2 p=vW.xz;
n=normalize(n);
vec3 v=normalize(cameraPosition-vW);vec3 r=reflect(-v,n);
float f=pow(1.-abs(dot(v,n)),3.)*.8+.1;
vec3 sky=mix(vec3(.16,.21,.25),vec3(.52,.59,.62),smoothstep(0.,1.,abs(r.y)));
float dd=max(dot(r,normalize(sun)),0.);float s=(pow(dd,160.)*3.+pow(dd,12.)*.35)*L;
vec3 col=mix(vec3(.07,.18,.22),sky,f)+s*vec3(.85,.93,.95);gl_FragColor=vec4(col,mix(.6,.95,f));}`}));
water.rotation.x=-Math.PI/2;scene.add(water);
let REST=0,SETTLED=true;
function drop(x,z,s){const cx=((x/SZ+.5)*N)|0,cy=((.5-z/SZ)*N)|0;for(let j=-3;j<=3;j++)for(let i=-3;i<=3;i++){const X=cx+i,Y=cy+j;if(X>0&&X<N-1&&Y>0&&Y<N-1)A[Y*N+X]-=s*Math.max(0,1-Math.hypot(i,j)/3.3)}}
function sim(){let mx=0;for(let i=0;i<N*N;i+=7){const v=A[i]<0?-A[i]:A[i];if(v>mx)mx=v}waterE+=(mx-waterE)*.2;if(mx<6e-4)return;
 for(let y=1;y<N-1;y++)for(let x=1;x<N-1;x++){const i=y*N+x;B[i]=((A[i-1]+A[i+1]+A[i-N]+A[i+N])*.5-B[i])*.93}
 const t=A;A=B;B=t;for(let i=0;i<N*N;i++){const v=128+A[i]*70;tex[i*4]=v<0?0:v>255?255:v}ht.needsUpdate=true}
function sampleH(x,z){const fx=(x/SZ+.5)*N-.5,fy=(.5-z/SZ)*N-.5,x0=Math.max(0,Math.min(N-2,Math.floor(fx))),y0=Math.max(0,Math.min(N-2,Math.floor(fy))),tx=fx-x0,ty=fy-y0,r=y0*N+x0;
 return A[r]*(1-tx)*(1-ty)+A[r+1]*tx*(1-ty)+A[r+N]*(1-tx)*ty+A[r+N+1]*tx*ty}

/* ---------- mood balls: a happy (yellow) or sad (blue) face sphere, added freely, independent of word data ---------- */
const WG=new THREE.Group();scene.add(WG);const MOOD=new Map();
function faceTex(bg,happy){const c=document.createElement("canvas");c.width=c.height=128;const g=c.getContext("2d");
 g.fillStyle=bg;g.fillRect(0,0,128,128);
 g.fillStyle="#2b2b2b";g.beginPath();g.arc(44,54,7,0,Math.PI*2);g.fill();g.beginPath();g.arc(84,54,7,0,Math.PI*2);g.fill();
 g.strokeStyle="#2b2b2b";g.lineWidth=6;g.lineCap="round";g.beginPath();
 if(happy)g.arc(64,64,22,.15*Math.PI,.85*Math.PI);else g.arc(64,104,22,1.15*Math.PI,1.85*Math.PI);
 g.stroke();return new THREE.CanvasTexture(c)}
function mkMood(rec){const tex=faceTex(rec.type==="happy"?"#f4d35e":"#5ea8d8",rec.type==="happy");
 const m=new THREE.MeshStandardMaterial({map:tex,roughness:.5,metalness:.05});
 const g=new THREE.Group();g.add(new THREE.Mesh(new THREE.SphereGeometry(.8,24,18),m));
 let a=0;const sd=String(rec.ts)+rec.type;for(const ch of sd)a=(a*31+ch.charCodeAt(0))>>>0;
 g.userData={mood:rec,ph:a%628/100,bx:((a%997)/997-.5)*26,bz:(((a>>5)%991)/991)*24-14};return g}
function addMoodBall(type){const rec={type,ts:Date.now()};S.moods.push(rec);save();
 const g=mkMood(rec);g.position.set(g.userData.bx,14,g.userData.bz);g.userData.drop=1;g.userData.vy=0;
 WG.add(g);MOOD.set(rec,g);hud()}
function syncMoods(){S.moods.forEach(rec=>{if(!MOOD.has(rec)){const g=mkMood(rec);g.position.set(g.userData.bx,.7,g.userData.bz);g.userData.drop=0;g.userData.vy=0;WG.add(g);MOOD.set(rec,g)}})}
syncMoods();
$("#moodHappy").onclick=()=>addMoodBall("happy");
$("#moodSad").onclick=()=>addMoodBall("sad");

/* ---------- camera: drag / pinch / wheel orbit ---------- */
const cam={y:.5,p:.38,d:22};let tgt=[.5,.38,22],fogT=new THREE.Color(0x0f2a2f),MX=0,MY=0,PX=0,PY=0;let LX=-99,LY=-99;addEventListener("pointermove",e=>{MX=e.clientX/innerWidth-.5;MY=.5-e.clientY/innerHeight;if(e.target!==cv||Math.hypot(e.clientX-LX,e.clientY-LY)<14)return;LX=e.clientX;LY=e.clientY;rc.setFromCamera(new THREE.Vector2(e.clientX/innerWidth*2-1,-(e.clientY/innerHeight)*2+1),camera);const p=new THREE.Vector3();if(rc.ray.intersectPlane(pl0,p)&&Math.abs(p.x)<SZ/2&&Math.abs(p.z)<SZ/2)drop(p.x,p.z,.3)});
const VW={pool:[.5,.38,22],study:[1.5,.2,13],review:[-1,.28,17],archive:[0,-.2,12],obs:[2.5,.7,26]};
const clamp=(v,a,b)=>Math.max(a,Math.min(b,v)),ptr=new Map();let moved=0,pd=1;
const pinch=()=>{const a=[...ptr.values()];return a.length<2?1:Math.hypot(a[0][0]-a[1][0],a[0][1]-a[1][1])||1};
const rc=new THREE.Raycaster(),pl0=new THREE.Plane(new THREE.Vector3(0,1,0),0);
function hitWord(e){rc.setFromCamera(new THREE.Vector2(e.clientX/innerWidth*2-1,-(e.clientY/innerHeight)*2+1),camera);
 const h=rc.intersectObjects(WG.children,true)[0];if(!h)return null;let o=h.object;while(o&&!o.userData.mood)o=o.parent;return o}
let dragCand=null,dragObj=null,dragPid=null;
cv.addEventListener("pointerdown",e=>{cv.setPointerCapture(e.pointerId);ptr.set(e.pointerId,[e.clientX,e.clientY]);moved=0;pd=pinch();dragCand=hitWord(e)});
cv.addEventListener("pointermove",e=>{const o=ptr.get(e.pointerId);if(!o)return;const dx=e.clientX-o[0],dy=e.clientY-o[1];ptr.set(e.pointerId,[e.clientX,e.clientY]);moved+=Math.abs(dx)+Math.abs(dy);
 if(dragCand&&moved>=6&&!dragObj){dragObj=dragCand;dragPid=e.pointerId}
 if(dragObj&&e.pointerId===dragPid){rc.setFromCamera(new THREE.Vector2(e.clientX/innerWidth*2-1,-(e.clientY/innerHeight)*2+1),camera);const p=new THREE.Vector3();
  if(rc.ray.intersectPlane(pl0,p)){const half=SZ/2-1.3,px=clamp(p.x,-half,half),pz=clamp(p.z,-half,half);
   dragObj.position.x=px;dragObj.position.z=pz;dragObj.userData.bx=px;dragObj.userData.bz=pz;drop(px,pz,.1)}}
 });
cv.addEventListener("pointerup",e=>{if(dragObj&&e.pointerId===dragPid){drop(dragObj.position.x,dragObj.position.z,.9);dragObj=null;dragPid=null}
 else if(ptr.size==1&&moved<6)pick(e);dragCand=null;ptr.delete(e.pointerId)});cv.addEventListener("pointercancel",e=>{if(e.pointerId===dragPid){dragObj=null;dragPid=null}dragCand=null;ptr.delete(e.pointerId)});
cv.addEventListener("wheel",e=>{e.preventDefault();},{passive:false});
function pick(e){const o=hitWord(e);
 if(o){card(o.userData.mood);drop(o.position.x,o.position.z,.6);return}
 rc.setFromCamera(new THREE.Vector2(e.clientX/innerWidth*2-1,-(e.clientY/innerHeight)*2+1),camera);const p=new THREE.Vector3();if(rc.ray.intersectPlane(pl0,p)&&Math.abs(p.x)<SZ/2&&Math.abs(p.z)<SZ/2)drop(p.x,p.z,1.2)}

let AC,gain,on=false,WS=null,waterVol=1,ambientVol=1;
if(bgm)bgm.volume=.45;
const TRACKS=[
 {t:"自定义 (梦核编4)",u:"tracks/00_-_custom.m4a"},
 {t:"A Prison Behind the Eyes",u:"tracks/01_-_A_Prison_Behind_the_Eyes.mp3"},
 {t:"Agnus Dei",u:"tracks/02_-_Agnus_Dei.mp3"},
 {t:"Between Two Thoughts",u:"tracks/03_-_Between_Two_Thoughts.mp3"},
 {t:"Blue Rose",u:"tracks/04_-_Blue_Rose.mp3"},
 {t:"Control",u:"tracks/05_-_Control.mp3"},
 {t:"Domain",u:"tracks/06_-_Domain.mp3"},
 {t:"Eternal",u:"tracks/07_-_Eternal.mp3"},
 {t:"Everlasting",u:"tracks/08_-_Everlasting.mp3"},
 {t:"Faint Order",u:"tracks/09_-_Faint_Order.mp3"},
 {t:"Fate Yet Woven",u:"tracks/10_-_Fate_Yet_Woven.mp3"},
 {t:"Ghost Of The Valley",u:"tracks/11_-_Ghost_Of_The_Valley.mp3"},
 {t:"Into The Veil",u:"tracks/12_-_Into_The_Veil.mp3"},
 {t:"Living Legacy",u:"tracks/13_-_Living_Legacy.mp3"},
 {t:"Omnia Lamentorum",u:"tracks/14_-_Omnia_Lamentorum.mp3"},
 {t:"Salt In The Frame",u:"tracks/15_-_Salt_In_The_Frame.mp3"},
 {t:"Sequin Stars",u:"tracks/16_-_Sequin_Stars.mp3"},
 {t:"Song Of The Shore",u:"tracks/17_-_Song_Of_The_Shore.mp3"},
 {t:"Strand",u:"tracks/18_-_Strand.mp3"},
 {t:"Turncoat Sunset",u:"tracks/19_-_Turncoat_Sunset.mp3"},
 {t:"What Happens After All This",u:"tracks/20_-_What_Happens_After_All_This.mp3"}
];
function populateTrackSel(){const sel=$("#trkSel");sel.innerHTML="";TRACKS.forEach((tr,i)=>{const o=document.createElement("option");o.value=i;o.textContent=tr.t;sel.appendChild(o)})}
populateTrackSel();
if(bgm){bgm.src=TRACKS[0].u}
$("#trkSel").onchange=e=>{const i=+e.target.value;if(!bgm)return;bgm.src=TRACKS[i].u;bgm.load();bgm.play().catch(()=>{})};
$("#trkAdd").onclick=()=>$("#trkFile").click();
$("#trkFile").onchange=e=>{const f=e.target.files[0];if(!f||!bgm)return;const u=URL.createObjectURL(f);const idx=TRACKS.length;TRACKS.push({t:f.name,u});populateTrackSel();$("#trkSel").value=idx;bgm.src=u;bgm.load();bgm.play().catch(()=>{})};
$("#uiT").onclick=()=>{document.body.classList.toggle("hu");$("#uiT").textContent=document.body.classList.contains("hu")?"展开界面":"收起界面"};
function tickClock(){$("#clkTime").textContent=new Date().toLocaleTimeString([],{hour:"2-digit",minute:"2-digit"})}
tickClock();setInterval(tickClock,15000);
let tmrSec=0,tmrRunning=false,tmrInt=null;
function fmtTimer(s){const h=String(Math.floor(s/3600)).padStart(2,"0"),m=String(Math.floor(s%3600/60)).padStart(2,"0"),ss=String(s%60).padStart(2,"0");return h+":"+m+":"+ss}
function renderTimer(){$("#clkTimer").textContent=fmtTimer(tmrSec)}
renderTimer();
$("#tmrBtn").onclick=()=>{tmrRunning=!tmrRunning;$("#tmrBtn").textContent=tmrRunning?"暂停计时":"继续计时";
 if(tmrRunning){tmrInt=setInterval(()=>{tmrSec++;renderTimer()},1000)}else{clearInterval(tmrInt)}};
$("#tmrReset").onclick=()=>{tmrRunning=false;clearInterval(tmrInt);tmrSec=0;renderTimer();$("#tmrBtn").textContent="开始计时"};
$("#mvs").oninput=e=>{if(bgm)bgm.volume=e.target.value/100};
$("#avs").oninput=e=>ambientVol=e.target.value/100;
function wsEnsure(){try{if(!AC)AC=new (window.AudioContext||window.webkitAudioContext)();if(AC.state==="suspended")AC.resume();if(WS)return;
 const sr=AC.sampleRate,n=Math.floor(sr*8),buf=AC.createBuffer(1,n,sr),d=buf.getChannelData(0);
 let b0=0,b1=0,b2=0,b3=0,b4=0,b5=0,b6=0;
 for(let i=0;i<n;i++){const w=Math.random()*2-1;b0=.99886*b0+w*.0555179;b1=.99332*b1+w*.0750759;b2=.969*b2+w*.15385;b3=.8665*b3+w*.310486;b4=.55*b4+w*.532952;b5=-.7616*b5-w*.016898;d[i]=(b0+b1+b2+b3+b4+b5+b6+w*.5362)*.11;b6=w*.115926}
 const hp=AC.createBiquadFilter();hp.type="highpass";hp.frequency.value=350;hp.Q.value=.5;
 const lp=AC.createBiquadFilter();lp.type="lowpass";lp.frequency.value=1800;lp.Q.value=.4;
 const bp=AC.createBiquadFilter();bp.type="bandpass";bp.frequency.value=750;bp.Q.value=.3;
 const env=AC.createGain();env.gain.value=0;hp.connect(lp).connect(bp).connect(env).connect(AC.destination);
 WS={buf,hp,env,src:null,running:false,modTime:0,idleTime:2,driftTarget:1,driftCurrent:1,lastDriftT:0}}catch(e){}}
function wsStart(){if(!WS||WS.running)return;const s=AC.createBufferSource();s.buffer=WS.buf;s.loop=true;s.connect(WS.hp);s.start();WS.src=s;WS.running=true}
function wsStop(){if(!WS||!WS.running)return;try{WS.src.stop()}catch(e){}try{WS.src.disconnect()}catch(e){}WS.src=null;WS.running=false}
cv.addEventListener("pointerdown",()=>{wsEnsure();if(bgm&&bgm.paused)bgm.play().catch(()=>{})});
const clock=new THREE.Clock();let rainT=0;const CK=["y","p","d"];
function loop(){requestAnimationFrame(loop);const t=clock.getElapsedTime();
 camera.position.set(0,4.2,19);camera.lookAt(0,1.8,-12);
 bg.lerp(fogT,.03);scene.fog.color.copy(bg);
 
 sim();WU.t.value=t;lightTick();
 if(AC&&gain){const tg=on?.065*ambientVol:0;gain.gain.value+=(tg-gain.gain.value)*.05}
 if(WS){const dt=.0167,strength=Math.min(1,waterE*2.4);
  if(strength>.02){WS.idleTime=0;if(!WS.running)wsStart()}else{WS.idleTime+=dt;if(WS.idleTime>2&&WS.running)wsStop()}
  WS.modTime+=dt;const lfo=1+.12*Math.sin(2*Math.PI*.08*WS.modTime);
  if(WS.modTime-WS.lastDriftT>5){WS.driftTarget=1+(Math.random()*2-1)*.1;WS.lastDriftT=WS.modTime}
  WS.driftCurrent+=(WS.driftTarget-WS.driftCurrent)*Math.min(1,dt/1.2);
  const target=Math.max(0,Math.min(.6,strength*.32*lfo*WS.driftCurrent*waterVol)),cur=WS.env.gain.value;
  WS.env.gain.setTargetAtTime(target,AC.currentTime,target>cur?.083:.5)}
 MOOD.forEach((g,rec)=>{const u=g.userData;
  if(u.drop){u.vy-=.012;g.position.y+=u.vy;if(g.position.y<=.7){u.drop=0;g.position.y=.7;drop(g.position.x,g.position.z,2.2)}}
  else{const rh=sampleH(g.position.x,g.position.z)*1.6,by=.6+rh;g.position.y+=(by+Math.sin(t*.8+u.ph)*.12-g.position.y)*.08;
   const gx=sampleH(g.position.x+.7,g.position.z)-sampleH(g.position.x-.7,g.position.z),gz=sampleH(g.position.x,g.position.z+.7)-sampleH(g.position.x,g.position.z-.7);
   g.rotation.z+=(gx*2.2-g.rotation.z)*.12;g.rotation.x=Math.sin(t*.4+u.ph)*.15+gz*2.2}});
 R.render(scene,camera)}loop();

/* ---------- rooms / UI ---------- */
const P=$("#panel"),C=$("#card");let Q=null;
const panel=h=>{P.innerHTML=`<button class="x" data-a="go" data-v="pool" aria-label="关闭">×</button>`+h};
function go(r){document.querySelectorAll("nav button").forEach(b=>b.classList.toggle("a",b.dataset.r==r));C.classList.remove("on");
 tgt=VW[r].slice();fogT=new THREE.Color(r=="archive"?0x0a2128:0x0f2a2f);$("#hint").style.opacity=r=="pool"?1:0;P.classList.toggle("on",r!="pool");
 if(r=="study"||r=="review")startQuiz(r);else if(r=="archive")archive();else if(r=="obs")obs()}
function card(rec){const d=new Date(rec.ts);
 C.innerHTML=`<button class="x" data-a="cc" aria-label="关闭">×</button><h2>${rec.type==="happy"?"😊 好心情":"🙁 不开心"}</h2><p class="dim">${d.toLocaleDateString("zh-CN")} ${d.toLocaleTimeString("zh-CN",{hour:"2-digit",minute:"2-digit"})}</p><button data-a="moodDel" data-v="${rec.ts}">删除这条记录</button>`;C.classList.add("on")}
const spk=w=>`<button data-a="say" data-v="en-GB" data-w="${esc(w.w)}">英音</button><button data-a="say" data-v="en-US" data-w="${esc(w.w)}">美音</button>`;

function startQuiz(mode){const l=S.words.filter(w=>mode=="study"?!w.learned:isDue(w)).sort((a,b)=>a.due-b.due).slice(0,10);
 if(!l.length)return panel(`<h2>${mode=="study"?"学习室":"复习回廊"}</h2><p>${mode=="study"?"没有未学习的新词了。去水下档案室导入更多词库吧。":"现在没有到期的单词。泳池里的物件都很安静。"}</p>`);
 Q={mode,list:l,i:0,ok:0,seen:0};nextQ()}
function nextQ(){if(Q.i>=Q.list.length)return panel(`<h2>本轮完成</h2><p>答对 ${Q.ok} / ${Q.list.length}。</p><button class="pri" data-a="go" data-v="pool">回到泳池看看</button><button data-a="again">再来一轮</button>`);
 const w=Q.w=Q.list[Q.i];
 if(Q.mode=="study"&&!Q.seen){Q.seen=1;return panel(`<small>新词 ${Q.i+1} / ${Q.list.length}</small><h2>${esc(w.w)}</h2><p class="dim">${esc(w.ph)} ${esc(w.pos)} ${spk(w)}</p><p>${esc(w.zh)}</p><p>${esc(w.def)}</p><p class="ex">${esc(w.ex)}</p><button class="pri" data-a="quiz">开始测验</button>`)}
 Q.seen=0;quizQ()}
function quizQ(){const w=Q.w,T=["ez","ze","sp"];if(w.ex)T.push("xw");if(w.def)T.push("dw");const t=T[Math.random()*T.length|0];
 const hd=`<small>${Q.mode=="study"?"学习":"复习"} ${Q.i+1} / ${Q.list.length}</small> ${spk(w)}`;
 if(t=="sp")return panel(hd+`<h3>${esc(w.zh)}</h3><p class="ex">${esc(w.def)}</p><input type="text" id="sp" placeholder="拼写英文单词" autocomplete="off" autocapitalize="off" spellcheck="false"><button class="pri" data-a="sp">提交</button>`);
 const o=shuf([w,...shuf(S.words.filter(x=>x!==w)).slice(0,3)]);
 const q={ez:esc(w.w),ze:esc(w.zh),xw:esc((w.ex||"").replace(new RegExp(w.w.replace(/[.*+?^${}()|[\]\\]/g,"\\$&"),"ig"),"＿＿＿")),dw:esc(w.def)}[t];
 panel(hd+`<h3>${q}</h3>`+o.map(x=>`<button class="opt" data-a="pick" data-v="${S.words.indexOf(x)}">${esc(t=="ez"?x.zh:x.w)}</button>`).join(""))}
function fin(ok){grade(Q.w,ok);if(ok)Q.ok++;P.insertAdjacentHTML("beforeend",`<p>${ok?"答对了。":"正确答案："+esc(Q.w.w)+"　"+esc(Q.w.zh)}</p><button class="pri" data-a="next">下一题</button>`)}
function archive(){panel(`<h2>水下档案室</h2><p class="dim">导入 CSV / TSV / TXT / JSON，或直接粘贴。每行：单词, 中文, 英文释义, 例句。带表头时可用 word, phonetic, pos, translation, definition, example。缺失内容会标为“待确认”。</p>
<select id="cat"><option>Biology</option><option>Physics</option><option>Chemistry</option><option>Mathematics</option><option selected>IELTS</option><option>Custom</option></select>
<textarea id="tx" rows="6" placeholder="resilient, 有韧性的, able to recover quickly, Children are often resilient."></textarea>
<input type="file" id="fl" accept=".csv,.tsv,.txt,.json"><div id="pv" class="dim"></div>
<button data-a="prev">预览</button><button class="pri" data-a="imp">确认导入</button>
<p class="dim">词库共 ${S.words.length} 词，其中 ${S.words.filter(x=>x.pending).length} 个待确认。</p>`)}
const HM={word:"w",phonetic:"ph",pos:"pos",translation:"zh",definition:"def",example:"ex"};
function parse(s){s=s.trim();if(!s)return[];try{const j=JSON.parse(s);if(Array.isArray(j))return j.map(o=>typeof o=="string"?{w:o}:{w:o.word||o.w,ph:o.phonetic,pos:o.pos,zh:o.translation||o.zh,def:o.definition||o.def,ex:o.example||o.ex})}catch(e){}
 const rows=s.split(/\r?\n/).filter(Boolean).map(l=>l.split(l.includes("\t")?"\t":l.includes("|")?"|":/[,，]/).map(v=>v.trim().replace(/^"|"$/g,"")));
 let cols=["w","zh","def","ex"];if(/^word$/i.test(rows[0][0]))cols=rows.shift().map(h=>HM[h.toLowerCase()]||"x");
 return rows.map(r=>{const o={};r.forEach((v,i)=>o[cols[i]]=v);return o})}
function plan(){const ex=new Set(S.words.map(x=>x.w.toLowerCase())),seen=new Set(),add=[];let dup=0,miss=0;
 parse($("#tx").value).forEach(o=>{if(!o.w)return;const k=o.w.toLowerCase();if(ex.has(k)||seen.has(k)){dup++;return}seen.add(k);if(!o.zh||!o.def)miss++;add.push(o)});return{add,dup,miss}}
const acts={go:v=>go(v),cc:()=>C.classList.remove("on"),say:(v,b)=>speak(b.dataset.w,v),again:()=>startQuiz(Q.mode),quiz:()=>quizQ(),next:()=>{Q.i++;nextQ()},
 moodDel(v){const ts=+v,idx=S.moods.findIndex(r=>r.ts===ts);if(idx<0)return;const rec=S.moods[idx],g=MOOD.get(rec);if(g){WG.remove(g);MOOD.delete(rec)}S.moods.splice(idx,1);save();hud();C.classList.remove("on")},
 pick(v){const ok=S.words[v]===Q.w;P.querySelectorAll(".opt").forEach(b=>{b.disabled=true;if(S.words[b.dataset.v]===Q.w)b.classList.add("ok");else if(b.dataset.v==v)b.classList.add("bad")});fin(ok)},
 sp(){const i=$("#sp");i.disabled=true;fin(i.value.trim().toLowerCase()==Q.w.w.toLowerCase())},
 prev(){try{const p=plan();$("#pv").textContent=`可导入 ${p.add.length} 个，重复跳过 ${p.dup} 个，内容不全 ${p.miss} 个。`}catch(e){$("#pv").textContent="格式无法识别，请检查分隔符或 JSON。"}},
 imp(){try{const p=plan(),c=$("#cat").value;p.add.forEach(o=>S.words.push({w:o.w,ph:o.ph||"",pos:o.pos||"",zh:o.zh||"",def:o.def||"",ex:o.ex||"",cat:c,pending:!o.zh||!o.def,learned:false,ease:2.5,int:0,lapses:0,due:0}));save();hud();archive();$("#pv").textContent=`已导入 ${p.add.length} 个单词，可在学习室开始学习。`}catch(e){$("#pv").textContent="导入失败，请先预览检查。"}}};
document.addEventListener("click",e=>{const b=e.target.closest("[data-a]");if(b)acts[b.dataset.a](b.dataset.v,b)});
document.querySelectorAll("nav button").forEach(b=>b.addEventListener("click",()=>go(b.dataset.r)));
P.addEventListener("change",e=>{if(e.target.id=="fl"){const f=e.target.files[0];if(!f)return;if(/\.xlsx?$/i.test(f.name)){$("#pv").textContent="暂不支持 Excel，请另存为 CSV 后导入。";return}const r=new FileReader();r.onload=()=>{$("#tx").value=r.result;acts.prev()};r.readAsText(f)}});
P.addEventListener("keydown",e=>{if(e.key=="Enter"&&e.target.id=="sp"&&!e.target.disabled)acts.sp()});
function obs(){const m=[0,0,0,0,0];S.words.forEach(x=>m[mast(x)]++);const L=S.words.filter(x=>x.learned).length,st=S.st,acc=st.tot?Math.round(st.ok/st.tot*100):0;
 let s=0,d=new Date();while(st.act[iso(d)]){s++;d.setDate(d.getDate()-1)}
 const mx=Math.max(1,...m),days=[];for(let i=6;i>=0;i--){const d=new Date();d.setDate(d.getDate()-i);days.push(st.nw[iso(d)]||0)}const dm=Math.max(1,...days);
 panel(`<h2>观测室</h2><p>累计学习 ${L} · 基本掌握及以上 ${m[3]+m[4]} · 正确率 ${acc}% · 连续学习 ${s} 天 · 待复习 ${S.words.filter(isDue).length} · 沉底 ${S.words.filter(isSunk).length}</p>
 <p class="dim">掌握程度分布</p>${MN.map((n,i)=>`<div class="bar"><span style="width:5em">${n}</span><i style="width:${m[i]/mx*60}%"></i>${m[i]}</div>`).join("")}
 <p class="dim">近 7 天新学单词</p><div class="bar" style="align-items:flex-end;height:60px">${days.map(v=>`<i style="width:24px;height:${4+v/dm*50}px"></i>`).join("")}</div>`)}

/* ---------- ambient toggle: filtered, slowly-sweeping noise to suggest distant flowing water (independent of the water-splash sound below) ---------- */
$("#snd").onclick=()=>{try{wsEnsure();if(!gain){const b=AC.createBuffer(1,AC.sampleRate*4,AC.sampleRate),d=b.getChannelData(0);for(let i=0;i<d.length;i++)d[i]=Math.random()*2-1;
 const s=AC.createBufferSource();s.buffer=b;s.loop=true;
 const lp=AC.createBiquadFilter();lp.type="lowpass";lp.frequency.value=2400;s.connect(lp);
 gain=AC.createGain();gain.gain.value=0;gain.connect(AC.destination);
 [[480,.6,.07,140],[1100,.7,.11,220]].forEach(q=>{const bp=AC.createBiquadFilter();bp.type="bandpass";bp.frequency.value=q[0];bp.Q.value=q[1];lp.connect(bp);bp.connect(gain);
  const lfo=AC.createOscillator();lfo.frequency.value=q[2];const lfoG=AC.createGain();lfoG.gain.value=q[3];lfo.connect(lfoG).connect(bp.frequency);lfo.start()});
 s.start()}
 on=!on;AC.resume();$("#snd").textContent="♪ 环境音 "+(on?"开":"关")}catch(e){}};
$("#wvs").oninput=e=>waterVol=e.target.value/100;
/* ---------- window light: manual slider or follow local clock ---------- */
function lightTick(){let L=LV;const c=new THREE.Color(0xe8fff8);
 if(AUTO){const d=new Date(),h=d.getHours()+d.getMinutes()/60,s=Math.sin(Math.PI*(h-6)/12);
  if(s>0){L=.1+.9*Math.pow(s,.7);c.lerp(new THREE.Color(0xffc88a),Math.max(0,1-s*3))}else{L=.05;c.set(0x8fa6ff)}
  $("#ls").value=Math.round(L*100)}
 LVc+=(L-LVc)*.05;LT.wm.color.copy(c).multiplyScalar(.2+.85*LVc);LT.sp.color.copy(c);LT.sp.intensity=.1+1.7*LVc;LT.pl.color.copy(c);LT.pl.intensity=.08+.7*LVc;
 LT.shaft.material.color.copy(c);LT.shaft.material.opacity=.008+.05*LVc;HL.intensity=.1+.3*LVc;WU.L.value=LVc}
$("#ls").oninput=e=>{AUTO=false;LV=e.target.value/100;$("#la").textContent="跟随时间：关"};
$("#la").onclick=()=>{AUTO=!AUTO;$("#la").textContent="跟随时间："+(AUTO?"开":"关")};
hud();
</script></body></html>
