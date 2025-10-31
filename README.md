<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Java & DSA Visualizer — Rochak Prajapati</title>
  <style>
    :root{
      --bg:#05060b;
      --panel:#081021;
      --accent1:#6ee7ff;
      --accent2:#9b7cff;
      --accent3:#3af78e;
      --muted:#99a0b3;
      --glow: 0 8px 30px rgba(110,231,255,0.08), 0 2px 8px rgba(155,124,255,0.06);
      --neon: 0 0 16px rgba(110,231,255,0.12), 0 0 32px rgba(155,124,255,0.06);
      font-family: "Inter", ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    html,body{height:100%;margin:0;background:linear-gradient(180deg,#02040a 0%,#071226 60%);color:#dbe6ff;}
    .wrap{
      max-width:1100px;margin:28px auto;padding:28px;border-radius:12px;background:linear-gradient(180deg, rgba(10,14,25,0.6), rgba(3,8,20,0.6));
      box-shadow: 0 10px 40px rgba(0,0,0,0.6); border:1px solid rgba(255,255,255,0.03);
      backdrop-filter: blur(6px);
    }
    header{display:flex;gap:16px;align-items:center;margin-bottom:18px}
    .avatar{width:72px;height:72px;border-radius:12px;background:linear-gradient(135deg,var(--accent2),var(--accent1));display:flex;align-items:center;justify-content:center;font-weight:700;color:#021;box-shadow:var(--glow)}
    h1{margin:0;font-size:20px}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    .grid{display:grid;grid-template-columns: 1fr 420px;gap:18px}
    /* LEFT: main visual area */
    .panel{
      background:linear-gradient(180deg, rgba(14,18,30,0.6), rgba(6,10,18,0.45));
      border-radius:10px;padding:14px;border:1px solid rgba(255,255,255,0.03);
      min-height:420px;box-shadow:var(--glow);
    }

    .code-area{background:#061424;border-radius:8px;padding:14px;color:#bfefff; font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", monospace; font-size:13px; position:relative; overflow:hidden}
    .code-title{display:flex;gap:10px;align-items:center;margin-bottom:10px}
    .dot{width:10px;height:10px;border-radius:50%}
    .dot.red{background:#ff5f6d;box-shadow:0 0 10px rgba(255,95,109,0.2)}
    .dot.yellow{background:#ffb86b}
    .dot.green{background:#30d158}
    .code-content{white-space:pre-wrap; line-height:1.45; min-height:160px}
    .cursor{display:inline-block;width:10px;height:18px;background:var(--accent1);margin-left:3px;vertical-align:middle;animation:blink 900ms steps(2) infinite}
    @keyframes blink{50%{opacity:0.05}}

    /* OOPs box */
    .oops{margin-top:12px;background:linear-gradient(90deg, rgba(155,124,255,0.04), rgba(58,247,142,0.02)); padding:10px;border-radius:8px;color:#cfeffd; min-height:100px}
    .diagram{display:flex;flex-direction:column;gap:8px;align-items:center;justify-content:center;font-size:14px}
    .box{padding:8px 12px;border-radius:8px;border:1px dashed rgba(110,231,255,0.08);min-width:160px;text-align:center;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent)}
    .arrow{color:var(--accent2);font-weight:700}

    /* Right column panels */
    .right{display:flex;flex-direction:column;gap:12px}
    .small{background:var(--panel);border-radius:8px;padding:12px;border:1px solid rgba(255,255,255,0.03)}
    .viz-title{font-size:13px;color:var(--muted);margin-bottom:8px}
    /* Bubble sort viz */
    .bars{display:flex;gap:6px;align-items:end;height:160px}
    .bar{width:22px;background:linear-gradient(180deg,var(--accent1),var(--accent2));border-radius:4px;box-shadow:var(--neon);transition:height 300ms ease, transform 250ms ease}
    .bar.active{transform:translateY(-6px);filter:brightness(1.2)}
    /* Tree viz */
    .tree{display:flex;flex-wrap:wrap;justify-content:center;gap:12px;min-height:140px}
    .node{padding:8px 10px;border-radius:8px;background:linear-gradient(180deg,#072b1f,var(--accent3));color:#001;box-shadow:var(--glow);min-width:44px;text-align:center}
    /* Debug / deploy */
    .log{background:#031220;border-radius:6px;padding:10px;min-height:70px;color:var(--muted);font-size:13px;overflow:hidden}
    .badge{display:flex;align-items:center;gap:10px;justify-content:center;padding:10px;border-radius:10px;background:linear-gradient(90deg,#09122a,#061229);border:1px solid rgba(110,231,255,0.08)}
    .badge .label{background:linear-gradient(90deg,var(--accent2),var(--accent1));padding:6px 10px;border-radius:8px;color:#021;font-weight:700;box-shadow:var(--glow)}

    /* final overlay */
    .overlay{
      position:fixed;left:0;top:0;width:100%;height:100%;display:flex;align-items:center;justify-content:center;pointer-events:none;
    }
    .overlay .card{
      width:560px;background:linear-gradient(180deg, rgba(5,7,15,0.8), rgba(3,5,12,0.85));border-radius:12px;padding:20px;border:1px solid rgba(255,255,255,0.04);backdrop-filter: blur(8px);box-shadow:0 10px 80px rgba(20,10,60,0.6);transform:scale(0.92);opacity:0;transition:all 420ms ease;
    }
    .overlay .card.show{transform:scale(1);opacity:1;pointer-events:auto}
    .cloud{
      display:flex;gap:12px;align-items:center;justify-content:center;margin-bottom:12px;color:var(--muted)
    }

    /* responsive */
    @media (max-width:980px){
      .grid{grid-template-columns:1fr}
      .right{order:2}
    }
  </style>
</head>
<body>
  <div class="wrap" role="main">
    <header>
      <div class="avatar">RP</div>
      <div>
        <h1>Rochak Prajapati</h1>
        <p class="lead">B.Tech (CSE) 5th Sem · Java Developer · DSA Enthusiast · Aspiring Software Engineer</p>
      </div>
    </header>

    <div class="grid" aria-hidden="false">
      <div class="panel">
        <div class="code-area" aria-live="polite">
          <div class="code-title">
            <div class="dot red"></div><div class="dot yellow"></div><div class="dot green"></div>
            <div style="flex:1"></div>
            <div style="color:var(--muted);font-size:12px">Java Visualizer • 10–15s loop</div>
          </div>

          <div id="codeContent" class="code-content">
            <!-- typed code will appear here -->
          </div>
          <span id="cursor" class="cursor" aria-hidden="true"></span>

          <div class="oops" style="margin-top:14px">
            <div class="diagram" id="oopsDiagram">
              <div class="box">Class Animal</div>
            </div>
          </div>
        </div>
      </div>

      <div class="right">
        <div class="small">
          <div class="viz-title">DSA — Bubble Sort Visualization</div>
          <div id="bars" class="bars" role="img" aria-label="Bubble sort visualization"></div>
        </div>

        <div class="small">
          <div class="viz-title">DSA — Binary Tree Growth</div>
          <div id="tree" class="tree" role="img" aria-label="Binary tree growth"></div>
        </div>

        <div class="small">
          <div class="viz-title">Software Dev — Debug & Deploy</div>
          <div id="log" class="log">Ready to run sequence...</div>
        </div>

        <div class="small badge" style="margin-top:6px">
          <div style="flex:1;color:var(--muted);font-size:13px">Status</div>
          <div class="label">Aspiring Software Engineer</div>
        </div>
      </div>
    </div>
  </div>

  <div class="overlay" id="overlay" aria-hidden="true">
    <div class="card" id="finalCard" role="dialog" aria-modal="true">
      <div class="cloud">
        <div style="font-weight:700;color:var(--accent1);font-size:18px">Deployed → Cloud</div>
      </div>
      <div style="text-align:center;margin-bottom:8px">
        <div style="font-size:20px;font-weight:700;color:#cfeffd">Software Engineer</div>
        <div style="font-size:13px;color:var(--muted);margin-top:6px">Visual demo: Java • OOPs • DSA • DevOps</div>
      </div>
      <div style="display:flex;justify-content:center;margin-top:14px">
        <div class="badge">
          <svg width="28" height="28" viewBox="0 0 24 24" style="filter:drop-shadow(0 4px 10px rgba(0,0,0,0.4));margin-right:10px">
            <circle cx="12" cy="12" r="10" fill="#6ee7ff"/>
            <path d="M9 12l2 2 4-4" stroke="#021" stroke-width="1.6" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <div style="font-weight:700;color:#021">Badge Earned</div>
        </div>
      </div>
    </div>
  </div>

  <script>
    /******************************
     * TIMINGS (ms) - tweak here *
     ******************************/
    const TIMINGS = {
      typeSpeed: 24,        // typing speed
      pauseAfterType: 900,  // wait after typing the Java snippet
      showOOPsAfter: 1400,
      bubbleStart: 2200,
      bubbleStep: 350,
      treeStart: 4200,
      debugStart: 6200,
      deployStart: 8200,
      finalShow: 9200,
      totalLoop: 12000      // loop length
    };

    /***********************
     * Java code to type   *
     ***********************/
    const JAVA_SNIPPET = [
`public class HelloWorld {`,
`    public static void main(String[] args) {`,
`        System.out.println("Hello, World!");`,
`    }`,
`}`,
``,
`// OOPs: Inheritance & Polymorphism`,
`class Animal { void speak(){ System.out.println("..."); } }`,
`class Dog extends Animal { void speak(){ System.out.println("Woof!"); } }`,
``,
`// DSA example: Bubble Sort (simple)`,
`// arrays: [64,34,25,12,22,11,90]`,
``
    ].join('\n');

    /* Elements */
    const codeEl = document.getElementById('codeContent');
    const cursor = document.getElementById('cursor');
    const oopsEl = document.getElementById('oopsDiagram');
    const barsEl = document.getElementById('bars');
    const treeEl = document.getElementById('tree');
    const logEl = document.getElementById('log');
    const overlay = document.getElementById('overlay');
    const finalCard = document.getElementById('finalCard');

    /* Utility sleep */
    const sleep = ms => new Promise(r => setTimeout(r, ms));

    /* Typing effect */
    async function typeCode(text){
      codeEl.textContent = '';
      for(let i=0;i<text.length;i++){
        codeEl.textContent += text[i];
        // scroll to bottom if overflow
        codeEl.parentElement.scrollTop = codeEl.parentElement.scrollHeight;
        await sleep(TIMINGS.typeSpeed);
      }
    }

    /* OOPs diagram animation */
    async function showOOPs(){
      oopsEl.innerHTML = `<div class="box">Class Animal</div>`;
      await sleep(700);
      oopsEl.innerHTML += `<div class="arrow">↓ Inheritance</div>`;
      await sleep(500);
      oopsEl.innerHTML += `<div class="box">Class Dog</div>`;
      await sleep(700);
      oopsEl.innerHTML += `<div style="font-size:12px;color:var(--muted);margin-top:8px">Object created: <strong>Dog d = new Dog();</strong></div>`;
    }

    /* Bubble sort visualization */
    function createBars(arr){
      barsEl.innerHTML = '';
      arr.forEach(v=>{
        const div = document.createElement('div');
        div.className = 'bar';
        div.style.height = (v*2.6)+'px';
        barsEl.appendChild(div);
      });
    }
    async function bubbleSortAnim(arr){
      createBars(arr);
      const bars = () => Array.from(barsEl.children);
      for(let i=0;i<arr.length;i++){
        for(let j=0;j<arr.length-i-1;j++){
          const list = bars();
          list[j].classList.add('active');
          list[j+1].classList.add('active');
          await sleep(TIMINGS.bubbleStep);
          if(arr[j] > arr[j+1]){
            // swap heights
            [arr[j],arr[j+1]] = [arr[j+1],arr[j]];
            list[j].style.height = (arr[j]*2.6)+'px';
            list[j+1].style.height = (arr[j+1]*2.6)+'px';
          }
          list[j].classList.remove('active');
          list[j+1].classList.remove('active');
        }
      }
    }

    /* Binary Tree growth */
    async function growTree(){
      treeEl.innerHTML = '';
      const nodes = [
        ['50'],
        ['30','70'],
        ['20','40','60','80']
      ];
      for(let level=0; level<nodes.length; level++){
        await sleep(260);
        nodes[level].forEach(n=>{
          const el = document.createElement('div');
          el.className = 'node';
          el.textContent = n;
          treeEl.appendChild(el);
        });
      }
    }

    /* Debug & Deploy logs */
    async function debugAndDeploy(){
      logEl.textContent = 'Running tests...';
      await sleep(600);
      logEl.textContent += '\nError: NullPointerException at Line 12';
      await sleep(900);
      logEl.textContent += '\nDebugging...';
      await sleep(800);
      logEl.textContent += '\nFixed! Building artifact...';
      await sleep(700);
      logEl.textContent += '\nDeploying to cloud...';
    }

    /* Show final overlay badge */
    async function showFinalOverlay(){
      overlay.setAttribute('aria-hidden','false');
      finalCard.classList.add('show');
      await sleep(1800);
      // auto hide after a while
      await sleep(2200);
      finalCard.classList.remove('show');
      overlay.setAttribute('aria-hidden','true');
    }

    /* Orchestrator loop */
    async function runSequence(){
      try {
        // Reset
        codeEl.textContent = '';
        oopsEl.innerHTML = `<div class="box">Class Animal</div>`;
        barsEl.innerHTML = '';
        treeEl.innerHTML = '';
        logEl.textContent = 'Ready to run sequence...';
        overlay.setAttribute('aria-hidden','true');

        // Typing
        await typeCode(JAVA_SNIPPET);
        await sleep(TIMINGS.pauseAfterType);

        // OOPs
        await showOOPs();
        await sleep(TIMINGS.showOOPsAfter);

        // Bubble sort
        const arr = [64,34,25,12,22,11,90];
        await bubbleSortAnim(arr.slice());
        await sleep(300);

        // Tree
        await growTree();
        await sleep(400);

        // Debug & deploy
        await debugAndDeploy();
        await sleep(800);

        // Final overlay
        await showFinalOverlay();

      } catch(e){
        console.error(e);
      } finally {
        // loop
        setTimeout(runSequence, TIMINGS.totalLoop);
      }
    }

    // Start on load
    window.addEventListener('load', ()=> {
      // kickoff loop
      runSequence();
    });

    /* Accessibility: allow pause/resume by pressing space */
    let paused = false;
    window.addEventListener('keydown', (e)=>{
      if(e.code === 'Space'){ e.preventDefault();
        paused = !paused;
        if(paused){
          TIMINGS.typeSpeed = 999999;
        } else {
          TIMINGS.typeSpeed = 24;
        }
      }
    });
  </script>
</body>
</html>
