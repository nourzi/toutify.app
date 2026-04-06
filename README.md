<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Toutify</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet"/>
<style>
:root{
  --bg:#08080c;--s1:#111118;--s2:#18181f;--s3:#22222c;--s4:#2a2a38;
  --border:rgba(255,255,255,0.07);--border2:rgba(255,255,255,0.13);
  --text:#eeeef5;--muted:#7a7a9a;--dim:#44445a;
  --acc:#6c5fff;--acc2:#9b8fff;--acc-glow:rgba(108,95,255,0.2);
  --green:#22d98a;--amber:#f0a500;--red:#ff4d4d;--pink:#ff5fa0;--teal:#00d4cc;--blue:#3b9eff;
  --fh:'Syne',sans-serif;--fb:'DM Sans',sans-serif;
  --r:14px;--rs:8px;
}
*{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--text);font-family:var(--fb);min-height:100vh;overflow-x:hidden;}
button{cursor:pointer;font-family:var(--fb);border:none;outline:none;}
input,textarea,select{font-family:var(--fb);outline:none;}
a{color:inherit;text-decoration:none;}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px;height:4px;}
::-webkit-scrollbar-thumb{background:var(--s4);border-radius:4px;}

/* ── LAYOUT ── */
.root{display:flex;min-height:100vh;}
.sidebar{width:220px;background:var(--s1);border-right:1px solid var(--border);display:flex;flex-direction:column;padding:0;flex-shrink:0;position:sticky;top:0;height:100vh;overflow-y:auto;}
.main{flex:1;min-width:0;padding:2rem 2rem 4rem;max-width:980px;}

/* SIDEBAR */
.sb-logo{padding:1.4rem 1.2rem 1rem;border-bottom:1px solid var(--border);}
.sb-logo h1{font-family:var(--fh);font-size:20px;font-weight:800;letter-spacing:-.5px;}
.sb-logo h1 span{color:var(--acc2);}
.sb-logo .sb-user{font-size:11px;color:var(--muted);margin-top:3px;}
.sb-xp{padding:.8rem 1.2rem;border-bottom:1px solid var(--border);}
.sb-lvl-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:5px;}
.sb-lvl{font-family:var(--fh);font-size:11px;font-weight:700;background:var(--acc);color:#fff;border-radius:999px;padding:2px 8px;}
.sb-xp-track{height:5px;background:var(--s3);border-radius:999px;overflow:hidden;}
.sb-xp-fill{height:100%;background:linear-gradient(90deg,var(--acc),var(--teal));border-radius:999px;transition:width .6s ease;}
.sb-xp-txt{font-size:10px;color:var(--muted);margin-top:3px;}
.sb-nav{padding:.6rem 0;flex:1;}
.sb-section{font-size:10px;font-weight:700;color:var(--dim);letter-spacing:.08em;padding:.6rem 1.2rem .3rem;font-family:var(--fh);}
.nav-item{display:flex;align-items:center;gap:9px;padding:.55rem 1.2rem;font-size:13px;color:var(--muted);cursor:pointer;transition:all .15s;border-left:2px solid transparent;}
.nav-item:hover{color:var(--text);background:var(--s2);}
.nav-item.active{color:var(--text);background:var(--s2);border-left-color:var(--acc);}
.nav-item .ni{font-size:15px;width:18px;text-align:center;}
.sb-bottom{padding:.8rem 1.2rem;border-top:1px solid var(--border);}
.sb-streak{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--muted);}
.sb-streak-fire{color:var(--amber);font-size:16px;}

/* SCREENS */
.screen{display:none;animation:fadeUp .25s ease;}
.screen.active{display:block;}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* COMMON */
.page-title{font-family:var(--fh);font-size:24px;font-weight:800;margin-bottom:4px;}
.page-sub{font-size:13px;color:var(--muted);margin-bottom:1.5rem;}
.sec-head{font-family:var(--fh);font-size:14px;font-weight:700;margin-bottom:.7rem;}
.card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem 1.4rem;}
.card2{background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem 1.1rem;}
.grid2{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;}
.grid3{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;}
.grid4{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:10px;}
.stat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem;}
.stat-box{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem 1rem;text-align:center;}
.stat-n{font-family:var(--fh);font-size:26px;font-weight:800;}
.stat-l{font-size:11px;color:var(--muted);margin-top:2px;}
.divider{border:none;border-top:1px solid var(--border);margin:1.2rem 0;}
.badge-pill{display:inline-flex;align-items:center;gap:4px;font-size:11px;font-weight:700;padding:3px 9px;border-radius:999px;font-family:var(--fh);}
.prog-bar{height:5px;background:var(--s3);border-radius:999px;overflow:hidden;}
.prog-fill{height:100%;border-radius:999px;transition:width .5s ease;}
.btn{display:inline-flex;align-items:center;gap:6px;padding:9px 18px;font-size:13px;font-weight:600;border-radius:var(--rs);border:1px solid var(--border2);background:var(--s2);color:var(--text);transition:all .2s;font-family:var(--fh);}
.btn:hover{background:var(--s3);border-color:rgba(255,255,255,.2);}
.btn-acc{background:var(--acc);border-color:var(--acc);color:#fff;}
.btn-acc:hover{background:var(--acc2);border-color:var(--acc2);}
.btn-sm{padding:6px 13px;font-size:12px;}
.btn-xs{padding:4px 10px;font-size:11px;}
.btn-danger{background:rgba(255,77,77,.15);border-color:var(--red);color:var(--red);}
.btn-danger:hover{background:rgba(255,77,77,.25);}
.inp{background:var(--s2);border:1px solid var(--border2);border-radius:var(--rs);padding:9px 13px;color:var(--text);font-size:13px;width:100%;transition:border-color .2s;}
.inp:focus{border-color:var(--acc);}
textarea.inp{resize:vertical;min-height:80px;line-height:1.6;}
.tag{font-size:11px;font-weight:700;padding:2px 8px;border-radius:999px;font-family:var(--fh);}
.row{display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.col{display:flex;flex-direction:column;gap:8px;}
.lbl{font-size:12px;color:var(--muted);margin-bottom:4px;display:block;}
.toast{position:fixed;bottom:24px;right:24px;background:var(--s2);border:1px solid var(--border2);border-radius:var(--rs);padding:10px 16px;font-size:13px;z-index:9999;transform:translateY(80px);opacity:0;transition:all .3s;pointer-events:none;max-width:300px;}
.toast.show{transform:translateY(0);opacity:1;}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:500;align-items:center;justify-content:center;padding:1rem;}
.modal-bg.open{display:flex;}
.modal{background:var(--s1);border:1px solid var(--border2);border-radius:var(--r);padding:1.5rem;width:100%;max-width:460px;max-height:90vh;overflow-y:auto;}
.modal-title{font-family:var(--fh);font-size:18px;font-weight:700;margin-bottom:1rem;}
.close-btn{background:none;border:none;color:var(--muted);font-size:20px;cursor:pointer;margin-left:auto;display:block;}

/* ── ONBOARDING / AUTH ── */
#screen-auth{display:flex;align-items:center;justify-content:center;min-height:100vh;background:var(--bg);}
.auth-box{width:100%;max-width:400px;text-align:center;}
.auth-logo{font-family:var(--fh);font-size:36px;font-weight:800;margin-bottom:4px;}
.auth-logo span{color:var(--acc2);}
.auth-sub{font-size:14px;color:var(--muted);margin-bottom:2rem;}
.auth-tabs{display:flex;background:var(--s2);border-radius:var(--rs);padding:4px;margin-bottom:1.5rem;}
.auth-tab{flex:1;padding:8px;font-size:13px;font-weight:600;border-radius:6px;background:none;color:var(--muted);transition:all .2s;font-family:var(--fh);}
.auth-tab.active{background:var(--acc);color:#fff;}
.auth-form{display:flex;flex-direction:column;gap:10px;}
.auth-divider{text-align:center;font-size:12px;color:var(--muted);margin:.5rem 0;}

/* ── HOME ── */
.subjects-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(155px,1fr));gap:10px;margin-bottom:1.5rem;}
.subj-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1rem;cursor:pointer;transition:all .2s;position:relative;overflow:hidden;}
.subj-card::after{content:'';position:absolute;top:0;left:0;right:0;height:3px;}
.subj-card:hover{transform:translateY(-2px);border-color:var(--border2);}
.subj-card.sel{border-color:var(--acc);}
.subj-icon{font-size:24px;margin-bottom:8px;}
.subj-name{font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:4px;}
.subj-meta{font-size:11px;color:var(--muted);margin-bottom:7px;}
.add-subj{background:none;border:1px dashed var(--border2);border-radius:var(--r);padding:1rem;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;color:var(--muted);transition:all .2s;min-height:110px;}
.add-subj:hover{border-color:var(--acc);color:var(--acc);}

/* ── FLASHCARDS ── */
.fc-wrap{display:flex;flex-direction:column;align-items:center;gap:1rem;}
.flashcard{width:100%;max-width:540px;min-height:230px;perspective:1000px;cursor:pointer;}
.fc-inner{position:relative;width:100%;min-height:230px;transform-style:preserve-3d;transition:transform .5s ease;border-radius:var(--r);}
.fc-inner.flipped{transform:rotateY(180deg);}
.fc-face{position:absolute;width:100%;min-height:230px;backface-visibility:hidden;border-radius:var(--r);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:2rem;text-align:center;border:1px solid var(--border2);}
.fc-front{background:var(--s1);}
.fc-back{background:var(--s2);transform:rotateY(180deg);}
.fc-lbl{font-size:10px;font-family:var(--fh);font-weight:700;letter-spacing:.08em;color:var(--muted);margin-bottom:12px;}
.fc-q{font-size:17px;font-weight:500;line-height:1.6;}
.fc-sub{font-size:12px;color:var(--muted);margin-top:8px;}
.fc-dots{display:flex;gap:5px;}
.fc-dot{width:7px;height:7px;border-radius:50%;background:var(--s4);}
.fc-dot.done{background:var(--green);}
.fc-dot.cur{background:var(--acc);}
.rate-btns{display:flex;gap:8px;}

/* ── QUIZ ── */
.q-card{background:var(--s1);border:1px solid var(--border2);border-radius:var(--r);padding:1.4rem 1.6rem;font-size:16px;font-weight:500;line-height:1.6;margin-bottom:1rem;}
.opts{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.opt{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:12px 16px;color:var(--text);font-size:13px;text-align:left;transition:all .2s;}
.opt:hover:not(:disabled){border-color:var(--acc);background:var(--s2);}
.opt.correct{background:rgba(34,217,138,.1);border-color:var(--green);color:var(--green);}
.opt.wrong{background:rgba(255,77,77,.1);border-color:var(--red);color:var(--red);}
.opt:disabled{cursor:default;}
.timer-bar{height:4px;background:var(--acc);border-radius:999px;transition:width 1s linear;margin-bottom:12px;}
.res-score{font-family:var(--fh);font-size:60px;font-weight:800;text-align:center;}

/* ── LEADERBOARD ── */
.lb-row{display:flex;align-items:center;gap:12px;padding:.75rem 1rem;border-bottom:1px solid var(--border);transition:background .15s;}
.lb-row:hover{background:var(--s2);}
.lb-rank{font-family:var(--fh);font-size:14px;font-weight:800;min-width:28px;text-align:center;}
.lb-avatar{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-size:13px;font-weight:700;flex-shrink:0;}
.lb-info{flex:1;}
.lb-name{font-size:13px;font-weight:600;}
.lb-sub{font-size:11px;color:var(--muted);}
.lb-xp{font-family:var(--fh);font-size:14px;font-weight:700;color:var(--acc2);}
.lb-me{background:var(--acc-glow);border-radius:var(--rs);}

/* ── BATTLE ── */
.battle-search{display:flex;gap:8px;margin-bottom:1rem;}
.player-result{display:flex;align-items:center;gap:10px;padding:.8rem 1rem;background:var(--s2);border-radius:var(--rs);margin-bottom:8px;cursor:pointer;transition:all .2s;border:1px solid var(--border);}
.player-result:hover{border-color:var(--acc);}
.battle-arena{display:grid;grid-template-columns:1fr auto 1fr;gap:1rem;align-items:start;}
.battle-player{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1rem;text-align:center;}
.battle-vs{font-family:var(--fh);font-size:20px;font-weight:800;color:var(--muted);align-self:center;text-align:center;}
.battle-score{font-family:var(--fh);font-size:32px;font-weight:800;}
.battle-prog{height:8px;border-radius:999px;overflow:hidden;background:var(--s3);margin-top:6px;}

/* ── AI TUTOR ── */
.chat-box{background:var(--s1);border:1px solid var(--border);border-radius:var(--r) var(--r) 0 0;min-height:320px;max-height:420px;overflow-y:auto;padding:1rem;display:flex;flex-direction:column;gap:10px;}
.msg{display:flex;gap:8px;max-width:85%;}
.msg.user{align-self:flex-end;flex-direction:row-reverse;}
.msg-av{width:28px;height:28px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;font-family:var(--fh);}
.msg.msg-ai .msg-av{background:var(--acc);color:#fff;}
.msg.msg-user .msg-av{background:var(--s3);color:var(--muted);}
.msg-bub{padding:9px 13px;border-radius:12px;font-size:13px;line-height:1.6;}
.msg.msg-ai .msg-bub{background:var(--s2);border:1px solid var(--border);border-radius:4px 12px 12px 12px;}
.msg.msg-user .msg-bub{background:var(--acc);color:#fff;border-radius:12px 4px 12px 12px;}
.chat-input-bar{display:flex;gap:8px;padding:10px;background:var(--s2);border:1px solid var(--border);border-top:none;border-radius:0 0 var(--r) var(--r);}
.chat-input-bar input{flex:1;background:var(--s3);border:1px solid var(--border);border-radius:var(--rs);padding:9px 13px;color:var(--text);font-size:13px;}
.chat-input-bar input:focus{border-color:var(--acc);}
.typing-dots{display:flex;gap:4px;align-items:center;}
.tdot{width:6px;height:6px;border-radius:50%;background:var(--muted);animation:td 1.2s infinite;}
.tdot:nth-child(2){animation-delay:.2s;}.tdot:nth-child(3){animation-delay:.4s;}
@keyframes td{0%,60%,100%{transform:translateY(0);}30%{transform:translateY(-6px);}}

/* ── UPLOAD ── */
.upload-zone{border:2px dashed var(--border2);border-radius:var(--r);padding:2.5rem;text-align:center;cursor:pointer;transition:all .2s;}
.upload-zone:hover,.upload-zone.drag{border-color:var(--acc);background:var(--acc-glow);}
.yt-form{display:flex;gap:8px;margin-top:1rem;}
.gen-item{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.8rem 1rem;display:flex;gap:10px;align-items:flex-start;}
.gen-q{font-size:13px;font-weight:500;flex:1;}
.gen-a{font-size:12px;color:var(--muted);flex:1;}

/* ── STUDY MODES ── */
.mode-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;}
.mode-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem;cursor:pointer;transition:all .2s;text-align:center;}
.mode-card:hover{border-color:var(--border2);transform:translateY(-2px);}
.mode-icon{font-size:30px;margin-bottom:10px;}
.mode-name{font-family:var(--fh);font-size:14px;font-weight:700;margin-bottom:4px;}
.mode-desc{font-size:12px;color:var(--muted);line-height:1.5;}

/* Pomodoro timer */
.pomo-ring{position:relative;width:180px;height:180px;margin:0 auto 1.5rem;}
.pomo-svg{transform:rotate(-90deg);}
.pomo-track{fill:none;stroke:var(--s3);stroke-width:10;}
.pomo-prog{fill:none;stroke:var(--acc);stroke-width:10;stroke-linecap:round;transition:stroke-dashoffset .9s ease;}
.pomo-time{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-size:32px;font-weight:800;}
.pomo-phase{text-align:center;font-size:12px;color:var(--muted);margin-bottom:1rem;font-family:var(--fh);letter-spacing:.06em;text-transform:uppercase;}
.pomo-btns{display:flex;justify-content:center;gap:8px;}

/* ── MAPS ── */
.map-canvas{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);position:relative;height:360px;overflow:hidden;}
.mnode{position:absolute;border-radius:var(--rs);padding:7px 13px;font-size:12px;font-weight:700;font-family:var(--fh);cursor:pointer;transition:all .2s;z-index:2;white-space:nowrap;}
.mnode:hover{transform:scale(1.06);}
.mnode.center{background:var(--acc);color:#fff;font-size:13px;padding:9px 16px;}
.mnode.leaf{background:var(--s2);border:1px solid var(--border2);color:var(--text);}
.mnode.leaf:hover{border-color:var(--acc);color:var(--acc);}
.map-svg-layer{position:absolute;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:1;}

/* ── PROGRESS ── */
.prog-subj{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.1rem 1.3rem;}
.prog-header{display:flex;align-items:center;gap:8px;margin-bottom:10px;}
.week-bars{display:flex;align-items:flex-end;gap:5px;height:70px;}
.wbar-wrap{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;height:100%;justify-content:flex-end;}
.wbar{width:100%;border-radius:3px 3px 0 0;min-height:3px;}
.wlbl{font-size:9px;color:var(--muted);font-family:var(--fh);}
.streak-days{display:flex;gap:5px;}
.sday{width:32px;height:32px;border-radius:7px;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;font-family:var(--fh);}
.sday.done{background:var(--green);color:#fff;}
.sday.today{background:var(--acc);color:#fff;}
.sday.miss{background:var(--s3);color:var(--muted);}

/* ── LEVELS / BADGES ── */
.lvl-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:10px;}
.lvl-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:.9rem;text-align:center;}
.lvl-card.unlocked{border-color:var(--acc);}
.lvl-card.current{border-color:var(--green);background:rgba(34,217,138,.04);}
.lvl-card.locked{opacity:.4;}
.lvl-n{font-family:var(--fh);font-size:28px;font-weight:800;}
.lvl-name{font-size:10px;font-family:var(--fh);font-weight:700;color:var(--muted);margin-top:2px;}
.lvl-req{font-size:9px;color:var(--muted);margin-top:3px;}
.badge-wrap{display:flex;flex-wrap:wrap;gap:8px;}
.bdg{background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);padding:8px 12px;display:flex;align-items:center;gap:8px;}
.bdg.locked{opacity:.35;}
.bdg-icon{font-size:20px;}
.bdg-name{font-size:12px;font-weight:700;font-family:var(--fh);}
.bdg-desc{font-size:10px;color:var(--muted);}

/* ── ADMIN ── */
.admin-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem;}
.admin-stat{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem;text-align:center;}
.admin-n{font-family:var(--fh);font-size:22px;font-weight:800;}
.admin-l{font-size:11px;color:var(--muted);}
.users-table{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;}
.ut-head{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr auto;gap:8px;padding:.7rem 1rem;background:var(--s2);font-size:11px;font-weight:700;color:var(--muted);font-family:var(--fh);letter-spacing:.04em;}
.ut-row{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr auto;gap:8px;padding:.7rem 1rem;border-top:1px solid var(--border);align-items:center;font-size:13px;transition:background .15s;}
.ut-row:hover{background:var(--s2);}
.ut-name{display:flex;align-items:center;gap:8px;}
.ut-av{width:28px;height:28px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;font-family:var(--fh);}
.ut-status{font-size:11px;padding:2px 7px;border-radius:999px;font-family:var(--fh);font-weight:700;}
.ut-status.active{background:rgba(34,217,138,.15);color:var(--green);}
.ut-status.inactive{background:var(--s3);color:var(--muted);}
.admin-pass{font-size:12px;color:var(--muted);margin-top:6px;}
.admin-locked{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:400px;gap:1rem;text-align:center;}

/* SPINNER */
.spin{display:inline-block;width:14px;height:14px;border:2px solid rgba(255,255,255,.2);border-top-color:#fff;border-radius:50%;animation:sp .7s linear infinite;}
@keyframes sp{to{transform:rotate(360deg);}}

/* RESPONSIVE */
@media(max-width:700px){
  .sidebar{display:none;}
  .main{padding:1rem 1rem 4rem;}
  .opts{grid-template-columns:1fr;}
  .stat-grid{grid-template-columns:repeat(2,1fr);}
  .admin-stats{grid-template-columns:repeat(2,1fr);}
  .battle-arena{grid-template-columns:1fr;}
  .ut-head,.ut-row{grid-template-columns:2fr 1fr 1fr auto;}
  .ut-row .ut-lv,.ut-row .ut-subj,.ut-head .ut-lhd:nth-child(3),.ut-head .ut-lhd:nth-child(4){display:none;}
  .mobile-nav{display:flex;}
}
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:var(--s1);border-top:1px solid var(--border);z-index:200;padding:.4rem;}
.mob-btn{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;padding:.4rem;font-size:9px;color:var(--muted);background:none;border:none;font-family:var(--fh);font-weight:700;transition:color .15s;}
.mob-btn.active{color:var(--acc2);}
.mob-icon{font-size:18px;}
</style>
</head>
<body>

<!-- AUTH SCREEN -->
<div id="screen-auth">
  <div class="auth-box">
    <div class="auth-logo">Tout<span>ify</span></div>
    <p class="auth-sub">Study anything. Beat everyone.</p>
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchAuthTab('login',this)">Sign in</button>
      <button class="auth-tab" onclick="switchAuthTab('register',this)">Create account</button>
    </div>
    <div class="auth-form" id="login-form">
      <input class="inp" id="li-user" placeholder="Username"/>
      <input class="inp" id="li-pass" placeholder="Password" type="password"/>
      <button class="btn btn-acc" style="justify-content:center;" onclick="doLogin()">Sign in →</button>
      <!-- Admin login: admin / toutify2024 (hidden) -->
    </div>
    <div class="auth-form" id="register-form" style="display:none;">
      <input class="inp" id="reg-user" placeholder="Choose a username"/>
      <input class="inp" id="reg-email" placeholder="Email address"/>
      <input class="inp" id="reg-pass" placeholder="Password" type="password"/>
      <button class="btn btn-acc" style="justify-content:center;" onclick="doRegister()">Create account →</button>
    </div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app" style="display:none;" class="root">
  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="sb-logo">
      <h1>Tout<span>ify</span></h1>
      <div class="sb-user" id="sb-username">Loading...</div>
    </div>
    <div class="sb-xp">
      <div class="sb-lvl-row">
        <span id="sb-lvl-label" class="sb-lvl">Lv 1</span>
        <span style="font-size:11px;color:var(--muted);" id="sb-lvl-name">Novice</span>
      </div>
      <div class="sb-xp-track"><div class="sb-xp-fill" id="sb-xp-fill" style="width:0%"></div></div>
      <div class="sb-xp-txt" id="sb-xp-txt">0 / 300 XP</div>
    </div>
    <nav class="sb-nav">
      <div class="sb-section">STUDY</div>
      <div class="nav-item active" onclick="nav('home')"><span class="ni">🏠</span>Home</div>
      <div class="nav-item" onclick="nav('flashcards')"><span class="ni">🃏</span>Flashcards</div>
      <div class="nav-item" onclick="nav('quiz')"><span class="ni">📝</span>Quiz</div>
      <div class="nav-item" onclick="nav('tutor')"><span class="ni">🤖</span>AI Tutor</div>
      <div class="nav-item" onclick="nav('maps')"><span class="ni">🗺️</span>Concept Maps</div>
      <div class="nav-item" onclick="nav('study')"><span class="ni">⏱️</span>Study Modes</div>
      <div class="nav-item" onclick="nav('upload')"><span class="ni">📤</span>Upload Notes</div>
      <div class="sb-section">SOCIAL</div>
      <div class="nav-item" onclick="nav('leaderboard')"><span class="ni">🏆</span>Leaderboard</div>
      <div class="nav-item" onclick="nav('battle')"><span class="ni">⚔️</span>Battle</div>
      <div class="sb-section">STATS</div>
      <div class="nav-item" onclick="nav('progress')"><span class="ni">📊</span>Progress</div>
      <div class="nav-item" onclick="nav('levels')"><span class="ni">⭐</span>Levels</div>
      <div class="nav-item" id="admin-nav-item" style="display:none;" onclick="nav('admin')"><span class="ni">🔧</span>Admin Panel</div>
    </nav>
    <div class="sb-bottom">
      <div class="sb-streak"><span class="sb-streak-fire">🔥</span><span id="sb-streak-txt">0 day streak</span></div>
      <button class="btn btn-sm btn-danger" style="width:100%;justify-content:center;margin-top:8px;" onclick="doLogout()">Sign out</button>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div class="main">

    <!-- HOME -->
    <div class="screen active" id="scr-home">
      <p class="page-title" id="home-greeting">Welcome back!</p>
      <p class="page-sub">What are you studying today?</p>
      <div class="stat-grid">
        <div class="stat-box"><div class="stat-n" style="color:var(--acc)" id="h-streak">0</div><div class="stat-l">day streak 🔥</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--green)" id="h-cards">0</div><div class="stat-l">cards studied</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--amber)" id="h-quizzes">0</div><div class="stat-l">quizzes done</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--teal)" id="h-acc">—</div><div class="stat-l">avg accuracy</div></div>
      </div>
      <p class="sec-head">Your subjects</p>
      <div class="subjects-grid" id="subj-grid">
        <button class="add-subj" onclick="openModal('add-subj-modal')">
          <span style="font-size:22px;">+</span>
          <span style="font-size:12px;font-family:var(--fh);font-weight:700;">Add subject</span>
        </button>
      </div>
      <p class="sec-head">Quick start</p>
      <div class="row">
        <button class="btn btn-acc btn-sm" onclick="nav('flashcards')">Study flashcards</button>
        <button class="btn btn-sm" onclick="nav('quiz')">Take a quiz</button>
        <button class="btn btn-sm" onclick="nav('battle')">Challenge someone ⚔️</button>
        <button class="btn btn-sm" onclick="nav('study')">Study modes ⏱️</button>
      </div>
    </div>

    <!-- FLASHCARDS -->
    <div class="screen" id="scr-flashcards">
      <p class="page-title">Flashcards</p>
      <p class="page-sub">Tap to flip. Rate yourself to track progress.</p>
      <div class="row" id="fc-subj-pick" style="margin-bottom:1rem;"></div>
      <div class="fc-wrap">
        <div class="row" style="width:100%;max-width:540px;justify-content:space-between;">
          <span style="font-size:13px;color:var(--muted);" id="fc-counter">Card 1 / 6</span>
          <div class="fc-dots" id="fc-dots"></div>
        </div>
        <div class="flashcard" onclick="flipCard()">
          <div class="fc-inner" id="fc-inner">
            <div class="fc-face fc-front">
              <div class="fc-lbl">QUESTION</div>
              <div class="fc-q" id="fc-q">Loading...</div>
              <div class="fc-sub">Tap to reveal answer</div>
            </div>
            <div class="fc-face fc-back">
              <div class="fc-lbl">ANSWER</div>
              <div class="fc-q" id="fc-a"></div>
            </div>
          </div>
        </div>
        <div class="rate-btns" id="rate-btns" style="display:none;">
          <button class="btn btn-sm" style="border-color:var(--red);color:var(--red);" onclick="rateCard(0)">Again</button>
          <button class="btn btn-sm" style="border-color:var(--amber);color:var(--amber);" onclick="rateCard(1)">Hard</button>
          <button class="btn btn-sm" style="border-color:var(--green);color:var(--green);" onclick="rateCard(2)">Good</button>
          <button class="btn btn-sm" style="border-color:var(--teal);color:var(--teal);" onclick="rateCard(3)">Easy</button>
        </div>
        <div class="row">
          <button class="btn btn-sm" onclick="prevCard()">← Prev</button>
          <button class="btn btn-sm btn-acc" onclick="nextCard()">Next →</button>
        </div>
      </div>
    </div>

    <!-- QUIZ -->
    <div class="screen" id="scr-quiz">
      <p class="page-title">Quiz</p>
      <p class="page-sub">Timed multiple choice questions.</p>
      <div id="quiz-setup">
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head" style="margin-bottom:.6rem;">Subject</p>
          <div class="row" id="qz-subj-pick"></div>
        </div>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head" style="margin-bottom:.6rem;">Questions</p>
          <div class="row">
            <button class="btn btn-sm qz-n-btn btn-acc" data-n="5" onclick="setQN(5,this)">5</button>
            <button class="btn btn-sm qz-n-btn" data-n="10" onclick="setQN(10,this)">10</button>
            <button class="btn btn-sm qz-n-btn" data-n="20" onclick="setQN(20,this)">20</button>
          </div>
        </div>
        <button class="btn btn-acc" onclick="startQuiz()">Start quiz →</button>
      </div>
      <div id="quiz-game" style="display:none;">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;">
          <span style="font-size:12px;color:var(--muted);" id="q-ctr">Q 1/5</span>
          <span style="font-family:var(--fh);font-size:13px;font-weight:700;color:var(--acc);" id="q-score-live">0 pts</span>
        </div>
        <div class="timer-bar" id="timer-bar"></div>
        <div class="q-card" id="q-text"></div>
        <div class="opts" id="q-opts"></div>
        <div id="q-exp" style="display:none;font-size:13px;color:var(--muted);padding:10px 14px;background:var(--s1);border-radius:var(--rs);border:1px solid var(--border);line-height:1.6;margin-top:8px;"></div>
        <button class="btn btn-sm btn-acc" id="q-next" style="display:none;margin-top:10px;" onclick="nextQ()">Next →</button>
      </div>
      <div id="quiz-result" style="display:none;text-align:center;padding:2rem;">
        <div class="res-score" id="res-score"></div>
        <p style="font-size:15px;color:var(--muted);margin:8px 0 4px;" id="res-lbl"></p>
        <p style="font-size:12px;color:var(--acc2);margin-bottom:1.5rem;" id="res-xp"></p>
        <div class="row" style="justify-content:center;">
          <button class="btn btn-acc" onclick="resetQuiz()">Try again</button>
          <button class="btn" onclick="nav('leaderboard')">See leaderboard</button>
        </div>
      </div>
    </div>

    <!-- LEADERBOARD -->
    <div class="screen" id="scr-leaderboard">
      <p class="page-title">Leaderboard</p>
      <p class="page-sub">Global rankings — updated in real time.</p>
      <div class="row" style="margin-bottom:1rem;">
        <button class="btn btn-sm btn-acc" onclick="renderLB('global')">Global</button>
        <button class="btn btn-sm" onclick="renderLB('weekly')">This week</button>
        <button class="btn btn-sm" onclick="renderLB('friends')">Friends</button>
      </div>
      <div class="card" style="padding:0;overflow:hidden;" id="lb-table"></div>
    </div>

    <!-- BATTLE -->
    <div class="screen" id="scr-battle">
      <p class="page-title">Battle ⚔️</p>
      <p class="page-sub">Search for a player and challenge them to a quiz duel.</p>
      <div id="battle-lobby">
        <div class="battle-search">
          <input class="inp" id="battle-search-inp" placeholder="Search username..." oninput="searchPlayers()"/>
        </div>
        <div id="battle-results"></div>
        <div class="card" style="margin-top:1rem;">
          <p class="sec-head">Online now</p>
          <div id="online-players"></div>
        </div>
      </div>
      <div id="battle-game" style="display:none;">
        <div class="battle-arena" id="battle-arena"></div>
        <div style="margin-top:1rem;" id="battle-q-area"></div>
      </div>
      <div id="battle-result" style="display:none;text-align:center;padding:2rem;">
        <div id="battle-res-content"></div>
        <button class="btn btn-acc" style="margin-top:1rem;" onclick="resetBattle()">Play again</button>
      </div>
    </div>

    <!-- AI TUTOR -->
    <div class="screen" id="scr-tutor">
      <p class="page-title">AI Tutor</p>
      <p class="page-sub">Ask anything. Get clear, exam-ready explanations.</p>
      <div class="row" id="tutor-subj-pick" style="margin-bottom:.8rem;"></div>
      <div class="chat-box" id="chat-box">
        <div class="msg msg-ai">
          <div class="msg-av">T</div>
          <div class="msg-bub">Hey! I'm your Toutify AI tutor. Pick a subject and ask me anything — concepts, problem-solving, definitions, or exam tips. Let's get studying! 📚</div>
        </div>
      </div>
      <div class="chat-input-bar">
        <input type="text" id="chat-inp" placeholder="Ask a question..." onkeydown="if(event.key==='Enter')sendChat()"/>
        <button class="btn btn-acc btn-sm" id="chat-send" onclick="sendChat()">Send</button>
      </div>
      <div class="row" style="margin-top:.8rem;flex-wrap:wrap;" id="quick-qs"></div>
    </div>

    <!-- CONCEPT MAPS -->
    <div class="screen" id="scr-maps">
      <p class="page-title">Concept Maps</p>
      <p class="page-sub">Visual overviews. Click any node to ask the AI tutor about it.</p>
      <div class="row" id="map-subj-pick" style="margin-bottom:.8rem;"></div>
      <div class="row" id="map-topic-pick" style="margin-bottom:.8rem;"></div>
      <div class="map-canvas" id="map-canvas"></div>
    </div>

    <!-- STUDY MODES -->
    <div class="screen" id="scr-study">
      <p class="page-title">Study Modes</p>
      <p class="page-sub">Find the method that works best for you.</p>
      <div id="study-home">
        <div class="mode-grid">
          <div class="mode-card" onclick="openMode('pomodoro')">
            <div class="mode-icon">🍅</div>
            <div class="mode-name">Pomodoro</div>
            <div class="mode-desc">25 min focus + 5 min breaks. Classic productivity technique.</div>
          </div>
          <div class="mode-card" onclick="openMode('blurting')">
            <div class="mode-icon">✍️</div>
            <div class="mode-name">Blurting</div>
            <div class="mode-desc">Write down everything you know. Check what you missed.</div>
          </div>
          <div class="mode-card" onclick="openMode('feynman')">
            <div class="mode-icon">🧑‍🏫</div>
            <div class="mode-name">Feynman Method</div>
            <div class="mode-desc">Explain a concept simply. The AI checks your understanding.</div>
          </div>
          <div class="mode-card" onclick="openMode('spaced')">
            <div class="mode-icon">📅</div>
            <div class="mode-name">Spaced Repetition</div>
            <div class="mode-desc">Cards due today based on your last rating. Optimal retention.</div>
          </div>
          <div class="mode-card" onclick="openMode('sprint')">
            <div class="mode-icon">⚡</div>
            <div class="mode-name">Speed Sprint</div>
            <div class="mode-desc">Answer as many questions as possible in 60 seconds.</div>
          </div>
          <div class="mode-card" onclick="openMode('deepwork')">
            <div class="mode-icon">🧘</div>
            <div class="mode-name">Deep Work</div>
            <div class="mode-desc">No distractions. Timed session with ambient focus music.</div>
          </div>
        </div>
      </div>

      <!-- POMODORO -->
      <div id="mode-pomodoro" style="display:none;text-align:center;max-width:380px;margin:0 auto;">
        <button class="btn btn-sm" style="margin-bottom:1.5rem;" onclick="closeMode()">← Back</button>
        <div class="pomo-ring">
          <svg class="pomo-svg" width="180" height="180" viewBox="0 0 180 180">
            <circle class="pomo-track" cx="90" cy="90" r="80"/>
            <circle class="pomo-prog" id="pomo-circle" cx="90" cy="90" r="80" stroke-dasharray="502" stroke-dashoffset="0"/>
          </svg>
          <div class="pomo-time" id="pomo-time">25:00</div>
        </div>
        <div class="pomo-phase" id="pomo-phase">FOCUS</div>
        <div style="font-size:12px;color:var(--muted);margin-bottom:1rem;" id="pomo-session">Session 1 of 4</div>
        <div class="pomo-btns">
          <button class="btn btn-acc" id="pomo-start-btn" onclick="togglePomo()">Start</button>
          <button class="btn btn-sm" onclick="resetPomo()">Reset</button>
        </div>
        <div style="margin-top:1.5rem;text-align:left;" class="card">
          <p class="sec-head">Session log</p>
          <div id="pomo-log" style="font-size:12px;color:var(--muted);min-height:40px;"></div>
        </div>
      </div>

      <!-- BLURTING -->
      <div id="mode-blurting" style="display:none;max-width:600px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Choose a topic to blurt</p>
          <div class="row" id="blurt-subj" style="margin-bottom:.8rem;"></div>
          <textarea class="inp" id="blurt-input" placeholder="Write EVERYTHING you know about this topic from memory. Don't look at your notes! When done, click Check." rows="6"></textarea>
          <button class="btn btn-acc btn-sm" style="margin-top:8px;" onclick="checkBlurt()">Check my knowledge →</button>
        </div>
        <div id="blurt-result" style="display:none;" class="card">
          <p class="sec-head">AI Feedback</p>
          <div id="blurt-feedback" style="font-size:13px;line-height:1.7;color:var(--muted);"></div>
        </div>
      </div>

      <!-- FEYNMAN -->
      <div id="mode-feynman" style="display:none;max-width:600px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Explain it like I'm 10</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:.8rem;">Pick a concept and explain it in the simplest possible terms. The AI will identify gaps in your understanding.</p>
          <input class="inp" id="feynman-topic" placeholder="Topic (e.g. 'DNA replication')" style="margin-bottom:8px;"/>
          <textarea class="inp" id="feynman-input" placeholder="Explain the concept as simply as possible..." rows="5"></textarea>
          <button class="btn btn-acc btn-sm" style="margin-top:8px;" onclick="checkFeynman()">Analyze my explanation →</button>
        </div>
        <div id="feynman-result" style="display:none;" class="card">
          <p class="sec-head">Analysis</p>
          <div id="feynman-feedback" style="font-size:13px;line-height:1.7;color:var(--muted);"></div>
        </div>
      </div>

      <!-- SPEED SPRINT -->
      <div id="mode-sprint" style="display:none;max-width:580px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div id="sprint-setup">
          <p class="sec-head">Choose subject</p>
          <div class="row" id="sprint-subj" style="margin-bottom:1rem;"></div>
          <button class="btn btn-acc" onclick="startSprint()">Start 60s sprint ⚡</button>
        </div>
        <div id="sprint-game" style="display:none;">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
            <span style="font-family:var(--fh);font-size:22px;font-weight:800;color:var(--acc);" id="sprint-timer">60</span>
            <span style="font-family:var(--fh);font-size:15px;font-weight:700;" id="sprint-score">0 correct</span>
          </div>
          <div class="timer-bar" id="sprint-bar" style="margin-bottom:12px;"></div>
          <div class="q-card" id="sprint-q"></div>
          <div class="opts" id="sprint-opts"></div>
        </div>
        <div id="sprint-result" style="display:none;text-align:center;padding:1.5rem;">
          <div style="font-family:var(--fh);font-size:48px;font-weight:800;color:var(--acc);" id="sprint-final"></div>
          <p style="color:var(--muted);margin:6px 0 1rem;font-size:14px;">questions answered correctly in 60s</p>
          <button class="btn btn-acc" onclick="startSprint()">Play again</button>
        </div>
      </div>

      <!-- DEEP WORK -->
      <div id="mode-deepwork" style="display:none;max-width:460px;text-align:center;">
        <button class="btn btn-sm" style="margin-bottom:1.5rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Deep work session</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:1rem;">Set your session length and intention. No interruptions.</p>
          <label class="lbl">Session duration</label>
          <div class="row" style="margin-bottom:.8rem;">
            <button class="btn btn-sm dw-dur btn-acc" data-m="30" onclick="setDW(30,this)">30 min</button>
            <button class="btn btn-sm dw-dur" data-m="60" onclick="setDW(60,this)">60 min</button>
            <button class="btn btn-sm dw-dur" data-m="90" onclick="setDW(90,this)">90 min</button>
          </div>
          <label class="lbl">Session intention</label>
          <input class="inp" id="dw-intention" placeholder="e.g. Master the Krebs cycle" style="margin-bottom:8px;"/>
          <button class="btn btn-acc" style="width:100%;justify-content:center;" onclick="startDW()">Enter deep work 🧘</button>
        </div>
        <div id="dw-active" style="display:none;">
          <div style="font-family:var(--fh);font-size:42px;font-weight:800;margin-bottom:4px;" id="dw-timer">60:00</div>
          <p style="font-size:12px;color:var(--muted);margin-bottom:1rem;" id="dw-intention-display"></p>
          <div class="prog-bar" style="height:8px;margin-bottom:1rem;"><div class="prog-fill" id="dw-bar" style="width:100%;background:var(--teal);"></div></div>
          <button class="btn btn-danger btn-sm" onclick="endDW()">End session</button>
        </div>
      </div>

      <!-- SPACED REP info -->
      <div id="mode-spaced" style="display:none;max-width:560px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card">
          <p class="sec-head">Spaced repetition queue</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:1rem;">Cards due for review today based on your previous ratings. Rate each card honestly — the algorithm adapts.</p>
          <div id="spaced-cards"></div>
          <button class="btn btn-acc btn-sm" style="margin-top:.8rem;" onclick="nav('flashcards')">Go to Flashcards →</button>
        </div>
      </div>
    </div>

    <!-- UPLOAD -->
    <div class="screen" id="scr-upload">
      <p class="page-title">Upload Notes</p>
      <p class="page-sub">Add PDFs, YouTube videos, or paste text — AI generates study material.</p>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin-bottom:1.5rem;">
        <div class="card">
          <p class="sec-head">📄 Upload PDF</p>
          <div class="upload-zone" id="pdf-drop" onclick="document.getElementById('pdf-file').click()" ondragover="event.preventDefault();this.classList.add('drag')" ondragleave="this.classList.remove('drag')" ondrop="handleDrop(event)">
            <div style="font-size:32px;margin-bottom:8px;">📄</div>
            <p style="font-size:14px;font-weight:700;font-family:var(--fh);">Drop PDF here</p>
            <p style="font-size:12px;color:var(--muted);">or click to browse</p>
          </div>
          <input type="file" id="pdf-file" accept=".pdf" style="display:none;" onchange="handlePDF(event)"/>
          <div id="pdf-name" style="font-size:12px;color:var(--muted);margin-top:8px;"></div>
        </div>
        <div class="card">
          <p class="sec-head">▶️ YouTube Video</p>
          <p style="font-size:12px;color:var(--muted);margin-bottom:.8rem;">Paste a YouTube URL and we'll generate study material from the topic.</p>
          <input class="inp" id="yt-url" placeholder="https://youtube.com/watch?v=..."/>
          <button class="btn btn-acc btn-sm" style="margin-top:8px;width:100%;justify-content:center;" onclick="handleYT()">Generate from video</button>
        </div>
      </div>
      <div class="card" style="margin-bottom:1rem;">
        <p class="sec-head">📋 Paste text / lecture notes</p>
        <textarea class="inp" id="notes-txt" placeholder="Paste any study material, lecture notes, textbook excerpts..." rows="5"></textarea>
        <div class="row" style="margin-top:8px;">
          <div class="row" id="upload-subj-pick"></div>
          <button class="btn btn-acc btn-sm" onclick="generateNotes()" id="gen-btn">Generate study material</button>
        </div>
      </div>
      <div id="upload-results" style="display:none;">
        <p class="sec-head">Generated flashcards</p>
        <div class="col" id="gen-cards" style="margin-bottom:1rem;"></div>
        <div class="row">
          <button class="btn btn-acc btn-sm" onclick="addGenCards()">Add to deck</button>
          <button class="btn btn-sm" onclick="clearGen()">Clear</button>
        </div>
      </div>
    </div>

    <!-- PROGRESS -->
    <div class="screen" id="scr-progress">
      <p class="page-title">Progress</p>
      <p class="page-sub">Your learning journey at a glance.</p>
      <div class="grid2" id="prog-subjs" style="margin-bottom:1.5rem;"></div>
      <hr class="divider"/>
      <p class="sec-head">Weekly activity</p>
      <div class="card" style="margin-bottom:1.5rem;"><div class="week-bars" id="week-bars"></div></div>
      <p class="sec-head">Study streak</p>
      <div class="streak-days" id="streak-days"></div>
    </div>

    <!-- LEVELS -->
    <div class="screen" id="scr-levels">
      <p class="page-title">Levels & Badges</p>
      <p class="page-sub">Every XP point counts.</p>
      <div class="card" style="display:flex;align-items:center;gap:1.2rem;margin-bottom:1.5rem;">
        <div style="font-family:var(--fh);font-size:52px;font-weight:800;color:var(--acc);" id="cur-lvl-num">1</div>
        <div style="flex:1;">
          <p style="font-family:var(--fh);font-size:16px;font-weight:700;margin-bottom:4px;" id="cur-lvl-name">Novice</p>
          <p style="font-size:12px;color:var(--muted);margin-bottom:8px;" id="cur-lvl-xp">0 / 300 XP to Level 2</p>
          <div class="prog-bar"><div class="prog-fill" id="cur-lvl-fill" style="width:0%;background:linear-gradient(90deg,var(--acc),var(--teal));"></div></div>
        </div>
      </div>
      <div class="lvl-grid" id="lvl-grid" style="margin-bottom:1.5rem;"></div>
      <hr class="divider"/>
      <p class="sec-head">Badges</p>
      <div class="badge-wrap" id="badge-wrap"></div>
    </div>

    <!-- ADMIN -->
    <div class="screen" id="scr-admin">
      <div id="admin-locked-view" class="admin-locked">
        <div style="font-size:40px;">🔒</div>
        <p style="font-family:var(--fh);font-size:18px;font-weight:700;">Admin area</p>
        <p style="font-size:13px;color:var(--muted);">Enter the admin password to access</p>
        <input class="inp" id="admin-pw-inp" type="password" placeholder="Admin password" style="max-width:280px;"/>
        <button class="btn btn-acc" onclick="unlockAdmin()">Unlock</button>
        <!-- Admin password hidden -->
      </div>
      <div id="admin-panel" style="display:none;">
        <p class="page-title">Admin Panel 🔧</p>
        <p class="page-sub">Full visibility into all users and activity.</p>
        <div class="admin-stats" id="admin-stats-row"></div>
        <div class="row" style="margin-bottom:1rem;">
          <input class="inp" id="admin-search" placeholder="Search users..." oninput="filterAdminUsers()" style="max-width:260px;"/>
          <button class="btn btn-sm btn-acc" onclick="exportUsers()">Export CSV</button>
          <button class="btn btn-sm btn-danger" onclick="if(confirm('Reset ALL user data?'))resetAllUsers()">Reset all</button>
        </div>
        <div class="users-table" id="users-table"></div>
      </div>
    </div>

  </div><!-- /main -->
</div><!-- /app -->

<!-- MOBILE NAV -->
<nav class="mobile-nav" id="mob-nav">
  <button class="mob-btn active" onclick="nav('home')"><span class="mob-icon">🏠</span>Home</button>
  <button class="mob-btn" onclick="nav('flashcards')"><span class="mob-icon">🃏</span>Cards</button>
  <button class="mob-btn" onclick="nav('quiz')"><span class="mob-icon">📝</span>Quiz</button>
  <button class="mob-btn" onclick="nav('leaderboard')"><span class="mob-icon">🏆</span>Ranks</button>
  <button class="mob-btn" onclick="nav('battle')"><span class="mob-icon">⚔️</span>Battle</button>
</nav>

<!-- MODALS -->
<div class="modal-bg" id="add-subj-modal">
  <div class="modal">
    <p class="modal-title">Add a subject</p>
    <div style="margin-bottom:.8rem;"><label class="lbl">Name</label><input class="inp" id="ns-name" placeholder="e.g. Organic Chemistry"/></div>
    <div style="margin-bottom:.8rem;"><label class="lbl">Icon (emoji)</label><input class="inp" id="ns-icon" placeholder="🧪" style="width:80px;" maxlength="2"/></div>
    <div style="margin-bottom:1rem;">
      <label class="lbl">Color</label>
      <div class="row" id="ns-colors">
        <div style="width:22px;height:22px;border-radius:50%;background:#6c5fff;border:2px solid #fff;cursor:pointer;" data-c="#6c5fff" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#22d98a;border:2px solid transparent;cursor:pointer;" data-c="#22d98a" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#f0a500;border:2px solid transparent;cursor:pointer;" data-c="#f0a500" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#ff4d4d;border:2px solid transparent;cursor:pointer;" data-c="#ff4d4d" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#00d4cc;border:2px solid transparent;cursor:pointer;" data-c="#00d4cc" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#ff5fa0;border:2px solid transparent;cursor:pointer;" data-c="#ff5fa0" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#3b9eff;border:2px solid transparent;cursor:pointer;" data-c="#3b9eff" onclick="pickNSColor(this)"></div>
      </div>
    </div>
    <div class="row">
      <button class="btn btn-acc btn-sm" onclick="addSubject()">Add subject</button>
      <button class="btn btn-sm" onclick="closeModal('add-subj-modal')">Cancel</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const API = "https://api.anthropic.com/v1/messages";
const ADMIN_PASS = "toutify2024";
const LVL_NAMES = ["Novice","Apprentice","Scholar","Adept","Expert","Master","Professor","Genius","Sage","Legend"];
const LVL_XP = [300,600,1000,1500,2200,3000,4000,5200,6600,8200];

// ════════════════════════════════
//  DATA STORE
// ════════════════════════════════
function loadDB() { try { return JSON.parse(localStorage.getItem('toutify_db') || '{}'); } catch { return {}; } }
function saveDB(db) { localStorage.setItem('toutify_db', JSON.stringify(db)); }
function getUser(un) { const db = loadDB(); return db[un] || null; }
function saveUser(u) { const db = loadDB(); db[u.username] = u; saveDB(db); }
function getAllUsers() { const db = loadDB(); return Object.values(db); }

function createUser(username, email, password) {
  return {
    username, email, password,
    created: Date.now(),
    lastSeen: Date.now(),
    xp: 0, level: 1, streak: 0,
    cardsStudied: 0, quizzesDone: 0,
    quizHistory: [], // [{score,total,subject,ts}]
    subjects: [],
    extraCards: [],
    badges: [],
    weeklyXP: [0,0,0,0,0,0,0],
    streakDays: [false,false,false,false,false,false,true],
    totalAccuracy: 0, accuracyCount: 0,
  };
}

// ════════════════════════════════
//  AUTH
// ════════════════════════════════
let CU = null; // current user

function switchAuthTab(tab, el) {
  document.querySelectorAll('.auth-tab').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('login-form').style.display = tab === 'login' ? 'flex' : 'none';
  document.getElementById('register-form').style.display = tab === 'register' ? 'flex' : 'none';
}

function doLogin() {
  const un = document.getElementById('li-user').value.trim();
  const pw = document.getElementById('li-pass').value;
  if (!un || !pw) { toast('Please fill in all fields'); return; }
  if (un === 'admin' && pw === ADMIN_PASS) {
    CU = createUser('admin','admin@toutify.com','admin');
    CU.isAdmin = true; CU.xp = 9999; CU.level = 10;
    bootApp(); return;
  }
  const u = getUser(un);
  if (!u) { toast('User not found'); return; }
  if (u.password !== pw) { toast('Wrong password'); return; }
  CU = u;
  CU.lastSeen = Date.now();
  saveUser(CU);
  bootApp();
}

function doRegister() {
  const un = document.getElementById('reg-user').value.trim();
  const em = document.getElementById('reg-email').value.trim();
  const pw = document.getElementById('reg-pass').value;
  if (!un || !em || !pw) { toast('Fill in all fields'); return; }
  if (un.length < 3) { toast('Username must be 3+ chars'); return; }
  if (getUser(un)) { toast('Username taken!'); return; }
  CU = createUser(un, em, pw);
  saveUser(CU);
  bootApp();
}

function doLogout() {
  if (CU && !CU.isAdmin) saveUser(CU);
  CU = null;
  document.getElementById('app').style.display = 'none';
  document.getElementById('screen-auth').style.display = 'flex';
  document.getElementById('mob-nav').style.display = 'none';
}

function bootApp() {
  document.getElementById('screen-auth').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  document.getElementById('mob-nav').style.display = 'flex';
  if (CU.isAdmin) document.getElementById('admin-nav-item').style.display = 'flex';
  updateSidebar();
  renderHome();
  renderSubjPickers();
  renderProgress();
  renderWeeklyBars();
  renderStreak();
  renderLevels();
  renderBadges();
  loadFC();
  renderQZSubj();
  renderLB('global');
  renderOnlinePlayers();
  renderSprintSubj();
  renderBlurtSubj();
  renderMapSubj();
  renderMapTopics();
  drawMap();
  toast(`Welcome back, ${CU.username}! 👋`);
}

// ════════════════════════════════
//  NAVIGATION
// ════════════════════════════════
let currentScreen = 'home';
function nav(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById('scr-'+id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.querySelectorAll('.mob-btn').forEach(b => b.classList.remove('active'));
  const navMap = {home:0,flashcards:1,quiz:2,tutor:3,maps:4,study:5,upload:6,leaderboard:8,battle:9,progress:11,levels:12,admin:13};
  const ni = document.querySelectorAll('.nav-item');
  if (navMap[id] !== undefined) ni[navMap[id]]?.classList.add('active');
  currentScreen = id;
  if (id === 'maps') { setTimeout(()=>{ renderMapTopics(); drawMap(); }, 60); }
  if (id === 'leaderboard') renderLB('global');
  if (id === 'admin') { renderAdminPanel(); }
}

// ════════════════════════════════
//  SIDEBAR / XP
// ════════════════════════════════
function updateSidebar() {
  document.getElementById('sb-username').textContent = CU.username;
  const lvlXP = LVL_XP[CU.level - 1] || 300;
  const pct = Math.round((CU.xp / lvlXP) * 100);
  document.getElementById('sb-xp-fill').style.width = pct + '%';
  document.getElementById('sb-xp-txt').textContent = `${CU.xp} / ${lvlXP} XP`;
  document.getElementById('sb-lvl-label').textContent = 'Lv ' + CU.level;
  document.getElementById('sb-lvl-name').textContent = LVL_NAMES[CU.level - 1] || 'Legend';
  document.getElementById('sb-streak-txt').textContent = CU.streak + ' day streak';
}

function gainXP(amount) {
  CU.xp += amount;
  const needed = LVL_XP[CU.level - 1] || 300;
  if (CU.xp >= needed) {
    CU.xp -= needed;
    CU.level = Math.min(CU.level + 1, 10);
    toast(`🎉 Level up! You're now Level ${CU.level} — ${LVL_NAMES[CU.level-1]}!`);
    renderLevels();
  }
  CU.weeklyXP[6] = (CU.weeklyXP[6] || 0) + amount;
  if (!CU.isAdmin) saveUser(CU);
  updateSidebar();
  updateLevelScreen();
}

function updateLevelScreen() {
  const lvlXP = LVL_XP[CU.level - 1] || 300;
  const pct = Math.round((CU.xp / lvlXP) * 100);
  const el1 = document.getElementById('cur-lvl-num');
  const el2 = document.getElementById('cur-lvl-name');
  const el3 = document.getElementById('cur-lvl-xp');
  const el4 = document.getElementById('cur-lvl-fill');
  if (el1) el1.textContent = CU.level;
  if (el2) el2.textContent = LVL_NAMES[CU.level - 1];
  if (el3) el3.textContent = `${CU.xp} / ${lvlXP} XP to Level ${CU.level + 1}`;
  if (el4) el4.style.width = pct + '%';
}

// ════════════════════════════════
//  HOME
// ════════════════════════════════
function renderHome() {
  const hr = new Date().getHours();
  const greet = hr < 12 ? 'Good morning' : hr < 17 ? 'Good afternoon' : 'Good evening';
  document.getElementById('home-greeting').textContent = `${greet}, ${CU.username}! 👋`;
  document.getElementById('h-streak').textContent = CU.streak;
  document.getElementById('h-cards').textContent = CU.cardsStudied;
  document.getElementById('h-quizzes').textContent = CU.quizzesDone;
  const acc = CU.accuracyCount > 0 ? Math.round(CU.totalAccuracy / CU.accuracyCount) + '%' : '—';
  document.getElementById('h-acc').textContent = acc;
  renderSubjGrid();
}

function renderSubjGrid() {
  const grid = document.getElementById('subj-grid');
  const addBtn = grid.querySelector('.add-subj');
  grid.innerHTML = '';
  CU.subjects.forEach((s, i) => {
    const card = document.createElement('div');
    card.className = 'subj-card';
    card.innerHTML = `<style>.subj-card:nth-child(${i+1})::after{background:${s.color};}</style>
      <div class="subj-icon">${s.icon}</div>
      <div class="subj-name">${s.name}</div>
      <div class="subj-meta" style="color:${s.color}">${s.progress || 0}% mastery</div>
      <div class="prog-bar"><div class="prog-fill" style="width:${s.progress||0}%;background:${s.color};"></div></div>`;
    card.onclick = () => { subjState.active = i; renderSubjPickers(); toast('Switched to ' + s.name); };
    grid.appendChild(card);
  });
  const ab = document.createElement('button');
  ab.className = 'add-subj';
  ab.innerHTML = '<span style="font-size:22px;">+</span><span style="font-size:12px;font-family:var(--fh);font-weight:700;">Add subject</span>';
  ab.onclick = () => openModal('add-subj-modal');
  grid.appendChild(ab);
}

// ════════════════════════════════
//  SUBJECT MANAGEMENT
// ════════════════════════════════
let subjState = { active: 0, nsColor: '#6c5fff' };
let fcDB = {}, qzDB = {};

const DEFAULT_FC = {
  "Biochemistry": [
    {q:"What is ATP's role in the cell?",a:"ATP is the main energy currency — it stores and transfers chemical energy for metabolic reactions."},
    {q:"Name the 4 levels of protein structure.",a:"Primary (sequence), Secondary (α-helices, β-sheets), Tertiary (3D fold), Quaternary (multi-subunit)."},
    {q:"What enzyme starts glycolysis?",a:"Hexokinase phosphorylates glucose to glucose-6-phosphate."},
    {q:"What is the Michaelis-Menten equation?",a:"v = Vmax[S] / (Km + [S]). Km is the substrate concentration at half-maximal velocity."},
    {q:"What is the central dogma?",a:"DNA → RNA → Protein. Information flows from replication through transcription to translation."},
    {q:"What does NAD+ do in respiration?",a:"Accepts electrons to become NADH, which donates electrons to the electron transport chain."},
  ],
  "Physics": [
    {q:"State Newton's Second Law.",a:"F = ma — net force equals mass times acceleration."},
    {q:"Formula for kinetic energy?",a:"KE = ½mv², where m = mass and v = velocity."},
    {q:"State Ohm's Law.",a:"V = IR — voltage equals current times resistance."},
    {q:"What is the speed of light?",a:"≈ 3 × 10⁸ m/s in a vacuum."},
    {q:"What is the photoelectric effect?",a:"Light hitting metal ejects electrons; energy of electrons depends on frequency, not intensity."},
    {q:"State conservation of energy.",a:"Energy cannot be created or destroyed, only converted from one form to another."},
  ],
  "History": [
    {q:"When did WWI begin and end?",a:"July 28 1914 — November 11 1918."},
    {q:"What triggered the French Revolution?",a:"Economic crisis, food shortages, inequality between Estates, and Enlightenment ideas."},
    {q:"Who was China's first Emperor?",a:"Qin Shi Huang, who unified China in 221 BCE."},
    {q:"What was the Cold War?",a:"Geopolitical tension between the US and USSR from 1947–1991, without direct military conflict."},
  ],
  "Mathematics": [
    {q:"State the Pythagorean theorem.",a:"a² + b² = c², where c is the hypotenuse of a right triangle."},
    {q:"What is a derivative?",a:"The instantaneous rate of change of a function — slope of the tangent line at a point."},
    {q:"What is Euler's identity?",a:"e^(iπ) + 1 = 0."},
    {q:"What is a logarithm?",a:"log_b(x) = y means b^y = x. It's the inverse of exponentiation."},
  ]
};

const DEFAULT_QZ = {
  "Biochemistry": [
    {q:"Which molecule is the 'energy currency' of cells?",opts:["ADP","GTP","ATP","NADH"],c:2,e:"ATP stores and transfers energy in all living cells."},
    {q:"The Krebs cycle occurs in:",opts:["Cytoplasm","Mitochondrial matrix","Nucleus","Ribosome"],c:1,e:"The Krebs cycle runs in the mitochondrial matrix."},
    {q:"Which amino acid contains sulfur?",opts:["Alanine","Glycine","Cysteine","Leucine"],c:2,e:"Cysteine has a thiol (-SH) group and forms disulfide bonds."},
    {q:"Product of glycolysis?",opts:["Acetyl-CoA","Pyruvate","Oxaloacetate","Citrate"],c:1,e:"Glycolysis converts glucose to 2 pyruvate molecules."},
    {q:"Which enzyme unwinds DNA?",opts:["Ligase","Primase","Helicase","Polymerase"],c:2,e:"Helicase breaks hydrogen bonds between base pairs."},
    {q:"Beta-oxidation breaks down:",opts:["Proteins","Carbohydrates","Fatty acids","Nucleotides"],c:2,e:"Beta-oxidation breaks fatty acids into acetyl-CoA."},
    {q:"Bond linking amino acids?",opts:["Hydrogen","Peptide","Ionic","Disulfide"],c:1,e:"Peptide bonds form between carboxyl and amino groups."},
    {q:"NADH donates electrons to which ETC complex?",opts:["I","II","III","IV"],c:0,e:"NADH donates electrons to Complex I."},
  ],
  "Physics": [
    {q:"SI unit of force?",opts:["Joule","Watt","Newton","Pascal"],c:2,e:"Newton (N) = kg·m/s²."},
    {q:"Which wave needs no medium?",opts:["Sound","Water","Seismic","Electromagnetic"],c:3,e:"EM waves travel through vacuum."},
    {q:"Unit of electrical resistance?",opts:["Volt","Ampere","Watt","Ohm"],c:3,e:"Resistance is measured in Ohms (Ω)."},
    {q:"Formula for power?",opts:["P=Fd","P=W/t","P=mv","P=ma"],c:1,e:"Power = Work / Time."},
    {q:"Sound travels fastest in:",opts:["Air","Water","Steel","Vacuum"],c:2,e:"Sound travels fastest in steel (~5000 m/s)."},
    {q:"Acceleration due to gravity on Earth?",opts:["8.9","9.8","10.8","11.2"],c:1,e:"Standard gravity is 9.8 m/s²."},
  ],
  "History": [
    {q:"Berlin Wall fell in?",opts:["1985","1987","1989","1991"],c:2,e:"November 9, 1989."},
    {q:"Who wrote The Communist Manifesto?",opts:["Lenin & Stalin","Marx & Engels","Rousseau & Voltaire","Weber & Durkheim"],c:1,e:"Karl Marx and Friedrich Engels, 1848."},
    {q:"WWII ended in?",opts:["1943","1944","1945","1946"],c:2,e:"May 8 (Europe) and September 2 (Pacific), 1945."},
    {q:"Renaissance started in?",opts:["France","England","Germany","Italy"],c:3,e:"Italy, 14th century, especially Florence."},
  ],
  "Mathematics": [
    {q:"Derivative of sin(x)?",opts:["cos(x)","-cos(x)","sin(x)","-sin(x)"],c:0,e:"d/dx[sin(x)] = cos(x)."},
    {q:"7! equals?",opts:["2520","5040","720","40320"],c:1,e:"7! = 5040."},
    {q:"Sum of angles in a triangle?",opts:["90°","180°","270°","360°"],c:1,e:"Always 180°."},
    {q:"log₁₀(1000)?",opts:["2","3","4","10"],c:1,e:"10³ = 1000."},
    {q:"Integral of 1/x?",opts:["1/x²","ln|x|","e^x","-1/x²"],c:1,e:"∫(1/x)dx = ln|x| + C."},
  ]
};

const CONCEPT_MAPS = {
  "Biochemistry": {
    topics: ["Metabolism","Proteins","Cell Signaling"],
    maps: {
      "Metabolism": {center:"Metabolism",nodes:[{l:"Glycolysis",x:60,y:50},{l:"Krebs Cycle",x:220,y:40},{l:"ETC",x:400,y:50},{l:"ATP Synthesis",x:300,y:170},{l:"Pyruvate",x:150,y:130},{l:"Acetyl-CoA",x:290,y:90},{l:"Gluconeogenesis",x:55,y:190},{l:"Fatty Acid Ox.",x:190,y:240}]},
      "Proteins": {center:"Proteins",nodes:[{l:"Primary",x:50,y:50},{l:"Secondary",x:210,y:40},{l:"Tertiary",x:370,y:50},{l:"Quaternary",x:470,y:150},{l:"Peptide bonds",x:50,y:180},{l:"α-Helix",x:180,y:170},{l:"β-Sheet",x:310,y:170},{l:"Disulfide bonds",x:420,y:250}]},
    }
  },
  "Physics": {
    topics: ["Mechanics","Waves","Electricity"],
    maps: {
      "Mechanics": {center:"Mechanics",nodes:[{l:"Newton's Laws",x:55,y:50},{l:"Kinematics",x:230,y:40},{l:"Momentum",x:400,y:55},{l:"Energy",x:470,y:170},{l:"Force",x:65,y:180},{l:"Gravity",x:195,y:200},{l:"Friction",x:330,y:195},{l:"Work",x:430,y:265}]},
    }
  },
  "History": {
    topics: ["Modern History","Ancient History"],
    maps: {
      "Modern History": {center:"Modern History",nodes:[{l:"WWI",x:60,y:55},{l:"WWII",x:230,y:40},{l:"Cold War",x:390,y:55},{l:"Colonialism",x:480,y:165},{l:"Revolutions",x:55,y:190},{l:"Nationalism",x:210,y:200},{l:"Industrialization",x:360,y:195},{l:"Decolonization",x:440,y:265}]},
    }
  },
  "Mathematics": {
    topics: ["Calculus","Algebra","Statistics"],
    maps: {
      "Calculus": {center:"Calculus",nodes:[{l:"Limits",x:60,y:55},{l:"Derivatives",x:230,y:40},{l:"Integrals",x:385,y:55},{l:"Series",x:470,y:170},{l:"Chain Rule",x:65,y:185},{l:"MVT",x:205,y:185},{l:"FTC",x:350,y:185},{l:"Riemann Sums",x:440,y:265}]},
    }
  }
};

let nsColor = '#6c5fff';
function pickNSColor(el) {
  document.querySelectorAll('#ns-colors > div').forEach(d => d.style.borderColor = 'transparent');
  el.style.borderColor = '#fff';
  nsColor = el.dataset.c;
}

function addSubject() {
  const name = document.getElementById('ns-name').value.trim();
  const icon = document.getElementById('ns-icon').value.trim() || '📖';
  if (!name) { toast('Enter a subject name'); return; }
  CU.subjects.push({ name, icon, color: nsColor, progress: 0, cards: 0, quizzes: 0 });
  if (!fcDB[name]) fcDB[name] = [];
  if (!qzDB[name]) qzDB[name] = [];
  saveUser(CU);
  closeModal('add-subj-modal');
  renderHome();
  renderSubjPickers();
  renderProgress();
  document.getElementById('ns-name').value = '';
  document.getElementById('ns-icon').value = '';
  toast(`${icon} ${name} added!`);
}

function getFC(subj) {
  const extras = (CU.extraCards||[]).filter(c=>c.subject===subj);
  return [...(DEFAULT_FC[subj]||[]), ...(fcDB[subj]||[]), ...extras];
}
function getQZ(subj) { return [...(DEFAULT_QZ[subj]||[]), ...(qzDB[subj]||[])]; }

function renderSubjPickers() {
  const pickers = [
    {id:'fc-subj-pick', stateProp:'fcSubj'},
    {id:'qz-subj-pick', stateProp:'qzSubj'},
    {id:'tutor-subj-pick', stateProp:'tutorSubj'},
    {id:'map-subj-pick', stateProp:'mapSubj'},
    {id:'upload-subj-pick', stateProp:'uploadSubj'},
  ];
  const allSubjs = [...Object.keys(DEFAULT_FC), ...CU.subjects.map(s=>s.name)];
  const uniq = [...new Set(allSubjs)];
  pickers.forEach(({id, stateProp}) => {
    const el = document.getElementById(id);
    if (!el) return;
    if (!subjState[stateProp]) subjState[stateProp] = 0;
    el.innerHTML = '';
    uniq.forEach((s, i) => {
      const btn = document.createElement('button');
      btn.className = 'btn btn-sm' + (i === subjState[stateProp] ? ' btn-acc' : '');
      btn.textContent = s;
      btn.onclick = () => {
        subjState[stateProp] = i;
        renderSubjPickers();
        if (stateProp === 'fcSubj') { fcState.idx = 0; fcState.flipped = false; loadFC(); }
        if (stateProp === 'mapSubj') { subjState.mapTopic = 0; renderMapTopics(); drawMap(); }
        if (stateProp === 'tutorSubj') renderQuickQs();
      };
      el.appendChild(btn);
    });
  });
  renderQuickQs();
}

function activeSubjName(prop) {
  const allSubjs = [...Object.keys(DEFAULT_FC), ...CU.subjects.map(s=>s.name)];
  const uniq = [...new Set(allSubjs)];
  return uniq[subjState[prop] || 0] || 'Biochemistry';
}

// ════════════════════════════════
//  FLASHCARDS
// ════════════════════════════════
let fcState = { idx: 0, flipped: false };

function loadFC() {
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub);
  if (!cards.length) {
    document.getElementById('fc-q').textContent = 'No cards yet! Upload notes to add cards.';
    document.getElementById('fc-a').textContent = '';
    document.getElementById('fc-counter').textContent = 'No cards';
    document.getElementById('fc-dots').innerHTML = '';
    return;
  }
  const i = fcState.idx % cards.length;
  const card = cards[i];
  document.getElementById('fc-q').textContent = card.q;
  document.getElementById('fc-a').textContent = card.a;
  document.getElementById('fc-counter').textContent = `Card ${i+1} / ${cards.length}`;
  fcState.flipped = false;
  document.getElementById('fc-inner').classList.remove('flipped');
  document.getElementById('rate-btns').style.display = 'none';
  // dots
  const dotsEl = document.getElementById('fc-dots');
  dotsEl.innerHTML = '';
  const total = Math.min(cards.length, 8);
  for (let d = 0; d < total; d++) {
    const dot = document.createElement('div');
    dot.className = 'fc-dot' + (d < i ? ' done' : d === i ? ' cur' : '');
    dotsEl.appendChild(dot);
  }
}

function flipCard() {
  if (!fcState.flipped) {
    fcState.flipped = true;
    document.getElementById('fc-inner').classList.add('flipped');
    document.getElementById('rate-btns').style.display = 'flex';
  }
}

function rateCard(r) {
  gainXP([5,10,15,20][r]);
  CU.cardsStudied++;
  saveUser(CU);
  renderHome();
  document.getElementById('h-cards').textContent = CU.cardsStudied;
  toast(['Reviewing again soon...','Hard — noted','Good job! +15XP','Easy! +20XP'][r]);
  nextCard();
}

function nextCard() {
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub);
  fcState.idx = (fcState.idx + 1) % (cards.length || 1);
  loadFC();
}
function prevCard() {
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub);
  fcState.idx = (fcState.idx - 1 + (cards.length||1)) % (cards.length||1);
  loadFC();
}

// ════════════════════════════════
//  QUIZ
// ════════════════════════════════
let qzState = { n: 5, questions: [], idx: 0, score: 0, answered: false, timerInt: null };

function renderQZSubj() { renderSubjPickers(); }

function setQN(n, el) {
  qzState.n = n;
  document.querySelectorAll('.qz-n-btn').forEach(b => { b.classList.remove('btn-acc'); });
  el.classList.add('btn-acc');
}

function startQuiz() {
  const sub = activeSubjName('qzSubj');
  const pool = getQZ(sub);
  if (!pool.length) { toast('No quiz questions for this subject!'); return; }
  const shuffled = [...pool].sort(() => Math.random() - .5);
  qzState.questions = shuffled.slice(0, Math.min(qzState.n, shuffled.length));
  qzState.idx = 0; qzState.score = 0; qzState.answered = false;
  document.getElementById('quiz-setup').style.display = 'none';
  document.getElementById('quiz-game').style.display = 'block';
  document.getElementById('quiz-result').style.display = 'none';
  loadQ();
}

let timerVal = 20;
function loadQ() {
  if (qzState.idx >= qzState.questions.length) { showQResult(); return; }
  const q = qzState.questions[qzState.idx];
  qzState.answered = false;
  document.getElementById('q-ctr').textContent = `Q ${qzState.idx+1}/${qzState.questions.length}`;
  document.getElementById('q-score-live').textContent = qzState.score + ' pts';
  document.getElementById('q-text').textContent = q.q;
  document.getElementById('q-exp').style.display = 'none';
  document.getElementById('q-next').style.display = 'none';
  const optsEl = document.getElementById('q-opts');
  optsEl.innerHTML = '';
  q.opts.forEach((o, i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => answerQ(i);
    optsEl.appendChild(btn);
  });
  clearInterval(qzState.timerInt);
  timerVal = 20;
  document.getElementById('timer-bar').style.width = '100%';
  document.getElementById('timer-bar').style.background = 'var(--acc)';
  qzState.timerInt = setInterval(() => {
    timerVal--;
    const pct = Math.round((timerVal/20)*100);
    document.getElementById('timer-bar').style.width = pct + '%';
    document.getElementById('timer-bar').style.background = timerVal > 10 ? 'var(--acc)' : timerVal > 5 ? 'var(--amber)' : 'var(--red)';
    if (timerVal <= 0) { clearInterval(qzState.timerInt); if (!qzState.answered) answerQ(-1); }
  }, 1000);
}

function answerQ(chosen) {
  if (qzState.answered) return;
  qzState.answered = true;
  clearInterval(qzState.timerInt);
  const q = qzState.questions[qzState.idx];
  document.querySelectorAll('.opt').forEach((b, i) => {
    b.disabled = true;
    if (i === q.c) b.classList.add('correct');
    else if (i === chosen && chosen !== q.c) b.classList.add('wrong');
  });
  const correct = chosen === q.c;
  if (correct) { qzState.score += 10; gainXP(20); }
  document.getElementById('q-exp').textContent = '💡 ' + q.e;
  document.getElementById('q-exp').style.display = 'block';
  document.getElementById('q-next').style.display = 'inline-flex';
}

function nextQ() { qzState.idx++; loadQ(); }

function showQResult() {
  document.getElementById('quiz-game').style.display = 'none';
  document.getElementById('quiz-result').style.display = 'block';
  const total = qzState.questions.length;
  const correct = qzState.score / 10;
  const pct = Math.round((correct / total) * 100);
  document.getElementById('res-score').textContent = pct + '%';
  document.getElementById('res-score').style.color = pct >= 80 ? 'var(--green)' : pct >= 60 ? 'var(--amber)' : 'var(--red)';
  document.getElementById('res-lbl').textContent = `${correct}/${total} correct — ${pct >= 80 ? '🎉 Excellent!' : pct >= 60 ? '👍 Good job!' : '📚 Keep practicing!'}`;
  document.getElementById('res-xp').textContent = `+${correct * 20} XP earned`;
  CU.quizzesDone++;
  CU.totalAccuracy = (CU.totalAccuracy || 0) + pct;
  CU.accuracyCount = (CU.accuracyCount || 0) + 1;
  CU.quizHistory = CU.quizHistory || [];
  CU.quizHistory.push({ score: correct, total, subject: activeSubjName('qzSubj'), ts: Date.now() });
  saveUser(CU);
  renderHome();
  renderLB('global');
}

function resetQuiz() {
  document.getElementById('quiz-game').style.display = 'none';
  document.getElementById('quiz-result').style.display = 'none';
  document.getElementById('quiz-setup').style.display = 'block';
}

// ════════════════════════════════
//  LEADERBOARD
// ════════════════════════════════
function renderLB(mode) {
  const lb = document.getElementById('lb-table');
  let users = getAllUsers().filter(u => u.username !== 'admin');

  // Add demo users if empty
  if (users.length < 5) {
    const demos = [
      {username:'Sarah_K',xp:2400,level:5,streak:12,quizzesDone:28,accuracyCount:28,totalAccuracy:2268,lastSeen:Date.now()-3600000},
      {username:'Omar_M',xp:1800,level:4,streak:8,quizzesDone:20,accuracyCount:20,totalAccuracy:1680,lastSeen:Date.now()-7200000},
      {username:'Lena_R',xp:3100,level:6,streak:21,quizzesDone:35,accuracyCount:35,totalAccuracy:2905,lastSeen:Date.now()-1800000},
      {username:'Alex_T',xp:950,level:3,streak:4,quizzesDone:12,accuracyCount:12,totalAccuracy:936,lastSeen:Date.now()-86400000},
      {username:'Mia_W',xp:560,level:2,streak:2,quizzesDone:8,accuracyCount:8,totalAccuracy:624,lastSeen:Date.now()-172800000},
    ];
    demos.forEach(d => { if (!getUser(d.username)) { const db = loadDB(); db[d.username] = {...createUser(d.username,'',''),...d}; saveDB(db); } });
    users = getAllUsers().filter(u => u.username !== 'admin');
  }

  // Add current user if not in DB
  if (CU && !CU.isAdmin) {
    const found = users.find(u => u.username === CU.username);
    if (!found) users.push(CU);
  }

  if (mode === 'weekly') users.sort((a,b) => ((b.weeklyXP||[]).reduce((s,v)=>s+v,0)) - ((a.weeklyXP||[]).reduce((s,v)=>s+v,0)));
  else users.sort((a,b) => (b.xp + (b.level-1)*1000) - (a.xp + (a.level-1)*1000));

  const colors = ['#FFD700','#C0C0C0','#CD7F32'];
  lb.innerHTML = '';
  users.forEach((u, i) => {
    const isMe = CU && u.username === CU.username;
    const acc = u.accuracyCount > 0 ? Math.round(u.totalAccuracy / u.accuracyCount) + '%' : '—';
    const xpTotal = u.xp + (u.level - 1) * 500;
    const row = document.createElement('div');
    row.className = 'lb-row' + (isMe ? ' lb-me' : '');
    row.innerHTML = `
      <div class="lb-rank" style="color:${colors[i]||'var(--muted)'}">${i < 3 ? ['🥇','🥈','🥉'][i] : i+1}</div>
      <div class="lb-avatar" style="background:${stringToColor(u.username)}22;color:${stringToColor(u.username)}">${u.username.slice(0,2).toUpperCase()}</div>
      <div class="lb-info">
        <div class="lb-name">${u.username}${isMe ? ' <span style="font-size:10px;color:var(--acc2);">(you)</span>' : ''}</div>
        <div class="lb-sub">Lv ${u.level} · ${LVL_NAMES[(u.level||1)-1]} · ${u.streak||0}🔥 · ${acc} avg</div>
      </div>
      <div class="lb-xp">${xpTotal.toLocaleString()} XP</div>`;
    lb.appendChild(row);
  });
}

function stringToColor(str) {
  const colors = ['#6c5fff','#22d98a','#f0a500','#ff5fa0','#00d4cc','#3b9eff','#ff4d4d'];
  let hash = 0;
  for (let i = 0; i < str.length; i++) hash = str.charCodeAt(i) + ((hash << 5) - hash);
  return colors[Math.abs(hash) % colors.length];
}

// ════════════════════════════════
//  BATTLE
// ════════════════════════════════
let battleState = { opponent: null, myScore: 0, oppScore: 0, questions: [], idx: 0, total: 5 };

function renderOnlinePlayers() {
  const el = document.getElementById('online-players');
  if (!el) return;
  const users = getAllUsers().filter(u => u.username !== 'admin' && (!CU || u.username !== CU.username)).slice(0,6);
  if (!users.length) { el.innerHTML = '<p style="font-size:13px;color:var(--muted);">No other players yet. Share Toutify with friends!</p>'; return; }
  el.innerHTML = '';
  users.forEach(u => {
    const div = document.createElement('div');
    div.className = 'player-result';
    div.innerHTML = `
      <div class="lb-avatar" style="width:32px;height:32px;background:${stringToColor(u.username)}22;color:${stringToColor(u.username)};font-size:11px;font-family:var(--fh);font-weight:700;border-radius:50%;display:flex;align-items:center;justify-content:center;">${u.username.slice(0,2).toUpperCase()}</div>
      <div style="flex:1;"><div style="font-size:13px;font-weight:600;">${u.username}</div><div style="font-size:11px;color:var(--muted);">Lv ${u.level} · ${u.quizzesDone||0} quizzes done</div></div>
      <button class="btn btn-sm btn-acc" onclick="challengePlayer('${u.username}')">Challenge ⚔️</button>`;
    el.appendChild(div);
  });
}

function searchPlayers() {
  const q = document.getElementById('battle-search-inp').value.trim().toLowerCase();
  const el = document.getElementById('battle-results');
  if (!q) { el.innerHTML = ''; return; }
  const users = getAllUsers().filter(u => u.username !== 'admin' && (!CU || u.username !== CU.username) && u.username.toLowerCase().includes(q));
  el.innerHTML = '';
  if (!users.length) { el.innerHTML = '<p style="font-size:13px;color:var(--muted);padding:.5rem 0;">No users found.</p>'; return; }
  users.forEach(u => {
    const div = document.createElement('div');
    div.className = 'player-result';
    div.innerHTML = `
      <div class="lb-avatar" style="width:32px;height:32px;background:${stringToColor(u.username)}22;color:${stringToColor(u.username)};font-size:11px;font-family:var(--fh);font-weight:700;border-radius:50%;display:flex;align-items:center;justify-content:center;">${u.username.slice(0,2).toUpperCase()}</div>
      <div style="flex:1;"><div style="font-size:13px;font-weight:600;">${u.username}</div><div style="font-size:11px;color:var(--muted);">Lv ${u.level}</div></div>
      <button class="btn btn-sm btn-acc" onclick="challengePlayer('${u.username}')">Challenge ⚔️</button>`;
    el.appendChild(div);
  });
}

function challengePlayer(username) {
  const opp = getUser(username);
  if (!opp) { toast('Player not found'); return; }
  battleState.opponent = opp;
  battleState.myScore = 0; battleState.oppScore = 0; battleState.idx = 0;
  // pick random subject from defaults
  const subjects = Object.keys(DEFAULT_QZ);
  const sub = subjects[Math.floor(Math.random() * subjects.length)];
  const pool = getQZ(sub);
  battleState.questions = [...pool].sort(()=>Math.random()-.5).slice(0,battleState.total);
  document.getElementById('battle-lobby').style.display = 'none';
  document.getElementById('battle-game').style.display = 'block';
  document.getElementById('battle-result').style.display = 'none';
  renderBattleArena();
  loadBattleQ();
}

function renderBattleArena() {
  const opp = battleState.opponent;
  const myPct = Math.round((battleState.myScore / battleState.total) * 100);
  const oppPct = Math.round((battleState.oppScore / battleState.total) * 100);
  document.getElementById('battle-arena').innerHTML = `
    <div class="battle-player">
      <div style="font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:8px;">${CU.username}</div>
      <div class="battle-score" style="color:var(--acc)">${battleState.myScore}</div>
      <div class="battle-prog"><div style="height:100%;border-radius:999px;background:var(--acc);width:${myPct}%;transition:width .3s;"></div></div>
    </div>
    <div class="battle-vs">VS</div>
    <div class="battle-player">
      <div style="font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:8px;">${opp.username}</div>
      <div class="battle-score" style="color:var(--pink)">${battleState.oppScore}</div>
      <div class="battle-prog"><div style="height:100%;border-radius:999px;background:var(--pink);width:${oppPct}%;transition:width .3s;"></div></div>
    </div>`;
}

function loadBattleQ() {
  if (battleState.idx >= battleState.questions.length) { showBattleResult(); return; }
  const q = battleState.questions[battleState.idx];
  const el = document.getElementById('battle-q-area');
  el.innerHTML = `
    <div class="q-card">${q.q}</div>
    <div class="opts" id="battle-opts"></div>`;
  const optsEl = document.getElementById('battle-opts');
  q.opts.forEach((o, i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => answerBattle(i);
    optsEl.appendChild(btn);
  });
}

function answerBattle(chosen) {
  const q = battleState.questions[battleState.idx];
  const correct = chosen === q.c;
  document.querySelectorAll('#battle-opts .opt').forEach((b, i) => {
    b.disabled = true;
    if (i === q.c) b.classList.add('correct');
    else if (i === chosen && !correct) b.classList.add('wrong');
  });
  if (correct) { battleState.myScore++; gainXP(15); }
  // Simulate opponent: 60% chance to get it right
  if (Math.random() < 0.6) battleState.oppScore++;
  renderBattleArena();
  setTimeout(() => { battleState.idx++; loadBattleQ(); }, 1000);
}

function showBattleResult() {
  document.getElementById('battle-game').style.display = 'none';
  document.getElementById('battle-result').style.display = 'block';
  const win = battleState.myScore > battleState.oppScore;
  const tie = battleState.myScore === battleState.oppScore;
  const xpGain = win ? 100 : tie ? 50 : 25;
  gainXP(xpGain);
  document.getElementById('battle-res-content').innerHTML = `
    <div style="font-size:52px;margin-bottom:8px;">${win ? '🏆' : tie ? '🤝' : '😤'}</div>
    <div style="font-family:var(--fh);font-size:28px;font-weight:800;color:${win?'var(--green)':tie?'var(--amber)':'var(--red)'};">${win ? 'Victory!' : tie ? 'Tie!' : 'Defeat'}</div>
    <p style="color:var(--muted);margin:8px 0;font-size:14px;">${CU.username}: ${battleState.myScore} · ${battleState.opponent.username}: ${battleState.oppScore}</p>
    <p style="color:var(--acc2);font-size:13px;">+${xpGain} XP earned</p>`;
}

function resetBattle() {
  battleState = { opponent: null, myScore: 0, oppScore: 0, questions: [], idx: 0, total: 5 };
  document.getElementById('battle-lobby').style.display = 'block';
  document.getElementById('battle-game').style.display = 'none';
  document.getElementById('battle-result').style.display = 'none';
  document.getElementById('battle-search-inp').value = '';
  document.getElementById('battle-results').innerHTML = '';
  renderOnlinePlayers();
}

// ════════════════════════════════
//  AI TUTOR
// ════════════════════════════════
let chatHistory = [];

function renderQuickQs() {
  const sub = activeSubjName('tutorSubj');
  const qs = {
    "Biochemistry":["Explain the Krebs cycle","What is enzyme inhibition?","How does DNA replication work?","Summarize glycolysis"],
    "Physics":["Explain Newton's laws","What is quantum mechanics?","How do electromagnetic waves work?","Explain entropy"],
    "History":["Key causes of WWI","French Revolution summary","What was the Cold War?","Effects of colonialism"],
    "Mathematics":["Explain derivatives simply","What is a limit?","How to integrate by parts?","What is Euler's identity?"],
  };
  const el = document.getElementById('quick-qs');
  if (!el) return;
  const list = qs[sub] || [`Ask me anything about ${sub}`];
  el.innerHTML = '';
  list.forEach(q => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-xs';
    btn.style.fontSize = '11px';
    btn.textContent = q;
    btn.onclick = () => { document.getElementById('chat-inp').value = q; sendChat(); };
    el.appendChild(btn);
  });
}

async function sendChat() {
  const inp = document.getElementById('chat-inp');
  const msg = inp.value.trim();
  if (!msg) return;
  inp.value = '';
  const sub = activeSubjName('tutorSubj');
  appendMsg('user', msg);
  chatHistory.push({ role:'user', content: msg });
  const tid = appendTyping();
  document.getElementById('chat-send').disabled = true;
  try {
    const res = await fetch(API, {
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514', max_tokens:1000,
        system:`You are Toutify, a friendly study tutor specializing in ${sub} for university students. Give clear, concise explanations under 150 words. Use bullet points and examples when helpful.`,
        messages: chatHistory.slice(-10),
      })
    });
    const data = await res.json();
    removeTyping(tid);
    const reply = data.content?.map(c=>c.text||'').join('') || "Couldn't get a response. Try again!";
    chatHistory.push({ role:'assistant', content: reply });
    appendMsg('ai', reply);
    gainXP(5);
  } catch {
    removeTyping(tid);
    appendMsg('ai', "Connection issue. Please try again.");
  }
  document.getElementById('chat-send').disabled = false;
}

function appendMsg(role, text) {
  const box = document.getElementById('chat-box');
  const div = document.createElement('div');
  div.className = `msg msg-${role}`;
  div.innerHTML = `<div class="msg-av">${role==='ai'?'T':'U'}</div><div class="msg-bub">${text.replace(/\n/g,'<br/>')}</div>`;
  box.appendChild(div);
  box.scrollTop = box.scrollHeight;
}

function appendTyping() {
  const box = document.getElementById('chat-box');
  const id = 'td-' + Date.now();
  const div = document.createElement('div');
  div.className = 'msg msg-ai'; div.id = id;
  div.innerHTML = `<div class="msg-av">T</div><div class="msg-bub"><div class="typing-dots"><div class="tdot"></div><div class="tdot"></div><div class="tdot"></div></div></div>`;
  box.appendChild(div);
  box.scrollTop = box.scrollHeight;
  return id;
}
function removeTyping(id) { const el = document.getElementById(id); if(el) el.remove(); }

// ════════════════════════════════
//  CONCEPT MAPS
// ════════════════════════════════
let mapState = { subj: 0, topic: 0 };

function renderMapSubj() { renderSubjPickers(); }
function renderMapTopics() {
  const el = document.getElementById('map-topic-pick');
  if (!el) return;
  const sub = activeSubjName('mapSubj');
  const data = CONCEPT_MAPS[sub];
  if (!data) { el.innerHTML = ''; return; }
  el.innerHTML = '';
  data.topics.forEach((t, i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i === (subjState.mapTopic||0) ? ' btn-acc' : '');
    btn.textContent = t;
    btn.onclick = () => { subjState.mapTopic = i; renderMapTopics(); drawMap(); };
    el.appendChild(btn);
  });
}

function drawMap() {
  const canvas = document.getElementById('map-canvas');
  if (!canvas) return;
  const sub = activeSubjName('mapSubj');
  const data = CONCEPT_MAPS[sub];
  if (!data) { canvas.innerHTML = '<p style="padding:2rem;color:var(--muted);text-align:center;">No map available yet.</p>'; return; }
  const topicName = data.topics[subjState.mapTopic || 0] || data.topics[0];
  const mapDef = data.maps[topicName] || Object.values(data.maps)[0];
  if (!mapDef) return;
  canvas.innerHTML = '';
  const w = canvas.clientWidth || 600;
  const h = canvas.clientHeight || 360;
  const cx = Math.round(w / 2), cy = Math.round(h / 2 - 10);
  const svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
  svg.className = 'map-svg-layer';
  svg.setAttribute('viewBox', `0 0 ${w} ${h}`);
  mapDef.nodes.forEach(n => {
    const nx = Math.round(n.x + 55), ny = Math.round(n.y + 60);
    const line = document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1',cx); line.setAttribute('y1',cy);
    line.setAttribute('x2',nx+40); line.setAttribute('y2',ny+14);
    line.setAttribute('stroke','rgba(255,255,255,0.08)'); line.setAttribute('stroke-width','1.5');
    svg.appendChild(line);
  });
  canvas.appendChild(svg);
  const cNode = document.createElement('div');
  cNode.className = 'mnode center';
  cNode.style.cssText = `left:${cx-55}px;top:${cy-18}px;`;
  cNode.textContent = mapDef.center;
  canvas.appendChild(cNode);
  mapDef.nodes.forEach(n => {
    const node = document.createElement('div');
    node.className = 'mnode leaf';
    node.style.cssText = `left:${n.x+35}px;top:${n.y+50}px;`;
    node.textContent = n.l;
    node.onclick = () => { subjState.tutorSubj = subjState.mapSubj; nav('tutor'); document.getElementById('chat-inp').value = `Explain ${n.l} in ${sub}`; sendChat(); };
    canvas.appendChild(node);
  });
}

// ════════════════════════════════
//  STUDY MODES
// ════════════════════════════════
let currentMode = null;
let pomoState = { running:false, phase:'focus', session:1, timeLeft:25*60, interval:null };
let dwState = { duration:30, interval:null, start:0 };
let sprintState = { interval:null, timeLeft:60, score:0, subj:'Biochemistry' };

function openMode(id) {
  document.getElementById('study-home').style.display = 'none';
  document.querySelectorAll('[id^="mode-"]').forEach(el => el.style.display = 'none');
  document.getElementById('mode-'+id).style.display = 'block';
  currentMode = id;
  if (id === 'spaced') renderSpacedCards();
  if (id === 'sprint') renderSprintSubj();
  if (id === 'blurting') renderBlurtSubj();
}

function closeMode() {
  document.querySelectorAll('[id^="mode-"]').forEach(el => el.style.display = 'none');
  document.getElementById('study-home').style.display = 'block';
  clearInterval(pomoState.interval);
  clearInterval(dwState.interval);
  clearInterval(sprintState.interval);
  currentMode = null;
}

// POMODORO
const POMO_PHASES = [{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'LONG BREAK',mins:15}];
let pomoPhaseIdx = 0;

function resetPomo() {
  clearInterval(pomoState.interval);
  pomoState = {running:false,phase:'focus',session:1,timeLeft:25*60,interval:null};
  pomoPhaseIdx = 0;
  updatePomoUI();
  document.getElementById('pomo-start-btn').textContent = 'Start';
  document.getElementById('pomo-log').innerHTML = '';
}

function togglePomo() {
  if (pomoState.running) {
    clearInterval(pomoState.interval);
    pomoState.running = false;
    document.getElementById('pomo-start-btn').textContent = 'Resume';
  } else {
    pomoState.running = true;
    document.getElementById('pomo-start-btn').textContent = 'Pause';
    pomoState.interval = setInterval(() => {
      pomoState.timeLeft--;
      if (pomoState.timeLeft <= 0) {
        const phase = POMO_PHASES[pomoPhaseIdx];
        const log = document.getElementById('pomo-log');
        log.innerHTML += `<div style="margin-bottom:4px;">✓ ${phase.name} session complete</div>`;
        if (phase.name === 'FOCUS') { gainXP(30); }
        pomoPhaseIdx = (pomoPhaseIdx + 1) % POMO_PHASES.length;
        const next = POMO_PHASES[pomoPhaseIdx];
        pomoState.timeLeft = next.mins * 60;
        pomoState.session = Math.floor(pomoPhaseIdx / 2) + 1;
      }
      updatePomoUI();
    }, 1000);
  }
}

function updatePomoUI() {
  const phase = POMO_PHASES[pomoPhaseIdx];
  const m = Math.floor(pomoState.timeLeft / 60).toString().padStart(2,'0');
  const s = (pomoState.timeLeft % 60).toString().padStart(2,'0');
  document.getElementById('pomo-time').textContent = `${m}:${s}`;
  document.getElementById('pomo-phase').textContent = phase.name;
  document.getElementById('pomo-session').textContent = `Session ${Math.floor(pomoPhaseIdx/2)+1} of 4`;
  const totalSecs = phase.mins * 60;
  const prog = (pomoState.timeLeft / totalSecs);
  const circ = 2 * Math.PI * 80;
  const offset = circ * (1 - prog);
  const circle = document.getElementById('pomo-circle');
  if (circle) {
    circle.setAttribute('stroke-dasharray', circ);
    circle.setAttribute('stroke-dashoffset', offset);
    circle.setAttribute('stroke', phase.name === 'FOCUS' ? 'var(--acc)' : 'var(--green)');
  }
}

// BLURTING
function renderBlurtSubj() {
  const el = document.getElementById('blurt-subj');
  if (!el) return;
  const subjs = [...Object.keys(DEFAULT_FC),...CU.subjects.map(s=>s.name)];
  el.innerHTML = '';
  subjs.forEach((s,i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i===0?' btn-acc':'');
    btn.textContent = s;
    btn.onclick = () => { document.querySelectorAll('#blurt-subj .btn').forEach(b=>b.classList.remove('btn-acc')); btn.classList.add('btn-acc'); };
    el.appendChild(btn);
  });
}

async function checkBlurt() {
  const text = document.getElementById('blurt-input').value.trim();
  const activeBtn = document.querySelector('#blurt-subj .btn-acc');
  const sub = activeBtn ? activeBtn.textContent : 'Biochemistry';
  if (!text || text.length < 20) { toast('Write more before checking!'); return; }
  document.getElementById('blurt-result').style.display = 'none';
  const btn = document.querySelector('#mode-blurting .btn-acc[onclick]');
  try {
    const res = await fetch(API, {
      method:'POST', headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514', max_tokens:1000,
        system:`You are a study coach. Evaluate the student's blurt attempt about ${sub}. Identify: (1) what they got right, (2) key things they missed, (3) any misconceptions. Be encouraging but honest. Keep response under 200 words.`,
        messages:[{role:'user',content:`My blurt about ${sub}:\n\n${text}`}]
      })
    });
    const data = await res.json();
    const reply = data.content?.map(c=>c.text||'').join('') || 'Could not analyze. Try again.';
    document.getElementById('blurt-feedback').innerHTML = reply.replace(/\n/g,'<br/>');
    document.getElementById('blurt-result').style.display = 'block';
    gainXP(25);
  } catch { toast('Error connecting to AI. Try again.'); }
}

// FEYNMAN
async function checkFeynman() {
  const topic = document.getElementById('feynman-topic').value.trim();
  const explanation = document.getElementById('feynman-input').value.trim();
  if (!topic || !explanation) { toast('Fill in both fields'); return; }
  try {
    const res = await fetch(API, {
      method:'POST', headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514', max_tokens:1000,
        system:`You are a Feynman method coach. Analyze the student's simple explanation of "${topic}". Rate their simplicity (is it actually simple?), accuracy (any errors?), and completeness (what's missing?). Then give one suggestion to simplify further. Keep under 200 words. Be encouraging.`,
        messages:[{role:'user',content:`My simple explanation of "${topic}":\n\n${explanation}`}]
      })
    });
    const data = await res.json();
    const reply = data.content?.map(c=>c.text||'').join('') || 'Could not analyze.';
    document.getElementById('feynman-feedback').innerHTML = reply.replace(/\n/g,'<br/>');
    document.getElementById('feynman-result').style.display = 'block';
    gainXP(25);
  } catch { toast('Error connecting to AI. Try again.'); }
}

// SPEED SPRINT
let sprintSubjName = 'Biochemistry';

function renderSprintSubj() {
  const el = document.getElementById('sprint-subj');
  if (!el) return;
  const subjs = [...Object.keys(DEFAULT_QZ),...CU.subjects.map(s=>s.name)];
  el.innerHTML = '';
  subjs.forEach((s,i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i===0?' btn-acc':'');
    btn.textContent = s;
    btn.onclick = () => { document.querySelectorAll('#sprint-subj .btn').forEach(b=>b.classList.remove('btn-acc')); btn.classList.add('btn-acc'); sprintSubjName=s; };
    el.appendChild(btn);
  });
}

let sprintPool = [], sprintIdx = 0, sprintCorrect = 0, sprintTimerVal = 60;

function startSprint() {
  const pool = getQZ(sprintSubjName);
  if (!pool.length) { toast('No questions for this subject!'); return; }
  sprintPool = [...pool].sort(()=>Math.random()-.5);
  sprintIdx = 0; sprintCorrect = 0; sprintTimerVal = 60;
  document.getElementById('sprint-setup').style.display = 'none';
  document.getElementById('sprint-result').style.display = 'none';
  document.getElementById('sprint-game').style.display = 'block';
  document.getElementById('sprint-timer').textContent = '60';
  document.getElementById('sprint-score').textContent = '0 correct';
  document.getElementById('sprint-bar').style.width = '100%';
  clearInterval(sprintState.interval);
  sprintState.interval = setInterval(() => {
    sprintTimerVal--;
    document.getElementById('sprint-timer').textContent = sprintTimerVal;
    const pct = Math.round((sprintTimerVal/60)*100);
    document.getElementById('sprint-bar').style.width = pct+'%';
    document.getElementById('sprint-bar').style.background = sprintTimerVal > 20 ? 'var(--acc)' : 'var(--red)';
    if (sprintTimerVal <= 0) {
      clearInterval(sprintState.interval);
      document.getElementById('sprint-game').style.display = 'none';
      document.getElementById('sprint-result').style.display = 'block';
      document.getElementById('sprint-final').textContent = sprintCorrect;
      gainXP(sprintCorrect * 5);
      toast(`Sprint done! ${sprintCorrect} correct · +${sprintCorrect*5} XP`);
    }
  }, 1000);
  loadSprintQ();
}

function loadSprintQ() {
  const q = sprintPool[sprintIdx % sprintPool.length];
  document.getElementById('sprint-q').textContent = q.q;
  const el = document.getElementById('sprint-opts');
  el.innerHTML = '';
  q.opts.forEach((o,i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => {
      if (i === q.c) { sprintCorrect++; document.getElementById('sprint-score').textContent = sprintCorrect + ' correct'; }
      sprintIdx++;
      loadSprintQ();
    };
    el.appendChild(btn);
  });
}

// DEEP WORK
let dwDuration = 30;
function setDW(m, el) {
  dwDuration = m;
  document.querySelectorAll('.dw-dur').forEach(b => b.classList.remove('btn-acc'));
  el.classList.add('btn-acc');
}

function startDW() {
  const intention = document.getElementById('dw-intention').value.trim() || 'Deep work session';
  document.getElementById('dw-intention-display').textContent = '🎯 ' + intention;
  document.getElementById('dw-active').style.display = 'block';
  dwState.start = Date.now();
  dwState.total = dwDuration * 60;
  clearInterval(dwState.interval);
  dwState.interval = setInterval(() => {
    const elapsed = Math.floor((Date.now() - dwState.start) / 1000);
    const left = Math.max(0, dwState.total - elapsed);
    const m = Math.floor(left/60).toString().padStart(2,'0');
    const s = (left%60).toString().padStart(2,'0');
    document.getElementById('dw-timer').textContent = `${m}:${s}`;
    const pct = Math.round((left/dwState.total)*100);
    document.getElementById('dw-bar').style.width = pct + '%';
    if (left <= 0) { clearInterval(dwState.interval); gainXP(60); toast('Deep work session complete! +60 XP 🧘'); }
  }, 1000);
}

function endDW() {
  clearInterval(dwState.interval);
  document.getElementById('dw-active').style.display = 'none';
  const elapsed = Math.floor((Date.now() - dwState.start) / 1000);
  const xp = Math.round((elapsed / dwState.total) * 60);
  gainXP(xp);
  toast(`Session ended. +${xp} XP earned`);
}

// SPACED REP
function renderSpacedCards() {
  const el = document.getElementById('spaced-cards');
  if (!el) return;
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub).slice(0, 5);
  el.innerHTML = '';
  if (!cards.length) { el.innerHTML = '<p style="font-size:13px;color:var(--muted);">No cards yet for this subject.</p>'; return; }
  cards.forEach(c => {
    const div = document.createElement('div');
    div.className = 'card2';
    div.style.marginBottom = '8px';
    div.innerHTML = `<div style="font-size:13px;font-weight:500;margin-bottom:4px;">${c.q}</div><div style="font-size:12px;color:var(--muted);">${c.a}</div>`;
    el.appendChild(div);
  });
}

// ════════════════════════════════
//  UPLOAD
// ════════════════════════════════
let genCards = [];

function handleDrop(e) {
  e.preventDefault();
  document.getElementById('pdf-drop').classList.remove('drag');
  const file = e.dataTransfer.files[0];
  if (file && file.type === 'application/pdf') processPDFFile(file);
}

function handlePDF(e) {
  const file = e.target.files[0];
  if (file) processPDFFile(file);
}

function processPDFFile(file) {
  document.getElementById('pdf-name').textContent = `📄 ${file.name} loaded`;
  const reader = new FileReader();
  reader.onload = function() {
    // Simulate PDF extraction
    const text = `[PDF: ${file.name}] Extracted ${file.size/1000}KB document. Generate flashcards for main topics.`;
    document.getElementById('notes-txt').value = text;
    toast('✅ PDF loaded! Click "Generate study material"');
  };
  reader.readAsText(file);
}

function handleYT() {
  const url = document.getElementById('yt-url').value.trim();
  if (!url || !url.includes('youtube')) { toast('Please enter a valid YouTube URL'); return; }
  const videoId = url.match(/v=([^&]+)/)?.[1] || url.match(/youtu.be\/([^?]+)/)?.[1];
  if (videoId) {
    document.getElementById('notes-txt').value = `[YouTube Video ID: ${videoId}] — Generate comprehensive flashcards and study questions about the key concepts typically covered in a university lecture on this topic.`;
    toast('YouTube video linked! Click Generate to create study material.');
  } else {
    toast('Could not parse video ID. Try pasting notes directly.');
  }
}

async function generateNotes() {
  const text = document.getElementById('notes-txt').value.trim();
  if (!text || text.length < 20) { toast('Add some content first!'); return; }
  const sub = activeSubjName('uploadSubj');
  const btn = document.getElementById('gen-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spin"></span> Generating...';
  try {
    const res = await fetch(API, {
      method:'POST', headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514', max_tokens:1000,
        system:`Generate exactly 6 flashcard Q&A pairs for ${sub} students based on the provided content. Respond ONLY with valid JSON array, no markdown or preamble: [{"q":"question","a":"answer"},...]`,
        messages:[{role:'user',content:`Create 6 flashcards from:\n\n${text.slice(0,2500)}`}]
      })
    });
    const data = await res.json();
    let raw = data.content?.map(c=>c.text||'').join('') || '[]';
    raw = raw.replace(/```json|```/g,'').trim();
    genCards = JSON.parse(raw).map(c=>({...c,subject:sub}));
    renderGenCards();
    gainXP(30);
    toast(`${genCards.length} flashcards generated! +30 XP`);
  } catch(e) { toast('Generation failed. Try again.'); console.error(e); }
  btn.disabled = false;
  btn.textContent = 'Generate study material';
}

function renderGenCards() {
  const el = document.getElementById('gen-cards');
  el.innerHTML = '';
  genCards.forEach(c => {
    const div = document.createElement('div');
    div.className = 'gen-item';
    div.innerHTML = `<span class="gen-q">Q: ${c.q}</span><span class="gen-a">A: ${c.a}</span>`;
    el.appendChild(div);
  });
  document.getElementById('upload-results').style.display = 'block';
}

function addGenCards() {
  CU.extraCards = CU.extraCards || [];
  CU.extraCards.push(...genCards);
  const sub = CU.subjects.find(s => s.name === (genCards[0]?.subject));
  if (sub) sub.cards = (sub.cards || 0) + genCards.length;
  saveUser(CU);
  toast(`${genCards.length} cards added to deck!`);
  clearGen();
}

function clearGen() {
  genCards = [];
  document.getElementById('upload-results').style.display = 'none';
  document.getElementById('notes-txt').value = '';
  document.getElementById('yt-url').value = '';
  document.getElementById('pdf-name').textContent = '';
}

// ════════════════════════════════
//  PROGRESS
// ════════════════════════════════
function renderProgress() {
  const el = document.getElementById('prog-subjs');
  if (!el) return;
  el.innerHTML = '';
  const allSubjs = [...Object.keys(DEFAULT_FC), ...CU.subjects.map(s=>s.name)];
  const uniq = [...new Set(allSubjs)];
  uniq.forEach(name => {
    const subj = CU.subjects.find(s=>s.name===name) || {name,icon:'📖',color:'var(--acc)',progress:0,cards:0,quizzes:0};
    const card = document.createElement('div');
    card.className = 'prog-subj';
    card.innerHTML = `
      <div class="prog-header">
        <span style="font-size:18px;">${subj.icon||'📖'}</span>
        <span style="font-family:var(--fh);font-size:14px;font-weight:700;">${name}</span>
        <span style="margin-left:auto;font-family:var(--fh);font-size:13px;font-weight:700;color:${subj.color||'var(--acc)'};">${subj.progress||0}%</span>
      </div>
      <div class="prog-bar" style="margin-bottom:8px;"><div class="prog-fill" style="width:${subj.progress||0}%;background:${subj.color||'var(--acc)'};"></div></div>
      <div style="font-size:11px;color:var(--muted);">${subj.cards||0} cards · ${subj.quizzes||0} quizzes</div>`;
    el.appendChild(card);
  });
}

function renderWeeklyBars() {
  const el = document.getElementById('week-bars');
  if (!el) return;
  const days = ['M','T','W','T','F','S','S'];
  const vals = CU.weeklyXP || [0,0,0,0,0,0,0];
  const max = Math.max(...vals, 1);
  el.innerHTML = '';
  days.forEach((d,i) => {
    const wrap = document.createElement('div');
    wrap.className = 'wbar-wrap';
    const bar = document.createElement('div');
    bar.className = 'wbar';
    const h = Math.max(3, Math.round((vals[i]/max)*60));
    bar.style.cssText = `height:${h}px;background:${i===6?'var(--acc)':'var(--s4)'};`;
    const lbl = document.createElement('div');
    lbl.className = 'wlbl'; lbl.textContent = d;
    wrap.appendChild(bar); wrap.appendChild(lbl);
    el.appendChild(wrap);
  });
}

function renderStreak() {
  const el = document.getElementById('streak-days');
  if (!el) return;
  const days = ['M','T','W','T','F','S','S'];
  const statuses = CU.streakDays || [false,false,false,false,false,false,true];
  el.innerHTML = '';
  days.forEach((d,i) => {
    const div = document.createElement('div');
    div.className = `sday ${i===6?'today':statuses[i]?'done':'miss'}`;
    div.textContent = d;
    el.appendChild(div);
  });
}

// ════════════════════════════════
//  LEVELS & BADGES
// ════════════════════════════════
const BADGES_DEF = [
  {icon:'🔥',name:'First flame',desc:'Study for the first time',cond:u=>u.cardsStudied>=1},
  {icon:'📚',name:'Bookworm',desc:'Study 50 cards',cond:u=>u.cardsStudied>=50},
  {icon:'🧠',name:'Brain power',desc:'Study 200 cards',cond:u=>u.cardsStudied>=200},
  {icon:'🏆',name:'Quiz champion',desc:'Complete 10 quizzes',cond:u=>u.quizzesDone>=10},
  {icon:'⚡',name:'Speed demon',desc:'Finish a 60s sprint',cond:u=>u.quizzesDone>=5},
  {icon:'🔢',name:'Scholar',desc:'Reach Level 3',cond:u=>u.level>=3},
  {icon:'⭐',name:'Expert',desc:'Reach Level 5',cond:u=>u.level>=5},
  {icon:'💎',name:'Legend',desc:'Reach Level 8',cond:u=>u.level>=8},
];

function renderLevels() {
  const grid = document.getElementById('lvl-grid');
  if (!grid) return;
  grid.innerHTML = '';
  for (let i = 1; i <= 10; i++) {
    const card = document.createElement('div');
    const unlocked = i <= CU.level;
    const current = i === CU.level;
    card.className = `lvl-card ${current?'current':unlocked?'unlocked':'locked'}`;
    card.innerHTML = `<div class="lvl-n" style="color:${current?'var(--green)':unlocked?'var(--acc)':'var(--dim)'}">${i}</div>
      <div class="lvl-name">${LVL_NAMES[i-1]}</div>
      <div class="lvl-req">${current?'Current':unlocked?'✓':LVL_XP[i-1].toLocaleString()+' XP'}</div>`;
    grid.appendChild(card);
  }
  updateLevelScreen();
}

function renderBadges() {
  const el = document.getElementById('badge-wrap');
  if (!el) return;
  el.innerHTML = '';
  BADGES_DEF.forEach(b => {
    const earned = b.cond(CU);
    const div = document.createElement('div');
    div.className = 'bdg' + (earned ? '' : ' locked');
    div.innerHTML = `<span class="bdg-icon">${b.icon}</span><div><div class="bdg-name">${b.name}</div><div class="bdg-desc">${b.desc}</div></div>`;
    el.appendChild(div);
  });
}

// ════════════════════════════════
//  ADMIN
// ════════════════════════════════
let adminUnlocked = false;

function unlockAdmin() {
  const pw = document.getElementById('admin-pw-inp').value;
  if (pw === ADMIN_PASS) {
    adminUnlocked = true;
    document.getElementById('admin-locked-view').style.display = 'none';
    document.getElementById('admin-panel').style.display = 'block';
    renderAdminPanel();
  } else { toast('Wrong password'); }
}

function renderAdminPanel() {
  if (!adminUnlocked && !CU?.isAdmin) return;
  if (!adminUnlocked) adminUnlocked = true;
  const users = getAllUsers().filter(u => u.username !== 'admin');
  const active = users.filter(u => Date.now() - (u.lastSeen||0) < 86400000);
  const totalCards = users.reduce((a,u) => a+(u.cardsStudied||0), 0);
  const totalQuizzes = users.reduce((a,u) => a+(u.quizzesDone||0), 0);

  const statsEl = document.getElementById('admin-stats-row');
  if (statsEl) statsEl.innerHTML = `
    <div class="admin-stat"><div class="admin-n" style="color:var(--acc)">${users.length}</div><div class="admin-l">total users</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--green)">${active.length}</div><div class="admin-l">active today</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--amber)">${totalCards}</div><div class="admin-l">cards studied</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--teal)">${totalQuizzes}</div><div class="admin-l">quizzes done</div></div>`;

  renderUsersTable(users);
}

function renderUsersTable(users) {
  const el = document.getElementById('users-table');
  if (!el) return;
  el.innerHTML = `<div class="ut-head">
    <div class="ut-lhd">User</div>
    <div class="ut-lhd">Level</div>
    <div class="ut-lhd ut-subj">XP</div>
    <div class="ut-lhd ut-lv">Quizzes</div>
    <div class="ut-lhd">Status</div>
    <div class="ut-lhd">Actions</div>
  </div>`;
  users.forEach(u => {
    const active = Date.now() - (u.lastSeen||0) < 86400000;
    const row = document.createElement('div');
    row.className = 'ut-row';
    row.innerHTML = `
      <div class="ut-name"><div class="ut-av" style="background:${stringToColor(u.username)}22;color:${stringToColor(u.username)}">${u.username.slice(0,2).toUpperCase()}</div>${u.username}<span style="font-size:10px;color:var(--muted);margin-left:4px;">${u.email||''}</span></div>
      <div>Lv ${u.level||1}</div>
      <div class="ut-subj">${(u.xp||0).toLocaleString()}</div>
      <div class="ut-lv">${u.quizzesDone||0}</div>
      <div><span class="ut-status ${active?'active':'inactive'}">${active?'Active':'Inactive'}</span></div>
      <div style="display:flex;gap:6px;">
        <button class="btn btn-xs" onclick="viewUser('${u.username}')">View</button>
        <button class="btn btn-xs btn-danger" onclick="deleteUser('${u.username}')">Delete</button>
      </div>`;
    el.appendChild(row);
  });
}

function filterAdminUsers() {
  const q = document.getElementById('admin-search').value.toLowerCase();
  const users = getAllUsers().filter(u => u.username !== 'admin' && u.username.toLowerCase().includes(q));
  renderUsersTable(users);
}

function viewUser(un) {
  const u = getUser(un);
  if (!u) return;
  const acc = u.accuracyCount > 0 ? Math.round(u.totalAccuracy/u.accuracyCount)+'%' : '—';
  toast(`${un}: Lv${u.level} · ${u.xp}XP · ${u.quizzesDone} quizzes · ${acc} acc · ${u.streak||0}🔥`);
}

function deleteUser(un) {
  if (!confirm(`Delete user "${un}"? This cannot be undone.`)) return;
  const db = loadDB();
  delete db[un];
  saveDB(db);
  renderAdminPanel();
  toast(`User ${un} deleted.`);
}

function resetAllUsers() {
  const db = loadDB();
  Object.keys(db).forEach(k => {
    if (k !== 'admin') delete db[k];
  });
  saveDB(db);
  renderAdminPanel();
  toast('All user data reset.');
}

function exportUsers() {
  const users = getAllUsers().filter(u => u.username !== 'admin');
  const csv = ['Username,Email,Level,XP,Streak,Cards,Quizzes,Accuracy,Last Seen',
    ...users.map(u => `${u.username},${u.email||''},${u.level||1},${u.xp||0},${u.streak||0},${u.cardsStudied||0},${u.quizzesDone||0},${u.accuracyCount>0?Math.round(u.totalAccuracy/u.accuracyCount)+'%':'—'},${new Date(u.lastSeen||0).toLocaleDateString()}`)
  ].join('\n');
  const blob = new Blob([csv], {type:'text/csv'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'toutify_users.csv';
  a.click();
}

// ════════════════════════════════
//  UTILS
// ════════════════════════════════
function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(t._timeout);
  t._timeout = setTimeout(() => t.classList.remove('show'), 3000);
}

function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// Close modals on bg click
document.querySelectorAll('.modal-bg').forEach(bg => {
  bg.addEventListener('click', e => { if (e.target === bg) bg.classList.remove('open'); });
});
</script>
</body>
</html>
