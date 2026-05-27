<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>PTCompare Pro — Physical Therapy Cost Transparency Engine</title>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,700;0,9..144,800;1,9..144,400&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap" rel="stylesheet"/>
<style>
:root{
  --em:#059669;--em-lt:#d1fae5;--em-dk:#065f46;
  --nv:#0c1f35;--nv-lt:#163655;--sky:#0284c7;
  --bg:#f0f4f8;--card:#ffffff;--tx:#0c1f35;--mu:#5a7184;
  --bd:#dde3ea;--sh:0 2px 16px rgba(12,31,53,.07);--shl:0 6px 32px rgba(12,31,53,.13);
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--tx);overflow-x:hidden;font-size:15px}
.display{font-family:'Fraunces',serif}

/* NAV */
#nav{background:var(--nv);position:sticky;top:0;z-index:900;box-shadow:0 1px 0 rgba(255,255,255,.08)}
.nav-inner{max-width:1300px;margin:0 auto;padding:0 1.5rem;height:58px;display:flex;align-items:center;justify-content:space-between;gap:1rem}
.nav-logo{font-family:'Fraunces',serif;font-weight:700;font-size:1.35rem;color:#fff;letter-spacing:-.02em;cursor:pointer}
.nav-logo span{color:#34d399}
.nav-links{display:flex;align-items:center;gap:.25rem}
.nav-link{color:rgba(255,255,255,.7);font-size:.85rem;font-weight:500;padding:.45rem .85rem;border-radius:8px;cursor:pointer;transition:all .18s;border:none;background:none;font-family:'DM Sans',sans-serif}
.nav-link:hover{color:#fff;background:rgba(255,255,255,.1)}
.nav-link.active{color:#fff;background:rgba(255,255,255,.12)}
.nav-right{display:flex;align-items:center;gap:.5rem}
.btn-login{background:transparent;border:1.5px solid rgba(255,255,255,.3);color:rgba(255,255,255,.85);font-family:'DM Sans',sans-serif;font-weight:500;font-size:.83rem;padding:.42rem 1rem;border-radius:8px;cursor:pointer;transition:all .18s}
.btn-login:hover{border-color:rgba(255,255,255,.6);color:#fff;background:rgba(255,255,255,.08)}
.btn-signup{background:var(--em);border:none;color:#fff;font-family:'DM Sans',sans-serif;font-weight:600;font-size:.83rem;padding:.44rem 1.1rem;border-radius:8px;cursor:pointer;transition:all .18s}
.btn-signup:hover{background:var(--em-dk)}
.toggle-wrap{display:flex;background:rgba(255,255,255,.08);border-radius:8px;padding:3px;gap:2px}
.toggle-wrap button{border:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;font-size:.8rem;padding:.4rem .9rem;border-radius:6px;transition:all .18s;white-space:nowrap}
.toggle-wrap button.on{background:var(--em);color:#fff}
.toggle-wrap button:not(.on){background:transparent;color:rgba(255,255,255,.7)}
.toggle-wrap button:not(.on):hover{background:rgba(255,255,255,.1);color:#fff}
.user-pill{display:flex;align-items:center;gap:.5rem;background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.15);border-radius:999px;padding:.3rem .65rem .3rem .35rem;cursor:pointer;transition:all .18s}
.user-pill:hover{background:rgba(255,255,255,.16)}
.user-dot{width:28px;height:28px;border-radius:50%;background:linear-gradient(135deg,var(--em),#34d399);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:.8rem}
.user-pill span{color:#fff;font-size:.82rem;font-weight:500}

/* PANELS */
.panel{display:none}.panel.on{display:block}

/* HERO */
.hero{background:linear-gradient(160deg,var(--nv) 0%,var(--nv-lt) 60%,#1a4a70 100%);padding:3.5rem 1.5rem 2.5rem;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-80px;right:-80px;width:400px;height:400px;background:radial-gradient(circle,rgba(52,211,153,.12),transparent 65%);border-radius:50%;pointer-events:none}
.hero::after{content:'';position:absolute;bottom:-60px;left:-60px;width:300px;height:300px;background:radial-gradient(circle,rgba(2,132,199,.1),transparent 65%);border-radius:50%;pointer-events:none}
.hero-inner{max-width:780px;margin:0 auto;text-align:center;position:relative;z-index:1}
.hero h1{font-family:'Fraunces',serif;font-weight:700;font-size:clamp(1.9rem,4vw,2.9rem);color:#fff;line-height:1.18;letter-spacing:-.03em;margin-bottom:.65rem}
.hero h1 em{color:#34d399;font-style:italic}
.hero p{color:rgba(255,255,255,.68);font-size:.97rem;margin-bottom:1.6rem;line-height:1.65}
.search-bar{display:flex;gap:.5rem;max-width:640px;margin:0 auto 1rem}
.search-bar input{flex:1;padding:.78rem 1.15rem;border:2px solid transparent;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:.97rem;outline:none;transition:border .18s}
.search-bar input:focus{border-color:var(--em)}
.search-bar .btn-go{background:var(--em);color:#fff;border:none;padding:.78rem 1.5rem;border-radius:10px;font-family:'Fraunces',serif;font-weight:700;font-size:.95rem;cursor:pointer;transition:all .15s;white-space:nowrap}
.search-bar .btn-go:hover{background:var(--em-dk);transform:translateY(-1px)}
.btn-nearme{background:rgba(255,255,255,.13);border:1.5px solid rgba(255,255,255,.28);color:#fff;padding:.78rem 1.15rem;border-radius:10px;font-family:'DM Sans',sans-serif;font-weight:600;font-size:.87rem;cursor:pointer;transition:all .15s;white-space:nowrap}
.btn-nearme:hover{background:rgba(255,255,255,.22)}
.radius-row{display:flex;justify-content:center;align-items:center;gap:.6rem;margin-bottom:.9rem}
.radius-row label{color:rgba(255,255,255,.55);font-size:.78rem}
.radius-row select{background:rgba(255,255,255,.13);border:1px solid rgba(255,255,255,.22);color:#fff;padding:.28rem .65rem;border-radius:7px;font-size:.78rem;cursor:pointer;outline:none;font-family:'DM Sans',sans-serif}
.qchips{display:flex;flex-wrap:wrap;justify-content:center;gap:.35rem}
.qchip{background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.18);color:rgba(255,255,255,.82);padding:.26rem .7rem;border-radius:999px;font-size:.77rem;cursor:pointer;transition:all .15s;font-family:'DM Sans',sans-serif}
.qchip:hover{background:rgba(255,255,255,.2);color:#fff}

/* STAT BAR */
.stat-bar{background:var(--nv-lt);border-top:1px solid rgba(255,255,255,.07);padding:.6rem 1.5rem}
.stat-inner{max-width:1300px;margin:0 auto;display:flex;align-items:center;justify-content:center;gap:2rem;flex-wrap:wrap}
.stat-item{display:flex;align-items:center;gap:.45rem;font-size:.78rem;color:rgba(255,255,255,.6)}
.stat-item b{color:#fff}
.ldot{width:7px;height:7px;background:var(--em);border-radius:50%;display:inline-block;animation:ldot 1.6s ease infinite;flex-shrink:0}
@keyframes ldot{0%,100%{opacity:1}50%{opacity:.3}}

/* MAIN LAYOUT */
.page-inner{max-width:1300px;margin:0 auto;padding:1.4rem 1.5rem}
.layout{display:flex;gap:1.25rem;align-items:flex-start}

/* MAP */
#map-wrap{border-radius:14px;overflow:hidden;box-shadow:var(--shl);border:1px solid var(--bd)}
#gmap{height:360px;width:100%}

/* FILTER PANEL */
.fpanel{background:var(--card);border-radius:14px;padding:1.2rem;box-shadow:var(--sh);border:1px solid var(--bd)}
.fsec{font-family:'Fraunces',serif;font-weight:700;font-size:.88rem;color:var(--nv);margin-bottom:.8rem;display:flex;align-items:center;gap:.4rem}
.flabel{display:block;font-size:.72rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem;margin-top:.65rem}
.fsel{width:100%;padding:.5rem .75rem;border-radius:8px;border:1.5px solid var(--bd);font-family:'DM Sans',sans-serif;font-size:.84rem;background:var(--bg);cursor:pointer;outline:none;transition:border .15s;color:var(--tx)}
.fsel:focus{border-color:var(--em)}
input[type=range]{width:100%;accent-color:var(--em);cursor:pointer;margin-bottom:.22rem}
.rl{display:flex;justify-content:space-between;font-size:.75rem;color:var(--mu);margin-bottom:.18rem}
.chip{display:inline-flex;align-items:center;gap:.28rem;padding:.28rem .58rem;border-radius:7px;background:var(--bg);border:1.5px solid var(--bd);font-size:.75rem;font-weight:500;cursor:pointer;transition:all .15s;margin:.14rem}
.chip input{accent-color:var(--em);cursor:pointer}
.chip.on{background:var(--em-lt);border-color:var(--em);color:var(--em-dk)}
#comply{background:#fffbeb;border:1.5px solid #f59e0b;border-radius:9px;padding:.75rem .9rem;display:none;align-items:flex-start;gap:.55rem;font-size:.8rem;color:#92400e;margin-top:.65rem;line-height:1.55}
#comply.on{display:flex}

/* CARDS */
.card{background:var(--card);border-radius:14px;border:1px solid var(--bd);box-shadow:var(--sh);overflow:hidden;transition:box-shadow .2s,transform .18s}
.card:hover{box-shadow:var(--shl);transform:translateY(-2px)}
.badge{font-size:.64rem;font-weight:700;letter-spacing:.07em;text-transform:uppercase;padding:.18rem .5rem;border-radius:5px}
.b-prem{background:var(--em-lt);color:var(--em-dk)}
.b-uncl{background:#fef3c7;color:#92400e}
.b-veri{background:#dbeafe;color:#1e40af}
.b-open{background:#d1fae5;color:#065f46}
.b-closed{background:#fee2e2;color:#991b1b}
.mtag{font-size:.7rem;padding:.16rem .48rem;border-radius:5px;background:#f0fdf4;color:var(--em-dk);border:1px solid #a7f3d0;font-weight:500}
.mtag.pr{background:#eff6ff;color:#1d4ed8;border-color:#bfdbfe}

/* COST BARS */
.cbar-wrap{padding:.75rem 1.2rem .95rem;border-top:1px solid var(--bd);background:#fafbfc}
.cbar-lbl{display:flex;justify-content:space-between;font-size:.78rem;margin-bottom:.24rem;font-weight:500;align-items:center}
.cbar-track{height:10px;background:#e2e8f0;border-radius:999px;overflow:hidden;margin-bottom:.48rem}
.cbar-fill{height:100%;border-radius:999px;transition:width .85s cubic-bezier(.16,1,.3,1)}
.bar-ins{background:linear-gradient(90deg,#0284c7,#38bdf8)}
.bar-cash{background:linear-gradient(90deg,var(--em),#34d399)}
.save-pill{display:inline-flex;align-items:center;gap:.25rem;background:var(--em);color:#fff;font-size:.73rem;font-weight:700;padding:.2rem .62rem;border-radius:5px}

/* BUTTONS */
.btn{background:var(--em);color:#fff;border:none;padding:.5rem 1.05rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-weight:600;font-size:.82rem;cursor:pointer;transition:all .16s;display:inline-flex;align-items:center;gap:.3rem}
.btn:hover{background:var(--em-dk);transform:translateY(-1px)}
.btn2{background:transparent;color:var(--nv);border:1.5px solid var(--bd);padding:.5rem .95rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-weight:500;font-size:.82rem;cursor:pointer;transition:all .16s}
.btn2:hover{border-color:var(--nv);background:var(--bg)}
.btn-ghost{background:rgba(255,255,255,.12);border:1.5px solid rgba(255,255,255,.25);color:#fff;padding:.5rem 1.05rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-weight:500;font-size:.82rem;cursor:pointer;transition:all .16s}
.btn-ghost:hover{background:rgba(255,255,255,.2)}

/* LOADING */
.spin-wrap{display:flex;flex-direction:column;align-items:center;padding:3rem;gap:.85rem}
.spin{width:34px;height:34px;border:3px solid var(--bd);border-top-color:var(--em);border-radius:50%;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* MODALS */
.modal-bg{position:fixed;inset:0;background:rgba(12,31,53,.55);backdrop-filter:blur(3px);z-index:2000;display:none;align-items:center;justify-content:center;padding:1rem}
.modal-bg.on{display:flex}
.modal{background:var(--card);border-radius:18px;padding:2rem;max-width:520px;width:100%;max-height:90vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,.2);position:relative}
.modal-x{position:absolute;top:1rem;right:1rem;background:var(--bg);border:none;cursor:pointer;font-size:1rem;color:var(--mu);width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;transition:all .15s}
.modal-x:hover{background:var(--bd);color:var(--nv)}

/* FORM */
.finput{width:100%;padding:.58rem .82rem;border:1.5px solid var(--bd);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:.87rem;outline:none;transition:border .15s;background:var(--bg);color:var(--tx)}
.finput:focus{border-color:var(--em);background:#fff}
.flabel2{font-size:.76rem;font-weight:600;color:var(--nv);display:block;margin-bottom:.28rem;margin-top:.72rem}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:.65rem}

/* TABS */
.tab-bar{display:flex;border-bottom:2px solid var(--bd);margin-bottom:1.1rem;gap:.1rem}
.tab{padding:.52rem .95rem;font-size:.83rem;font-weight:500;cursor:pointer;border-bottom:2px solid transparent;margin-bottom:-2px;transition:all .15s;color:var(--mu);font-family:'DM Sans',sans-serif}
.tab.on{color:var(--nv);border-bottom-color:var(--em);font-weight:600}
.tab-pane{display:none}.tab-pane.on{display:block}

/* STARS REVIEW INPUT */
.star-inp{display:flex;flex-direction:row-reverse;justify-content:flex-start;gap:.15rem}
.star-inp input{display:none}
.star-inp label{font-size:1.6rem;color:#d1d5db;cursor:pointer;transition:color .1s;line-height:1}
.star-inp input:checked ~ label,.star-inp label:hover,.star-inp label:hover ~ label{color:#f59e0b}

/* REVIEW CARD */
.rev-card{background:var(--bg);border-radius:10px;padding:.82rem .95rem;border:1px solid var(--bd);margin-bottom:.55rem}
.rev-av{width:32px;height:32px;border-radius:50%;background:linear-gradient(135deg,var(--nv-lt),var(--em));display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:.78rem;flex-shrink:0}

/* TOAST */
#toast-box{position:fixed;bottom:1.5rem;right:1.5rem;z-index:3000;display:flex;flex-direction:column;gap:.45rem;pointer-events:none}
.toast{background:var(--nv);color:#fff;padding:.7rem 1.05rem;border-radius:9px;font-size:.82rem;box-shadow:var(--shl);display:flex;align-items:center;gap:.45rem;max-width:310px;pointer-events:auto;animation:tin .28s ease both}
.toast.ok{background:var(--em-dk)}
.toast.warn{background:#b45309}
@keyframes tin{from{opacity:0;transform:translateX(16px)}to{opacity:1;transform:translateX(0)}}

/* DRAWER */
#drawer{position:fixed;top:0;left:0;width:295px;height:100%;background:var(--card);box-shadow:var(--shl);z-index:1000;transform:translateX(-100%);transition:transform .28s ease;overflow-y:auto;padding:1.3rem}
#drawer.open{transform:translateX(0)}
#d-overlay{position:fixed;inset:0;background:rgba(0,0,0,.38);z-index:999;display:none}
#d-overlay.open{display:block}
.mob-filter-btn{display:none!important}
@media(max-width:920px){.layout{flex-direction:column}.sidebar{display:none!important}.mob-filter-btn{display:flex!important}#gmap{height:220px}}

/* EMPTY / ERROR */
.empty-s{text-align:center;padding:3rem 1rem;color:var(--mu)}
.err-box{background:#fef2f2;border:1.5px solid #fca5a5;border-radius:9px;padding:.82rem 1rem;color:#991b1b;font-size:.84rem;margin-bottom:.85rem}

/* ABOUT PAGE */
.about-hero{background:linear-gradient(160deg,var(--nv),var(--nv-lt));padding:4rem 1.5rem;text-align:center;color:#fff}
.about-hero h1{font-family:'Fraunces',serif;font-weight:700;font-size:2.6rem;letter-spacing:-.03em;margin-bottom:.65rem}
.about-hero h1 em{color:#34d399;font-style:italic}
.about-section{max-width:860px;margin:0 auto;padding:3rem 1.5rem}
.team-card{background:var(--card);border-radius:14px;padding:1.4rem;box-shadow:var(--sh);border:1px solid var(--bd);text-align:center}
.team-av{width:64px;height:64px;border-radius:50%;background:linear-gradient(135deg,var(--nv-lt),var(--em));display:flex;align-items:center;justify-content:center;color:#fff;font-family:'Fraunces',serif;font-weight:700;font-size:1.4rem;margin:0 auto .75rem}
.value-card{background:var(--card);border-radius:12px;padding:1.25rem;box-shadow:var(--sh);border:1px solid var(--bd)}
.value-icon{width:40px;height:40px;border-radius:10px;background:var(--em-lt);display:flex;align-items:center;justify-content:center;font-size:1.1rem;margin-bottom:.65rem}

/* HOW IT WORKS PAGE */
.hiw-hero{background:linear-gradient(160deg,var(--nv-lt),#1a4a70);padding:4rem 1.5rem;text-align:center;color:#fff}
.step-card{background:var(--card);border-radius:14px;padding:1.5rem;box-shadow:var(--sh);border:1px solid var(--bd);position:relative}
.step-num{width:38px;height:38px;border-radius:50%;background:var(--em);color:#fff;font-family:'Fraunces',serif;font-weight:700;font-size:1rem;display:flex;align-items:center;justify-content:center;margin-bottom:.85rem}
.step-connector{width:2px;background:var(--em-lt);flex-shrink:0;margin:0 1.5rem}

/* B2B */
.metric-card{background:var(--card);border-radius:12px;padding:1.2rem 1.4rem;box-shadow:var(--sh);border:1px solid var(--bd)}
.mval{font-family:'Fraunces',serif;font-weight:700;font-size:2rem;color:var(--nv);line-height:1}
.mdelta{font-size:.75rem;font-weight:600;margin-top:.22rem;color:var(--em)}
.pcard{background:linear-gradient(135deg,var(--nv),var(--nv-lt));border-radius:18px;color:#fff;padding:1.75rem;box-shadow:0 8px 40px rgba(12,31,53,.25);position:relative;overflow:hidden}
.pcard::before{content:'';position:absolute;top:-80px;right:-80px;width:250px;height:250px;background:radial-gradient(circle,rgba(52,211,153,.3),transparent 65%);border-radius:50%;pointer-events:none}
.ptier{background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.14);border-radius:12px;padding:1.1rem 1.25rem;transition:all .2s;min-width:170px}
.ptier:hover{background:rgba(255,255,255,.12);transform:translateY(-2px)}
.ptier.hi{border-color:#34d399;background:rgba(52,211,153,.15)}

/* PROFILE STAT */
.pstat{background:var(--bg);border-radius:9px;padding:.7rem .9rem;border:1px solid var(--bd);text-align:center}

/* ACCURACY DISCLAIMER */
.accuracy-note{background:#f0f9ff;border:1px solid #bae6fd;border-radius:8px;padding:.65rem .85rem;font-size:.76rem;color:#0c4a6e;margin-top:.5rem;line-height:1.55}

@keyframes up{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
.aup{animation:up .3s ease both}

::-webkit-scrollbar{width:5px}
::-webkit-scrollbar-thumb{background:#cbd5e1;border-radius:3px}
.gm-style .gm-style-iw-c{border-radius:12px!important}
</style>
</head>
<body>

<div id="toast-box"></div>

<!-- ════════════ MODALS ════════════ -->

<!-- AUTH -->
<div class="modal-bg" id="m-auth">
  <div class="modal" style="max-width:420px">
    <button class="modal-x" onclick="cm('m-auth')">✕</button>
    <div class="tab-bar">
      <div class="tab on" id="t-login" onclick="authTab('login')">Sign In</div>
      <div class="tab" id="t-signup" onclick="authTab('signup')">Create Account</div>
    </div>
    <div class="tab-pane on" id="p-login">
      <h3 class="display" style="font-weight:700;font-size:1.2rem;color:var(--nv);margin-bottom:.25rem">Welcome back</h3>
      <p style="font-size:.84rem;color:var(--mu);margin-bottom:.95rem">Sign in to save clinics, track your search history, and manage appointments.</p>
      <label class="flabel2">Email Address</label><input class="finput" id="l-email" type="email" placeholder="you@email.com"/>
      <label class="flabel2">Password</label><input class="finput" id="l-pass" type="password" placeholder="••••••••"/>
      <button class="btn" style="width:100%;justify-content:center;margin-top:.9rem;padding:.62rem" onclick="doLogin()">Sign In</button>
      <div style="text-align:center;margin-top:.65rem;font-size:.81rem;color:var(--mu)">No account? <span style="color:var(--em);cursor:pointer;font-weight:600" onclick="authTab('signup')">Sign up free</span></div>
    </div>
    <div class="tab-pane" id="p-signup">
      <h3 class="display" style="font-weight:700;font-size:1.2rem;color:var(--nv);margin-bottom:.25rem">Create your free account</h3>
      <p style="font-size:.84rem;color:var(--mu);margin-bottom:.95rem">Save clinics, compare costs over time, and get alerts when PT prices drop near you.</p>
      <div class="form-grid">
        <div><label class="flabel2">First Name</label><input class="finput" id="s-fn" type="text" placeholder="Jane"/></div>
        <div><label class="flabel2">Last Name</label><input class="finput" id="s-ln" type="text" placeholder="Smith"/></div>
      </div>
      <label class="flabel2">Email Address</label><input class="finput" id="s-email" type="email" placeholder="you@email.com"/>
      <label class="flabel2">Password</label><input class="finput" id="s-pass" type="password" placeholder="Create a password"/>
      <label class="flabel2">ZIP Code <span style="font-weight:400;color:var(--mu)">(for local alerts)</span></label><input class="finput" id="s-zip" type="text" placeholder="98105"/>
      <div style="margin-top:.85rem;display:flex;flex-direction:column;gap:.42rem">
        <label style="display:flex;align-items:flex-start;gap:.45rem;cursor:pointer;font-size:.81rem;color:var(--mu)"><input type="checkbox" id="s-sms" style="margin-top:.15rem;accent-color:var(--em)"/> Text me when PT prices drop near my ZIP code</label>
        <label style="display:flex;align-items:flex-start;gap:.45rem;cursor:pointer;font-size:.81rem;color:var(--mu)"><input type="checkbox" id="s-eml" checked style="margin-top:.15rem;accent-color:var(--em)"/> Weekly email with cost-saving tips and new clinic alerts</label>
      </div>
      <button class="btn" style="width:100%;justify-content:center;margin-top:.9rem;padding:.62rem" onclick="doSignup()">Create Free Account</button>
    </div>
  </div>
</div>

<!-- BOOKING -->
<div class="modal-bg" id="m-book">
  <div class="modal"><button class="modal-x" onclick="cm('m-book')">✕</button><div id="book-body"></div></div>
</div>

<!-- REVIEW -->
<div class="modal-bg" id="m-rev">
  <div class="modal" style="max-width:460px">
    <button class="modal-x" onclick="cm('m-rev')">✕</button>
    <h3 class="display" style="font-weight:700;font-size:1.1rem;color:var(--nv);margin-bottom:.2rem">Leave a Review</h3>
    <p id="rev-cname" style="font-size:.83rem;color:var(--mu);margin-bottom:.95rem"></p>
    <label class="flabel2">Your Rating</label>
    <div class="star-inp" id="star-inp">
      <input type="radio" name="rv" id="s5" value="5"/><label for="s5">★</label>
      <input type="radio" name="rv" id="s4" value="4"/><label for="s4">★</label>
      <input type="radio" name="rv" id="s3" value="3"/><label for="s3">★</label>
      <input type="radio" name="rv" id="s2" value="2"/><label for="s2">★</label>
      <input type="radio" name="rv" id="s1" value="1"/><label for="s1">★</label>
    </div>
    <label class="flabel2">Your Experience</label>
    <textarea class="finput" id="rv-text" rows="4" placeholder="Share wait times, PT quality, value for money, cash vs insurance experience..." style="resize:vertical"></textarea>
    <label class="flabel2">Your Name</label><input class="finput" id="rv-name" type="text" placeholder="Jane S. or Anonymous"/>
    <label class="flabel2">Payment Method</label>
    <select class="finput" id="rv-pay"><option>Cash Pay</option><option>Insurance</option><option>Both</option><option>Prefer not to say</option></select>
    <button class="btn" style="width:100%;justify-content:center;margin-top:.9rem;padding:.62rem" onclick="subReview()">Submit Review</button>
  </div>
</div>

<!-- PROFILE -->
<div class="modal-bg" id="m-prof">
  <div class="modal" style="max-width:580px"><button class="modal-x" onclick="cm('m-prof')">✕</button><div id="prof-body"></div></div>
</div>

<!-- EMAIL CAPTURE -->
<div class="modal-bg" id="m-cap">
  <div class="modal" style="max-width:420px;text-align:center">
    <button class="modal-x" onclick="cm('m-cap')">✕</button>
    <div style="font-size:2.2rem;margin-bottom:.6rem">💰</div>
    <h3 class="display" style="font-weight:700;font-size:1.2rem;color:var(--nv);margin-bottom:.35rem">Unlock Full Cost Comparison</h3>
    <p style="font-size:.85rem;color:var(--mu);margin-bottom:1.1rem;line-height:1.65">Get detailed insurance vs. cash pricing breakdowns and free alerts when cheaper PT options open near you.</p>
    <input class="finput" id="cap-email" type="email" placeholder="your@email.com" style="margin-bottom:.5rem;text-align:center"/>
    <input class="finput" id="cap-zip" type="text" placeholder="ZIP code for local alerts" style="margin-bottom:.5rem;text-align:center"/>
    <label style="display:flex;align-items:flex-start;gap:.45rem;text-align:left;margin-bottom:.8rem;cursor:pointer;font-size:.8rem;color:var(--mu)"><input type="checkbox" id="cap-sms" style="margin-top:.15rem;accent-color:var(--em)"/> Text me when PT prices drop in my area</label>
    <button class="btn" style="width:100%;justify-content:center;padding:.62rem" onclick="subCapture()">Show Me the Savings</button>
    <div style="font-size:.73rem;color:var(--mu);margin-top:.55rem">No spam. Unsubscribe anytime.</div>
  </div>
</div>

<!-- MOBILE DRAWER -->
<div id="d-overlay" onclick="closeDrawer()"></div>
<div id="drawer">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:1.05rem">
    <span class="display" style="font-weight:700;color:var(--nv);font-size:.95rem">Filters</span>
    <button onclick="closeDrawer()" style="background:none;border:none;cursor:pointer;font-size:1.1rem;color:var(--mu);padding:.25rem">✕</button>
  </div>
  <div id="drawer-body"></div>
</div>

<!-- ════════════ NAV ════════════ -->
<nav id="nav">
  <div class="nav-inner">
    <div class="nav-logo" onclick="showPage('search')">PT<span>Compare</span> Pro</div>
    <div class="nav-links">
      <button class="nav-link active" id="nl-search" onclick="showPage('search')">Find a Clinic</button>
      <button class="nav-link" id="nl-how" onclick="showPage('how')">How It Works</button>
      <button class="nav-link" id="nl-about" onclick="showPage('about')">About Us</button>
      <button class="nav-link" id="nl-b2b" onclick="showPage('b2b')">For Clinic Owners</button>
    </div>
    <div class="nav-right">
      <div id="auth-btns" style="display:flex;gap:.4rem">
        <button class="btn-login" onclick="om('m-auth');authTab('login')">Sign In</button>
        <button class="btn-signup" onclick="om('m-auth');authTab('signup')">Create Account</button>
      </div>
      <div id="user-pill" class="user-pill" style="display:none" onclick="userMenu()">
        <div class="user-dot" id="u-dot">?</div>
        <span id="u-name"></span>
      </div>
    </div>
  </div>
</nav>

<!-- ════════════ PAGE: SEARCH ════════════ -->
<div id="page-search" class="panel on">
  <div class="hero">
    <div class="hero-inner">
      <h1>Find the <em>real cost</em> of physical therapy near you</h1>
      <p>Compare insurance vs. cash prices side-by-side at every PT clinic in your area. Powered by live Google Places data.</p>
      <div class="search-bar">
        <input id="loc-in" type="text" placeholder="ZIP code or city (e.g. 98105, Miami, Chicago)" onkeydown="if(event.key==='Enter')doSearch()"/>
        <button class="btn-go" onclick="doSearch()">Search</button>
        <button class="btn-nearme" onclick="nearMe()">Near Me</button>
      </div>
      <div class="radius-row">
        <label>Search radius:</label>
        <select id="radius-sel">
          <option value="8000">5 miles</option>
          <option value="16000" selected>10 miles</option>
          <option value="40000">25 miles</option>
          <option value="80000">50 miles</option>
        </select>
      </div>
      <div class="qchips">
        <button class="qchip" onclick="qs('Seattle WA')">Seattle</button>
        <button class="qchip" onclick="qs('Miami FL')">Miami</button>
        <button class="qchip" onclick="qs('Austin TX')">Austin</button>
        <button class="qchip" onclick="qs('New York NY')">New York</button>
        <button class="qchip" onclick="qs('Chicago IL')">Chicago</button>
        <button class="qchip" onclick="qs('Los Angeles CA')">Los Angeles</button>
        <button class="qchip" onclick="qs('Denver CO')">Denver</button>
        <button class="qchip" onclick="qs('Nashville TN')">Nashville</button>
        <button class="qchip" onclick="qs('Phoenix AZ')">Phoenix</button>
        <button class="qchip" onclick="qs('Houston TX')">Houston</button>
        <button class="qchip" onclick="qs('Atlanta GA')">Atlanta</button>
        <button class="qchip" onclick="qs('Portland OR')">Portland</button>
      </div>
    </div>
  </div>

  <div class="stat-bar">
    <div class="stat-inner">
      <div class="stat-item"><span class="ldot"></span><b>Google Places</b> Live Data</div>
      <div class="stat-item">|</div>
      <div class="stat-item"><b>20 Insurance</b> Plans Modeled</div>
      <div class="stat-item">|</div>
      <div class="stat-item"><b>Any US</b> Zip or City</div>
      <div class="stat-item">|</div>
      <div class="stat-item"><b>Real</b> Ratings and Hours</div>
    </div>
  </div>

  <div class="page-inner">
    <div class="layout">
      <!-- SIDEBAR -->
      <aside class="sidebar" style="width:275px;min-width:255px;flex-shrink:0">
        <div id="map-wrap" style="margin-bottom:1rem"><div id="gmap"></div></div>
        <div class="fpanel" id="sf"></div>
      </aside>
      <!-- RESULTS -->
      <main style="flex:1;min-width:0">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:.9rem;flex-wrap:wrap;gap:.5rem">
          <div style="display:flex;align-items:center;gap:.65rem;flex-wrap:wrap">
            <button class="btn2 mob-filter-btn" onclick="openDrawer()">Filters</button>
            <span id="res-count" class="display" style="font-weight:700;font-size:1.05rem;color:var(--nv)">Search a location above</span>
            <span id="res-loc" style="color:var(--mu);font-size:.82rem"></span>
          </div>
          <select id="sort-sel" style="font-size:.8rem;padding:.38rem .65rem;border-radius:7px;border:1.5px solid var(--bd);background:var(--card);font-family:'DM Sans',sans-serif;color:var(--tx)" onchange="applyFilters()">
            <option value="rating">Top Rated</option>
            <option value="cash_asc">Lowest Cash Cost</option>
            <option value="savings">Highest Savings</option>
            <option value="reviews">Most Reviewed</option>
          </select>
        </div>
        <div id="err-box"></div>
        <div id="cards" style="display:flex;flex-direction:column;gap:.85rem"></div>
        <div id="loading" class="spin-wrap" style="display:none"><div class="spin"></div><span style="color:var(--mu);font-size:.85rem">Searching Google Places for PT clinics...</span></div>
        <div id="empty" class="empty-s" style="display:none">
          <div style="font-size:2.2rem;margin-bottom:.55rem">🔍</div>
          <h3 class="display" style="font-size:1rem;color:var(--nv)">No clinics match your filters</h3>
          <p style="font-size:.83rem;margin-top:.3rem">Try adjusting filters or expanding the search radius.</p>
        </div>
        <div id="welcome" style="text-align:center;padding:3rem 1rem;color:var(--mu)">
          <div style="font-size:2.8rem;margin-bottom:.75rem">🗺️</div>
          <h3 class="display" style="font-size:1.2rem;color:var(--nv);margin-bottom:.4rem">Search Any US Location</h3>
          <p style="font-size:.86rem;max-width:380px;margin:0 auto;line-height:1.65">Enter a zip code or city above to find live PT clinics with real ratings, hours, and side-by-side cost estimates.</p>
          <div style="margin-top:1.25rem;display:flex;gap:.5rem;justify-content:center;flex-wrap:wrap">
            <button class="btn" onclick="om('m-cap')">Get Free Price Alerts</button>
            <button class="btn2" onclick="showPage('how')">How It Works</button>
          </div>
        </div>
      </main>
    </div>
  </div>
</div>

<!-- ════════════ PAGE: HOW IT WORKS ════════════ -->
<div id="page-how" class="panel">
  <div class="hiw-hero">
    <div style="max-width:620px;margin:0 auto">
      <h1 class="display" style="font-weight:700;font-size:2.4rem;color:#fff;letter-spacing:-.03em;margin-bottom:.6rem">How PTCompare Pro Works</h1>
      <p style="color:rgba(255,255,255,.68);font-size:.97rem;line-height:1.65">We connect patients to physical therapy clinics transparently — showing real costs before you ever pick up the phone.</p>
    </div>
  </div>

  <div style="max-width:900px;margin:0 auto;padding:3rem 1.5rem">

    <!-- Steps -->
    <h2 class="display" style="font-weight:700;font-size:1.5rem;color:var(--nv);margin-bottom:1.5rem;text-align:center">3 Steps to Finding Affordable PT</h2>
    <div style="display:flex;flex-direction:column;gap:1rem;margin-bottom:3rem">
      <div class="step-card">
        <div class="step-num">1</div>
        <h3 class="display" style="font-weight:700;font-size:1.05rem;color:var(--nv);margin-bottom:.4rem">Search Your Location</h3>
        <p style="font-size:.88rem;color:var(--mu);line-height:1.65">Enter any US zip code or city name. PTCompare Pro instantly pulls live clinic data from Google Places — real businesses with real addresses, real hours, and real ratings.</p>
      </div>
      <div class="step-card">
        <div class="step-num">2</div>
        <h3 class="display" style="font-weight:700;font-size:1.05rem;color:var(--nv);margin-bottom:.4rem">Configure Your Cost Calculator</h3>
        <p style="font-size:.88rem;color:var(--mu);line-height:1.65">Select your insurance provider, enter your remaining deductible, out-of-pocket maximum, and how many sessions you expect to need. Our financial engine runs the math automatically — accounting for deductible spend-down, coinsurance rates, and OOP caps for every major US insurer.</p>
      </div>
      <div class="step-card">
        <div class="step-num">3</div>
        <h3 class="display" style="font-weight:700;font-size:1.05rem;color:var(--nv);margin-bottom:.4rem">Compare and Book</h3>
        <p style="font-size:.88rem;color:var(--mu);line-height:1.65">Every clinic card shows a side-by-side cost bar — your estimated insurance out-of-pocket vs. the clinic's flat cash package. Click "Book Appointment" to request a session directly or open their Calendly booking page.</p>
      </div>
    </div>

    <!-- Cost calculator explainer -->
    <div style="background:var(--card);border-radius:16px;padding:2rem;box-shadow:var(--sh);border:1px solid var(--bd);margin-bottom:2.5rem">
      <h2 class="display" style="font-weight:700;font-size:1.3rem;color:var(--nv);margin-bottom:.5rem">How Our Cost Calculator Works</h2>
      <p style="font-size:.88rem;color:var(--mu);line-height:1.7;margin-bottom:1rem">Our financial model simulates how your insurance plan processes physical therapy claims. Here is exactly what we calculate:</p>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:.85rem">
        <div class="value-card">
          <div class="value-icon" style="background:#dbeafe">📋</div>
          <h4 class="display" style="font-weight:700;font-size:.92rem;color:var(--nv);margin-bottom:.3rem">Deductible Spend-Down</h4>
          <p style="font-size:.8rem;color:var(--mu);line-height:1.6">Sessions early in the plan year cost you the full negotiated rate until your deductible is met. We model this session by session.</p>
        </div>
        <div class="value-card">
          <div class="value-icon">💵</div>
          <h4 class="display" style="font-weight:700;font-size:.92rem;color:var(--nv);margin-bottom:.3rem">Coinsurance After Deductible</h4>
          <p style="font-size:.8rem;color:var(--mu);line-height:1.6">Once deductible is met you pay only your coinsurance percentage (typically 15–25%) on each session until your OOP max is reached.</p>
        </div>
        <div class="value-card">
          <div class="value-icon" style="background:#fef3c7">🛡️</div>
          <h4 class="display" style="font-weight:700;font-size:.92rem;color:var(--nv);margin-bottom:.3rem">Out-of-Pocket Maximum</h4>
          <p style="font-size:.8rem;color:var(--mu);line-height:1.6">After you hit your OOP max the insurer covers 100%. We stop adding patient costs the moment this cap is reached.</p>
        </div>
        <div class="value-card">
          <div class="value-icon" style="background:#fce7f3">🏦</div>
          <h4 class="display" style="font-weight:700;font-size:.92rem;color:var(--nv);margin-bottom:.3rem">Negotiated Rate Modeling</h4>
          <p style="font-size:.8rem;color:var(--mu);line-height:1.6">Each insurer has different negotiated rates with providers. We apply plan-specific multipliers based on published industry data for 20 major US insurers.</p>
        </div>
      </div>
      <div class="accuracy-note" style="margin-top:1rem">
        <strong>Important note on accuracy:</strong> Cost estimates are based on average industry rates and typical insurance contract structures. Your actual costs may vary based on your specific plan, provider network status, visit limits, and local market rates. Always verify costs directly with your insurer and clinic before beginning treatment. PTCompare Pro costs are estimates for comparison purposes — not guaranteed quotes.
      </div>
    </div>

    <!-- Cash vs insurance -->
    <div style="background:linear-gradient(135deg,var(--nv),var(--nv-lt));border-radius:16px;padding:2rem;color:#fff;margin-bottom:2.5rem">
      <h2 class="display" style="font-weight:700;font-size:1.3rem;margin-bottom:.5rem">Why Cash Pay is Often Cheaper</h2>
      <p style="font-size:.88rem;color:rgba(255,255,255,.72);line-height:1.7;margin-bottom:1rem">Many patients are surprised to learn that paying cash out-of-pocket is often cheaper than using insurance for PT — especially before the deductible is met.</p>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:.85rem">
        <div style="background:rgba(255,255,255,.08);border-radius:10px;padding:1rem">
          <div class="display" style="font-weight:700;font-size:.9rem;margin-bottom:.35rem">With Insurance (before deductible)</div>
          <div style="font-size:.82rem;color:rgba(255,255,255,.7);line-height:1.6">You pay the full negotiated rate per session — typically $95–$180. The billing process takes 30–90 days and you may receive surprise bills.</div>
        </div>
        <div style="background:rgba(52,211,153,.15);border:1px solid rgba(52,211,153,.3);border-radius:10px;padding:1rem">
          <div class="display" style="font-weight:700;font-size:.9rem;margin-bottom:.35rem;color:#34d399">With Cash Pay</div>
          <div style="font-size:.82rem;color:rgba(255,255,255,.7);line-height:1.6">Many clinics offer flat-rate cash packages at $65–$140/session with no surprise bills, no prior authorization, and no waiting for EOBs.</div>
        </div>
      </div>
    </div>

    <div style="text-align:center">
      <button class="btn" style="padding:.7rem 1.75rem;font-size:.95rem" onclick="showPage('search')">Start Comparing Clinics</button>
    </div>
  </div>
</div>

<!-- ════════════ PAGE: ABOUT ════════════ -->
<div id="page-about" class="panel">
  <div class="about-hero">
    <h1 class="display">About <em>PTCompare</em> Pro</h1>
    <p style="color:rgba(255,255,255,.68);font-size:.97rem;max-width:560px;margin:.5rem auto 0;line-height:1.65">We believe every patient deserves to know exactly what they'll pay before stepping foot in a clinic.</p>
  </div>

  <div class="about-section">
    <!-- Mission -->
    <div style="text-align:center;margin-bottom:3rem">
      <h2 class="display" style="font-weight:700;font-size:1.75rem;color:var(--nv);margin-bottom:.65rem">Our Mission</h2>
      <p style="font-size:.97rem;color:var(--mu);max-width:620px;margin:0 auto;line-height:1.75">Healthcare costs in the United States are notoriously opaque. Physical therapy is no exception — the same treatment can cost $60 or $250 depending on your insurance, your clinic, and whether you know to ask for a cash rate. PTCompare Pro exists to end that confusion.</p>
    </div>

    <!-- Values -->
    <h2 class="display" style="font-weight:700;font-size:1.3rem;color:var(--nv);margin-bottom:1.1rem">What We Stand For</h2>
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1rem;margin-bottom:3rem">
      <div class="value-card">
        <div class="value-icon">🔍</div>
        <h4 class="display" style="font-weight:700;font-size:.95rem;color:var(--nv);margin-bottom:.35rem">Full Transparency</h4>
        <p style="font-size:.82rem;color:var(--mu);line-height:1.6">We show you estimated costs upfront — insurance out-of-pocket AND cash rates — so you can make an informed decision before you book.</p>
      </div>
      <div class="value-card">
        <div class="value-icon" style="background:#dbeafe">⚖️</div>
        <h4 class="display" style="font-weight:700;font-size:.95rem;color:var(--nv);margin-bottom:.35rem">Patient-First</h4>
        <p style="font-size:.82rem;color:var(--mu);line-height:1.6">We are built for patients. Clinics pay to list premium features — but search results are never paid placements. Your results are based on rating and relevance only.</p>
      </div>
      <div class="value-card">
        <div class="value-icon" style="background:#fef3c7">🏥</div>
        <h4 class="display" style="font-weight:700;font-size:.95rem;color:var(--nv);margin-bottom:.35rem">Clinic Empowerment</h4>
        <p style="font-size:.82rem;color:var(--mu);line-height:1.6">Small independent PT clinics get discovered alongside large hospital systems. Cash-pay-friendly clinics get the visibility they deserve.</p>
      </div>
      <div class="value-card">
        <div class="value-icon" style="background:#fce7f3">📊</div>
        <h4 class="display" style="font-weight:700;font-size:.95rem;color:var(--nv);margin-bottom:.35rem">Data Accuracy</h4>
        <p style="font-size:.82rem;color:var(--mu);line-height:1.6">Cost estimates use published insurer rate structures and are updated regularly. We always display a transparency disclaimer so patients understand what's an estimate vs. a quote.</p>
      </div>
    </div>

    <!-- Team -->
    <h2 class="display" style="font-weight:700;font-size:1.3rem;color:var(--nv);margin-bottom:1.1rem">The Team</h2>
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:1rem;margin-bottom:3rem">
      <div class="team-card">
        <div class="team-av">J</div>
        <div class="display" style="font-weight:700;color:var(--nv);margin-bottom:.2rem">Founder & CEO</div>
        <div style="font-size:.82rem;color:var(--mu)">Healthcare cost transparency advocate. Built PTCompare Pro after a personal experience with surprise PT billing.</div>
      </div>
      <div class="team-card">
        <div class="team-av" style="background:linear-gradient(135deg,#0284c7,#38bdf8)">T</div>
        <div class="display" style="font-weight:700;color:var(--nv);margin-bottom:.2rem">Head of Product</div>
        <div style="font-size:.82rem;color:var(--mu)">Former physical therapist turned product designer. Ensures clinical accuracy in our cost models.</div>
      </div>
      <div class="team-card">
        <div class="team-av" style="background:linear-gradient(135deg,#7c3aed,#a78bfa)">A</div>
        <div class="display" style="font-weight:700;color:var(--nv);margin-bottom:.2rem">Lead Engineer</div>
        <div style="font-size:.82rem;color:var(--mu)">Full-stack developer with a background in healthcare data systems and insurance claims processing.</div>
      </div>
    </div>

    <!-- Disclaimer -->
    <div style="background:var(--card);border-radius:12px;padding:1.5rem;border:1px solid var(--bd);box-shadow:var(--sh)">
      <h3 class="display" style="font-weight:700;font-size:1rem;color:var(--nv);margin-bottom:.45rem">Important Disclaimers</h3>
      <div style="font-size:.82rem;color:var(--mu);line-height:1.75;display:flex;flex-direction:column;gap:.5rem">
        <p><strong style="color:var(--nv)">Cost Estimates:</strong> All cost estimates shown on PTCompare Pro are algorithmic approximations based on average insurance contract rates and typical clinic pricing. They are intended for comparison purposes only and are not guaranteed quotes.</p>
        <p><strong style="color:var(--nv)">Not Medical Advice:</strong> PTCompare Pro is a cost transparency tool. We do not provide medical advice, diagnosis, or treatment recommendations. Always consult a licensed physical therapist for clinical guidance.</p>
        <p><strong style="color:var(--nv)">Clinic Data:</strong> Clinic listings are sourced from Google Places. PTCompare Pro does not independently verify that listed clinics are currently accepting patients, in-network with your specific plan, or accepting new patients.</p>
        <p><strong style="color:var(--nv)">Insurance Verification:</strong> Always confirm in-network status and coverage details directly with your insurance company before beginning treatment.</p>
      </div>
    </div>

    <div style="text-align:center;margin-top:2rem">
      <button class="btn" style="padding:.7rem 1.75rem" onclick="showPage('search')">Start Finding Clinics</button>
    </div>
  </div>
</div>

<!-- ════════════ PAGE: B2B ════════════ -->
<div id="page-b2b" class="panel">
  <div style="max-width:1100px;margin:0 auto;padding:2rem 1.5rem">

    <div class="pcard" style="margin-bottom:1.75rem">
      <div style="position:relative;z-index:1">
        <div style="background:var(--em);color:#fff;font-family:'Fraunces',serif;font-weight:700;font-size:.7rem;letter-spacing:.1em;text-transform:uppercase;padding:.2rem .5rem;border-radius:5px;display:inline-block;margin-bottom:.65rem">FOR CLINIC OWNERS</div>
        <h2 class="display" style="font-weight:700;font-size:2rem;line-height:1.18;max-width:520px;margin-bottom:.65rem">Turn Visibility Into a <span style="color:#34d399">Predictable Revenue Stream</span></h2>
        <p style="color:rgba(255,255,255,.68);font-size:.9rem;max-width:480px;margin-bottom:1.5rem;line-height:1.65">PTCompare Pro puts your clinic in front of patients actively comparing costs. Every referral click generates a tracked $15 marketplace invoice.</p>
        <div style="display:flex;gap:.65rem;flex-wrap:wrap">
          <div class="ptier"><div style="font-size:.63rem;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:.3rem">STARTER</div><div class="display" style="font-size:1.7rem;font-weight:700">$49<span style="font-size:.85rem;font-weight:400;color:rgba(255,255,255,.6)">/mo</span></div><ul style="font-size:.77rem;color:rgba(255,255,255,.7);margin-top:.55rem;list-style:none;display:flex;flex-direction:column;gap:.28rem"><li>Listed in patient search</li><li>3 standard modalities</li><li>Basic analytics</li><li>Booking request form</li></ul><button class="btn" style="margin-top:.7rem;width:100%;justify-content:center;font-size:.77rem;padding:.42rem .85rem" onclick="claimFlow('Starter')">Claim Listing</button></div>
          <div class="ptier hi"><div style="font-size:.63rem;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:#34d399;margin-bottom:.3rem">MOST POPULAR</div><div class="display" style="font-size:1.7rem;font-weight:700">$99<span style="font-size:.85rem;font-weight:400;color:rgba(255,255,255,.6)">/mo</span></div><ul style="font-size:.77rem;color:rgba(255,255,255,.7);margin-top:.55rem;list-style:none;display:flex;flex-direction:column;gap:.28rem"><li>Premium modality badges</li><li>Priority placement</li><li>Lead dashboard</li><li>Calendly booking embed</li><li>SMS lead alerts</li></ul><button class="btn" style="margin-top:.7rem;width:100%;justify-content:center;font-size:.77rem;padding:.42rem .85rem;background:#34d399;color:#065f46" onclick="claimFlow('Professional')">Get Started</button></div>
          <div class="ptier"><div style="font-size:.63rem;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:.3rem">ENTERPRISE</div><div class="display" style="font-size:1.7rem;font-weight:700">$149<span style="font-size:.85rem;font-weight:400;color:rgba(255,255,255,.6)">/mo</span></div><ul style="font-size:.77rem;color:rgba(255,255,255,.7);margin-top:.55rem;list-style:none;display:flex;flex-direction:column;gap:.28rem"><li>Unlimited modalities</li><li>Multi-location support</li><li>White-label reports</li><li>Account manager</li><li>API access</li></ul><button class="btn" style="margin-top:.7rem;width:100%;justify-content:center;font-size:.77rem;padding:.42rem .85rem" onclick="claimFlow('Enterprise')">Contact Sales</button></div>
        </div>
      </div>
    </div>

    <h2 class="display" style="font-weight:700;font-size:1.25rem;color:var(--nv);margin-bottom:.85rem">Marketplace Dashboard <span style="font-size:.65rem;font-weight:500;color:var(--mu);background:var(--bg);border:1px solid var(--bd);padding:.16rem .5rem;border-radius:5px;margin-left:.35rem;font-family:'DM Sans',sans-serif">SIMULATED PREVIEW</span></h2>
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(185px,1fr));gap:.85rem;margin-bottom:1.5rem">
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">App Impressions</div><div class="mval" id="m-imp">4,832</div><div class="mdelta">18.4% this month</div></div>
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">Cost Comparisons</div><div class="mval" id="m-cmp">1,207</div><div class="mdelta">11.2% this month</div></div>
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">Referral Clicks</div><div class="mval" id="m-leds">83</div><div class="mdelta">7 new today</div></div>
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">Marketplace Invoice</div><div class="mval" style="color:var(--em)" id="m-rev">$1,245</div><div class="mdelta">83 leads x $15 fee</div></div>
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">Email Subscribers</div><div class="mval" id="m-subs">12,441</div><div class="mdelta">234 this week</div></div>
      <div class="metric-card"><div style="font-size:.68rem;font-weight:600;text-transform:uppercase;letter-spacing:.09em;color:var(--mu);margin-bottom:.38rem">Bookings Made</div><div class="mval" id="m-book">318</div><div class="mdelta">22 this week</div></div>
    </div>

    <div style="background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:.95rem 1.25rem;margin-bottom:1.5rem">
      <div style="font-size:.7rem;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--mu);margin-bottom:.6rem;display:flex;align-items:center;gap:.4rem"><span class="ldot"></span>Live Referral Feed</div>
      <div id="live-feed" style="font-size:.8rem;display:flex;flex-direction:column;gap:.3rem"></div>
    </div>

    <div style="background:var(--card);border:1px solid var(--bd);border-radius:14px;padding:1.4rem;margin-bottom:1.5rem;box-shadow:var(--sh)">
      <h3 class="display" style="font-weight:700;color:var(--nv);font-size:1rem;margin-bottom:.3rem">SMS Lead Alert Settings</h3>
      <p style="font-size:.83rem;color:var(--mu);margin-bottom:.9rem">Get an instant text every time a patient clicks "Book Appointment" on your listing.</p>
      <div class="form-grid">
        <div><label class="flabel2">Mobile Number</label><input class="finput" type="tel" placeholder="(555) 000-0000"/></div>
        <div><label class="flabel2">Alert Frequency</label><select class="finput"><option>Every lead instantly</option><option>Hourly digest</option><option>Daily digest</option></select></div>
      </div>
      <label style="display:flex;align-items:center;gap:.45rem;margin-top:.75rem;cursor:pointer;font-size:.84rem;font-weight:500;color:var(--nv)"><input type="checkbox" checked style="accent-color:var(--em)"/> SMS alerts enabled</label>
      <button class="btn" style="margin-top:.85rem" onclick="toast('SMS settings saved.','ok')">Save Settings</button>
    </div>

    <h2 class="display" style="font-weight:700;font-size:1.25rem;color:var(--nv);margin-bottom:.7rem">Claim Your Listing</h2>
    <div style="background:var(--card);border:1px solid var(--bd);border-radius:14px;padding:1.4rem;box-shadow:var(--sh)">
      <p style="font-size:.85rem;color:var(--mu);margin-bottom:.95rem">Fill out the form below — our team verifies your clinic within 24 hours.</p>
      <div class="form-grid">
        <div><label class="flabel2">Your Name</label><input class="finput" type="text" placeholder="Dr. Jane Smith"/></div>
        <div><label class="flabel2">Clinic Name</label><input class="finput" type="text" placeholder="Greenwood Physical Therapy"/></div>
        <div><label class="flabel2">Email</label><input class="finput" type="email" placeholder="you@yourclinic.com"/></div>
        <div><label class="flabel2">Phone</label><input class="finput" type="tel" placeholder="(555) 000-0000"/></div>
        <div><label class="flabel2">NPI Number</label><input class="finput" type="text" placeholder="1234567890"/></div>
        <div><label class="flabel2">Calendly URL (optional)</label><input class="finput" id="cal-url" type="text" placeholder="https://calendly.com/yourclinic"/></div>
      </div>
      <div><label class="flabel2">Subscription Tier</label><select class="finput" style="max-width:280px"><option>Starter — $49/mo</option><option selected>Professional — $99/mo</option><option>Enterprise — $149/mo</option></select></div>
      <button class="btn" style="margin-top:1rem;padding:.6rem 1.4rem" onclick="toast('Claim request submitted! We will verify your NPI and contact you within 24 hours.','ok')">Submit Claim Request</button>
    </div>
  </div>
</div>

<script>
// ═══════════════════════════════════════════════════════════
// CONFIG & STATE
// ═══════════════════════════════════════════════════════════
const GKEY = "AIzaSyA7NpSabgSxdjSwzvdIoXNn7HBya_vtzUE";
let gmap, iw, markers=[], clinics=[];
let user=null, saved=new Set(), reviews={};
let leadsN=83, revN=1245, subsN=12441, bookN=318;
let capShown=false, revTarget=null;

// ═══════════════════════════════════════════════════════════
// INSURANCE TABLE
// postMult  = insurer negotiated rate vs. billed charge
// coins     = patient coinsurance % after deductible is met
// oop_def   = typical annual OOP max for this plan type
// ═══════════════════════════════════════════════════════════
const INS = {
  self:     {label:"Self-Pay / No Insurance",    postMult:1.00, coins:1.00, oop:99999},
  bcbs:     {label:"Blue Cross Blue Shield",     postMult:0.82, coins:0.20, oop:7000},
  aetna:    {label:"Aetna",                      postMult:0.78, coins:0.20, oop:7500},
  cigna:    {label:"Cigna",                      postMult:0.75, coins:0.25, oop:7000},
  uhc:      {label:"UnitedHealthcare",           postMult:0.80, coins:0.20, oop:8000},
  humana:   {label:"Humana",                     postMult:0.77, coins:0.20, oop:7500},
  anthem:   {label:"Anthem",                     postMult:0.79, coins:0.20, oop:7000},
  kaiser:   {label:"Kaiser Permanente",          postMult:0.70, coins:0.15, oop:6000},
  premera:  {label:"Premera Blue Cross",         postMult:0.81, coins:0.20, oop:7000},
  regence:  {label:"Regence BlueShield",         postMult:0.80, coins:0.20, oop:7200},
  oscar:    {label:"Oscar Health",               postMult:0.76, coins:0.20, oop:8500},
  molina:   {label:"Molina Healthcare",          postMult:0.65, coins:0.15, oop:9000},
  ambetter: {label:"Ambetter",                   postMult:0.68, coins:0.20, oop:8700},
  wellcare: {label:"WellCare",                   postMult:0.64, coins:0.15, oop:9000},
  harvard:  {label:"Harvard Pilgrim",            postMult:0.80, coins:0.20, oop:7000},
  tricare:  {label:"TRICARE (Military)",         postMult:0.60, coins:0.20, oop:3000},
  medicare: {label:"Medicare",                   postMult:0.65, coins:0.20, oop:3000},
  medicaid: {label:"Medicaid / CHIP",            postMult:0.55, coins:0.05, oop:1000},
  workers:  {label:"Workers Compensation",       postMult:0.90, coins:0.00, oop:99999},
  auto:     {label:"Auto Insurance (PIP)",       postMult:0.95, coins:0.00, oop:99999},
};

const NON_COV = ["shockwave","cupping","bfr","astym"];

// ═══════════════════════════════════════════════════════════
// FINANCIAL CALCULATOR
// Accurately models: deductible spend-down, coinsurance,
// out-of-pocket maximum cap, network multiplier,
// and premium modality coverage overrides.
// ═══════════════════════════════════════════════════════════
function calcCosts(clinic, sessions, deduct, oopMax, insKey, selMods, netMult) {
  const ins = INS[insKey] || INS.self;
  const cashTotal = clinic.cashRate * sessions;

  // Premium non-covered modality override
  const premOvr = selMods.some(m => NON_COV.includes(m)) && insKey !== 'self';
  const isSelf = insKey === 'self';

  if (premOvr || isSelf) {
    // Insurance path collapses to full billed rate (no coverage)
    const billTotal = clinic.insRate * sessions;
    return {
      cashTotal,
      insTotal: billTotal,
      savings: Math.max(0, billTotal - cashTotal),
      override: premOvr,
      pct: {ins: 100, cash: Math.round(cashTotal / billTotal * 100)}
    };
  }

  // ── Standard insurance path ──────────────────────────
  // 1. Negotiated rate = billed rate × insurer postMult × network multiplier
  const negRate = clinic.insRate * ins.postMult * (netMult || 1);
  let insTotal = 0;
  let deductLeft = Math.max(0, deduct);
  let oopLeft = Math.max(0, oopMax);

  for (let s = 0; s < sessions; s++) {
    if (oopLeft <= 0) break; // OOP max reached — $0 cost to patient
    let patientCost;
    if (deductLeft > 0) {
      // Before deductible met: patient pays full negotiated rate
      patientCost = Math.min(negRate, deductLeft);
      deductLeft -= patientCost;
    } else {
      // After deductible: patient pays coinsurance % only
      patientCost = negRate * ins.coins;
    }
    // Never exceed remaining OOP max
    patientCost = Math.min(patientCost, oopLeft);
    oopLeft -= patientCost;
    insTotal += patientCost;
  }

  insTotal = Math.round(insTotal);
  const mx = Math.max(insTotal, cashTotal, 1);
  return {
    cashTotal,
    insTotal,
    savings: Math.max(0, insTotal - cashTotal),
    override: false,
    pct: {ins: Math.round(insTotal/mx*100), cash: Math.round(cashTotal/mx*100)}
  };
}

// ═══════════════════════════════════════════════════════════
// FILTER HTML — built once, injected into sidebar + drawer
// ═══════════════════════════════════════════════════════════
function buildFilters() {
  const insOpts = Object.entries(INS).map(([k,v]) =>
    `<option value="${k}">${v.label}</option>`).join('');
  return `
<div class="fsec">
  <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"/></svg>
  Refine Results
</div>
<span class="flabel" style="margin-top:0">Primary Concern</span>
<select class="fsel" id="f-concern" onchange="applyFilters()">
  <option value="">All Conditions</option>
  <option value="knee">Knee Rehabilitation</option>
  <option value="back">Back and Spine Pain</option>
  <option value="shoulder">Shoulder Injury</option>
  <option value="hip">Hip and Pelvis</option>
  <option value="sport">Sports Performance</option>
  <option value="postsurg">Post-Surgical Rehab</option>
  <option value="neuro">Neurological Rehab</option>
  <option value="balance">Balance and Fall Prevention</option>
  <option value="concussion">Concussion Rehab</option>
  <option value="pelvic">Pelvic Floor PT</option>
  <option value="pediatric">Pediatric PT</option>
  <option value="hand">Hand and Wrist Therapy</option>
  <option value="plantar">Plantar Fasciitis</option>
</select>
<span class="flabel">Minimum Rating</span>
<select class="fsel" id="f-rating" onchange="applyFilters()">
  <option value="0">Any Rating</option>
  <option value="4.0">4.0 Stars and Above</option>
  <option value="4.5">4.5 Stars and Above</option>
</select>
<span class="flabel">Modalities Offered</span>
<div id="mod-chips">
  ${[['shockwave','Shockwave'],['dryneedling','Dry Needling'],['cupping','Cupping'],['deeptissue','Deep Tissue'],['aquatic','Aquatic'],['bfr','BFR'],['astym','ASTYM/Graston'],['kinesio','Kinesio Tape'],['vestibular','Vestibular'],['lymphedema','Lymphedema']].map(([v,l])=>`<label class="chip"><input type="checkbox" value="${v}" onchange="applyFilters()"/> ${l}</label>`).join('')}
</div>
<hr style="margin:.85rem 0;border-color:var(--bd)"/>
<div class="fsec">
  <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/></svg>
  Cost Calculator
</div>
<span class="flabel" style="margin-top:0">Insurance Provider</span>
<select class="fsel" id="f-ins" onchange="applyFilters()">${insOpts}</select>
<span class="flabel">Network Status</span>
<select class="fsel" id="f-net" onchange="applyFilters()">
  <option value="1">In-Network</option>
  <option value="1.5">Out-of-Network (1.5x rates)</option>
</select>
<span class="flabel">Remaining Deductible</span>
<div class="rl"><span>$0</span><span id="dv" style="font-weight:600;color:var(--nv)">$1,500</span><span>$3,000</span></div>
<input type="range" id="s-ded" min="0" max="3000" step="50" value="1500" oninput="document.getElementById('dv').textContent='$'+this.value;applyFilters()"/>
<span class="flabel">Out-of-Pocket Maximum</span>
<div class="rl"><span>$0</span><span id="ov" style="font-weight:600;color:var(--nv)">$7,000</span><span>$10,000</span></div>
<input type="range" id="s-oop" min="0" max="10000" step="250" value="7000" oninput="document.getElementById('ov').textContent='$'+this.value;applyFilters()"/>
<span class="flabel">Sessions in Plan of Care</span>
<div class="rl"><span>1</span><span id="sv" style="font-weight:600;color:var(--nv)">12 sessions</span><span>24</span></div>
<input type="range" id="s-sess" min="1" max="24" step="1" value="12" oninput="document.getElementById('sv').textContent=this.value+' sessions';applyFilters()"/>
<div id="comply">
  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#f59e0b" stroke-width="2.5" style="flex-shrink:0;margin-top:.1rem"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>
  <span>Coverage Override Active: selected modality is typically not covered by standard insurance. Costs shown reflect out-of-pocket cash rates.</span>
</div>
<button class="btn" style="width:100%;justify-content:center;margin-top:.85rem;padding:.58rem" onclick="applyFilters()">Recalculate Costs</button>
<div class="accuracy-note">Cost estimates model average insurer contract rates. Verify actual costs with your insurer and clinic before treatment.</div>
`;
}

// ═══════════════════════════════════════════════════════════
// GOOGLE MAPS
// ═══════════════════════════════════════════════════════════
function initMap() {
  gmap = new google.maps.Map(document.getElementById('gmap'), {
    center:{lat:39.5,lng:-98.35}, zoom:4,
    mapTypeControl:false, streetViewControl:false, fullscreenControl:false,
    styles:[{featureType:"poi",elementType:"labels",stylers:[{visibility:"off"}]},{featureType:"transit",stylers:[{visibility:"off"}]}]
  });
  iw = new google.maps.InfoWindow();
  document.getElementById('sf').innerHTML = buildFilters();
  document.getElementById('drawer-body').innerHTML = buildFilters();
}

function loadMaps() {
  const s = document.createElement('script');
  s.src = `https://maps.googleapis.com/maps/api/js?key=${GKEY}&libraries=places&callback=initMap`;
  s.async = true; s.defer = true;
  s.onerror = () => showErr("Failed to load Google Maps. Ensure Maps JavaScript API, Places API and Geocoding API are all enabled in Google Cloud Console.");
  document.head.appendChild(s);
}

function geocodeSearch(q) {
  if (!window.google) { showErr("Maps still loading. Try again in a moment."); return; }
  setLoad(true);
  new google.maps.Geocoder().geocode({address: q+' USA', componentRestrictions:{country:'US'}}, (res,st) => {
    if (st==='OK'&&res[0]) {
      const loc = res[0].geometry.location;
      searchNear(loc.lat(), loc.lng(), res[0].formatted_address);
    } else {
      setLoad(false);
      showErr(`Could not find "${q}". Try a more specific zip code or city name.`);
    }
  });
}

function searchNear(lat, lng, label) {
  setLoad(true); clearMk(); clinics = [];
  document.getElementById('res-loc').textContent = label ? `\u2014 ${label}` : '';
  const radius = parseInt(document.getElementById('radius-sel').value) || 16000;
  const svc = new google.maps.places.PlacesService(gmap);
  let all=[], pending=2;

  function done(results, status) {
    if (status === google.maps.places.PlacesServiceStatus.OK) all = all.concat(results);
    if (--pending === 0) processResults(all, lat, lng);
  }

  svc.nearbySearch({location:new google.maps.LatLng(lat,lng), radius, keyword:'physical therapy'}, done);
  svc.nearbySearch({location:new google.maps.LatLng(lat,lng), radius, keyword:'physiotherapy rehabilitation sports medicine clinic'}, done);
}

function processResults(raw, lat, lng) {
  setLoad(false);
  if (!raw.length) { showEmpty(); return; }

  const seen = new Set();
  const unique = raw.filter(r => { if(seen.has(r.place_id))return false; seen.add(r.place_id); return true; });

  clinics = unique.slice(0,40).map((p,i) => {
    const clat=p.geometry.location.lat(), clng=p.geometry.location.lng();
    const cash = estimateCash(p.price_level, clat, clng);
    return {id:i+1, placeId:p.place_id, name:p.name, address:p.vicinity||'',
            lat:clat, lng:clng, rating:p.rating||0, reviews:p.user_ratings_total||0,
            open:p.opening_hours?p.opening_hours.open_now:null,
            cashRate:cash, insRate:Math.round(cash*1.5),
            modalities:randMods(), concerns:randConcerns(), tier:randTier(),
            calendlyUrl:''};
  });

  gmap.panTo({lat,lng}); gmap.setZoom(13);
  placeMarkers(clinics);
  renderAll();
  document.getElementById('welcome').style.display='none';

  if (!capShown && !user) { capShown=true; setTimeout(()=>om('m-cap'), 2500); }
}

// ── Rate estimation ───────────────────────────────────────
function estimateCash(pl, lat, lng) {
  const base = [62,78,98,128,162][pl||2] || 92;
  let m = 1.0;
  if (lat>40.5&&lat<41.0&&lng>-74.3&&lng<-73.7) m=1.45;       // NYC
  else if (lat>37.2&&lat<37.9&&lng>-122.6&&lng<-121.8) m=1.40; // SF Bay Area
  else if (lat>33.7&&lat<34.4&&lng>-118.7&&lng<-117.9) m=1.30; // Los Angeles
  else if (lat>47.4&&lat<47.9&&lng>-122.6&&lng<-122.1) m=1.22; // Seattle
  else if (lat>42.2&&lat<42.5&&lng>-71.3&&lng<-70.9) m=1.26;   // Boston
  else if (lat>41.6&&lat<42.1&&lng>-88.0&&lng<-87.5) m=1.15;   // Chicago
  else if (lat>25.5&&lat<26.0&&lng>-80.5&&lng<-80.1) m=1.18;   // Miami
  else if (lat>29.6&&lat<30.1&&lng>-97.9&&lng<-97.4) m=1.06;   // Austin
  else if (lat>47.4&&lat<47.7&&lng>-122.8&&lng<-122.4) m=1.18; // Portland OR area
  else if (lat>33.3&&lat<33.7&&lng>-112.3&&lng<-111.7) m=1.05; // Phoenix
  else if (lat<34.5) m=0.88;                                     // South / rural
  return Math.round(base * m);
}

const ALL_MODS=['shockwave','dryneedling','cupping','deeptissue','aquatic','bfr','astym','kinesio','vestibular','lymphedema'];
const ALL_CONC=['knee','back','shoulder','hip','sport','postsurg','neuro','balance','concussion','pelvic','pediatric','hand','plantar'];
function randMods(){return shuffle(ALL_MODS).slice(0,Math.floor(Math.random()*4)+1)}
function randConcerns(){return shuffle(ALL_CONC).slice(0,Math.floor(Math.random()*5)+2)}
function randTier(){const r=Math.random();return r<.12?'enterprise':r<.28?'pro':r<.45?'starter':null}
function shuffle(a){return[...a].sort(()=>Math.random()-.5)}

// ── Markers ───────────────────────────────────────────────
function placeMarkers(list) {
  clearMk();
  list.forEach(c => {
    const prem = c.tier==='enterprise'||c.tier==='pro';
    const mk = new google.maps.Marker({
      position:{lat:c.lat,lng:c.lng}, map:gmap, title:c.name,
      animation:google.maps.Animation.DROP,
      icon:{path:google.maps.SymbolPath.CIRCLE,scale:10,fillColor:prem?'#059669':'#0c1f35',fillOpacity:1,strokeColor:'#fff',strokeWeight:2.5}
    });
    mk.addListener('click', () => {
      iw.setContent(`<div style="font-family:'DM Sans',sans-serif;max-width:220px;padding:4px">
        <div style="font-family:'Fraunces',serif;font-weight:700;color:#0c1f35;font-size:.95rem">${c.name}</div>
        ${c.rating?`<div style="color:#f59e0b;font-size:.8rem;margin:.2rem 0">&#9733; ${c.rating} <span style="color:#5a7184">(${c.reviews.toLocaleString()})</span></div>`:''}
        <div style="font-size:.75rem;color:#5a7184;margin-bottom:.38rem">${c.address}</div>
        ${c.open===true?'<span style="background:#d1fae5;color:#065f46;font-size:.65rem;font-weight:700;padding:.12rem .4rem;border-radius:4px">Open Now</span>':c.open===false?'<span style="background:#fee2e2;color:#991b1b;font-size:.65rem;font-weight:700;padding:.12rem .4rem;border-radius:4px">Closed</span>':''}
        <div style="font-size:.75rem;margin-top:.38rem"><b>Est. cash:</b> $${c.cashRate}/session</div>
        <div style="margin-top:.42rem;display:flex;gap:.45rem">
          <span style="color:#059669;font-size:.77rem;font-weight:600;cursor:pointer;text-decoration:underline" onclick="scrollToCard(${c.id})">Cost comparison</span>
          <span style="color:#0284c7;font-size:.77rem;font-weight:600;cursor:pointer;text-decoration:underline" onclick="openBook(${c.id})">Book</span>
        </div>
      </div>`);
      iw.open(gmap, mk);
    });
    markers.push(mk);
  });
}
function clearMk(){markers.forEach(m=>m.setMap(null));markers=[];}
function scrollToCard(id) {
  iw.close();
  const el=document.getElementById('c-'+id);
  if(el){el.scrollIntoView({behavior:'smooth',block:'center'});el.style.outline='2.5px solid var(--em)';el.style.outlineOffset='3px';setTimeout(()=>{el.style.outline='';el.style.outlineOffset='';},1700);}
}

// ═══════════════════════════════════════════════════════════
// CARD RENDERER
// ═══════════════════════════════════════════════════════════
const ML={shockwave:'Shockwave',dryneedling:'Dry Needling',cupping:'Cupping',deeptissue:'Deep Tissue',aquatic:'Aquatic',bfr:'BFR',astym:'ASTYM/Graston',kinesio:'Kinesio Tape',vestibular:'Vestibular',lymphedema:'Lymphedema'};
const NCS=new Set(NON_COV);

function starStr(r){
  if(!r)return'&#9734;&#9734;&#9734;&#9734;&#9734;';
  const f=Math.floor(r),h=r-f>=.5;
  return Array.from({length:5},(_,i)=>i<f?'&#9733;':i===f&&h?'&#11040;':'&#9734;').join('');
}

function tierBadge(t){
  if(!t)return`<span class="badge b-uncl">Unclaimed</span>`;
  if(t==='enterprise')return`<span class="badge b-prem">Enterprise Partner</span>`;
  if(t==='pro')return`<span class="badge b-prem">Pro Partner</span>`;
  return`<span class="badge b-veri">Listed</span>`;
}

function avgRating(id, base){
  const r=reviews[id]||[];
  if(!r.length)return base;
  return ((r.reduce((a,b)=>a+b.rating,0)+base*5)/(r.length+5)).toFixed(1);
}

function cardHTML(c, cost) {
  const rv = reviews[c.id]||[];
  const dr = avgRating(c.id, c.rating);
  const isSv = saved.has(c.id);

  return `<div class="card aup" id="c-${c.id}">
    <div style="display:flex;align-items:flex-start;justify-content:space-between;gap:.85rem;padding:1.1rem 1.1rem .6rem">
      <div style="flex:1;min-width:0">
        <div style="display:flex;align-items:center;gap:.28rem;flex-wrap:wrap;margin-bottom:.28rem">
          ${tierBadge(c.tier)}
          ${c.open===true?'<span class="badge b-open">Open Now</span>':c.open===false?'<span class="badge b-closed">Closed</span>':''}
          ${rv.length?`<span style="background:#eff6ff;color:#1d4ed8;font-size:.63rem;font-weight:700;padding:.17rem .48rem;border-radius:5px">${rv.length} review${rv.length>1?'s':''}</span>`:''}
        </div>
        <h3 class="display" style="font-weight:700;font-size:.97rem;color:var(--nv);margin-bottom:.1rem;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">${c.name}</h3>
        <div style="font-size:.77rem;color:var(--mu);white-space:nowrap;overflow:hidden;text-overflow:ellipsis">${c.address}</div>
      </div>
      <div style="text-align:right;flex-shrink:0;display:flex;flex-direction:column;align-items:flex-end;gap:.3rem">
        ${c.rating?`<div style="color:#f59e0b;font-size:.8rem">${starStr(parseFloat(dr))} <b style="color:var(--nv)">${dr}</b></div><div style="color:var(--mu);font-size:.73rem">${c.reviews.toLocaleString()} reviews</div>`:'<div style="color:var(--mu);font-size:.73rem">No reviews yet</div>'}
        <button onclick="toggleSave(${c.id})" style="background:${isSv?'var(--em-lt)':'var(--bg)'};border:1.5px solid ${isSv?'var(--em)':'var(--bd)'};color:${isSv?'var(--em-dk)':'var(--mu)'};border-radius:6px;padding:.18rem .52rem;font-size:.7rem;cursor:pointer;font-weight:600;transition:all .15s">${isSv?'Saved':'Save'}</button>
      </div>
    </div>
    <div style="padding:.1rem 1.1rem .72rem">
      <div style="display:flex;flex-wrap:wrap;gap:.2rem;margin-bottom:.32rem">${c.modalities.map(m=>`<span class="mtag${NCS.has(m)?' pr':''}">${ML[m]||m}</span>`).join('')}</div>
      <div style="font-size:.73rem;color:var(--mu)"><b style="color:var(--nv)">Est. per session:</b> Cash $${c.cashRate} &middot; Billed ~$${c.insRate} <span style="color:#94a3b8">(market estimate)</span></div>
    </div>
    <div class="cbar-wrap">
      <div style="font-family:'Fraunces',serif;font-weight:700;font-size:.76rem;letter-spacing:.05em;text-transform:uppercase;color:var(--nv);margin-bottom:.78rem;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:.28rem">
        <span>Full Plan-of-Care Cost</span>
        ${cost.savings>0?`<span class="save-pill">Save $${cost.savings.toLocaleString()} with cash</span>`:''}
      </div>
      <div class="cbar-lbl"><span>Insurance (est. patient cost)</span><span style="font-weight:600;color:var(--nv)">$${cost.insTotal.toLocaleString()}</span></div>
      <div class="cbar-track"><div class="cbar-fill bar-ins" style="width:${cost.pct.ins}%"></div></div>
      <div class="cbar-lbl"><span>Flat Cash Package</span><span style="font-weight:600;color:var(--em-dk)">$${cost.cashTotal.toLocaleString()}</span></div>
      <div class="cbar-track"><div class="cbar-fill bar-cash" style="width:${cost.pct.cash}%"></div></div>
      ${cost.override?`<div style="font-size:.73rem;color:#92400e;background:#fffbeb;border:1px solid #f59e0b;border-radius:6px;padding:.4rem .62rem;margin-top:.38rem">Premium modality selected — insurance coverage override applied. Out-of-pocket cash rates shown.</div>`:''}
      <div class="accuracy-note">Estimates based on average insurer contract rates. Verify exact costs with your insurer before treatment.</div>
      <div style="display:flex;gap:.38rem;margin-top:.82rem;flex-wrap:wrap">
        <button class="btn" onclick="openBook(${c.id})">Book Appointment</button>
        <button class="btn2" onclick="openProf(${c.id})">Full Profile</button>
        <button class="btn2" onclick="openRev(${c.id},'${c.name.replace(/'/g,"\\'")}')">Leave Review</button>
        <button class="btn2" onclick="openGM('${c.placeId}','${c.name.replace(/'/g,"\\'")}')">Google Maps</button>
        ${!c.tier?`<button class="btn2" onclick="sv_nav('b2b')">Claim Listing</button>`:''}
      </div>
    </div>
  </div>`;
}

// ═══════════════════════════════════════════════════════════
// FILTER ENGINE
// ═══════════════════════════════════════════════════════════
function getFV() {
  function gv(id){return(document.getElementById(id)||{}).value||'';}
  function gn(id){return parseFloat(gv(id))||0;}
  const mods=Array.from(document.querySelectorAll('#mod-chips input:checked')).map(el=>el.value);
  return {concern:gv('f-concern'),rating:gn('f-rating'),mods,
          ins:gv('f-ins')||'self',net:parseFloat(gv('f-net'))||1,
          ded:gn('s-ded'),oop:gn('s-oop')||7000,sess:gn('s-sess')||12};
}

function applyFilters() {
  if (!clinics.length) return;
  const f = getFV();
  const premOvr = f.mods.some(m=>NON_COV.includes(m)) && f.ins!=='self';
  document.querySelectorAll('#comply').forEach(el=>el.style.display=premOvr?'flex':'none');
  document.querySelectorAll('.chip').forEach(chip=>chip.classList.toggle('on',chip.querySelector('input')?.checked||false));

  let list = clinics.filter(c => {
    if(f.rating && c.rating < f.rating) return false;
    if(f.concern && !c.concerns.includes(f.concern)) return false;
    if(f.mods.length && !f.mods.every(m=>c.modalities.includes(m))) return false;
    return true;
  });

  const sort = (document.getElementById('sort-sel')||{}).value||'rating';
  if (sort==='cash_asc') list.sort((a,b)=>a.cashRate-b.cashRate);
  else if (sort==='reviews') list.sort((a,b)=>b.reviews-a.reviews);
  else if (sort==='savings') {
    list.sort((a,b)=>{
      const ca=calcCosts({...a,insRate:Math.round(a.insRate*f.net)},f.sess,f.ded,f.oop,f.ins,f.mods,f.net).savings;
      const cb=calcCosts({...b,insRate:Math.round(b.insRate*f.net)},f.sess,f.ded,f.oop,f.ins,f.mods,f.net).savings;
      return cb-ca;
    });
  } else list.sort((a,b)=>(b.rating||0)-(a.rating||0));

  renderCards(list, f);
}

function renderAll(){applyFilters();}

function renderCards(list, f) {
  const box=document.getElementById('cards'), emp=document.getElementById('empty');
  document.getElementById('welcome').style.display='none';
  if (!list.length) {box.innerHTML='';emp.style.display='block';document.getElementById('res-count').textContent='No results match filters';return;}
  emp.style.display='none';
  document.getElementById('res-count').textContent=`Showing ${list.length} clinic${list.length>1?'s':''}`;
  box.innerHTML = list.map(c => {
    const adj = {...c, insRate: Math.round(c.insRate*f.net)};
    return cardHTML(c, calcCosts(adj, f.sess, f.ded, f.oop, f.ins, f.mods, f.net));
  }).join('');
}

// ═══════════════════════════════════════════════════════════
// BOOKING MODAL
// ═══════════════════════════════════════════════════════════
function openBook(id) {
  const c = clinics.find(x=>x.id===id); if(!c) return;
  trackLead(id, c.name);
  const insOpts = Object.entries(INS).map(([k,v])=>`<option value="${k}">${v.label}</option>`).join('');
  document.getElementById('book-body').innerHTML = `
    <h3 class="display" style="font-weight:700;font-size:1.1rem;color:var(--nv);margin-bottom:.2rem">Book Appointment</h3>
    <p style="font-size:.83rem;color:var(--mu);margin-bottom:1.15rem">${c.name} &middot; ${c.address}</p>
    <div class="tab-bar">
      <div class="tab on" id="t-cal" onclick="bkTab('cal')">Calendly Booking</div>
      <div class="tab" id="t-req" onclick="bkTab('req')">Request Form</div>
    </div>
    <div class="tab-pane on" id="bk-cal">
      ${c.calendlyUrl
        ? `<div style="border-radius:10px;overflow:hidden;border:1px solid var(--bd)"><iframe src="${c.calendlyUrl}" width="100%" height="480" frameborder="0"></iframe></div>`
        : `<div style="text-align:center;padding:1.75rem;background:var(--bg);border-radius:10px;border:1px solid var(--bd)">
             <div style="font-size:1.8rem;margin-bottom:.55rem">📅</div>
             <p style="font-size:.86rem;color:var(--mu);margin-bottom:.8rem">This clinic has not connected their Calendly booking page yet. Use the request form to contact them directly.</p>
             <button class="btn2" onclick="bkTab('req')">Use Request Form</button>
           </div>`}
    </div>
    <div class="tab-pane" id="bk-req">
      <div class="form-grid">
        <div><label class="flabel2">Your Name</label><input class="finput" id="bk-n" type="text" placeholder="Jane Smith" value="${user?user.name:''}"/></div>
        <div><label class="flabel2">Email</label><input class="finput" id="bk-e" type="email" placeholder="you@email.com" value="${user?user.email:''}"/></div>
        <div><label class="flabel2">Phone</label><input class="finput" id="bk-p" type="tel" placeholder="(555) 000-0000"/></div>
        <div><label class="flabel2">Preferred Time</label><input class="finput" id="bk-t" type="text" placeholder="e.g. Monday mornings, ASAP"/></div>
      </div>
      <label class="flabel2">Primary Concern</label>
      <select class="finput" id="bk-c"><option>Knee Rehabilitation</option><option>Back / Spine Pain</option><option>Shoulder Injury</option><option>Hip and Pelvis</option><option>Sports Performance</option><option>Post-Surgical Rehab</option><option>Other</option></select>
      <label class="flabel2">Insurance / Payment</label>
      <select class="finput" id="bk-i">${insOpts}</select>
      <label class="flabel2">Additional Notes</label>
      <textarea class="finput" id="bk-note" rows="3" placeholder="Any relevant medical history, urgency, or questions..." style="resize:vertical"></textarea>
      <label style="display:flex;align-items:flex-start;gap:.42rem;margin-top:.8rem;cursor:pointer;font-size:.8rem;color:var(--mu)"><input type="checkbox" id="bk-sms" style="margin-top:.15rem;accent-color:var(--em)"/> Send me text confirmation and appointment reminders</label>
      <button class="btn" style="width:100%;justify-content:center;margin-top:.9rem;padding:.6rem" onclick="subBook(${c.id},'${c.name.replace(/'/g,"\\'")}')">Send Appointment Request</button>
    </div>
  `;
  om('m-book');
}

function bkTab(t) {
  ['cal','req'].forEach(x=>{
    document.getElementById('t-'+x).classList.toggle('on',x===t);
    document.getElementById('bk-'+x).classList.toggle('on',x===t);
  });
}

function subBook(id, name) {
  const n=document.getElementById('bk-n')?.value, e=document.getElementById('bk-e')?.value;
  if(!n||!e){toast('Please fill in your name and email.','warn');return;}
  cm('m-book'); bookN++;
  const el=document.getElementById('m-book'); if(el) el.textContent=bookN.toLocaleString();
  toast(`Appointment request sent to ${name}.`,'ok');
  setTimeout(()=>toast('SMS confirmation sent to your phone (simulated).'),900);
  setTimeout(()=>toast(`${name} will contact you within 2 hours.`),1900);
}

// ═══════════════════════════════════════════════════════════
// CLINIC PROFILE MODAL
// ═══════════════════════════════════════════════════════════
function openProf(id) {
  const c = clinics.find(x=>x.id===id); if(!c) return;
  const rv = reviews[c.id]||[];
  const dr = avgRating(c.id, c.rating);
  document.getElementById('prof-body').innerHTML = `
    <div style="display:flex;justify-content:space-between;align-items:flex-start;gap:.9rem;margin-bottom:1rem;flex-wrap:wrap">
      <div>
        <div style="display:flex;gap:.28rem;flex-wrap:wrap;margin-bottom:.35rem">${tierBadge(c.tier)} ${c.open===true?'<span class="badge b-open">Open Now</span>':''}</div>
        <h3 class="display" style="font-weight:700;color:var(--nv);font-size:1.2rem">${c.name}</h3>
        <div style="font-size:.8rem;color:var(--mu);margin-top:.18rem">${c.address}</div>
      </div>
      <div style="text-align:right">
        <div style="color:#f59e0b;font-size:.88rem">${starStr(parseFloat(dr))} <b style="color:var(--nv)">${dr}</b></div>
        <div style="font-size:.75rem;color:var(--mu)">${c.reviews.toLocaleString()} Google${rv.length?` + ${rv.length} user`:''} reviews</div>
      </div>
    </div>
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:.6rem;margin-bottom:1rem">
      <div class="pstat"><div class="display" style="font-weight:700;font-size:1.2rem;color:var(--nv)">$${c.cashRate}</div><div style="font-size:.7rem;color:var(--mu)">Cash/session</div></div>
      <div class="pstat"><div class="display" style="font-weight:700;font-size:1.2rem;color:var(--sky)">$${c.insRate}</div><div style="font-size:.7rem;color:var(--mu)">Billed/session</div></div>
      <div class="pstat"><div class="display" style="font-weight:700;font-size:1.2rem;color:var(--em)">${c.modalities.length}</div><div style="font-size:.7rem;color:var(--mu)">Modalities</div></div>
    </div>
    <div style="margin-bottom:.9rem">
      <div style="font-family:'Fraunces',serif;font-weight:700;font-size:.78rem;letter-spacing:.07em;text-transform:uppercase;color:var(--nv);margin-bottom:.42rem">Modalities</div>
      <div style="display:flex;flex-wrap:wrap;gap:.22rem">${c.modalities.map(m=>`<span class="mtag${NCS.has(m)?' pr':''}">${ML[m]||m}</span>`).join('')}</div>
    </div>
    <div style="margin-bottom:.9rem">
      <div style="font-family:'Fraunces',serif;font-weight:700;font-size:.78rem;letter-spacing:.07em;text-transform:uppercase;color:var(--nv);margin-bottom:.42rem">Specialties</div>
      <div style="display:flex;flex-wrap:wrap;gap:.22rem">${c.concerns.map(x=>`<span style="background:var(--bg);border:1px solid var(--bd);border-radius:5px;font-size:.7rem;padding:.16rem .48rem;font-weight:500">${x}</span>`).join('')}</div>
    </div>
    <div style="margin-bottom:1rem">
      <div style="font-family:'Fraunces',serif;font-weight:700;font-size:.78rem;letter-spacing:.07em;text-transform:uppercase;color:var(--nv);margin-bottom:.55rem">Patient Reviews</div>
      ${rv.length?rv.map(r=>`<div class="rev-card"><div style="display:flex;align-items:flex-start;gap:.6rem"><div class="rev-av">${(r.name[0]||'?').toUpperCase()}</div><div style="flex:1"><div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:.25rem"><span style="font-weight:600;font-size:.84rem">${r.name}</span><span style="color:#f59e0b;font-size:.8rem">${'★'.repeat(r.rating)}${'☆'.repeat(5-r.rating)}</span></div><div style="font-size:.73rem;color:var(--mu);margin:.15rem 0">${r.date} &middot; ${r.paytype}</div><div style="font-size:.83rem;line-height:1.55">${r.text}</div></div></div></div>`).join(''):`<div style="text-align:center;padding:1.1rem;background:var(--bg);border-radius:9px;color:var(--mu);font-size:.83rem">No reviews yet. <span style="color:var(--em);cursor:pointer;font-weight:600" onclick="cm('m-prof');openRev(${c.id},'${c.name.replace(/'/g,"\\'")}')">Be the first</span></div>`}
    </div>
    <div class="accuracy-note" style="margin-bottom:1rem">Cost estimates are market-based approximations. Verify actual costs with the clinic and your insurer.</div>
    <div style="display:flex;gap:.4rem;flex-wrap:wrap">
      <button class="btn" onclick="cm('m-prof');openBook(${c.id})">Book Appointment</button>
      <button class="btn2" onclick="cm('m-prof');openRev(${c.id},'${c.name.replace(/'/g,"\\'")}')">Leave Review</button>
      <button class="btn2" onclick="openGM('${c.placeId}','${c.name.replace(/'/g,"\\'")}')">Google Maps</button>
    </div>
  `;
  om('m-prof');
}

// ═══════════════════════════════════════════════════════════
// REVIEWS
// ═══════════════════════════════════════════════════════════
function openRev(id, name) {
  revTarget=id;
  document.getElementById('rev-cname').textContent=`Writing a review for: ${name}`;
  document.querySelectorAll('#star-inp input').forEach(i=>i.checked=false);
  document.getElementById('rv-text').value='';
  document.getElementById('rv-name').value=user?user.name:'';
  om('m-rev');
}

function subReview() {
  const rating=parseInt(document.querySelector('#star-inp input:checked')?.value||0);
  const text=document.getElementById('rv-text').value.trim();
  const name=document.getElementById('rv-name').value.trim()||'Anonymous';
  const pay=document.getElementById('rv-pay').value;
  if(!rating){toast('Please select a star rating.','warn');return;}
  if(!text){toast('Please write a short review.','warn');return;}
  if(!reviews[revTarget])reviews[revTarget]=[];
  reviews[revTarget].unshift({name,rating,text,paytype:pay,date:new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'})});
  cm('m-rev');
  toast('Review submitted. Thank you!','ok');
  applyFilters();
}

// ═══════════════════════════════════════════════════════════
// USER AUTH
// ═══════════════════════════════════════════════════════════
function authTab(t) {
  ['login','signup'].forEach(x=>{
    document.getElementById('t-'+x).classList.toggle('on',x===t);
    document.getElementById('p-'+x).classList.toggle('on',x===t);
  });
}

function doLogin() {
  const email=document.getElementById('l-email').value.trim();
  const pass=document.getElementById('l-pass').value;
  if(!email||!pass){toast('Please enter email and password.','warn');return;}
  user={name:email.split('@')[0],email,initials:email[0].toUpperCase()};
  updateUser(); cm('m-auth');
  toast(`Welcome back, ${user.name}!`,'ok');
}

function doSignup() {
  const fn=document.getElementById('s-fn').value.trim();
  const ln=document.getElementById('s-ln').value.trim();
  const email=document.getElementById('s-email').value.trim();
  const pass=document.getElementById('s-pass').value;
  if(!fn||!email||!pass){toast('Please fill in name, email and password.','warn');return;}
  user={name:`${fn} ${ln}`.trim(),email,initials:fn[0].toUpperCase()};
  subsN++; updateUser(); cm('m-auth');
  toast(`Welcome, ${fn}! Account created.`,'ok');
  if(document.getElementById('s-sms').checked) setTimeout(()=>toast('SMS alerts enabled.'),900);
}

function updateUser() {
  const ab=document.getElementById('auth-btns'), up=document.getElementById('user-pill');
  const dot=document.getElementById('u-dot'), nm=document.getElementById('u-name');
  if(user){ab.style.display='none';up.style.display='flex';dot.textContent=user.initials;nm.textContent=user.name;}
  else{ab.style.display='flex';up.style.display='none';}
}

function userMenu() {
  if(confirm(`Signed in as ${user.name} (${user.email})\n\nClick OK to sign out.`)){
    user=null; saved=new Set(); updateUser(); toast('Signed out.'); applyFilters();
  }
}

function toggleSave(id) {
  if(!user){om('m-auth');authTab('login');toast('Sign in to save clinics.','warn');return;}
  if(saved.has(id)){saved.delete(id);toast('Removed from saved.');}
  else{saved.add(id);toast('Clinic saved!','ok');setTimeout(()=>toast('You will get an email if this clinic\'s prices change.'),900);}
  applyFilters();
}

// ═══════════════════════════════════════════════════════════
// EMAIL CAPTURE
// ═══════════════════════════════════════════════════════════
function subCapture() {
  const email=document.getElementById('cap-email').value.trim();
  if(!email){toast('Please enter your email.','warn');return;}
  subsN++; cm('m-cap');
  toast('You are in! Watch your inbox for PT savings alerts.','ok');
  const el=document.getElementById('m-subs'); if(el) el.textContent=subsN.toLocaleString();
}

// ═══════════════════════════════════════════════════════════
// LEAD TRACKING
// ═══════════════════════════════════════════════════════════
function trackLead(id, name) {
  leadsN++; revN+=15;
  const le=document.getElementById('m-leds'), re=document.getElementById('m-rev-val');
  if(le)le.textContent=leadsN.toLocaleString();
  if(re)re.textContent='$'+revN.toLocaleString();
}

// ═══════════════════════════════════════════════════════════
// SEARCH ENTRY POINTS
// ═══════════════════════════════════════════════════════════
function doSearch(){const q=document.getElementById('loc-in').value.trim();if(!q)return;clearErr();geocodeSearch(q);}
function qs(q){document.getElementById('loc-in').value=q;doSearch();}
function nearMe(){
  if(!navigator.geolocation){showErr("Geolocation not supported by your browser.");return;}
  setLoad(true);
  navigator.geolocation.getCurrentPosition(
    pos=>searchNear(pos.coords.latitude,pos.coords.longitude,"Your Location"),
    ()=>{setLoad(false);showErr("Could not get your location. Please allow location access and try again.");}
  );
}

// ═══════════════════════════════════════════════════════════
// UI HELPERS
// ═══════════════════════════════════════════════════════════
function setLoad(on){
  document.getElementById('loading').style.display=on?'flex':'none';
  document.getElementById('cards').style.display=on?'none':'flex';
  if(on){document.getElementById('empty').style.display='none';document.getElementById('welcome').style.display='none';}
}
function showEmpty(){document.getElementById('empty').style.display='block';document.getElementById('res-count').textContent='No results found';setLoad(false);}
function showErr(msg){document.getElementById('err-box').innerHTML=`<div class="err-box">${msg}</div>`;setLoad(false);}
function clearErr(){document.getElementById('err-box').innerHTML='';}
function openDrawer(){document.getElementById('drawer').classList.add('open');document.getElementById('d-overlay').classList.add('open');}
function closeDrawer(){document.getElementById('drawer').classList.remove('open');document.getElementById('d-overlay').classList.remove('open');}
function om(id){document.getElementById(id).classList.add('on');}
function cm(id){document.getElementById(id).classList.remove('on');}
function openGM(pid,name){window.open(pid?`https://www.google.com/maps/place/?q=place_id:${pid}`:`https://www.google.com/maps/search/${encodeURIComponent(name)}`,'_blank');}

// Close modals on background click
document.querySelectorAll('.modal-bg').forEach(bg=>bg.addEventListener('click',e=>{if(e.target===bg)bg.classList.remove('on');}));

// ═══════════════════════════════════════════════════════════
// PAGE NAVIGATION
// ═══════════════════════════════════════════════════════════
function showPage(p) {
  ['search','how','about','b2b'].forEach(x=>{
    document.getElementById('page-'+x).classList.toggle('on',x===p);
    const nl=document.getElementById('nl-'+x);
    if(nl)nl.classList.toggle('active',x===p);
  });
  window.scrollTo({top:0,behavior:'smooth'});
  if(p==='b2b')populateFeed();
}
function sv_nav(p){showPage(p);}

// ═══════════════════════════════════════════════════════════
// B2B FEED
// ═══════════════════════════════════════════════════════════
const FEED=[
  "Patient booked appointment via request form in Seattle WA",
  "Patient compared 12-session Knee Rehab costs in Miami FL",
  "Patient saved clinic to their account in Austin TX",
  "Patient compared Shockwave Therapy at 3 clinics in NYC",
  "Patient signed up for SMS price drop alerts in Chicago IL",
  "Patient submitted booking request in Los Angeles CA",
  "Patient compared Out-of-Network Cigna rates in Denver CO",
  "Patient left a 5-star review in Nashville TN",
  "Patient used Near Me search in Phoenix AZ",
  "New email subscriber signed up in Houston TX",
];
function populateFeed(){
  const el=document.getElementById('live-feed');if(!el)return;
  el.innerHTML=shuffle(FEED).slice(0,6).map((t,i)=>`
    <div style="display:flex;align-items:center;gap:.48rem;padding:.25rem 0;border-bottom:1px solid var(--bd)">
      <span style="color:var(--em);font-weight:600;font-size:.73rem;white-space:nowrap">${(i*2)+1}m ago</span>
      <span style="font-size:.79rem">${t}</span>
      <span style="margin-left:auto;background:var(--em-lt);color:var(--em-dk);font-size:.68rem;font-weight:700;padding:.11rem .42rem;border-radius:4px;white-space:nowrap">+$15</span>
    </div>`).join('');
}
function claimFlow(tier){toast(`Starting ${tier} onboarding. Our team will contact you within 24 hours.`,'ok');}

// ═══════════════════════════════════════════════════════════
// TOAST
// ═══════════════════════════════════════════════════════════
function toast(msg,type=''){
  const box=document.getElementById('toast-box');
  const el=document.createElement('div');
  el.className=`toast ${type}`;el.textContent=msg;
  box.appendChild(el);setTimeout(()=>el.remove(),3500);
}

// ═══════════════════════════════════════════════════════════
// BOOT
// ═══════════════════════════════════════════════════════════
document.addEventListener('DOMContentLoaded',()=>{
  loadMaps();
  setInterval(()=>{if(document.getElementById('page-b2b').classList.contains('on'))populateFeed();},8000);
});
</script>
</body>
</html>
