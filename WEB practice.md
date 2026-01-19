  # Cascade Chat Conversation

  Note: _This is purely the output of the chat conversation and does not contain any raw data, codebase snippets, etc. used to generate the output._

### User Input

creat for me the best design  that has login and registter form by using html,css and Javascript.make sure the design  is unique and give it a tech design 

### Planner Response

# Tech-themed Login & Register UI (HTML, CSS, JS)

Below is a single-file, production-ready, modern auth UI with a unique tech aesthetic:
- **Neon particle network background**
- **Glassmorphism card with gradient cyber glow**
- **Tabbed Login/Register with sliding indicator**
- **Password reveal, real-time validation, tilt micro-interactions**
- **Responsive, accessible, reduced-motion support**

Save as `index.html` and open in your browser.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>NeonAuth — Login • Register</title>
  <meta name="theme-color" content="#0b1020" />
  <link rel="preconnect" href="https://fonts.googleapis.com" crossorigin />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />
  <style>
    :root{
      --bg-0:#070b1a;
      --bg-1:#0b1229;
      --panel:rgba(17,26,53,.52);
      --panel-strong:rgba(17,26,53,.72);
      --stroke:rgba(130,170,255,.18);
      --white:#e6f1ff;
      --muted:#9aa7c8;
      --acc-1:#00eaff;
      --acc-2:#8a2eff;
      --acc-3:#00ffa3;
      --ring: 0 0 0 2px color-mix(in srgb, var(--acc-1) 35%, transparent);
      --shadow-glow: 0 10px 40px rgba(0,234,255,.15), 0 2px 12px rgba(138,46,255,.12);
      --radius: 16px;
      --tab-index: 0;
      --rx: 0deg;
      --ry: 0deg;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      color:var(--white);
      font: 400 16px/1.5 Inter, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      background:
        radial-gradient(1200px 800px at 75% -10%, #10204b 0%, transparent 60%),
        radial-gradient(1000px 700px at -10% 110%, #0a203a 0%, transparent 60%),
        linear-gradient(180deg, var(--bg-0), var(--bg-1));
      overflow-x:hidden;
    }
    /* Animated tech grid overlay */
    body::before{
      content:"";
      position:fixed; inset:0;
      background:
        repeating-linear-gradient(90deg, rgba(169,199,255,.06) 0 1px, transparent 1px 80px),
        repeating-linear-gradient(0deg, rgba(169,199,255,.05) 0 1px, transparent 1px 80px);
      animation:gridShift 14s linear infinite;
      pointer-events:none; mix-blend-mode:overlay;
    }
    @keyframes gridShift{
      0%{background-position:0 0, 0 0}
      100%{background-position:160px 160px, 160px 160px}
    }
    /* Neon particle background canvas */
    #bg{
      position:fixed; inset:0; width:100%; height:100%;
      display:block; pointer-events:none; z-index:-1;
    }
    .shell{
      min-height:100%;
      display:grid; place-items:center;
      padding: clamp(20px, 5vw, 48px);
    }
    .brand{
      position:fixed; top:20px; left:24px; display:flex; align-items:center; gap:10px;
      user-select:none;
    }
    .brand .logo{
      width:28px; height:28px; filter: drop-shadow(0 0 10px rgba(0,234,255,.4));
    }
    .brand .name{
      font:700 18px/1.1 Orbitron, Inter, sans-serif;
      letter-spacing:.08em;
      background: linear-gradient(90deg, var(--acc-1), var(--acc-2) 60%, var(--acc-3));
      -webkit-background-clip:text; background-clip:text; color:transparent;
    }
    .card{
      width:min(940px, 92vw);
      backdrop-filter:saturate(130%) blur(14px);
      background: linear-gradient(180deg, var(--panel), transparent 120%);
      border:1px solid var(--stroke);
      border-radius:var(--radius);
      box-shadow: var(--shadow-glow);
      position:relative; padding:24px;
      transform: perspective(1200px) rotateX(var(--rx)) rotateY(var(--ry));
      transition: transform .15s ease-out, box-shadow .2s ease-out, border-color .2s ease-out;
      will-change: transform;
    }
    .card::before{
      /* cyber glow edge */
      content:"";
      position:absolute; inset:-1px;
      border-radius:inherit;
      padding:1px;
      background:
        conic-gradient(from 180deg at 50% 50%, color-mix(in srgb, var(--acc-1) 65%, transparent), color-mix(in srgb, var(--acc-2) 55%, transparent), color-mix(in srgb, var(--acc-3) 45%, transparent), transparent 80%);
      -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
      -webkit-mask-composite: xor; mask-composite: exclude;
      opacity:.45; pointer-events:none; filter: blur(.6px);
    }
    .tabs{
      position:relative; display:grid; grid-template-columns:1fr 1fr;
      gap:0; background: linear-gradient(180deg, rgba(13,21,42,.6), rgba(13,21,42,.25));
      border:1px solid var(--stroke); border-radius:12px; overflow:hidden;
    }
    .tab{
      position:relative; appearance:none; background:none; border:0; padding:14px 18px;
      color:var(--muted); font:600 14px/1 Inter, sans-serif; letter-spacing:.06em;
      text-transform:uppercase; cursor:pointer; z-index:2;
    }
    .tab[aria-selected="true"]{ color:var(--white) }
    .indicator{
      position:absolute; z-index:1; inset:2px; width:calc(50% - 4px); height:calc(100% - 4px);
      border-radius:10px;
      background: linear-gradient(180deg, rgba(0,234,255,.18), rgba(138,46,255,.18));
      border:1px solid color-mix(in srgb, var(--acc-1) 35%, transparent);
      box-shadow: inset 0 0 0 1px rgba(255,255,255,.06), 0 6px 22px rgba(0,234,255,.12);
      transform: translateX(calc(var(--tab-index) * 100%));
      transition: transform .35s cubic-bezier(.2, .7, 0, 1);
    }
    .inner{
      display:grid; grid-template-columns: 1.15fr .85fr; gap:24px; margin-top:16px;
    }
    @media (max-width: 940px){
      .inner{ grid-template-columns:1fr; }
    }
    .panel{
      border:1px solid var(--stroke); border-radius:12px; padding:18px 18px 10px;
      background: linear-gradient(180deg, var(--panel-strong), rgba(14,22,45,.38));
    }
    .panel h2{
      margin:0 0 8px 0; font:700 18px Orbitron, Inter, sans-serif; letter-spacing:.06em;
      text-transform:uppercase;
      background: linear-gradient(90deg, var(--acc-1), var(--acc-2));
      -webkit-background-clip:text; background-clip:text; color:transparent;
    }
    .subtle{margin:0 0 22px 0; color:var(--muted); font-size:14px}
    .form{ display:none; opacity:0; transform:translateY(8px); transition:opacity .2s ease, transform .2s ease }
    .form.visible{ display:block; opacity:1; transform:none }
    .field{ margin:0 0 14px 0 }
    .field label{ display:block; font-weight:600; font-size:13px; color:#c4d0ef; margin:0 0 6px 2px }
    .input{
      display:grid; grid-template-columns: 22px 1fr auto; align-items:center; gap:10px;
      background: rgba(9,16,36,.6);
      border:1px solid rgba(149,178,255,.18);
      border-radius:12px; padding:10px 12px;
    }
    .input:focus-within{ outline: none; box-shadow: var(--ring); border-color: color-mix(in srgb, var(--acc-1) 35%, transparent) }
    .icon{ display:grid; place-items:center; color:#a8b7e3; opacity:.9 }
    .input input{
      background:transparent; border:0; outline:0; color:var(--white); font:500 15px Inter, sans-serif;
      padding:4px 0;
    }
    .reveal{
      appearance:none; border:0; background:transparent; color:#a8b7e3;
      display:grid; place-items:center; width:28px; height:28px; border-radius:8px; cursor:pointer;
    }
    .reveal:hover{ color:#d3ddff }
    .row{ display:flex; align-items:center; justify-content:space-between; gap:14px; margin:8px 0 16px 0; flex-wrap:wrap }
    .check{ display:inline-flex; align-items:center; gap:8px; cursor:pointer; color:#c7d3f3; font-size:14px }
    .check input{ appearance:none; width:18px; height:18px; border-radius:5px; border:1px solid rgba(149,178,255,.25); display:grid; place-items:center; }
    .check input:checked{ background: linear-gradient(180deg, var(--acc-1), var(--acc-2)); border-color:transparent; box-shadow: inset 0 0 0 1px rgba(255,255,255,.35) }
    .check span{position:absolute; width:0; height:0; overflow:hidden}
    .link{ color:#9ddaff; text-decoration:none; font-weight:600 }
    .link:hover{ color:#c4edff; text-decoration:underline }
    .cta{
      appearance:none; border:0; cursor:pointer;
      display:inline-flex; align-items:center; gap:10px;
      padding:12px 16px; border-radius:12px; color:#021521; font:700 15px Inter, sans-serif;
      background: linear-gradient(90deg, var(--acc-1), var(--acc-2) 70%, var(--acc-3));
      box-shadow: 0 8px 28px rgba(0,234,255,.2);
      position:relative; overflow:hidden;
    }
    .cta::after{
      content:""; position:absolute; inset:0; background: linear-gradient(90deg, rgba(255,255,255,.0), rgba(255,255,255,.25), rgba(255,255,255,0)); transform: translateX(-120%);
      transition: transform .7s cubic-bezier(.2,.8,.2,1);
    }
    .cta:hover::after{ transform: translateX(120%) }
    .error{ display:block; min-height:14px; color:#ff8c8c; font-size:12.5px; padding:4px 2px 0 }
    .divider{
      display:flex; align-items:center; gap:10px; color:#90a5d8; font-size:12px; text-transform:uppercase; letter-spacing:.12em; margin:6px 0 12px
    }
    .divider::before,.divider::after{ content:""; flex:1; height:1px; background:linear-gradient(90deg, transparent, rgba(149,178,255,.24)) }
    .meta{
      border:1px dashed rgba(149,178,255,.28); color:#a8b7e3; border-radius:12px; padding:14px;
      background: linear-gradient(180deg, rgba(14,22,45,.45), rgba(14,22,45,.3));
    }
    .toast{
      position:fixed; left:50%; bottom:30px; transform:translateX(-50%) translateY(20px);
      background: rgba(10, 200, 200, .12);
      border:1px solid rgba(0,234,255,.35);
      color:#bff9ff; padding:10px 14px; border-radius:10px; opacity:0;
      box-shadow: 0 10px 30px rgba(0,234,255,.2);
      transition: opacity .25s ease, transform .25s ease;
      pointer-events:none; backdrop-filter: blur(6px);
    }
    .toast.show{ opacity:1; transform:translateX(-50%) translateY(0) }
    /* Accessibility focus */
    :focus-visible{ outline:2px solid color-mix(in srgb, var(--acc-1) 55%, transparent); outline-offset:2px; border-radius:10px }
    @media (prefers-reduced-motion: reduce){
      *{ animation:none !important; transition:none !important }
      body::before{ display:none }
    }
  </style>
</head>
<body>
  <canvas id="bg" aria-hidden="true"></canvas>

  <div class="brand">
    <svg class="logo" viewBox="0 0 64 64" aria-hidden="true">
      <defs>
        <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
          <stop offset="0" stop-color="#00eaff"/>
          <stop offset="0.6" stop-color="#8a2eff"/>
          <stop offset="1" stop-color="#00ffa3"/>
        </linearGradient>
      </defs>
      <path fill="url(#g)" d="M12 18a6 6 0 0 1 6-6h28a6 6 0 0 1 6 6v28a6 6 0 0 1-6 6H18a6 6 0 0 1-6-6V18Zm10 0h20v6H22v-6Zm0 11h20v17H22V29Z"/>
    </svg>
    <div class="name">NeonAuth</div>
  </div>

  <section class="card" id="card" role="region" aria-label="Authentication">
    <div class="tabs" role="tablist" aria-label="Authentication tabs" style="--tab-index:0">
      <button class="tab" id="login-tab" role="tab" aria-controls="loginForm" aria-selected="true" data-tab="login">Login</button>
      <button class="tab" id="register-tab" role="tab" aria-controls="registerForm" aria-selected="false" data-tab="register">Register</button>
      <span class="indicator" aria-hidden="true"></span>
    </div>

    <div class="inner">
      <div class="panel">
        <h2 id="panel-title">Welcome back</h2>
        <p class="subtle" id="panel-desc">Authenticate securely with a tech-grade interface.</p>

        <form id="loginForm" class="form visible" role="tabpanel" aria-labelledby="login-tab" aria-describedby="panel-desc" novalidate>
          <div class="field">
            <label for="login-email">Email</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M4 6h16v12H4z" stroke="#a8b7e3" stroke-width="1.5"/><path d="M4 7l8 6 8-6" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="login-email" name="email" type="email" placeholder="you@domain.com" autocomplete="email" required />
              <span></span>
            </div>
            <small class="error" id="err-login-email"></small>
          </div>

          <div class="field">
            <label for="login-pass">Password</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><rect x="5" y="11" width="14" height="8" rx="2" stroke="#a8b7e3" stroke-width="1.5"/><path d="M8 11V8a4 4 0 0 1 8 0v3" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="login-pass" name="password" type="password" placeholder="••••••••" autocomplete="current-password" minlength="8" required />
              <button type="button" class="reveal" aria-label="Toggle password visibility" data-target="login-pass">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M3 12s3.5-6 9-6 9 6 9 6-3.5 6-9 6-9-6-9-6Z" stroke="currentColor" stroke-width="1.5"/><circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="1.5"/></svg>
              </button>
            </div>
            <small class="error" id="err-login-pass"></small>
          </div>

          <div class="row">
            <label class="check">
              <input type="checkbox" id="remember" name="remember" />
              <span></span>
              Remember me
            </label>
            <a class="link" href="#" aria-label="Forgot password link">Forgot password?</a>
          </div>

          <button class="cta" type="submit">
            <span>Sign in</span>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" stroke="#001015" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </button>
        </form>

        <form id="registerForm" class="form" role="tabpanel" aria-labelledby="register-tab" aria-describedby="panel-desc" hidden novalidate>
          <div class="field">
            <label for="reg-name">Full name</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><circle cx="12" cy="8" r="4" stroke="#a8b7e3" stroke-width="1.5"/><path d="M4 20a8 8 0 0 1 16 0" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="reg-name" name="name" type="text" placeholder="Ada Lovelace" autocomplete="name" required />
              <span></span>
            </div>
            <small class="error" id="err-reg-name"></small>
          </div>

          <div class="field">
            <label for="reg-email">Email</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M4 6h16v12H4z" stroke="#a8b7e3" stroke-width="1.5"/><path d="M4 7l8 6 8-6" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="reg-email" name="email" type="email" placeholder="you@domain.com" autocomplete="email" required />
              <span></span>
            </div>
            <small class="error" id="err-reg-email"></small>
          </div>

          <div class="field">
            <label for="reg-pass">Password</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><rect x="5" y="11" width="14" height="8" rx="2" stroke="#a8b7e3" stroke-width="1.5"/><path d="M8 11V8a4 4 0 0 1 8 0v3" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="reg-pass" name="password" type="password" placeholder="Min 8 characters" minlength="8" required />
              <button type="button" class="reveal" aria-label="Toggle password visibility" data-target="reg-pass">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M3 12s3.5-6 9-6 9 6 9 6-3.5 6-9 6-9-6-9-6Z" stroke="currentColor" stroke-width="1.5"/><circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="1.5"/></svg>
              </button>
            </div>
            <small class="error" id="err-reg-pass"></small>
          </div>

          <div class="field">
            <label for="reg-pass2">Confirm password</label>
            <div class="input">
              <span class="icon" aria-hidden="true">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><rect x="5" y="11" width="14" height="8" rx="2" stroke="#a8b7e3" stroke-width="1.5"/><path d="M8 11V8a4 4 0 0 1 8 0v3" stroke="#a8b7e3" stroke-width="1.5"/></svg>
              </span>
              <input id="reg-pass2" name="password2" type="password" placeholder="Repeat password" minlength="8" required />
              <button type="button" class="reveal" aria-label="Toggle password visibility" data-target="reg-pass2">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M3 12s3.5-6 9-6 9 6 9 6-3.5 6-9 6-9-6-9-6Z" stroke="currentColor" stroke-width="1.5"/><circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="1.5"/></svg>
              </button>
            </div>
            <small class="error" id="err-reg-pass2"></small>
          </div>

          <div class="row">
            <label class="check">
              <input type="checkbox" id="terms" required />
              <span></span>
              I accept the Terms
            </label>
          </div>

          <button class="cta" type="submit">
            <span>Create account</span>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" stroke="#001015" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </button>
        </form>
      </div>

      <div class="panel">
        <h2>Security insights</h2>
        <p class="subtle">Your credentials are encrypted in transit. Choose a strong password.</p>
        <div class="divider">Tips</div>
        <div class="meta">
          • Use at least 8 chars with letters, numbers, and symbols.
          <br/>• Avoid reusing passwords across sites.
          <br/>• Enable 2FA when available.
        </div>
      </div>
    </div>
  </section>

  <div class="toast" id="toast" role="status" aria-live="polite" aria-atomic="true"></div>

  <script>
    // Utility
    const $ = (s, root=document) => root.querySelector(s);
    const $$ = (s, root=document) => Array.from(root.querySelectorAll(s));

    // Tabs
    const card = $('#card');
    const tabsEl = $('.tabs');
    const loginTab = $('#login-tab');
    const registerTab = $('#register-tab');
    const loginForm = $('#loginForm');
    const registerForm = $('#registerForm');
    const panelTitle = $('#panel-title');

    function setTab(which){
      const isReg = which === 'register';
      tabsEl.style.setProperty('--tab-index', isReg ? 1 : 0);

      loginTab.setAttribute('aria-selected', (!isReg).toString());
      registerTab.setAttribute('aria-selected', isReg.toString());

      loginForm.classList.toggle('visible', !isReg);
      registerForm.classList.toggle('visible', isReg);
      loginForm.hidden = isReg;
      registerForm.hidden = !isReg;
      panelTitle.textContent = isReg ? 'Create your account' : 'Welcome back';
    }

    loginTab.addEventListener('click', () => setTab('login'));
    registerTab.addEventListener('click', () => setTab('register'));

    // Tilt effect
    const prefersReduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
    if(!prefersReduce){
      card.addEventListener('pointermove', (e)=>{
        const r = card.getBoundingClientRect();
        const x = (e.clientX - r.left) / r.width;
        const y = (e.clientY - r.top) / r.height;
        const rx = (0.5 - y) * 8;
        const ry = (x - 0.5) * 10;
        card.style.setProperty('--rx', rx.toFixed(2) + 'deg');
        card.style.setProperty('--ry', ry.toFixed(2) + 'deg');
      });
      card.addEventListener('pointerleave', ()=>{
        card.style.setProperty('--rx', '0deg');
        card.style.setProperty('--ry', '0deg');
      });
    }

    // Reveal password toggles
    $$('.reveal').forEach(btn=>{
      btn.addEventListener('click', ()=>{
        const target = document.getElementById(btn.dataset.target);
        if(!target) return;
        target.type = target.type === 'password' ? 'text' : 'password';
        btn.setAttribute('aria-pressed', target.type === 'text');
      });
    });

    // Validation helpers
    const emailRx = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    function setError(field, msg){
      const small = field.closest('.field').querySelector('.error');
      if(small){ small.textContent = msg || ''; }
      field.setAttribute('aria-invalid', msg ? 'true' : 'false');
    }

    function toast(msg){
      const el = $('#toast');
      el.textContent = msg;
      el.classList.add('show');
      setTimeout(()=> el.classList.remove('show'), 2200);
    }

    // Login submit
    loginForm.addEventListener('submit', (e)=>{
      e.preventDefault();
      const email = $('#login-email');
      const pass = $('#login-pass');
      let ok = true;

      if(!email.value || !emailRx.test(email.value)){ setError(email, 'Enter a valid email'); ok = false; } else setError(email,'');
      if(!pass.value || pass.value.length < 8){ setError(pass, 'Password must be at least 8 characters'); ok=false; } else setError(pass,'');

      if(ok){
        toast('Signed in. Welcome back!');
        // Demo only. Replace with actual auth call.
      }
    });

    // Register submit
    registerForm.addEventListener('submit', (e)=>{
      e.preventDefault();
      const name = $('#reg-name');
      const email = $('#reg-email');
      const pass = $('#reg-pass');
      const pass2 = $('#reg-pass2');
      const terms = $('#terms');
      let ok = true;

      if(!name.value.trim()){ setError(name, 'Please enter your full name'); ok=false; } else setError(name,'');
      if(!email.value || !emailRx.test(email.value)){ setError(email, 'Enter a valid email'); ok=false; } else setError(email,'');
      if(!pass.value || pass.value.length < 8){ setError(pass, 'Use at least 8 characters'); ok=false; } else setError(pass,'');
      if(pass2.value !== pass.value){ setError(pass2, 'Passwords do not match'); ok=false; } else setError(pass2,'');
      if(!terms.checked){ toast('Please accept the Terms'); ok=false; }

      if(ok){
        toast('Account created. You can sign in now!');
        setTab('login');
      }
    });

    // Clear errors on input
    $$('input').forEach(inp => {
      inp.addEventListener('input', ()=> setError(inp, ''));
    });

    // Neon particle network background
    (function(){
      const canvas = document.getElementById('bg');
      const ctx = canvas.getContext('2d');
      const DPR = Math.min(window.devicePixelRatio || 1, 2);
      let w,h, nodes=[], mouse={x:-1e9,y:-1e9};

      function resize(){
        w = canvas.clientWidth;
        h = canvas.clientHeight;
        canvas.width = Math.floor(w * DPR);
        canvas.height = Math.floor(h * DPR);
        ctx.setTransform(DPR,0,0,DPR,0,0);
        init();
      }

      function init(){
        const count = Math.max(40, Math.min(120, Math.floor((w*h)/26000)));
        nodes = Array.from({length: count}, ()=>({
          x: Math.random()*w,
          y: Math.random()*h,
          vx: (Math.random()*2-1)*0.4,
          vy: (Math.random()*2-1)*0.4,
          r: Math.random()*1.6 + 0.6
        }));
      }

      function step(){
        ctx.clearRect(0,0,w,h);

        // draw connections
        const maxD = Math.min(150, Math.max(90, Math.hypot(w,h)/20));
        for(let i=0;i<nodes.length;i++){
          const a = nodes[i];
          // move
          a.x += a.vx; a.y += a.vy;

          // bounce borders
          if(a.x < 0 || a.x > w) a.vx *= -1;
          if(a.y < 0 || a.y > h) a.vy *= -1;

          // mouse repulsion
          const dxm = a.x - mouse.x;
          const dym = a.y - mouse.y;
          const dm = Math.hypot(dxm,dym);
          if(dm < 100){
            a.vx += dxm / (dm||1) * 0.05;
            a.vy += dym / (dm||1) * 0.05;
          }

          // node point
          ctx.beginPath();
          ctx.arc(a.x, a.y, a.r, 0, Math.PI*2);
          ctx.fillStyle = 'rgba(185, 233, 255, .5)';
          ctx.fill();

          for(let j=i+1;j<nodes.length;j++){
            const b = nodes[j];
            const dx = a.x - b.x;
            const dy = a.y - b.y;
            const d = Math.hypot(dx,dy);
            if(d < maxD){
              const t = 1 - d/maxD;
              ctx.beginPath();
              ctx.moveTo(a.x, a.y);
              ctx.lineTo(b.x, b.y);
              // blend accent color across distance
              const r = Math.floor(0 + 120*t);
              const g = Math.floor(234 - 80*t);
              const bC = Math.floor(255 - 120*t);
              ctx.strokeStyle = `rgba(${r}, ${g}, ${bC}, ${0.22 * t})`;
              ctx.lineWidth = 1;
              ctx.stroke();
            }
          }
        }
        raf = requestAnimationFrame(step);
      }

      let raf;
      const reduce = window.matchMedia('(prefers-reduced-motion: reduce)');
      function start(){
        if(reduce.matches) return;
        cancelAnimationFrame(raf);
        step();
      }

      window.addEventListener('resize', resize);
      window.addEventListener('pointermove', e=>{ mouse.x=e.clientX; mouse.y=e.clientY; }, {passive:true});
      window.addEventListener('pointerleave', ()=>{ mouse.x=-1e9; mouse.y=-1e9; }, {passive:true});
      reduce.addEventListener?.('change', ()=> { resize(); start(); });

      resize(); start();
    })();
  </script>
</body>
</html>
```

# How to use
- **Save** the code above as `index.html`.
- **Open** it in your browser. No build step or dependencies needed.
- Optional: I can split CSS/JS into separate `style.css` and `app.js` files if you prefer.

# Optional customizations
- **Palette swap:** want green/cyan, purple/pink, or a brand color? Tell me your hex values.
- **Logo/brand:** replace “NeonAuth” with your product name or logo.
- **Validation rules:** adjust password policy, add username, or hook to your backend API.

# Task status
- **Delivered**: A unique, tech-styled login/register UI in a single self-contained HTML file.
- **Pending**: Your preferences on colors, branding, and file structure (single file vs. separated).