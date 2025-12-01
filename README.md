<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>AMANDA — Dashboard Arsip (FIXED)</title>

<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;800&display=swap" rel="stylesheet">

<style>
  :root{
    --accent: #1e3c72;
    --accent2: #2a5298;
    --accent-soft: #4ea8de;
    --header-bg: linear-gradient(120deg, #1e3c72, #2a5298, #4ea8de);
  }

  *{box-sizing:border-box;margin:0;padding:0;}
  body{
    font-family:'Nunito',sans-serif;
    min-height:100vh;
    background:#f4f7fb;
    color:#222;
  }

  /* ======================================================
     LOGIN SCREEN
  ====================================================== */
  .login-screen{
    position:fixed;inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    background:linear-gradient(180deg, rgba(20,40,80,0.65), rgba(40,60,100,0.35));
    z-index:9999;
    padding:20px;
  }

  .login-card{
    width:420px;
    max-width:95%;
    background:linear-gradient(180deg, rgba(255,255,255,0.96), rgba(250,253,255,0.98));
    border-radius:18px;
    box-shadow:0 18px 50px rgba(2,8,23,0.45);
    padding:26px;
    animation:fadeIn .5s ease;
  }

  .login-title{font-size:22px;font-weight:800;margin-bottom:4px;color:#1e3c72;}
  .login-sub{font-size:14px;margin-bottom:20px;color:#3d4e74;}
  .login-label{display:block;margin-top:12px;font-size:14px;font-weight:700;color:#1e3c72;}
  .login-input{width:100%;padding:12px;border-radius:12px;border:1px solid #d9e1ef;margin-top:6px;background:white;}

  .btn{padding:10px 16px;border-radius:10px;border:none;cursor:pointer;font-weight:700;transition:.2s;}
  .btn.primary{background:linear-gradient(90deg,var(--accent),var(--accent2));color:white;}
  .btn.minimal{width:100%;background:white;color:#1e3c72;border:1px solid #d4dcee;margin-top:14px;}
  .btn.minimal:hover{background:#f5f8ff;}

  header{padding:22px 32px;display:flex;align-items:center;gap:20px;background:var(--header-bg);color:white;box-shadow:0 6px 18px rgba(0,0,0,0.18);border-bottom-left-radius:16px;border-bottom-right-radius:16px;display:none;}
  .logo{width:74px;height:74px;} .logo img{width:100%;height:100%;object-fit:contain;}
  h1{font-size:23px;font-weight:900;margin:0;} p.small{font-size:14px;opacity:.9;margin-top:2px;}

  .container{max-width:1300px;margin:22px auto;padding:0 20px;display:none;}
  .layout{display:grid;grid-template-columns:260px 1fr;gap:20px;}
  .sidebar{background:linear-gradient(160deg,#ffffff,#e8edf7);border-radius:24px;box-shadow:0 6px 26px rgba(0,0,0,0.08);padding:20px;position:relative;overflow:hidden;}
  .sidebar::before {
    pointer-events: none;content:"";position:absolute;top:-40%;left:-40%;width:200%;height:200%;background:radial-gradient(circle at center, rgba(78,168,222,0.14), transparent 65%);filter:blur(80px);}
  .sidebar-title{font-weight:800;font-size:18px;color:#1e3c72;margin-bottom:16px;position:relative;z-index:2;}
  #roleBadge{font-size:12px;padding:6px 10px;border-radius:12px;background:#eef4ff;color:#1e3c72;font-weight:800;box-shadow:0 3px 10px rgba(30,60,114,0.1);}
  .nav-item{padding:12px 16px;border-radius:14px;cursor:pointer;margin-bottom:10px;display:flex;align-items:center;gap:12px;font-weight:700;color:#2d3e5e;position:relative;overflow:hidden;transition:all .25s ease;z-index:2;}
  .menu-icon{width:20px;height:20px;font-size:17px;} .nav-item::before{content:"";position:absolute;top:0;left:-100%;width:100%;height:100%;background:linear-gradient(90deg,transparent,rgba(78,168,222,0.18),transparent);transition:0.42s;} .nav-item:hover::before{ left:100%; }
  .nav-item:hover{color:#1e3c72;background:rgba(78,168,222,0.12);box-shadow:0 0 12px rgba(78,168,222,0.25);transform:translateX(4px);} .nav-item.active{background:linear-gradient(90deg,#1e3c72,#2a5298);color:white;box-shadow:0 0 14px rgba(30,60,114,0.35);transform:translateX(4px);}
  .sidebar-footer{margin-top:20px;display:flex;justify-content:space-between;align-items:center;font-size:12px;color:#6a7a8a;}
  main.main{position:relative;min-height:70vh;border-radius:20px;overflow:hidden;}
  .dashboard-bg{position:absolute;inset:0;background:url('unnamed (1).jpg') center/cover no-repeat;filter:brightness(0.75);} .dashboard-overlay{position:absolute;inset:0;background:rgba(255,255,255,0.55);backdrop-filter:blur(10px);} .content-wrap{position:relative;z-index:5;padding:18px;}
  .card{background:rgba(255,255,255,0.9);backdrop-filter:blur(14px);border-radius:20px;padding:20px;margin-bottom:18px;box-shadow:0 10px 25px rgba(0,0,0,0.05);} .dashboard{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px;} .stat-card{background:white;padding:18px;border-radius:18px;box-shadow:0 4px 18px rgba(0,0,0,0.06);transition:0.25s;cursor:pointer;} .stat-card:hover{transform:translateY(-6px);box-shadow:0 8px 24px rgba(0,0,0,0.08);} table{width:100%;border-collapse:collapse;margin-top:10px;} th,td{padding:10px;font-size:14px;border-bottom:1px solid #e0e7ef;} th{background:#f0f4ff;font-weight:800;color:#1e3c72;} .grid-form{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px;margin-top:10px;} input[type=text]{width:100%;padding:10px;border-radius:10px;border:1px solid #d7e1f0;} .btn.danger{background:linear-gradient(90deg,#ff5f6d,#ff3b3b);color:white;} .modal{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(0,0,0,0.4);z-index:9999;display:none;} .modal-card{background:white;padding:22px;border-radius:16px;width:96%;max-width:600px;} @keyframes fadeIn{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}} .fadeIn{animation:fadeIn .4s ease;}
</style>
</head>

<body>

<!-- LOGIN SCREEN -->
<div id="loginScreen" class="login-screen">
  <div class="login-card">
    <div class="login-title">Masuk ke AMANDA</div>
    <div class="login-sub">Pilih metode masuk sesuai peran Anda</div>

    <!-- Admin Login -->
    <label class="login-label">Username Admin</label>
    <input id="username" class="login-input" type="text" placeholder="username admin">

    <label class="login-label">Password</label>
    <input id="password" class="login-input" type="password" placeholder="password">

    <button class="btn primary" style="margin-top:16px;width:100%;" onclick="loginAdmin()">
      Masuk sebagai Admin
    </button>

    <!-- Pengguna (Viewer) -->
    <button class="btn minimal" onclick="loginPengguna()">
      Masuk sebagai Pengguna
    </button>
  </div>
</div>


<!-- HEADER -->
<header id="mainHeader">
  <div class="logo"><img src="Amanda-Arsip.png" alt="Logo"></div>
  <div><h1>AMANDA</h1><p class="small">Aplikasi Manajemen Data Arsip Statis</p></div>
</header>


<!-- MAIN APP CONTAINER -->
<div class="container" id="mainApp">
  <div class="layout">

    <!-- SIDEBAR -->
    <aside class="sidebar">
      <div class="sidebar-title">Menu
        <span id="roleBadge">GUEST</span>
      </div>

      <div id="menu"></div>

      <div class="sidebar-footer">
        <span>AMANDA v1</span>
        <button id="logoutBtn" class="btn primary" style="padding:6px 12px;font-size:12px;">Logout</button>
      </div>
    </aside>

    <!-- MAIN -->
    <main class="main">
      <div class="dashboard-bg"></div>
      <div class="dashboard-overlay"></div>
      <div class="content-wrap" id="content"></div>
    </main>

  </div>
</div>

<!-- MODAL -->
<div id="modal" class="modal">
  <div class="modal-card fadeIn">
    <h3 id="modalTitle">Edit Data</h3>
    <div id="modalBody"></div>
    <div style="margin-top:12px;text-align:right;">
      <button class="btn" onclick="closeModal()">Tutup</button>
    </div>
  </div>
</div>

<script>
/* ===================== CREDENTIALS & AUTH ===================== */
const CREDENTIALS = {
  admin: { username: 'admin', password: 'admin123', role: 'admin' },
  pengguna: { username: 'pengguna', password: 'pengguna123', role: 'pengguna' }
};

/* ===================== DATA MODULES ===================== */
const ICONS = {
  dashboard: "🏠",
  jumlah_arsip_statis: "📦",
  rekap_arsip_SIKN: "📊",
  pemusnahan_Arsip: "🔥",
  Arsip_permanen: "♾️",
  penyelamatan_bencana: "🚨",
  skpd_digabung: "🔗",
  skpd_dibubarkan: "❌",
  alih_media: "🔁",
  penerbitan_izin: "📝",
  arsip_vital: "🔒"
};

const MODULES = [
  {key:'jumlah_arsip_statis',title:'Jumlah Arsip Statis'},
  {key:'rekap_arsip_SIKN',title:'Rekap Arsip SIKN'},
  {key:'pemusnahan_Arsip',title:'Pemusnahan Arsip'},
  {key:'Arsip_permanen',title:'Arsip Permanen'},
  {key:'penyelamatan_bencana',title:'Penyelamatan Bencana'},
  {key:'skpd_digabung',title:'SKPD Digabung'},
  {key:'skpd_dibubarkan',title:'SKPD Dibubarkan'},
  {key:'alih_media',title:'Alih Media'},
  {key:'penerbitan_izin',title:'Penerbitan Izin'},
  {key:'arsip_vital',title:'Arsip Vital'}
].map(m=>({
  ...m,
  fields:[
    {id:'pencipta_arsip', label:'Pencipta Arsip'},
    {id:'uraian_arsip', label:'Uraian Arsip'},
    {id:'tahun', label:'Tahun'},
    {id:'jumlah_arsip', label:'Jumlah Arsip'},
    {id:'jumlah_berkas', label:'Jumlah Berkas'},
    {id:'jumlah_boks', label:'Jumlah Boks'},
    {id:'keterangan', label:'Keterangan'},
    {id:'link_drive', label:'Tautan Google Drive'}
  ]
}));

/* ===================== IndexedDB ===================== */
let db;
const DB_NAME = 'amanda-drive';
const DB_VERSION = 2;

function openDB(){
  return new Promise((resolve, reject) => {
    const req = indexedDB.open(DB_NAME, DB_VERSION);
    req.onupgradeneeded = (e) => {
      db = e.target.result;
      MODULES.forEach(m => {
        if(!db.objectStoreNames.contains(m.key)){
          db.createObjectStore(m.key, { keyPath: 'id', autoIncrement: true });
        }
      });
    };
    req.onsuccess = (e) => { db = e.target.result; resolve(db); };
    req.onerror = (e) => reject(e);
  });
}

function store(name, mode='readonly'){
  return db.transaction(name, mode).objectStore(name);
}
function addRec(name, obj){ return new Promise((res, rej) => { const q = store(name,'readwrite').add(obj); q.onsuccess = ()=>res(); q.onerror = ()=>rej(); }); }
function putRec(name, obj){ return new Promise((res, rej) => { const q = store(name,'readwrite').put(obj); q.onsuccess = ()=>res(); q.onerror = ()=>rej(); }); }
function getAll(name){ return new Promise((res, rej) => { const q = store(name).getAll(); q.onsuccess = ()=>res(q.result || []); q.onerror = ()=>rej(q.error); }); }
function getOne(name, id){ return new Promise((res, rej) => { const q = store(name).get(Number(id)); q.onsuccess = ()=>res(q.result); q.onerror = ()=>rej(q.error); }); }
function delRec(name, id){ return new Promise((res, rej) => { const q = store(name,'readwrite').delete(Number(id)); q.onsuccess = ()=>res(); q.onerror = ()=>rej(); }); }

/* ===================== UI STATE ===================== */
let active = 'home';

/* Helper to safely get DOM elements (avoid referencing undefined globals) */
function $id(id){ return document.getElementById(id); }

/* ===================== AUTH & UI FUNCTIONS ===================== */
function loginAdmin(){
  const u = $id('username').value.trim();
  const p = $id('password').value.trim();
  if(u === CREDENTIALS.admin.username && p === CREDENTIALS.admin.password){
    localStorage.setItem('role','admin');
    localStorage.setItem('user', u);
    afterLogin();
  } else {
    alert('Username atau password admin salah.');
  }
}

function loginPengguna(){
  localStorage.setItem('role','pengguna');
  localStorage.setItem('user', CREDENTIALS.pengguna.username);
  afterLogin();
}

function logout(){
  try{
    localStorage.removeItem('role');
    localStorage.removeItem('user');

    // Reset UI safely
    active = 'home';
    const menuEl = $id('menu');
    const contentEl = $id('content');
    if(menuEl) menuEl.innerHTML = '';
    if(contentEl) contentEl.innerHTML = '';

    // Ensure modal closed
    closeModal();

    // show login screen, hide app
    $id('loginScreen').style.display = 'flex';
    $id('mainHeader').style.display = 'none';
    $id('mainApp').style.display = 'none';

    // reset inputs
    $id('username').value = '';
    $id('password').value = '';

  }catch(err){
    console.error('Logout error:', err);
  }
}

function showLoginScreen(){ $id('loginScreen').style.display = 'flex'; $id('mainHeader').style.display = 'none'; $id('mainApp').style.display = 'none'; }
function showMainApp(){ $id('loginScreen').style.display = 'none'; $id('mainHeader').style.display = 'flex'; $id('mainApp').style.display = 'block'; }

function afterLogin(){ updateRoleBadge(); showMainApp(); openDB().then(()=>{ renderMenu(); renderHome(); }).catch(e=>{ console.error('DB open failed', e); renderMenu(); renderHome(); }); }

function updateRoleBadge(){ const badge = $id('roleBadge'); const r = (localStorage.getItem('role') || 'pengguna').toUpperCase(); if(badge) badge.textContent = r; }

/* Init on load */
document.addEventListener('DOMContentLoaded', ()=>{
  // Attach logout handler to avoid inline onclick issues
  const logoutBtn = $id('logoutBtn');
  if(logoutBtn) logoutBtn.addEventListener('click', logout);

  const role = localStorage.getItem('role');
  if(!role){ showLoginScreen(); } else { showMainApp(); updateRoleBadge(); openDB().then(()=>{ renderMenu(); renderHome(); }); }
});

/* ===================== UI: Menu, Dashboard, Modules ===================== */
async function renderMenu(){
  const menuEl = $id('menu'); if(!menuEl) return;
  menuEl.innerHTML = '';
  const role = localStorage.getItem('role') || 'pengguna';

  // Dashboard
  const home = document.createElement('div');
  home.className = 'nav-item' + (active === 'home' ? ' active' : '');
  home.innerHTML = `<span class="menu-icon">${ICONS.dashboard}</span> Dashboard`;
  home.onclick = ()=>{ active='home'; renderMenu(); renderHome(); };
  menuEl.appendChild(home);

  // Modules
  MODULES.forEach(m=>{
    const d = document.createElement('div');
    d.className = 'nav-item' + (active === m.key ? ' active' : '');
    d.innerHTML = `<span class="menu-icon">${ICONS[m.key] || '📁'}</span> ${m.title}`;
    d.onclick = ()=>{ active = m.key; renderMenu(); renderModule(m); };
    menuEl.appendChild(d);
  });

  // Help / spacer
  const spacer = document.createElement('div'); spacer.style.height = '8px'; menuEl.appendChild(spacer);
  const help = document.createElement('div'); help.className = 'nav-item'; help.innerHTML = `<span class="menu-icon">❔</span> Bantuan`;
  help.onclick = ()=>{ alert('AMANDA — Aplikasi Manajemen Arsip\nHubungi admin untuk bantuan.'); };
  menuEl.appendChild(help);
}

async function renderHome(){
  const contentEl = $id('content'); if(!contentEl) return;
  contentEl.innerHTML = '<div class="card fadeIn"><h3>Dashboard</h3><p class="small">Ringkasan total per menu & per tahun.</p></div>';
  const grid = document.createElement('div'); grid.className = 'dashboard fadeIn';

  let global = {};

  for(const m of MODULES){
    const rows = await getAll(m.key);
    let totalMenu = { arsip:0, berkas:0, boks:0 };
    rows.forEach(r=>{ totalMenu.arsip += Number(r.jumlah_arsip) || 0; totalMenu.berkas += Number(r.jumlah_berkas) || 0; totalMenu.boks  += Number(r.jumlah_boks) || 0; });

    const per = {};
    rows.forEach(r=>{
      const t = (r.tahun?.trim()) || 'Tidak Ada Tahun';
      if(!per[t]) per[t] = { arsip:0, berkas:0, boks:0 };
      ['arsip','berkas','boks'].forEach(k=>{ const f = 'jumlah_' + k; per[t][k] += (+r[f] || 0); if(!global[t]) global[t] = { arsip:0, berkas:0, boks:0 }; global[t][k] += (+r[f] || 0); });
    });

    const card = document.createElement('div'); card.className = 'stat-card'; card.onclick = ()=>{ active = m.key; renderMenu(); renderModule(m); };

    let html = `<h3>${m.title}</h3><div style="font-size:13px;margin-top:6px;padding:8px;border-radius:8px;background:rgba(30,60,114,0.06)"><strong>TOTAL MENU</strong><br> 🗃 ${totalMenu.arsip} Arsip | 📁 ${totalMenu.berkas} Berkas | 📦 ${totalMenu.boks} Boks</div>`;

    const tahunList = Object.keys(per).sort((a,b)=>(+a||9999)-(+b||9999));
    if(tahunList.length === 0){ html += `<p class="small">Belum ada data</p>`; } else { tahunList.forEach(t=>{ const d = per[t]; html += `<div style="margin-top:8px;font-size:13px;padding:8px;border-radius:8px;background:rgba(255,255,255,0.9)">📅 <strong>${t}</strong> : ${d.arsip} Arsip | ${d.berkas} Berkas | ${d.boks} Boks</div>`; }); }

    card.innerHTML = html; grid.appendChild(card);
  }

  contentEl.appendChild(grid);

  // Rekap global
  const table = document.createElement('table'); table.innerHTML = '<thead><tr><th>Tahun</th><th>Total Arsip</th><th>Total Berkas</th><th>Total Boks</th></tr></thead>';
  const tb = document.createElement('tbody');
  Object.keys(global).sort((a,b)=>(+a||9999)-(+b||9999)).forEach(t=>{ const d = global[t]; tb.innerHTML += `<tr><td>${t}</td><td>${d.arsip}</td><td>${d.berkas}</td><td>${d.boks}</td></tr>`; });
  table.appendChild(tb);
  const ccard = document.createElement('div'); ccard.className = 'card fadeIn'; ccard.innerHTML = '<h3>Rekap Total Semua Modul Berdasarkan Tahun</h3>'; ccard.appendChild(table); contentEl.appendChild(ccard);
}

async function renderModule(mod){
  const contentEl = $id('content'); if(!contentEl) return;
  contentEl.innerHTML = '';
  const role = localStorage.getItem('role') || 'pengguna';

  const formCard = document.createElement('div'); formCard.className = 'card fadeIn';
  const form = document.createElement('form'); form.className = 'grid-form';
  form.onsubmit = async (e)=>{ e.preventDefault(); const fd = new FormData(form); const obj = {}; mod.fields.forEach(f=> obj[f.id] = fd.get(f.id)); await addRec(mod.key, obj); form.reset(); await loadTable(mod); };

  mod.fields.forEach(f=>{ const d = document.createElement('div'); d.innerHTML = `<label style="font-weight:700;color:#1e3c72">${f.label}</label><input name="${f.id}" type="text">`; form.appendChild(d); });
  form.innerHTML += `<div style="grid-column:1/-1;margin-top:6px;"><button class="btn primary">Simpan</button></div>`;
  formCard.innerHTML = `<h3>${mod.title}</h3><p class="small">Tambah, edit, atau hapus data.</p>`; formCard.appendChild(form); contentEl.appendChild(formCard);
  if(role !== 'admin'){ formCard.style.display = 'none'; }

  const wrap = document.createElement('div'); wrap.className = 'card fadeIn'; wrap.innerHTML = `<h3>Data ${mod.title}</h3><table><thead><tr><th>No</th>${mod.fields.map(f=>`<th>${f.label}</th>`).join('')}<th>Aksi</th></tr></thead><tbody></tbody></table>`;
  contentEl.appendChild(wrap);
  await loadTable(mod);
}

async function loadTable(mod){
  const rows = await getAll(mod.key);
  rows.sort((a,b)=>(+a.tahun||9999)-(+b.tahun||9999));
  const tbody = $id('content')?.querySelector('tbody'); if(!tbody) return;
  tbody.innerHTML = '';
  const role = localStorage.getItem('role') || 'pengguna';

  rows.forEach((r, i)=>{
    const tds = mod.fields.map(f=>{
      let val = r[f.id] || '';
      if(f.id === 'link_drive' && typeof val === 'string' && val.startsWith('http')){ val = `<a href="${val}" target="_blank">Bukti Dukung</a>`; }
      return `<td>${val}</td>`;
    }).join('');

    let aksiHtml = '';
    if(role === 'admin'){
      aksiHtml = `<button class="btn primary" onclick="editData(${r.id}, '${mod.key}')">Edit</button> <button class="btn danger" onclick="deleteData(${r.id}, '${mod.key}')">Hapus</button>`;
    } else { aksiHtml = `<span style="color:#8892a8;font-size:13px;">Hanya lihat</span>`; }

    tbody.innerHTML += `<tr><td style="width:48px">${i+1}</td>${tds}<td style="white-space:nowrap">${aksiHtml}</td></tr>`;
  });
}

async function editData(id, key){
  const mod = MODULES.find(m => m.key === key);
  const data = await getOne(key, id);
  const modal = $id('modal'); const body = $id('modalBody'); if(!modal || !body) return;
  modal.style.display = 'flex'; $id('modalTitle').textContent = `Edit — ${mod.title}`; body.innerHTML = '';

  const form = document.createElement('form'); form.className = 'grid-form';
  mod.fields.forEach(f=>{ const d = document.createElement('div'); d.innerHTML = `<label style="font-weight:700;color:#1e3c72">${f.label}</label><input name="${f.id}" type="text" value="${(data[f.id]||'')}">`; form.appendChild(d); });

  const saveBtn = document.createElement('button'); saveBtn.className = 'btn primary'; saveBtn.textContent = 'Simpan Perubahan'; saveBtn.type = 'submit'; form.appendChild(saveBtn);
  form.onsubmit = async (e)=>{ e.preventDefault(); const fd = new FormData(form); mod.fields.forEach(f => data[f.id] = fd.get(f.id)); await putRec(key, data); closeModal(); renderModule(mod); };
  body.appendChild(form);
}

function closeModal(){ const modal = $id('modal'); if(modal) modal.style.display = 'none'; const mb = $id('modalBody'); if(mb) mb.innerHTML = ''; const mt = $id('modalTitle'); if(mt) mt.textContent = 'Edit Data'; }

async function deleteData(id, key){ if(!confirm('Yakin hapus data ini?')) return; await delRec(key, id); const mod = MODULES.find(m=>m.key === key); renderModule(mod); }

</script>

</body>
</html>
