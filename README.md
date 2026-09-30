# MrCeo-Trading-AI-bot-
for trading assistance
from pathlib import Path

html = r'''<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Mr CEO Finance — Smart Money Planner</title>
<style>
:root{--bg:#070707;--panel:#11100d;--panel2:#17140e;--gold:#d8a84e;--gold2:#f2cf7a;--text:#f7f2e8;--muted:#aaa18f;--line:#30291c;--green:#65d69a;--red:#ff7070}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--text);font-family:Inter,system-ui,Arial,sans-serif}
button,input{font:inherit}.hidden{display:none!important}.app{min-height:100vh;background:radial-gradient(circle at 85% 0%,#3a2910 0,#070707 35%);padding:22px}
.login{max-width:430px;margin:8vh auto;padding:30px;border:1px solid var(--line);border-radius:24px;background:#0e0d0b;box-shadow:0 25px 80px #000}
.logo{font-weight:900;letter-spacing:2px;color:var(--gold2)}h1{font-size:34px;margin:10px 0}.sub{color:var(--muted);line-height:1.5}
.field{margin:18px 0}.field label{display:block;color:var(--muted);font-size:13px;margin-bottom:7px}input{width:100%;padding:14px;border-radius:12px;border:1px solid var(--line);background:#080807;color:#fff;outline:none}
.btn{border:0;border-radius:12px;padding:13px 16px;cursor:pointer;background:linear-gradient(135deg,var(--gold2),var(--gold));color:#15110a;font-weight:800}.btn.secondary{background:#191711;color:#f5dfaa;border:1px solid var(--line)}.stack{display:grid;gap:10px}
.nav{display:flex;justify-content:space-between;align-items:center;margin-bottom:22px}.navlinks{display:flex;gap:8px;flex-wrap:wrap}.navlinks button{background:#12110e;border:1px solid var(--line);color:#ddd1b7;padding:9px 12px;border-radius:10px;cursor:pointer}.navlinks button.active{border-color:var(--gold);color:var(--gold2)}
.grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px}.card{background:linear-gradient(145deg,#15130f,#0d0d0c);border:1px solid var(--line);border-radius:18px;padding:20px}.label{color:var(--muted);font-size:13px}.amount{font-size:27px;font-weight:850;margin-top:7px}.green{color:var(--green)}.red{color:var(--red)}
.layout{display:grid;grid-template-columns:1.5fr 1fr;gap:14px;margin-top:14px}.row{display:flex;justify-content:space-between;gap:15px;padding:14px 0;border-bottom:1px solid #272218}.row:last-child{border:0}.progress{height:9px;background:#242018;border-radius:10px;overflow:hidden}.bar{height:100%;background:linear-gradient(90deg,var(--gold),var(--gold2));border-radius:10px}
.page{display:none}.page.active{display:block}.section-title{margin:8px 0 14px}.chips{display:flex;gap:8px;flex-wrap:wrap}.chip{padding:8px 10px;border-radius:20px;background:#1a1710;color:#d7c394;border:1px solid var(--line)}
@media(max-width:850px){.grid{grid-template-columns:repeat(2,1fr)}.layout{grid-template-columns:1fr}}@media(max-width:520px){.app{padding:13px}.grid{grid-template-columns:1fr}.nav{align-items:flex-start;gap:12px;flex-direction:column}}
</style>
</head>
<body>
<div id="login" class="app">
  <div class="login">
    <div class="logo">MR CEO FINANCE</div>
    <h1>Secure your money.</h1>
    <p class="sub">A private finance planner for budgets, savings, goals and spending — with device biometric authentication when supported.</p>
    <div class="field"><label>EMAIL / USERNAME</label><input id="user" placeholder="you@example.com"></div>
    <div class="field"><label>PIN</label><input id="pin" type="password" inputmode="numeric" maxlength="6" placeholder="••••••"></div>
    <div class="stack">
      <button class="btn" onclick="login()">Enter Finance Hub</button>
      <button class="btn secondary" onclick="biometric()">♙ Use fingerprint / device biometric</button>
    </div>
    <p id="authMsg" class="sub" style="margin-top:15px;font-size:12px"></p>
  </div>
</div>

<div id="app" class="app hidden">
  <div class="nav">
    <div><div class="logo">MR CEO FINANCE</div><div class="sub">Private Money Command Centre</div></div>
    <div class="navlinks">
      <button class="active" onclick="showPage('dashboard',this)">Dashboard</button>
      <button onclick="showPage('budget',this)">Budget</button>
      <button onclick="showPage('goals',this)">Goals</button>
      <button onclick="showPage('transactions',this)">Transactions</button>
      <button onclick="showPage('security',this)">Security</button>
      <button onclick="logout()">Lock</button>
    </div>
  </div>

  <section id="dashboard" class="page active">
    <h2 class="section-title">Financial Overview</h2>
    <div class="grid">
      <div class="card"><div class="label">TOTAL BALANCE</div><div class="amount" id="balance">KSh 0</div></div>
      <div class="card"><div class="label">MONTHLY INCOME</div><div class="amount green">KSh 48,000</div></div>
      <div class="card"><div class="label">MONTHLY SPENDING</div><div class="amount red">KSh 26,400</div></div>
      <div class="card"><div class="label">SAVINGS RATE</div><div class="amount">45%</div></div>
    </div>
    <div class="layout">
      <div class="card"><h3>Monthly cash plan</h3>
        <div class="row"><span>Housing</span><b>KSh 8,000</b></div>
        <div class="row"><span>Food</span><b>KSh 7,500</b></div>
        <div class="row"><span>Transport</span><b>KSh 3,500</b></div>
        <div class="row"><span>Education</span><b>KSh 4,000</b></div>
        <div class="row"><span>Personal</span><b>KSh 3,400</b></div>
      </div>
      <div class="card"><h3>Savings goal</h3><p class="sub">Emergency fund</p><div class="amount">KSh 36,000 / 60,000</div><div class="progress" style="margin-top:14px"><div class="bar" style="width:60%"></div></div><p class="sub">60% complete</p><button class="btn" onclick="showPage('goals')">Manage goals</button></div>
    </div>
  </section>

  <section id="budget" class="page">
    <h2>Budget Planner</h2><div class="card">
      <div class="field"><label>MONTHLY INCOME (KSh)</label><input id="income" type="number" value="48000"></div>
      <div class="field"><label>ESSENTIALS (KSh)</label><input id="essentials" type="number" value="19000"></div>
      <div class="field"><label>OTHER SPENDING (KSh)</label><input id="other" type="number" value="7400"></div>
      <button class="btn" onclick="calculate()">Calculate plan</button>
      <div id="calc" style="margin-top:18px"></div>
    </div>
  </section>

  <section id="goals" class="page">
    <h2>Savings Goals</h2><div class="grid">
      <div class="card"><div class="label">EMERGENCY FUND</div><div class="amount">KSh 36,000</div><p class="sub">Target KSh 60,000</p><div class="progress"><div class="bar" style="width:60%"></div></div></div>
      <div class="card"><div class="label">NEW LAPTOP</div><div class="amount">KSh 42,000</div><p class="sub">Target KSh 80,000</p><div class="progress"><div class="bar" style="width:52.5%"></div></div></div>
      <div class="card"><div class="label">BUSINESS CAPITAL</div><div class="amount">KSh 18,500</div><p class="sub">Target KSh 100,000</p><div class="progress"><div class="bar" style="width:18.5%"></div></div></div>
    </div>
  </section>

  <section id="transactions" class="page">
    <h2>Recent Transactions</h2><div class="card">
      <div class="row"><span>University expenses</span><b class="red">− KSh 8,500</b></div>
      <div class="row"><span>Freelance income</span><b class="green">+ KSh 12,000</b></div>
      <div class="row"><span>Food & groceries</span><b class="red">− KSh 4,200</b></div>
      <div class="row"><span>Business sale</span><b class="green">+ KSh 7,800</b></div>
    </div>
  </section>

  <section id="security" class="page">
    <h2>Security Centre</h2><div class="card">
      <h3>Biometric access</h3><p class="sub">Use your phone's supported fingerprint, face, or device passkey through WebAuthn. Your fingerprint itself is not sent to this website.</p>
      <button class="btn" onclick="biometric(true)">Register this device</button>
      <p id="securityMsg" class="sub" style="margin-top:14px"></p>
      <hr style="border-color:var(--line);margin:22px 0">
      <h3>Auto-lock</h3><div class="chips"><span class="chip">5 minutes</span><span class="chip">15 minutes</span><span class="chip">30 minutes</span></div>
    </div>
  </section>
</div>
<script>
const $=id=>document.getElementById(id);
let balance=124600;
$('balance').textContent='KSh '+balance.toLocaleString();

function login(){
  const p=$('pin').value;
  if(p.length>=4){$('login').classList.add('hidden');$('app').classList.remove('hidden')}
  else $('authMsg').textContent='Enter a 4–6 digit PIN for demo access.';
}
function logout(){location.reload()}
function showPage(id,btn){
  document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
  $(id).classList.add('active');
  document.querySelectorAll('.navlinks button').forEach(x=>x.classList.remove('active'));
  if(btn)btn.classList.add('active');
}
function calculate(){
  const i=+$('income').value||0,e=+$('essentials').value||0,o=+$('other').value||0;
  const s=Math.max(0,i-e-o);
  $('calc').innerHTML='<div class="card"><div class="label">PLANNED SAVINGS / LEFTOVER</div><div class="amount green">KSh '+s.toLocaleString()+'</div><p class="sub">Suggested split: 50% needs • 20% goals • 20% flexible • 10% buffer. Adjust to your real situation.</p></div>';
}
async function biometric(register=false){
  const msg=register?$('securityMsg'):$('authMsg');
  if(!window.PublicKeyCredential || !navigator.credentials){msg.textContent='Biometric authentication is not supported in this browser/context. Use the PIN demo.';return}
  try{
    const challenge=crypto.getRandomValues(new Uint8Array(32));
    const publicKey={challenge,rp:{name:'Mr CEO Finance'},user:{id:crypto.getRandomValues(new Uint8Array(16)),name:'finance-user',displayName:'Finance User'},pubKeyCredParams:[{type:'public-key',alg:-7},{type:'public-key',alg:-257}],authenticatorSelection:{authenticatorAttachment:'platform',userVerification:'required'},timeout:60000,attestation:'none'};
    if(register){
      await navigator.credentials.create({publicKey});
      msg.textContent='Device biometric/passkey registration completed for this demo context.';
    }else{
      msg.textContent='Biometric verification must be performed by your device/browser; this preview cannot store or read your fingerprint.';
      $('login').classList.add('hidden');$('app').classList.remove('hidden');
    }
  }catch(e){msg.textContent='Biometric setup was cancelled or is unavailable here. Use your PIN instead.'}
}
</script>
</body></html>'''

path=Path("/mnt/data/mr_ceo_finance.html")
path.write_text(html,encoding="utf-8")
print(path, path.stat().st_size)
