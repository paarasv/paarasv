<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  :root{
    --bg:#0a0a0f;
    --surface:#111118;
    --surface2:#1a1a24;
    --border:#2a2a3a;
    --accent:#7c6aff;
    --accent2:#00e5a0;
    --accent3:#ff6b6b;
    --text:#e8e8f0;
    --muted:#6b6b88;
    --mono:'JetBrains Mono',monospace;
    --sans:'Syne',sans-serif;
  }
  body{background:var(--bg);color:var(--text);font-family:var(--mono);min-height:100vh;overflow-x:hidden}

  .cursor{display:inline-block;width:2px;height:1em;background:var(--accent);animation:blink 1s step-end infinite;vertical-align:text-bottom;margin-left:1px}
  @keyframes blink{0%,100%{opacity:1}50%{opacity:0}}

  .container{max-width:900px;margin:0 auto;padding:2rem 1.5rem}

  .terminal-bar{background:var(--surface);border:1px solid var(--border);border-radius:10px 10px 0 0;padding:.6rem 1rem;display:flex;align-items:center;gap:.5rem}
  .dot{width:12px;height:12px;border-radius:50%}
  .dot.r{background:#ff5f57}.dot.y{background:#febc2e}.dot.g{background:#28c840}
  .terminal-title{font-size:12px;color:var(--muted);margin-left:.5rem;font-family:var(--mono)}

  .terminal-body{background:var(--surface);border:1px solid var(--border);border-top:none;border-radius:0 0 10px 10px;padding:1.5rem;margin-bottom:1.5rem}

  .prompt{color:var(--accent2);font-size:13px}
  .cmd{color:var(--text);font-size:13px}
  .comment{color:var(--muted);font-size:12px}

  .hero{margin:1.5rem 0}
  .hero-name{font-family:var(--sans);font-size:2.4rem;font-weight:800;letter-spacing:-1px;line-height:1.1}
  .hero-name span{color:var(--accent)}
  .hero-sub{font-size:12px;color:var(--muted);margin-top:.3rem}
  .hero-sub b{color:var(--accent2)}
  .hero-desc{font-size:13px;color:#b0b0c8;line-height:1.7;margin-top:1rem;max-width:600px}
  .hero-desc a{color:var(--accent);text-decoration:none;border-bottom:1px solid var(--accent)}

  .stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1px;background:var(--border);border:1px solid var(--border);border-radius:10px;overflow:hidden;margin:1.5rem 0}
  .stat{background:var(--surface);padding:1.2rem 1rem;text-align:center;transition:background .2s}
  .stat:hover{background:var(--surface2)}
  .stat-num{font-family:var(--sans);font-size:2rem;font-weight:800;color:var(--accent);line-height:1}
  .stat-label{font-size:10px;color:var(--muted);margin-top:.4rem;text-transform:uppercase;letter-spacing:.05em}

  .section-title{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.15em;margin-bottom:1rem;display:flex;align-items:center;gap:.5rem}
  .section-title::after{content:'';flex:1;height:1px;background:var(--border)}

  .filter-bar{display:flex;gap:.5rem;flex-wrap:wrap;margin-bottom:1rem}
  .filter-btn{background:transparent;border:1px solid var(--border);color:var(--muted);padding:.3rem .8rem;border-radius:20px;font-family:var(--mono);font-size:11px;cursor:pointer;transition:all .2s}
  .filter-btn:hover,.filter-btn.active{background:var(--accent);border-color:var(--accent);color:#fff}

  .stack-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:.5rem}
  .skill-row{display:flex;align-items:center;gap:.75rem;padding:.5rem .75rem;border-radius:6px;border:1px solid transparent;transition:all .2s;cursor:default}
  .skill-row:hover{background:var(--surface2);border-color:var(--border)}
  .skill-row.hidden{display:none}
  .skill-name{font-size:12px;color:var(--text);min-width:120px;flex-shrink:0}
  .skill-bar-wrap{flex:1;background:var(--surface2);border-radius:20px;height:4px;overflow:hidden}
  .skill-bar{height:100%;border-radius:20px;background:var(--accent);transition:width .6s cubic-bezier(.4,0,.2,1)}
  .skill-pct{font-size:11px;color:var(--muted);min-width:32px;text-align:right}

  .timeline{position:relative;padding-left:1.5rem;margin:1rem 0}
  .timeline::before{content:'';position:absolute;left:0;top:6px;bottom:6px;width:1px;background:var(--border)}
  .tl-item{position:relative;margin-bottom:1.5rem}
  .tl-item::before{content:'';position:absolute;left:-1.56rem;top:6px;width:8px;height:8px;border-radius:50%;background:var(--accent);border:2px solid var(--bg)}
  .tl-company{font-family:var(--sans);font-weight:700;font-size:14px;color:var(--text)}
  .tl-role{font-size:12px;color:var(--accent2);margin:.2rem 0}
  .tl-period{font-size:11px;color:var(--muted)}

  .projects-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:.75rem;margin-top:1rem}
  .proj-card{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1rem;transition:all .25s;cursor:pointer;position:relative;overflow:hidden}
  .proj-card::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--accent)08,transparent);opacity:0;transition:opacity .3s}
  .proj-card:hover{border-color:var(--accent);transform:translateY(-2px)}
  .proj-card:hover::before{opacity:1}
  .proj-name{font-family:var(--sans);font-weight:700;font-size:14px;color:var(--text)}
  .proj-badge{display:inline-block;font-size:9px;background:var(--accent);color:#fff;padding:1px 6px;border-radius:20px;margin-left:.4rem;vertical-align:middle}
  .proj-desc{font-size:11px;color:var(--muted);margin:.4rem 0 .6rem;line-height:1.5}
  .proj-tags{display:flex;flex-wrap:wrap;gap:.3rem}
  .proj-tag{font-size:10px;background:var(--surface2);color:var(--accent);border:1px solid var(--border);padding:2px 7px;border-radius:4px;font-family:var(--mono)}

  .links-row{display:flex;gap:.75rem;flex-wrap:wrap;margin-top:1rem}
  .link-btn{display:flex;align-items:center;gap:.4rem;background:var(--surface2);border:1px solid var(--border);color:var(--text);padding:.5rem 1rem;border-radius:6px;font-family:var(--mono);font-size:12px;text-decoration:none;transition:all .2s}
  .link-btn:hover{border-color:var(--accent);color:var(--accent)}
  .link-dot{width:6px;height:6px;border-radius:50%;background:var(--accent2)}

  .github-stats{display:flex;gap:.75rem;flex-wrap:wrap;margin-top:.75rem}
  .github-stats img{border-radius:8px;border:1px solid var(--border);max-width:100%;height:auto}

  .fade-in{opacity:0;transform:translateY(12px);animation:fadeUp .5s forwards}
  @keyframes fadeUp{to{opacity:1;transform:translateY(0)}}

  @media(max-width:600px){
    .stats-grid{grid-template-columns:repeat(2,1fr)}
    .projects-grid,.stack-grid{grid-template-columns:1fr}
    .hero-name{font-size:1.8rem}
  }
</style>
</head>
<body>
<div class="container">

  <div class="terminal-bar">
    <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
    <span class="terminal-title">paarasv — github profile</span>
  </div>
  <div class="terminal-body">
    <div style="margin-bottom:.5rem"><span class="prompt">~ </span><span class="cmd">whoami</span></div>

    <div class="hero fade-in" style="animation-delay:.1s">
      <div class="hero-name">Paras Verma<span>.</span></div>
      <div class="hero-sub"><b>@paarasv</b> · VIT '25 · Sole Engineer @ Sera EmOS</div>
      <div class="hero-desc">
        iOS, GenAI pipelines, data infrastructure. I build things end-to-end — consumer apps shipped to production, agentic AI systems with longitudinal context, and platform tooling at scale. Currently sole engineer on <a href="https://seraemos.com" target="_blank">Sera (EmOS)</a>.
      </div>
    </div>
  </div>

  <div style="margin-bottom:.5rem"><span class="prompt">~ </span><span class="cmd">./stats</span></div>
  <div class="stats-grid fade-in" style="animation-delay:.2s">
    <div class="stat"><div class="stat-num" data-target="3">0</div><div class="stat-label">companies shipped at</div></div>
    <div class="stat"><div class="stat-num" data-target="2">0</div><div class="stat-label">iOS apps in production</div></div>
    <div class="stat"><div class="stat-num" data-target="4">0</div><div class="stat-label">Sera current version</div></div>
    <div class="stat"><div class="stat-num">1000<span style="color:var(--accent2)">+</span></div><div class="stat-label">audience reached (talks)</div></div>
  </div>

  <div style="margin:1.5rem 0 .5rem"><span class="prompt">~ </span><span class="cmd">cat stack.json</span></div>
  <div class="fade-in" style="animation-delay:.3s">
    <div class="section-title">stack — click to filter</div>
    <div class="filter-bar">
      <button class="filter-btn active" data-filter="all" onclick="filterStack(this,'all')">all</button>
      <button class="filter-btn" data-filter="mobile" onclick="filterStack(this,'mobile')">mobile</button>
      <button class="filter-btn" data-filter="backend" onclick="filterStack(this,'backend')">backend</button>
      <button class="filter-btn" data-filter="ai" onclick="filterStack(this,'ai')">ai / genai</button>
      <button class="filter-btn" data-filter="infra" onclick="filterStack(this,'infra')">infra</button>
    </div>
    <div class="stack-grid" id="stackGrid">
      <div class="skill-row" data-cat="mobile"><span class="skill-name">Swift</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="90" style="width:0%"></div></div><span class="skill-pct">90%</span></div>
      <div class="skill-row" data-cat="mobile"><span class="skill-name">SwiftUI</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="85" style="width:0%"></div></div><span class="skill-pct">85%</span></div>
      <div class="skill-row" data-cat="mobile"><span class="skill-name">Push / Realtime</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="80" style="width:0%;background:var(--accent2)"></div></div><span class="skill-pct">80%</span></div>
      <div class="skill-row" data-cat="backend"><span class="skill-name">Python / FastAPI</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="88" style="width:0%;background:var(--accent2)"></div></div><span class="skill-pct">88%</span></div>
      <div class="skill-row" data-cat="backend"><span class="skill-name">Node.js</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="78" style="width:0%"></div></div><span class="skill-pct">78%</span></div>
      <div class="skill-row" data-cat="backend"><span class="skill-name">TypeScript</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="75" style="width:0%"></div></div><span class="skill-pct">75%</span></div>
      <div class="skill-row" data-cat="backend"><span class="skill-name">REST APIs</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="90" style="width:0%;background:var(--accent2)"></div></div><span class="skill-pct">90%</span></div>
      <div class="skill-row" data-cat="ai"><span class="skill-name">LangGraph</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="85" style="width:0%;background:var(--accent3)"></div></div><span class="skill-pct">85%</span></div>
      <div class="skill-row" data-cat="ai"><span class="skill-name">RAG Pipelines</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="88" style="width:0%;background:var(--accent3)"></div></div><span class="skill-pct">88%</span></div>
      <div class="skill-row" data-cat="ai"><span class="skill-name">ChromaDB</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="80" style="width:0%;background:var(--accent3)"></div></div><span class="skill-pct">80%</span></div>
      <div class="skill-row" data-cat="ai"><span class="skill-name">Prompt Engineering</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="82" style="width:0%;background:var(--accent3)"></div></div><span class="skill-pct">82%</span></div>
      <div class="skill-row" data-cat="ai"><span class="skill-name">Ollama / Mistral</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="78" style="width:0%;background:var(--accent3)"></div></div><span class="skill-pct">78%</span></div>
      <div class="skill-row" data-cat="infra"><span class="skill-name">Docker</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="82" style="width:0%"></div></div><span class="skill-pct">82%</span></div>
      <div class="skill-row" data-cat="infra"><span class="skill-name">Airflow</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="80" style="width:0%"></div></div><span class="skill-pct">80%</span></div>
      <div class="skill-row" data-cat="infra"><span class="skill-name">PostgreSQL</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="78" style="width:0%"></div></div><span class="skill-pct">78%</span></div>
      <div class="skill-row" data-cat="infra"><span class="skill-name">CI/CD</span><div class="skill-bar-wrap"><div class="skill-bar" data-pct="72" style="width:0%"></div></div><span class="skill-pct">72%</span></div>
    </div>
  </div>

  <div style="margin:1.5rem 0 .5rem"><span class="prompt">~ </span><span class="cmd">git log --timeline</span></div>
  <div class="fade-in" style="animation-delay:.4s">
    <div class="section-title">timeline</div>
    <div class="timeline">
      <div class="tl-item">
        <div class="tl-company">PayU <span style="color:var(--muted);font-weight:400;font-size:12px">(Naspers Group)</span></div>
        <div class="tl-role">Software Engineer Intern · Data & AI Platform</div>
        <div class="tl-period">Nov 2024 – Apr 2025</div>
      </div>
      <div class="tl-item">
        <div class="tl-company">Plavox</div>
        <div class="tl-role">iOS Developer · Gaming Platform</div>
        <div class="tl-period">Jun 2024 – Nov 2024</div>
      </div>
      <div class="tl-item">
        <div class="tl-company">Guardian Life</div>
        <div class="tl-role">iOS Developer Intern · Group Business Insurance</div>
        <div class="tl-period">Jan 2024 – Jun 2024</div>
      </div>
      <div class="tl-item" style="margin-bottom:0">
        <div class="tl-company">VIT Vellore</div>
        <div class="tl-role">B.Tech Computer Science · CGPA 8.62</div>
        <div class="tl-period">Sep 2021 – Aug 2025</div>
      </div>
    </div>
  </div>

  <div style="margin:1.5rem 0 .5rem"><span class="prompt">~ </span><span class="cmd">ls ./projects</span></div>
  <div class="fade-in" style="animation-delay:.5s">
    <div class="section-title">projects</div>
    <div class="projects-grid">
      <div class="proj-card" onclick="openLink('https://seraemos.com')">
        <div class="proj-name">Sera (EmOS) <span class="proj-badge">v4</span></div>
        <div class="proj-desc">Agentic AI companion · sole engineer · seraemos.com<br>5-layer signal architecture · longitudinal context · RAG-backed retrieval</div>
        <div class="proj-tags">
          <span class="proj-tag">LangGraph</span><span class="proj-tag">FastAPI</span><span class="proj-tag">ChromaDB</span><span class="proj-tag">Ollama</span><span class="proj-tag">RAG</span><span class="proj-tag">Docker</span>
        </div>
      </div>
      <div class="proj-card">
        <div class="proj-name">PayU Data Platform</div>
        <div class="proj-desc">Pipeline observability · Statica AI schemas · FB Ads API integration</div>
        <div class="proj-tags">
          <span class="proj-tag">Airflow</span><span class="proj-tag">PostgreSQL</span><span class="proj-tag">Python</span><span class="proj-tag">GenAI</span>
        </div>
      </div>
      <div class="proj-card">
        <div class="proj-name">Plavox iOS App</div>
        <div class="proj-desc">Zero to production · gaming platform · push notifications + tournaments</div>
        <div class="proj-tags">
          <span class="proj-tag">Swift</span><span class="proj-tag">SwiftUI</span><span class="proj-tag">REST APIs</span>
        </div>
      </div>
      <div class="proj-card">
        <div class="proj-name">Guardian Claim Filing</div>
        <div class="proj-desc">Self-service insurance claims · SwiftLint enforced · 15% dead code eliminated</div>
        <div class="proj-tags">
          <span class="proj-tag">Swift</span><span class="proj-tag">SwiftLint</span><span class="proj-tag">Periphery</span>
        </div>
      </div>
    </div>
  </div>

  <div style="margin:1.5rem 0 .5rem"><span class="prompt">~ </span><span class="cmd">curl github-stats/paarasv</span></div>
  <div class="fade-in" style="animation-delay:.6s">
    <div class="section-title">github stats</div>
    <div class="github-stats">
      <img src="https://github-readme-streak-stats.herokuapp.com?user=paarasv&theme=dark&hide_border=true&background=111118&ring=7c6aff&fire=00e5a0&currStreakLabel=7c6aff" alt="streak stats">
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=paarasv&layout=compact&hide_border=true&theme=dark&bg_color=111118&title_color=7c6aff&text_color=e8e8f0" alt="top languages">
    </div>
  </div>

  <div style="margin:1.5rem 0 .5rem"><span class="prompt">~ </span><span class="cmd">./find-me --all</span></div>
  <div class="fade-in" style="animation-delay:.7s">
    <div class="section-title">find me</div>
    <div class="links-row">
      <a class="link-btn" href="mailto:parasverma.pv.tech@gmail.com"><div class="link-dot"></div>email</a>
      <a class="link-btn" href="https://linkedin.com/in/paras1111" target="_blank"><div class="link-dot" style="background:var(--accent)"></div>linkedin</a>
      <a class="link-btn" href="https://github.com/paarasv" target="_blank"><div class="link-dot" style="background:var(--muted)"></div>github</a>
      <a class="link-btn" href="https://seraemos.com" target="_blank"><div class="link-dot" style="background:var(--accent3)"></div>seraemos.com</a>
    </div>
  </div>

  <div style="margin-top:2rem;padding-top:1rem;border-top:1px solid var(--border);font-size:11px;color:var(--muted);display:flex;justify-content:space-between">
    <span>building in public · shipping in silence</span>
    <span>paarasv<span class="cursor"></span></span>
  </div>

</div>

<script>
function filterStack(btn, cat) {
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('.skill-row').forEach(row => {
    row.classList.toggle('hidden', cat !== 'all' && row.dataset.cat !== cat);
  });
  animateBars();
}

function animateBars() {
  setTimeout(() => {
    document.querySelectorAll('.skill-row:not(.hidden) .skill-bar').forEach(bar => {
      bar.style.width = bar.dataset.pct + '%';
    });
  }, 50);
}

function countUp(el, target) {
  let n = 0;
  const step = Math.ceil(target / 20);
  const t = setInterval(() => {
    n = Math.min(n + step, target);
    el.textContent = n;
    if (n >= target) clearInterval(t);
  }, 40);
}

window.addEventListener('load', () => {
  document.querySelectorAll('[data-target]').forEach(el => {
    countUp(el, parseInt(el.dataset.target));
  });
  animateBars();
});
</script>
</body>
</html>
