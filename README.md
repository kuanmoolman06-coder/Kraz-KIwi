<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KRAZ KIWI ★</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Unbounded:wght@300;400;700;900&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<style>
/* ─────────────────────────────────────────
   RESET & TOKENS
───────────────────────────────────────── */
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
:root{
  --red:#D10000;
  --red2:#FF0000;
  --yellow:#FFE600;
  --black:#050505;
  --white:#F5F0E8;
  --grey:#1A1A1A;
  --mid:#2C2C2C;
  --muted:#666;
  --A:'Anton',sans-serif;
  --U:'Unbounded',sans-serif;
  --I:'Instrument Serif',serif;
}
html{overflow-x:hidden;scroll-behavior:smooth;}
body{
  background:var(--black);
  color:var(--white);
  font-family:var(--U);
  overflow-x:hidden;
  cursor:none;
}

/* ─────────────────────────────────────────
   CURSOR
───────────────────────────────────────── */
#kk-cursor{
  position:fixed;top:0;left:0;z-index:9999;
  pointer-events:none;
  width:20px;height:20px;
  transform:translate(-50%,-50%);
  transition:transform .15s ease;
}
#kk-cursor::before{
  content:'★';
  font-size:20px;color:var(--red);
  display:block;line-height:1;
  transition:font-size .2s,color .2s;
  text-shadow:0 0 12px rgba(209,0,0,.6);
}
body:has(a:hover) #kk-cursor::before,
body:has(button:hover) #kk-cursor::before{
  font-size:32px;color:var(--yellow);
}

/* ─────────────────────────────────────────
   LOADER
───────────────────────────────────────── */
#loader{
  position:fixed;inset:0;background:var(--black);
  z-index:8000;
  display:grid;place-items:center;
}
.loader-inner{display:flex;flex-direction:column;align-items:center;gap:2rem;}
.loader-star{font-size:4rem;color:var(--red);animation:loaderSpin 1.2s linear infinite;text-shadow:0 0 30px rgba(209,0,0,.8);}
@keyframes loaderSpin{to{transform:rotate(360deg);}}
.loader-word{
  font-family:var(--A);font-size:3.5rem;letter-spacing:.2em;
  background:linear-gradient(90deg,var(--red) 0%,var(--white) 50%,var(--red) 100%);
  background-size:200% auto;
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  animation:shimmer 1.4s linear infinite;
}
@keyframes shimmer{to{background-position:200% center;}}
.loader-bar-wrap{width:160px;height:1px;background:#222;overflow:hidden;}
.loader-bar{height:1px;background:var(--red);width:0;animation:lbar 1.6s ease forwards;}
@keyframes lbar{to{width:100%;}}

/* ─────────────────────────────────────────
   TOP ALERT TICKER
───────────────────────────────────────── */
.alert-bar{background:var(--red);overflow:hidden;white-space:nowrap;padding:.5rem 0;position:relative;z-index:600;}
.alert-track{display:inline-flex;gap:0;animation:slide 20s linear infinite;}
.alert-bar:hover .alert-track{animation-play-state:paused;}
.alert-item{
  font-family:var(--A);font-size:.75rem;letter-spacing:.22em;text-transform:uppercase;
  color:var(--white);padding:0 2.5rem;display:flex;align-items:center;gap:.8rem;
}
.alert-star{color:var(--yellow);font-size:.65rem;}
@keyframes slide{0%{transform:translateX(0);}100%{transform:translateX(-50%);}}

/* ─────────────────────────────────────────
   NAV
───────────────────────────────────────── */
.nav{
  position:fixed;top:1.9rem;left:0;right:0;z-index:500;
  display:flex;align-items:center;justify-content:space-between;
  padding:0 4rem;
  transition:top .3s,padding .3s,background .3s,backdrop-filter .3s;
}
.nav.pinned{
  top:0;padding:1rem 4rem;
  background:rgba(5,5,5,.96);
  backdrop-filter:blur(16px);
  border-bottom:1px solid #1c1c1c;
}
.nav-logo{display:block;text-decoration:none;}
.nav-logo img{height:36px;filter:brightness(0) invert(1);display:block;transition:filter .3s;}
.nav-logo:hover img{filter:brightness(0) saturate(100%) invert(17%) sepia(99%) saturate(7414%) hue-rotate(1deg) brightness(96%) contrast(116%);}
.nav-links{display:flex;list-style:none;gap:3rem;}
.nav-links a{
  font-family:var(--U);font-size:.58rem;font-weight:700;letter-spacing:.22em;text-transform:uppercase;
  color:var(--muted);text-decoration:none;transition:color .2s;position:relative;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-.4rem;left:0;right:0;
  height:1px;background:var(--red);
  transform:scaleX(0);transform-origin:left;
  transition:transform .25s cubic-bezier(.77,0,.18,1);
}
.nav-links a:hover{color:var(--white);}
.nav-links a:hover::after,.nav-links a.active::after{transform:scaleX(1);}
.nav-links a.active{color:var(--white);}
.nav-cta{
  font-family:var(--U);font-size:.58rem;font-weight:900;letter-spacing:.16em;text-transform:uppercase;
  color:var(--black);background:var(--white);
  padding:.7rem 1.8rem;text-decoration:none;
  transition:background .2s,color .2s,transform .15s;display:inline-block;
}
.nav-cta:hover{background:var(--red);color:var(--white);transform:translateY(-1px);}

/* ─────────────────────────────────────────
   HERO
───────────────────────────────────────── */
.hero{
  min-height:100svh;
  display:grid;grid-template-rows:1fr auto;
  position:relative;overflow:hidden;padding-top:3rem;
}
.hero-bg{
  position:absolute;inset:0;
  background:
    repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(209,0,0,.04) 79px,rgba(209,0,0,.04) 80px),
    repeating-linear-gradient(90deg,transparent,transparent 79px,rgba(209,0,0,.04) 79px,rgba(209,0,0,.04) 80px);
  animation:bgdrift 30s linear infinite;
}
@keyframes bgdrift{to{background-position:80px 80px;}}
.hero-glow{
  position:absolute;width:700px;height:700px;
  background:radial-gradient(circle,rgba(209,0,0,.14) 0%,transparent 65%);
  top:50%;right:-100px;transform:translateY(-50%);
  pointer-events:none;animation:glowPulse 4s ease-in-out infinite;
}
@keyframes glowPulse{0%,100%{opacity:.7;transform:translateY(-50%) scale(1);}50%{opacity:1;transform:translateY(-50%) scale(1.08);}}
.hero-content{
  display:grid;grid-template-columns:1fr 1fr;
  align-items:center;padding:6rem 4rem 2rem;
  position:relative;z-index:2;gap:3rem;
}
.hero-left{display:flex;flex-direction:column;gap:2rem;}
.hero-eye{
  display:flex;align-items:center;gap:.8rem;
  font-family:var(--U);font-size:.55rem;font-weight:700;
  letter-spacing:.3em;text-transform:uppercase;color:var(--red);
  opacity:0;animation:riseUp .6s .3s forwards;
}
.hero-eye-star{font-size:.7rem;animation:spinStar 4s linear infinite;}
@keyframes spinStar{to{transform:rotate(360deg);}}
@keyframes riseUp{from{opacity:0;transform:translateY(20px);}to{opacity:1;transform:translateY(0);}}
.hero-h1{
  font-family:var(--A);font-size:clamp(5rem,9vw,9rem);
  line-height:.9;letter-spacing:.02em;text-transform:uppercase;
  opacity:0;animation:riseUp .7s .5s forwards;
}
.hero-h1 .line-white{color:var(--white);display:block;}
.hero-h1 .line-red{color:var(--red);display:block;}
.hero-h1 .line-stroke{-webkit-text-stroke:2px var(--white);color:transparent;display:block;}
.hero-sub{
  font-family:var(--I);font-style:italic;font-size:1.1rem;
  color:rgba(245,240,232,.55);line-height:1.8;max-width:380px;
  opacity:0;animation:riseUp .7s .7s forwards;
}
.hero-motto{
  font-family:var(--U);font-size:.58rem;font-weight:700;
  letter-spacing:.18em;text-transform:uppercase;color:var(--muted);
  border-left:3px solid var(--red);padding-left:1.2rem;
  opacity:0;animation:riseUp .7s .85s forwards;
}
.hero-actions{display:flex;align-items:center;gap:2rem;opacity:0;animation:riseUp .7s 1s forwards;}
.cta-primary{
  font-family:var(--U);font-size:.62rem;font-weight:900;
  letter-spacing:.16em;text-transform:uppercase;
  color:var(--black);background:var(--white);
  padding:1.1rem 2.8rem;text-decoration:none;
  display:inline-block;position:relative;overflow:hidden;transition:transform .2s;
}
.cta-primary::before{
  content:'';position:absolute;inset:0;background:var(--red);
  transform:translateY(100%);transition:transform .35s cubic-bezier(.77,0,.18,1);
}
.cta-primary:hover::before{transform:translateY(0);}
.cta-primary span{position:relative;z-index:1;transition:color .35s;}
.cta-primary:hover span{color:var(--white);}
.cta-primary:hover{transform:translateY(-2px);}
.cta-ghost{
  font-family:var(--U);font-size:.58rem;font-weight:700;
  letter-spacing:.16em;text-transform:uppercase;
  color:var(--muted);text-decoration:none;
  display:flex;align-items:center;gap:.6rem;transition:color .2s;
}
.cta-ghost svg{transition:transform .2s;}
.cta-ghost:hover{color:var(--white);}
.cta-ghost:hover svg{transform:translateX(5px);}
.hero-right{
  position:relative;display:flex;align-items:center;justify-content:center;
  min-height:560px;
}
.hero-product-img{
  position:relative;z-index:3;width:85%;max-width:460px;
  filter:drop-shadow(0 30px 80px rgba(209,0,0,.5));
  animation:heroFloat 7s ease-in-out infinite,riseUp .9s .4s both;
  transform-origin:center;
}
@keyframes heroFloat{0%,100%{transform:translateY(0) rotate(0deg);}33%{transform:translateY(-12px) rotate(.4deg);}66%{transform:translateY(-6px) rotate(-.3deg);}}
.hero-star-bg{
  position:absolute;font-size:28rem;
  color:rgba(209,0,0,.07);
  animation:heroStarSpin 40s linear infinite;
  z-index:1;line-height:1;text-shadow:0 0 100px rgba(209,0,0,.15);
}
@keyframes heroStarSpin{to{transform:rotate(360deg);}}
.orbit{
  position:absolute;width:440px;height:440px;
  border:1px solid rgba(209,0,0,.1);border-radius:50%;
  animation:orbit 25s linear infinite;z-index:2;
}
.orbit::before{
  content:'★';font-size:.85rem;color:var(--red);
  position:absolute;top:-10px;left:50%;transform:translateX(-50%);
  text-shadow:0 0 12px var(--red);
}
.orbit.o2{width:320px;height:320px;border-style:dashed;border-color:rgba(209,0,0,.07);animation-duration:18s;animation-direction:reverse;}
.orbit.o2::before{content:'✦';bottom:-10px;top:auto;left:25%;}
.orbit.o3{width:560px;height:560px;border-color:rgba(209,0,0,.05);animation-duration:40s;}
.orbit.o3::before{content:'★';bottom:-10px;top:auto;left:70%;}
@keyframes orbit{to{transform:rotate(360deg);}}
.hero-scroll{
  position:absolute;bottom:2.5rem;left:4rem;z-index:5;
  display:flex;align-items:center;gap:.8rem;
  opacity:0;animation:riseUp .6s 1.4s forwards;
}
.scroll-line{width:40px;height:1px;background:linear-gradient(to right,var(--red),transparent);position:relative;overflow:hidden;}
.scroll-line::after{content:'';position:absolute;top:0;left:-100%;width:100%;height:1px;background:var(--white);animation:scanLine 2s ease-in-out infinite;}
@keyframes scanLine{to{left:100%;}}
.scroll-txt{font-family:var(--U);font-size:.5rem;font-weight:700;letter-spacing:.25em;color:var(--muted);}
.hero-bottom{
  display:flex;justify-content:space-between;align-items:center;
  padding:1.5rem 4rem;border-top:1px solid #1c1c1c;
  position:relative;z-index:2;
}
.hero-stat{text-align:center;}
.hero-stat-n{font-family:var(--A);font-size:2rem;color:var(--red);display:block;line-height:1;}
.hero-stat-l{font-family:var(--U);font-size:.46rem;font-weight:700;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);margin-top:.3rem;display:block;}
.hero-divider{width:1px;height:40px;background:#1c1c1c;}

/* ─────────────────────────────────────────
   TICKERS
───────────────────────────────────────── */
.motto-ticker{background:var(--red);padding:.9rem 0;overflow:hidden;white-space:nowrap;}
.motto-track{display:inline-flex;animation:slide 28s linear infinite;}
.motto-item{
  font-family:var(--A);font-size:.82rem;letter-spacing:.2em;text-transform:uppercase;
  color:var(--white);padding:0 2.2rem;display:flex;align-items:center;gap:1rem;
}
.motto-sep{color:rgba(255,255,255,.3);font-size:.5rem;}

/* ─────────────────────────────────────────
   SECTION UTILS
───────────────────────────────────────── */
.sec{padding:6rem 4rem;}
.sec-eye{
  font-family:var(--U);font-size:.52rem;font-weight:700;
  letter-spacing:.28em;text-transform:uppercase;color:var(--red);
  display:flex;align-items:center;gap:.7rem;margin-bottom:1.2rem;
}
.sec-eye::before{content:'★';font-size:.6rem;}
.sec-h2{
  font-family:var(--A);font-size:clamp(3rem,6vw,6rem);
  line-height:.88;letter-spacing:.03em;text-transform:uppercase;margin-bottom:3rem;
}
.sec-h2 .stroke{-webkit-text-stroke:1.5px var(--white);color:transparent;}
.sec-h2 .red{color:var(--red);}
.rv{opacity:0;transform:translateY(36px);transition:opacity .75s ease,transform .75s ease;}
.rv.on{opacity:1;transform:none;}

/* ─────────────────────────────────────────
   SHOP — FULL CATALOG GRID
───────────────────────────────────────── */
.shop-sec{background:var(--black);padding:6rem 0 0;}
.shop-header{
  padding:0 4rem 4rem;
  display:flex;justify-content:space-between;align-items:flex-end;
}
/* Filter bar */
.shop-filters{
  display:flex;align-items:center;gap:.5rem;
  padding:0 4rem 3rem;
  overflow-x:auto;
}
.sf{
  font-family:var(--U);font-size:.5rem;font-weight:700;
  letter-spacing:.16em;text-transform:uppercase;
  background:transparent;border:1px solid #2a2a2a;color:var(--muted);
  padding:.55rem 1.2rem;cursor:pointer;
  transition:border-color .2s,color .2s,background .2s;
  white-space:nowrap;
}
.sf:hover,.sf.active{border-color:var(--red);color:var(--white);background:rgba(209,0,0,.06);}
/* Main hero product — tall feature */
.shop-feature{
  display:grid;grid-template-columns:1.6fr 1fr;
  gap:2px;background:#111;
  margin-bottom:2px;
}
/* Catalog grid — 3 col */
.catalog-grid{
  display:grid;grid-template-columns:repeat(3,1fr);
  gap:2px;background:#111;
}
/* Product card */
.pc{
  position:relative;overflow:hidden;
  background:var(--black);
  display:flex;flex-direction:column;justify-content:flex-end;
  text-decoration:none;color:inherit;
  min-height:480px;
}
.pc.tall{min-height:680px;}
.pc.feature-tall{min-height:760px;}
.pc-img{position:absolute;inset:0;overflow:hidden;}
.pc-img img{
  width:100%;height:100%;object-fit:cover;
  filter:grayscale(8%) contrast(1.1) brightness(.85);
  transition:transform .8s cubic-bezier(.25,.46,.45,.94),filter .5s;
}
.pc:hover .pc-img img{transform:scale(1.06);filter:grayscale(0%) contrast(1.12) brightness(.92);}
.pc-fade{
  position:absolute;inset:0;
  background:linear-gradient(to top,rgba(5,5,5,1) 0%,rgba(5,5,5,.75) 28%,rgba(5,5,5,.15) 60%,transparent 100%);
  z-index:2;
}
.pc-info{position:relative;z-index:3;padding:2.5rem;}
.pc-tag{
  font-family:var(--U);font-size:.48rem;font-weight:700;
  letter-spacing:.24em;text-transform:uppercase;color:var(--red);
  margin-bottom:.6rem;display:flex;align-items:center;gap:.5rem;
}
.pc-tag::before{content:'★';font-size:.5rem;}
.pc-name{font-family:var(--A);font-size:clamp(2rem,3.5vw,3.2rem);letter-spacing:.04em;margin-bottom:.5rem;line-height:.9;}
.pc-desc{font-family:var(--I);font-style:italic;font-size:.95rem;color:rgba(245,240,232,.45);margin-bottom:1.4rem;line-height:1.6;}
.pc-price{font-family:var(--U);font-size:.55rem;font-weight:700;letter-spacing:.16em;color:var(--muted);}
.pc-cta{
  position:absolute;bottom:2.5rem;right:2.5rem;z-index:4;
  font-family:var(--U);font-size:.52rem;font-weight:900;
  letter-spacing:.16em;text-transform:uppercase;
  background:var(--white);color:var(--black);
  padding:.6rem 1.4rem;
  opacity:0;transform:translateY(8px);
  transition:opacity .3s,transform .3s,background .2s;
  text-decoration:none;
}
.pc:hover .pc-cta{opacity:1;transform:translateY(0);}
.pc-cta:hover{background:var(--red);color:var(--white);}
.pc-badge{
  position:absolute;top:1.8rem;left:1.8rem;z-index:4;
  font-family:var(--U);font-size:.48rem;font-weight:900;
  letter-spacing:.16em;text-transform:uppercase;
  padding:.35rem .9rem;
}
.pc-badge.r{background:var(--red);color:var(--white);}
.pc-badge.y{background:var(--yellow);color:var(--black);}
.pc-badge.w{background:var(--white);color:var(--black);}
.pc-star{
  position:absolute;top:1.8rem;right:1.8rem;z-index:4;
  font-size:1.1rem;color:var(--red);
  text-shadow:0 0 12px var(--red);
  animation:starBeat 2.5s ease-in-out infinite;
}
@keyframes starBeat{0%,100%{opacity:.4;transform:scale(.8);}50%{opacity:1;transform:scale(1.1);}}
/* Image placeholder fallback style */
.pc-ph{
  position:absolute;inset:0;
  background:#0c0c0c;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:1rem;
  border:1px dashed #252525;
}
.pc-ph-icon{font-size:3.5rem;opacity:.12;}
.pc-ph-text{
  font-family:var(--A);font-size:.65rem;letter-spacing:.2em;
  color:#cc0000;text-align:center;line-height:1.8;opacity:.7;
}

/* ─────────────────────────────────────────
   MARQUEE
───────────────────────────────────────── */
.marquee-sec{
  overflow:hidden;white-space:nowrap;padding:2rem 0;
  border-top:1px solid #1c1c1c;border-bottom:1px solid #1c1c1c;
  background:var(--black);
}
.marquee-track{display:inline-flex;gap:0;animation:slide 35s linear infinite;}
.mq-item{
  font-family:var(--A);font-size:clamp(3rem,5vw,5rem);
  letter-spacing:.04em;text-transform:uppercase;
  padding:0 1.5rem;display:flex;align-items:center;gap:1.5rem;
}
.mq-item.solid{color:var(--white);}
.mq-item.hollow{-webkit-text-stroke:1px rgba(245,240,232,.3);color:transparent;}
.mq-item.red{color:var(--red);}
.mq-star{font-size:2rem;color:var(--red);animation:spinStar 5s linear infinite;}

/* ─────────────────────────────────────────
   STATEMENT
───────────────────────────────────────── */
.statement-sec{
  background:var(--red);padding:7rem 4rem;
  position:relative;overflow:hidden;
  display:flex;flex-direction:column;align-items:center;text-align:center;
}
.statement-sec::before{
  content:'★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★';
  position:absolute;top:0;left:0;right:0;
  font-size:1rem;letter-spacing:2.5rem;
  color:rgba(255,255,255,.08);padding:1rem 2rem;
  line-height:2;pointer-events:none;
}
.statement-sec::after{
  content:'★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★';
  position:absolute;bottom:0;left:0;right:0;
  font-size:1rem;letter-spacing:2.5rem;
  color:rgba(255,255,255,.08);padding:1rem 2rem;
  line-height:2;pointer-events:none;
}
.stmt-kicker{font-family:var(--U);font-size:.55rem;font-weight:700;letter-spacing:.3em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:2.5rem;}
.stmt-h{
  font-family:var(--A);font-size:clamp(4rem,8vw,8rem);
  line-height:.88;letter-spacing:.02em;text-transform:uppercase;
  color:var(--white);max-width:900px;position:relative;z-index:1;
}
.stmt-h .yellow{color:var(--yellow);}
.stmt-h .stroke{-webkit-text-stroke:2px var(--white);color:transparent;}
.stmt-sub{font-family:var(--I);font-style:italic;font-size:1.1rem;color:rgba(255,255,255,.6);margin-top:2.5rem;line-height:1.9;max-width:480px;position:relative;z-index:1;}
.stmt-btns{display:flex;gap:1.5rem;margin-top:3rem;position:relative;z-index:1;}
.btn-black{
  font-family:var(--U);font-size:.6rem;font-weight:900;letter-spacing:.16em;text-transform:uppercase;
  background:var(--black);color:var(--white);padding:1.1rem 2.8rem;text-decoration:none;
  transition:background .2s,transform .15s;display:inline-block;
}
.btn-black:hover{background:#111;transform:translateY(-2px);}
.btn-outline-w{
  font-family:var(--U);font-size:.6rem;font-weight:900;letter-spacing:.16em;text-transform:uppercase;
  color:rgba(255,255,255,.6);border:1px solid rgba(255,255,255,.3);
  padding:1.1rem 2.8rem;text-decoration:none;
  transition:border-color .2s,color .2s;display:inline-block;
}
.btn-outline-w:hover{border-color:var(--white);color:var(--white);}

/* ─────────────────────────────────────────
   MANTRAS GRID
───────────────────────────────────────── */
.mantras-sec{background:var(--black);padding:6rem 0;}
.mantras-header{padding:0 4rem 4rem;}
.mantras-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1px;background:#111;}
.mg{
  background:var(--black);padding:2.8rem 2.2rem;
  position:relative;overflow:hidden;transition:background .3s;cursor:default;
}
.mg::after{
  content:'';position:absolute;bottom:0;left:0;right:0;height:2px;
  background:var(--red);transform:scaleX(0);transform-origin:left;
  transition:transform .4s cubic-bezier(.77,0,.18,1);
}
.mg:hover{background:#0e0e0e;}
.mg:hover::after{transform:scaleX(1);}
.mg-star{font-size:1.3rem;color:var(--red);margin-bottom:1.2rem;display:block;opacity:.6;transition:opacity .3s;text-shadow:0 0 8px rgba(209,0,0,.5);}
.mg:hover .mg-star{opacity:1;}
.mg-text{font-family:var(--A);font-size:1.1rem;letter-spacing:.04em;line-height:1.25;color:rgba(245,240,232,.7);transition:color .3s;}
.mg:hover .mg-text{color:var(--white);}

/* ─────────────────────────────────────────
   ABOUT — FULL PAGE SECTION
───────────────────────────────────────── */
.about-hero{
  background:var(--black);
  min-height:100svh;
  display:grid;grid-template-columns:1fr 1fr;
  position:relative;overflow:hidden;
}
.about-hero-img{
  position:relative;overflow:hidden;
}
.about-hero-img img{
  width:100%;height:100%;object-fit:cover;
  filter:grayscale(20%) contrast(1.1) brightness(.7);
  transition:transform .8s ease;
}
.about-hero:hover .about-hero-img img{transform:scale(1.02);}
.about-hero-overlay{
  position:absolute;inset:0;
  background:linear-gradient(to right,transparent 55%,var(--black) 100%);
}
.about-body{
  display:flex;flex-direction:column;justify-content:center;
  padding:8rem 5rem 5rem;
  position:relative;z-index:2;
}
.about-h{
  font-family:var(--A);font-size:clamp(3.5rem,5.5vw,5.5rem);
  line-height:.88;letter-spacing:.03em;margin-bottom:2.5rem;
}
.about-h .red{color:var(--red);}
.about-h .stroke{-webkit-text-stroke:1.5px var(--white);color:transparent;}
.about-p{
  font-family:var(--I);font-style:italic;
  font-size:1.05rem;color:rgba(245,240,232,.55);
  line-height:2.1;margin-bottom:2rem;max-width:460px;
}
.about-motto{
  font-family:var(--U);font-size:.58rem;font-weight:700;
  letter-spacing:.16em;text-transform:uppercase;color:var(--muted);
  border-left:3px solid var(--red);padding-left:1.2rem;margin-bottom:2.5rem;
}
/* Values grid */
.about-values{
  display:grid;grid-template-columns:repeat(3,1fr);
  gap:1px;background:#111;margin-top:0;
}
.av{
  background:var(--grey);padding:3rem 2.5rem;
  position:relative;overflow:hidden;
  transition:background .3s;
}
.av::before{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
  background:var(--red);transform:scaleX(0);transform-origin:left;
  transition:transform .5s cubic-bezier(.77,0,.18,1);
}
.av:hover{background:#0e0e0e;}
.av:hover::before{transform:scaleX(1);}
.av-num{
  font-family:var(--A);font-size:4rem;color:rgba(209,0,0,.15);
  line-height:1;margin-bottom:1.2rem;display:block;
  transition:color .3s;
}
.av:hover .av-num{color:rgba(209,0,0,.35);}
.av-title{
  font-family:var(--A);font-size:1.6rem;letter-spacing:.04em;
  margin-bottom:.8rem;line-height:1;
}
.av-text{
  font-family:var(--I);font-style:italic;
  font-size:.95rem;color:rgba(245,240,232,.45);line-height:1.8;
}
/* Founder quote */
.founder-quote{
  background:var(--red);padding:6rem 4rem;
  position:relative;overflow:hidden;
  display:flex;flex-direction:column;align-items:flex-start;
}
.founder-quote::after{
  content:'❝';font-family:var(--A);font-size:25rem;
  color:rgba(255,255,255,.05);
  position:absolute;right:-2rem;top:-4rem;
  line-height:1;pointer-events:none;
}
.fq-kicker{font-family:var(--U);font-size:.52rem;font-weight:700;letter-spacing:.3em;text-transform:uppercase;color:rgba(255,255,255,.45);margin-bottom:2rem;}
.fq-text{
  font-family:var(--A);font-size:clamp(1.8rem,3.5vw,3.5rem);
  line-height:1.15;letter-spacing:.02em;max-width:800px;
  position:relative;z-index:1;
}
.fq-attr{
  font-family:var(--I);font-style:italic;
  font-size:1rem;color:rgba(255,255,255,.5);
  margin-top:2.5rem;position:relative;z-index:1;
}

/* ─────────────────────────────────────────
   CONTACT — FULL SECTION
───────────────────────────────────────── */
.contact-hero{
  background:var(--grey);
  display:grid;grid-template-columns:1fr 1fr;
  min-height:70vh;
}
.contact-left{
  padding:6rem 5rem;
  display:flex;flex-direction:column;justify-content:center;
  border-right:1px solid #222;
}
.contact-right{
  padding:6rem 5rem;
  display:flex;flex-direction:column;justify-content:center;
  background:var(--black);
}
.contact-h{
  font-family:var(--A);font-size:clamp(3rem,5vw,5.5rem);
  line-height:.88;letter-spacing:.03em;margin-bottom:2rem;
}
.contact-h .red{color:var(--red);}
.contact-h .stroke{-webkit-text-stroke:1.5px var(--white);color:transparent;}
.contact-sub{
  font-family:var(--I);font-style:italic;
  font-size:1.05rem;color:rgba(245,240,232,.45);
  line-height:2;margin-bottom:3rem;max-width:380px;
}
.contact-items{display:flex;flex-direction:column;gap:1px;background:#1c1c1c;}
.ci{
  background:var(--grey);display:flex;align-items:center;gap:1.5rem;
  padding:2rem 2.2rem;text-decoration:none;color:inherit;
  position:relative;overflow:hidden;transition:background .2s;
}
.ci::before{
  content:'';position:absolute;left:0;top:0;bottom:0;width:2px;
  background:var(--red);transform:scaleY(0);transform-origin:bottom;
  transition:transform .3s cubic-bezier(.77,0,.18,1);
}
.ci:hover{background:#0d0d0d;}
.ci:hover::before{transform:scaleY(1);}
.ci-icon{font-size:1.2rem;width:44px;height:44px;border:1px solid #2a2a2a;display:grid;place-items:center;flex-shrink:0;transition:border-color .2s;}
.ci:hover .ci-icon{border-color:var(--red);}
.ci-label{font-family:var(--U);font-size:.5rem;font-weight:700;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);margin-bottom:.4rem;}
.ci-val{font-family:var(--I);font-size:1rem;color:var(--white);}
/* Order form */
.order-form{display:flex;flex-direction:column;gap:1.2rem;}
.of-h{font-family:var(--A);font-size:2.2rem;letter-spacing:.04em;margin-bottom:.5rem;}
.of-sub{font-family:var(--I);font-style:italic;font-size:.95rem;color:rgba(245,240,232,.4);line-height:1.8;margin-bottom:1.5rem;}
.of-input,.of-select,.of-textarea{
  background:#0e0e0e;border:1px solid #1c1c1c;
  color:var(--white);font-family:var(--I);font-style:italic;font-size:1rem;
  padding:1rem 1.4rem;outline:none;
  transition:border-color .2s;width:100%;
}
.of-input:focus,.of-select:focus,.of-textarea:focus{border-color:var(--red);}
.of-input::placeholder,.of-textarea::placeholder{color:var(--muted);}
.of-select{appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath d='M2 4l4 4 4-4' stroke='%23666' stroke-width='1.5' fill='none'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 1.2rem center;}
.of-textarea{resize:vertical;min-height:120px;font-style:italic;}
.of-row{display:grid;grid-template-columns:1fr 1fr;gap:1rem;}

/* ─────────────────────────────────────────
   CONTACT STRIP (HOME)
───────────────────────────────────────── */
.contact-strip{
  background:var(--black);padding:6rem 4rem;
  display:grid;grid-template-columns:1fr 1fr;
  gap:6rem;align-items:start;border-top:1px solid #1c1c1c;
}
.nl-form{display:flex;flex-direction:column;gap:1.2rem;}
.nl-input{
  background:#0e0e0e;border:1px solid #1c1c1c;
  color:var(--white);font-family:var(--I);font-style:italic;font-size:1rem;
  padding:1rem 1.4rem;outline:none;transition:border-color .2s;width:100%;
}
.nl-input:focus{border-color:var(--red);}
.nl-input::placeholder{color:var(--muted);}
.nl-check{display:flex;align-items:flex-start;gap:.8rem;font-family:var(--I);font-style:italic;font-size:.9rem;color:var(--muted);line-height:1.6;cursor:pointer;}
.nl-check input{width:15px;height:15px;flex-shrink:0;margin-top:3px;accent-color:var(--red);}

/* ─────────────────────────────────────────
   FOOTER
───────────────────────────────────────── */
footer{background:#050505;border-top:1px solid #111;position:relative;}
footer::before{content:'';display:block;height:2px;background:linear-gradient(90deg,transparent,var(--red),transparent);}
.foot-inner{display:grid;grid-template-columns:1.8fr 1fr 1fr 1fr;gap:3rem;padding:4.5rem 4rem;border-bottom:1px solid #111;}
.foot-logo img{height:42px;filter:brightness(0) invert(1);margin-bottom:1.8rem;display:block;}
.foot-bio{font-family:var(--I);font-style:italic;font-size:.9rem;color:var(--muted);line-height:1.8;max-width:240px;}
.foot-col-title{font-family:var(--U);font-size:.5rem;font-weight:700;letter-spacing:.24em;text-transform:uppercase;color:#333;margin-bottom:1.5rem;}
.foot-links{display:flex;flex-direction:column;gap:.9rem;}
.foot-links a{font-family:var(--U);font-size:.55rem;font-weight:400;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);text-decoration:none;transition:color .2s;}
.foot-links a:hover{color:var(--red);}
.foot-bottom{display:flex;justify-content:space-between;align-items:center;padding:1.8rem 4rem;flex-wrap:wrap;gap:1rem;}
.foot-copy{font-family:var(--U);font-size:.5rem;font-weight:400;letter-spacing:.14em;color:#333;}
.foot-tag{font-family:var(--A);font-size:1.1rem;letter-spacing:.1em;color:#222;}
.foot-tag span{color:var(--red);}

/* ─────────────────────────────────────────
   RESPONSIVE
───────────────────────────────────────── */
@media(max-width:1024px){
  .nav{padding:0 2rem;}
  .nav.pinned{padding:1rem 2rem;}
  .hero-content{grid-template-columns:1fr;padding:6rem 2rem 2rem;}
  .hero-right{display:none;}
  .hero-bottom{padding:1.5rem 2rem;}
  .shop-header{padding:0 2rem 3rem;}
  .shop-filters{padding:0 2rem 2rem;}
  .shop-feature{grid-template-columns:1fr;}
  .catalog-grid{grid-template-columns:1fr 1fr;}
  .about-hero{grid-template-columns:1fr;}
  .about-hero-img{display:none;}
  .about-body{padding:5rem 2rem;}
  .about-values{grid-template-columns:1fr;}
  .contact-hero{grid-template-columns:1fr;}
  .contact-right{padding:4rem 2rem;}
  .contact-left{padding:4rem 2rem;}
  .contact-strip{grid-template-columns:1fr;gap:3rem;padding:5rem 2rem;}
  .mantras-grid{grid-template-columns:1fr 1fr;}
  .mantras-header{padding:0 2rem 3rem;}
  .statement-sec{padding:5rem 2rem;}
  .foot-inner{grid-template-columns:1fr 1fr;padding:3rem 2rem;}
  .foot-bottom{padding:1.5rem 2rem;}
  .founder-quote{padding:4rem 2rem;}
  .of-row{grid-template-columns:1fr;}
}
</style>
</head>
<body>

<!-- CURSOR -->
<div id="kk-cursor"></div>

<!-- LOADER -->
<div id="loader">
  <div class="loader-inner">
    <div class="loader-star">★</div>
    <div class="loader-word">KRAZ KIWI</div>
    <div class="loader-bar-wrap"><div class="loader-bar"></div></div>
  </div>
</div>

<!-- ALERT BAR -->
<div class="alert-bar">
  <div class="alert-track">
    <div class="alert-item"><span class="alert-star">★</span> New Collection — SS 2026 <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> Limited Drops — Order Before They're Gone <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> WhatsApp: 076 646 1594 <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> Born From The Ashes Of Defiance <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> New Collection — SS 2026 <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> Limited Drops — Order Before They're Gone <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> WhatsApp: 076 646 1594 <span class="alert-star">★</span></div>
    <div class="alert-item"><span class="alert-star">★</span> Born From The Ashes Of Defiance <span class="alert-star">★</span></div>
  </div>
</div>

<!-- NAV -->
<nav class="nav" id="nav">
  <a href="#home" class="nav-logo" onclick="showSection('home')">
    <!-- ═══ LOGO IMAGE ═══ -->
    <!-- src="photos/kraz-kiwi-logo.png" — use your actual logo file -->
    <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/published/untitled707-20260224120111.png?1771927737" alt="Kraz Kiwi">
  </a>
  <ul class="nav-links">
    <li><a href="#home" onclick="showSection('home')" class="nav-link active" data-section="home">Home</a></li>
    <li><a href="#shop" onclick="showSection('shop')" class="nav-link" data-section="shop">Shop</a></li>
    <li><a href="#about" onclick="showSection('about')" class="nav-link" data-section="about">About</a></li>
    <li><a href="#updates" class="nav-link">Updates</a></li>
    <li><a href="#contact" onclick="showSection('contact')" class="nav-link" data-section="contact">Contact</a></li>
  </ul>
  <a href="#shop" onclick="showSection('shop')" class="nav-cta">★ Shop Now</a>
</nav>

<!-- ═══════════════════════════════════════════════════
     HOME SECTION
═══════════════════════════════════════════════════ -->
<div id="section-home">

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-glow"></div>
  <div class="hero-content">
    <div class="hero-left">
      <div class="hero-eye"><span class="hero-eye-star">★</span>New Collection — SS 2026</div>
      <h1 class="hero-h1">
        <span class="line-white">OUT</span>
        <span class="line-red">WORK</span>
        <span class="line-stroke">YOUR</span>
        <span class="line-white">PAST.</span>
      </h1>
      <p class="hero-sub">Born from collapse. Built for those who chose risk over routine. When you wear this — rooms change.</p>
      <div class="hero-motto"><span>★</span> Risen from pressure. Built for confidence.</div>
      <div class="hero-actions">
        <a href="#shop" onclick="showSection('shop')" class="cta-primary"><span>★ Shop the Collection</span></a>
        <a href="#about" onclick="showSection('about')" class="cta-ghost">
          Our Story
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></svg>
        </a>
      </div>
    </div>
    <div class="hero-right">
      <div class="hero-star-bg">★</div>
      <div class="orbit o3"></div>
      <div class="orbit o2"></div>
      <div class="orbit"></div>
      <!-- ═══ HERO LOGO / PRODUCT IMAGE ═══ -->
      <!-- Swap src to a product or brand image: src="photos/hero-feature.jpg" -->
      <img class="hero-product-img"
        src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/published/untitled711-20260224120058.png?1771929889"
        alt="Kraz Kiwi">
    </div>
  </div>
  <div class="hero-bottom">
    <div class="hero-stat"><span class="hero-stat-n">★</span><span class="hero-stat-l">Born Defiant</span></div>
    <div class="hero-divider"></div>
    <div class="hero-stat"><span class="hero-stat-n">9</span><span class="hero-stat-l">Pieces Dropped</span></div>
    <div class="hero-divider"></div>
    <div class="hero-stat"><span class="hero-stat-n">100%</span><span class="hero-stat-l">No Limits</span></div>
    <div class="hero-divider"></div>
    <div class="hero-stat"><span class="hero-stat-n">∞</span><span class="hero-stat-l">Rising Still</span></div>
  </div>
  <div class="hero-scroll"><div class="scroll-line"></div><span class="scroll-txt">★ Scroll</span></div>
</section>

<!-- MOTTO TICKER -->
<div class="motto-ticker">
  <div class="motto-track">
    <div class="motto-item">★ Outwork Your Past <span class="motto-sep">◆</span></div>
    <div class="motto-item">Become Proof That Limits Can Be Broken <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Outlast Doubt, Outwork Fear <span class="motto-sep">◆</span></div>
    <div class="motto-item">Pressure Creates Diamonds <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ You Were Not Built To Stay Small <span class="motto-sep">◆</span></div>
    <div class="motto-item">Rise Anyway <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Become Undeniable <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Outwork Your Past <span class="motto-sep">◆</span></div>
    <div class="motto-item">Become Proof That Limits Can Be Broken <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Outlast Doubt, Outwork Fear <span class="motto-sep">◆</span></div>
    <div class="motto-item">Pressure Creates Diamonds <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ You Were Not Built To Stay Small <span class="motto-sep">◆</span></div>
    <div class="motto-item">Rise Anyway <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Become Undeniable <span class="motto-sep">◆</span></div>
  </div>
</div>

<!-- FEATURED PRODUCTS (HOME PREVIEW) -->
<section class="shop-sec rv">
  <div class="shop-header">
    <div>
      <div class="sec-eye">Featured Drops</div>
      <h2 class="sec-h2">THE <span class="red">DROP</span>.<br><span class="stroke">SS 2026</span></h2>
    </div>
    <a href="#shop" onclick="showSection('shop')" class="cta-ghost" style="align-self:flex-end;">
      Full Catalog
      <svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></svg>
    </a>
  </div>
  <div class="shop-feature">
    <!-- FEATURED — LOST SOULS (TALL HERO CARD) -->
    <a href="#shop" onclick="showSection('shop')" class="pc feature-tall rv" style="transition-delay:.1s">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             LOST SOULS PIECE — INSERT PHOTO HERE
             File suggestion: photos/lost-souls-piece.jpg
             Original on Weebly: picsart-26-02-24-12-39-15-523_orig.png
        ═══════════════════════════════════════════════ -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/picsart-26-02-24-12-39-15-523_orig.png"
          alt="Lost Souls Piece"
          onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>LOST SOULS PIECE<br>INSERT PHOTO HERE<br>photos/lost-souls-piece.jpg</div></div>'">
      </div>
      <div class="pc-star">★</div>
      <div class="pc-badge r">★ New Drop</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Signature Collection</div>
        <div class="pc-name">Lost Souls<br>Piece</div>
        <div class="pc-desc">Exactly where you need to be.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <a href="#contact" onclick="showSection('contact')" class="pc-cta">★ Order Now</a>
    </a>
    <!-- RIGHT COLUMN — 2 stacked -->
    <div style="display:grid;grid-template-rows:1fr 1fr;gap:2px;background:#111;">
      <!-- HIGH ROLLER PIECE -->
      <a href="#shop" onclick="showSection('shop')" class="pc rv" style="transition-delay:.2s">
        <div class="pc-img">
          <!-- ═══════════════════════════════════════════════
               HIGH ROLLER PIECE — INSERT PHOTO HERE
               File suggestion: photos/high-roller-piece.jpg
               Original on Weebly: photoroom-20260223-110432_orig.png
          ═══════════════════════════════════════════════ -->
          <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/photoroom-20260223-110432_orig.png"
            alt="High Roller Piece"
            onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>HIGH ROLLER PIECE<br>photos/high-roller-piece.jpg</div></div>'">
        </div>
        <div class="pc-badge y">★ Hot</div>
        <div class="pc-fade"></div>
        <div class="pc-info">
          <div class="pc-tag">Lucky Series</div>
          <div class="pc-name">High Roller<br>Piece</div>
          <div class="pc-desc">Feelin' Lucky?</div>
          <div class="pc-price">R XXX — Order Now</div>
        </div>
        <a href="#contact" onclick="showSection('contact')" class="pc-cta">★ Order Now</a>
      </a>
      <!-- STARGAZER PIECE -->
      <a href="#shop" onclick="showSection('shop')" class="pc rv" style="transition-delay:.3s">
        <div class="pc-img">
          <!-- ═══════════════════════════════════════════════
               STARGAZER PIECE — INSERT PHOTO HERE
               File suggestion: photos/stargazer-piece.jpg
               Original on Weebly: editor/untitled754-20260303145839.png
          ═══════════════════════════════════════════════ -->
          <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/editor/untitled754-20260303145839.png?1772553375"
            alt="Stargazer Piece"
            onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>STARGAZER PIECE<br>photos/stargazer-piece.jpg</div></div>'">
        </div>
        <div class="pc-star" style="animation-delay:.6s">★</div>
        <div class="pc-fade"></div>
        <div class="pc-info">
          <div class="pc-tag">Sky Series</div>
          <div class="pc-name">Stargazer<br>Piece</div>
          <div class="pc-desc">Look to the stars.</div>
          <div class="pc-price">R XXX — Order Now</div>
        </div>
        <a href="#contact" onclick="showSection('contact')" class="pc-cta">★ Order Now</a>
      </a>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-sec">
  <div class="marquee-track">
    <div class="mq-item solid">Confidence<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Superiority</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Defiance<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Power</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Identity<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Freedom</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Confidence<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Superiority</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Defiance<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Power</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Identity<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Freedom</div>
    <div class="mq-item red">★</div>
  </div>
</div>

<!-- STATEMENT -->
<div class="statement-sec rv">
  <div class="stmt-kicker">★ ★ ★ &nbsp; Kraz Kiwi — SS 2026 &nbsp; ★ ★ ★</div>
  <div class="stmt-h">
    BECOME<br>
    <span class="yellow">UNDENIABLE</span><br>
    <span class="stroke">OR STAY</span><br>
    FORGOTTEN.
  </div>
  <p class="stmt-sub">You've already survived days you thought would destroy you. Push beyond the version of you that wanted to quit.</p>
  <div class="stmt-btns">
    <a href="#shop" onclick="showSection('shop')" class="btn-black">★ Shop Now</a>
    <a href="#about" onclick="showSection('about')" class="btn-outline-w">Read Our Story</a>
  </div>
</div>

<!-- SECOND TICKER -->
<div class="motto-ticker" style="background:#0e0e0e;border-top:1px solid #1a1a1a;border-bottom:1px solid #1a1a1a;">
  <div class="motto-track" style="animation-duration:35s;animation-direction:reverse;">
    <div class="motto-item">★ Impossible Is Usually Just Untested <span class="motto-sep">◆</span></div>
    <div class="motto-item">Stand Where Nobody Expected You To Stand <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Greatness Begins Where Comfort Ends <span class="motto-sep">◆</span></div>
    <div class="motto-item">Make Resilience Your Signature <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Survive The Storm — Then Become It <span class="motto-sep">◆</span></div>
    <div class="motto-item">Every Legend Was Once Underestimated <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Impossible Is Usually Just Untested <span class="motto-sep">◆</span></div>
    <div class="motto-item">Stand Where Nobody Expected You To Stand <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Greatness Begins Where Comfort Ends <span class="motto-sep">◆</span></div>
    <div class="motto-item">Make Resilience Your Signature <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Survive The Storm — Then Become It <span class="motto-sep">◆</span></div>
    <div class="motto-item">Every Legend Was Once Underestimated <span class="motto-sep">◆</span></div>
  </div>
</div>

<!-- MANTRAS -->
<section class="mantras-sec rv">
  <div class="mantras-header">
    <div class="sec-eye">Words We Live By</div>
    <h2 class="sec-h2" style="margin-bottom:0;">THE <span class="red">MANTRAS</span>.<span class="stroke"> ★</span></h2>
  </div>
  <div class="mantras-grid">
    <div class="mg rv" style="transition-delay:.05s"><span class="mg-star">★</span><div class="mg-text">Defy what they said couldn't be done.</div></div>
    <div class="mg rv" style="transition-delay:.1s"><span class="mg-star">★</span><div class="mg-text">Become proof that limits can be broken.</div></div>
    <div class="mg rv" style="transition-delay:.15s"><span class="mg-star">★</span><div class="mg-text">Outlast doubt. Outwork fear.</div></div>
    <div class="mg rv" style="transition-delay:.2s"><span class="mg-star">★</span><div class="mg-text">Pressure creates diamonds — keep going.</div></div>
    <div class="mg rv" style="transition-delay:.25s"><span class="mg-star">★</span><div class="mg-text">Even mountains move with enough force.</div></div>
    <div class="mg rv" style="transition-delay:.3s"><span class="mg-star">★</span><div class="mg-text">You were not built to stay small.</div></div>
    <div class="mg rv" style="transition-delay:.35s"><span class="mg-star">★</span><div class="mg-text">Be stronger than the excuses around you.</div></div>
    <div class="mg rv" style="transition-delay:.4s"><span class="mg-star">★</span><div class="mg-text">Turn every setback into momentum.</div></div>
    <div class="mg rv" style="transition-delay:.45s"><span class="mg-star">★</span><div class="mg-text">The harder the path, the greater the story.</div></div>
    <div class="mg rv" style="transition-delay:.5s"><span class="mg-star">★</span><div class="mg-text">Refuse to live an ordinary life.</div></div>
    <div class="mg rv" style="transition-delay:.55s"><span class="mg-star">★</span><div class="mg-text">Impossible is usually just untested.</div></div>
    <div class="mg rv" style="transition-delay:.6s"><span class="mg-star">★</span><div class="mg-text">Stand where nobody expected you to stand.</div></div>
    <div class="mg rv" style="transition-delay:.65s"><span class="mg-star">★</span><div class="mg-text">Greatness begins where comfort ends.</div></div>
    <div class="mg rv" style="transition-delay:.7s"><span class="mg-star">★</span><div class="mg-text">Make resilience your signature.</div></div>
    <div class="mg rv" style="transition-delay:.75s"><span class="mg-star">★</span><div class="mg-text">When the world says stop — become unstoppable.</div></div>
    <div class="mg rv" style="transition-delay:.8s"><span class="mg-star">★</span><div class="mg-text">Rise anyway.</div></div>
    <div class="mg rv" style="transition-delay:.85s"><span class="mg-star">★</span><div class="mg-text">Carry the weight, then lift higher.</div></div>
    <div class="mg rv" style="transition-delay:.9s"><span class="mg-star">★</span><div class="mg-text">If the odds are against you — become the exception.</div></div>
    <div class="mg rv" style="transition-delay:.95s"><span class="mg-star">★</span><div class="mg-text">You've already survived what you thought would end you.</div></div>
    <div class="mg rv" style="transition-delay:1s"><span class="mg-star">★</span><div class="mg-text">Push beyond the version of you that wanted to quit.</div></div>
  </div>
</section>

<!-- HOME CONTACT STRIP -->
<section class="contact-strip rv">
  <div>
    <div class="sec-eye">Get In Touch</div>
    <h2 class="sec-h2" style="font-size:clamp(3rem,5vw,5rem);">LET'S<br><span class="red">TALK</span>.<span class="stroke"> ★</span></h2>
    <p style="font-family:var(--I);font-style:italic;color:var(--muted);font-size:1rem;line-height:1.9;margin-bottom:3rem;max-width:340px;">Ready to order? Have a question? We move fast. Reach out now.</p>
    <div class="contact-items">
      <a href="tel:0766461594" class="ci">
        <div class="ci-icon">📞</div>
        <div><div class="ci-label">Phone / WhatsApp</div><div class="ci-val">076 646 1594</div></div>
      </a>
      <a href="#contact" onclick="showSection('contact')" class="ci">
        <div class="ci-icon">✉️</div>
        <div><div class="ci-label">Online Orders</div><div class="ci-val">Order via the contact form</div></div>
      </a>
      <a href="tel:0766461594" class="ci">
        <div class="ci-icon">⚡</div>
        <div><div class="ci-label">Response Time</div><div class="ci-val">Within 24 hours</div></div>
      </a>
    </div>
  </div>
  <div class="rv" style="transition-delay:.2s">
    <div class="sec-eye">Newsletter</div>
    <h2 class="sec-h2" style="font-size:clamp(2.5rem,4vw,4rem);">FIRST TO<br><span class="red">KNOW. ★</span></h2>
    <p style="font-family:var(--I);font-style:italic;color:var(--muted);font-size:1rem;line-height:1.9;margin-bottom:2rem;">New drops, exclusive access, campaign stories.<br>No noise — just signal.</p>
    <div class="nl-form">
      <input class="nl-input" type="email" placeholder="your@email.com">
      <label class="nl-check"><input type="checkbox"> I agree to receiving updates and exclusive offers from Kraz Kiwi.</label>
      <a href="#" class="cta-primary" style="align-self:flex-start;"><span>★ Subscribe</span></a>
    </div>
  </div>
</section>

<!-- THIRD TICKER -->
<div class="motto-ticker" style="background:var(--red);">
  <div class="motto-track" style="animation-duration:22s;">
    <div class="motto-item">★ Break the cycle — rewrite the outcome <span class="motto-sep">◆</span></div>
    <div class="motto-item">Strength is built in the moments nobody sees <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Become the version of yourself that once felt unreachable <span class="motto-sep">◆</span></div>
    <div class="motto-item">Don't wait for belief — create it <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Break the cycle — rewrite the outcome <span class="motto-sep">◆</span></div>
    <div class="motto-item">Strength is built in the moments nobody sees <span class="motto-sep">◆</span></div>
    <div class="motto-item">★ Become the version of yourself that once felt unreachable <span class="motto-sep">◆</span></div>
    <div class="motto-item">Don't wait for belief — create it <span class="motto-sep">◆</span></div>
  </div>
</div>

</div><!-- END HOME -->


<!-- ═══════════════════════════════════════════════════
     SHOP SECTION — FULL CATALOG
═══════════════════════════════════════════════════ -->
<div id="section-shop" style="display:none;">

<!-- SHOP HERO BANNER -->
<div style="min-height:45vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:10rem 4rem 5rem;position:relative;overflow:hidden;border-bottom:1px solid #1c1c1c;">
  <div style="position:absolute;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(209,0,0,.04) 79px,rgba(209,0,0,.04) 80px),repeating-linear-gradient(90deg,transparent,transparent 79px,rgba(209,0,0,.04) 79px,rgba(209,0,0,.04) 80px);"></div>
  <div style="position:relative;z-index:2;">
    <div class="sec-eye" style="justify-content:center;">SS 2026 Collection</div>
    <h1 style="font-family:var(--A);font-size:clamp(5rem,10vw,10rem);line-height:.88;letter-spacing:.03em;text-transform:uppercase;">
      THE <span style="color:var(--red)">FULL</span><br>
      <span style="-webkit-text-stroke:2px var(--white);color:transparent;">CATALOG.</span>
    </h1>
    <p style="font-family:var(--I);font-style:italic;font-size:1.1rem;color:rgba(245,240,232,.45);margin-top:2rem;line-height:1.9;max-width:500px;margin-left:auto;margin-right:auto;">
      Nine pieces. Each one built with intention. Worn by those who refuse limits.
    </p>
  </div>
</div>

<!-- FILTER BAR -->
<div class="shop-filters" style="padding:2rem 4rem;">
  <button class="sf active">★ All Pieces</button>
  <button class="sf">Signature</button>
  <button class="sf">Lilith '26</button>
  <button class="sf">Lucky Series</button>
  <button class="sf">Limited</button>
</div>

<!-- CATALOG — ALL 9 PIECES -->
<div style="padding:0;background:#111;">

  <!-- ROW 1 — Feature + 2 side by side -->
  <div class="shop-feature" style="margin-bottom:2px;">

    <!-- LOST SOULS PIECE — FEATURE TALL -->
    <a href="#contact" onclick="showSection('contact')" class="pc feature-tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             LOST SOULS PIECE — INSERT PHOTO HERE
             Rename your file to: photos/lost-souls-piece.jpg
             (or any name you like, just update the src below)
             Original Weebly filename: picsart-26-02-24-12-39-15-523_orig.png
        ═══════════════════════════════════════════════ -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/picsart-26-02-24-12-39-15-523_orig.png"
          alt="Lost Souls Piece"
          onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>LOST SOULS PIECE<br>Insert photo here:<br>photos/lost-souls-piece.jpg</div></div>'">
      </div>
      <div class="pc-star">★</div>
      <div class="pc-badge r">★ Signature</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Signature Collection</div>
        <div class="pc-name">Lost Souls<br>Piece</div>
        <div class="pc-desc">Exactly where you need to be.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

    <!-- RIGHT STACK -->
    <div style="display:grid;grid-template-rows:1fr 1fr;gap:2px;background:#111;">

      <!-- HIGH ROLLER PIECE -->
      <a href="#contact" onclick="showSection('contact')" class="pc">
        <div class="pc-img">
          <!-- ═══════════════════════════════════════════════
               HIGH ROLLER PIECE — INSERT PHOTO HERE
               File: photos/high-roller-piece.jpg
               Original: photoroom-20260223-110432_orig.png
          ═══════════════════════════════════════════════ -->
          <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/photoroom-20260223-110432_orig.png"
            alt="High Roller Piece"
            onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>HIGH ROLLER PIECE<br>photos/high-roller-piece.jpg</div></div>'">
        </div>
        <div class="pc-badge y">★ Hot</div>
        <div class="pc-fade"></div>
        <div class="pc-info">
          <div class="pc-tag">Lucky Series</div>
          <div class="pc-name">High Roller<br>Piece</div>
          <div class="pc-desc">Feelin' Lucky?</div>
          <div class="pc-price">R XXX — Order Now</div>
        </div>
        <div class="pc-cta">★ Order Now</div>
      </a>

      <!-- COLD AS ICE PIECE -->
      <a href="#contact" onclick="showSection('contact')" class="pc">
        <div class="pc-img">
          <!-- ═══════════════════════════════════════════════
               COLD AS ICE PIECE — INSERT PHOTO HERE
               File: photos/cold-as-ice-piece.jpg
               Original: picsart-26-02-27-01-38-23-675-copy_orig.png
          ═══════════════════════════════════════════════ -->
          <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/picsart-26-02-27-01-38-23-675-copy_orig.png"
            alt="Cold As Ice Piece"
            onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>COLD AS ICE PIECE<br>photos/cold-as-ice-piece.jpg</div></div>'">
        </div>
        <div class="pc-star" style="animation-delay:.5s">★</div>
        <div class="pc-fade"></div>
        <div class="pc-info">
          <div class="pc-tag">Ice Series</div>
          <div class="pc-name">Cold As Ice<br>Piece</div>
          <div class="pc-desc">Nothing cooler. Period.</div>
          <div class="pc-price">R XXX — Order Now</div>
        </div>
        <div class="pc-cta">★ Order Now</div>
      </a>

    </div>
  </div>

  <!-- ROW 2 — 3 equal cards -->
  <div class="catalog-grid" style="margin-bottom:2px;">

    <!-- MOVING ON PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             MOVING ON PIECE — INSERT PHOTO HERE
             File: photos/moving-on-piece.jpg
             Original: edited/untitled754-20260303145924.png
        ═══════════════════════════════════════════════ -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/edited/untitled754-20260303145924.png?1772553204"
          alt="Moving On Piece"
          onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>MOVING ON PIECE<br>photos/moving-on-piece.jpg</div></div>'">
      </div>
      <div class="pc-badge w">★ New</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Signature Series</div>
        <div class="pc-name">Moving On<br>Piece</div>
        <div class="pc-desc">Leave it in the past. For good.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

    <!-- STARGAZER PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             STARGAZER PIECE — INSERT PHOTO HERE
             File: photos/stargazer-piece.jpg
             Original: editor/untitled754-20260303145839.png
        ═══════════════════════════════════════════════ -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/editor/untitled754-20260303145839.png?1772553375"
          alt="Stargazer Piece"
          onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>STARGAZER PIECE<br>photos/stargazer-piece.jpg</div></div>'">
      </div>
      <div class="pc-star" style="animation-delay:1s">★</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Sky Series</div>
        <div class="pc-name">Stargazer<br>Piece</div>
        <div class="pc-desc">Look to the stars.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

    <!-- GREEN LUCK PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             GREEN LUCK PIECE — INSERT PHOTO HERE
             File: photos/green-luck-piece.jpg
             Original: untitled780-20260306194519_orig.png
             (This piece has 2 views — use the main front photo here)
        ═══════════════════════════════════════════════ -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/untitled780-20260306194519_orig.png"
          alt="Green Luck Piece"
          onerror="this.parentElement.innerHTML='<div class=pc-ph><div class=pc-ph-icon>📸</div><div class=pc-ph-text>GREEN LUCK PIECE<br>photos/green-luck-piece.jpg</div></div>'">
      </div>
      <div class="pc-badge r">★ Limited</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Lucky Series</div>
        <div class="pc-name">Green Luck<br>Piece</div>
        <div class="pc-desc">Deadly charm.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

  </div>

  <!-- ROW 3 — LILITH '26 COLLECTION (3 pieces) -->
  <!-- RED BANNER -->
  <div style="background:var(--red);padding:2.5rem 4rem;display:flex;align-items:center;justify-content:space-between;">
    <div>
      <div style="font-family:var(--U);font-size:.52rem;font-weight:700;letter-spacing:.28em;color:rgba(255,255,255,.5);margin-bottom:.5rem;">★ EXCLUSIVE COLLECTION</div>
      <div style="font-family:var(--A);font-size:clamp(2rem,4vw,4rem);line-height:1;letter-spacing:.03em;">LILITH '26 SERIES</div>
    </div>
    <div style="font-family:var(--I);font-style:italic;font-size:1.1rem;color:rgba(255,255,255,.6);max-width:320px;text-align:right;line-height:1.8;">Charming. Dangerous. Entirely yours. Three pieces from the dark side of confidence.</div>
  </div>

  <div class="catalog-grid">

    <!-- LILITH '26 PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             LILITH '26 PIECE — INSERT PHOTO HERE
             File: photos/lilith-26-piece.jpg
             (This piece was listed as "Lilith' 26 piece — Charming Devil" on Weebly)
             No original Weebly photo found — add your own
        ═══════════════════════════════════════════════ -->
        <div class="pc-ph">
          <div class="pc-ph-icon">📸</div>
          <div class="pc-ph-text">LILITH '26 PIECE<br>Insert photo here:<br>photos/lilith-26-piece.jpg</div>
        </div>
      </div>
      <div class="pc-star">★</div>
      <div class="pc-badge r">★ Lilith '26</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Lilith '26 Series</div>
        <div class="pc-name">Lilith '26<br>Piece</div>
        <div class="pc-desc">Charming Devil.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

    <!-- BLEED OUT PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             BLEED OUT PIECE — INSERT PHOTO HERE
             File: photos/bleed-out-piece.jpg
             (Listed as "bleed out piece — intoxicating love" on Weebly)
             No original Weebly photo found — add your own
        ═══════════════════════════════════════════════ -->
        <div class="pc-ph">
          <div class="pc-ph-icon">📸</div>
          <div class="pc-ph-text">BLEED OUT PIECE<br>Insert photo here:<br>photos/bleed-out-piece.jpg</div>
        </div>
      </div>
      <div class="pc-badge y">★ Limited</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Lilith '26 Series</div>
        <div class="pc-name">Bleed Out<br>Piece</div>
        <div class="pc-desc">Intoxicating love.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

    <!-- THORN BLOOM PIECE -->
    <a href="#contact" onclick="showSection('contact')" class="pc tall">
      <div class="pc-img">
        <!-- ═══════════════════════════════════════════════
             THORN BLOOM PIECE — INSERT PHOTO HERE
             File: photos/thorn-bloom-piece.jpg
             (Listed as "Thorn bloom piece — Beautiful Thorns" on Weebly)
             No original Weebly photo found — add your own
        ═══════════════════════════════════════════════ -->
        <div class="pc-ph">
          <div class="pc-ph-icon">📸</div>
          <div class="pc-ph-text">THORN BLOOM PIECE<br>Insert photo here:<br>photos/thorn-bloom-piece.jpg</div>
        </div>
      </div>
      <div class="pc-star" style="animation-delay:1.5s">★</div>
      <div class="pc-badge r">★ Lilith '26</div>
      <div class="pc-fade"></div>
      <div class="pc-info">
        <div class="pc-tag">Lilith '26 Series</div>
        <div class="pc-name">Thorn Bloom<br>Piece</div>
        <div class="pc-desc">Beautiful thorns.</div>
        <div class="pc-price">R XXX — Order Now</div>
      </div>
      <div class="pc-cta">★ Order Now</div>
    </a>

  </div>

</div><!-- end catalog -->

<!-- SHOP CTA FOOTER -->
<div style="background:var(--black);padding:5rem 4rem;text-align:center;border-top:1px solid #1c1c1c;">
  <div class="sec-eye" style="justify-content:center;">Ready To Wear It?</div>
  <h2 style="font-family:var(--A);font-size:clamp(3rem,6vw,6rem);line-height:.88;letter-spacing:.03em;margin-bottom:1.5rem;">
    ORDER <span style="color:var(--red)">NOW.</span><br>
    <span style="-webkit-text-stroke:1.5px var(--white);color:transparent;">WEAR LOUDER.</span>
  </h2>
  <p style="font-family:var(--I);font-style:italic;color:rgba(245,240,232,.45);font-size:1.05rem;line-height:2;margin-bottom:3rem;max-width:440px;margin-left:auto;margin-right:auto;">
    All pieces ordered via WhatsApp or the contact form. Limited quantities. Don't sleep on it.
  </p>
  <div style="display:flex;gap:1.5rem;justify-content:center;flex-wrap:wrap;">
    <a href="tel:0766461594" class="cta-primary"><span>★ WhatsApp Us</span></a>
    <a href="#contact" onclick="showSection('contact')" class="btn-outline-w" style="border-color:#2a2a2a;color:var(--muted);">Place an Order</a>
  </div>
</div>

</div><!-- END SHOP -->


<!-- ═══════════════════════════════════════════════════
     ABOUT SECTION
═══════════════════════════════════════════════════ -->
<div id="section-about" style="display:none;">

<!-- ABOUT HERO -->
<div class="about-hero" style="padding-top:5rem;">
  <div class="about-hero-img">
    <!-- ═══════════════════════════════════════════════
         ABOUT / BRAND LIFESTYLE PHOTO — INSERT HERE
         File: photos/brand-lifestyle.jpg
         (Use a strong, moody lookbook or founder photo)
         Original Weebly: img-20260220-wa0005_orig.jpg
    ═══════════════════════════════════════════════ -->
    <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/img-20260220-wa0005_orig.jpg"
      alt="Kraz Kiwi Story"
      onerror="this.closest('.about-hero-img').style.background='#0e0e0e'">
    <div class="about-hero-overlay"></div>
  </div>
  <div class="about-body">
    <div class="sec-eye">The Origin</div>
    <div class="about-h">
      RISEN<br>
      FROM <span class="red">ASHES</span>.<br>
      <span class="stroke">BUILT</span><br>
      DEFIANT.
    </div>
    <p class="about-p">
      Born from the ashes of defiance. The brand was built from collapse. After walking away from a future that looked secure but felt empty, its founder chose risk over routine. What started as one decision on a random Saturday became a commitment to live louder, move bolder, and reject average.
    </p>
    <p class="about-p">
      Risen from pressure. Built for confidence. Created for those who refuse limits.
    </p>
    <div class="about-motto">★ &nbsp; Pursue something louder, bolder, and your own.</div>
  </div>
</div>

<!-- FOUNDER QUOTE -->
<div class="founder-quote">
  <div class="fq-kicker">★ Words From The Founder</div>
  <div class="fq-text">
    "One Saturday. One decision. Everything changed. I didn't wait for permission to build something real — I built it from the wreckage of everything that almost held me back."
  </div>
  <div class="fq-attr">— Founder, Kraz Kiwi &nbsp; ★ &nbsp; SS 2026</div>
</div>

<!-- VALUES SECTION -->
<div style="background:var(--black);padding:6rem 0;">
  <div style="padding:0 4rem 4rem;">
    <div class="sec-eye">What We Stand For</div>
    <h2 class="sec-h2">THE <span class="red">PILLARS</span>.<span class="stroke"> ★</span></h2>
  </div>
  <div class="about-values">
    <div class="av">
      <span class="av-num">01</span>
      <div class="av-title">CONFIDENCE</div>
      <div class="av-text">Not the kind that's given to you. The kind you forge — through the moments nobody else sees, through the grind that never stops, through every doubt you buried and kept moving anyway.</div>
    </div>
    <div class="av">
      <span class="av-num">02</span>
      <div class="av-title">SUPERIORITY</div>
      <div class="av-text">Not arrogance. Earned dominance. The quiet knowledge that you've outworked, outthought, and outlasted everyone who told you it couldn't be done. Wear that like armour.</div>
    </div>
    <div class="av">
      <span class="av-num">03</span>
      <div class="av-title">FREEDOM</div>
      <div class="av-text">To become your highest form. To pursue something louder, bolder, and entirely your own. This brand was born in the space between who you were and who you refuse to stop becoming.</div>
    </div>
    <div class="av">
      <span class="av-num">04</span>
      <div class="av-title">DEFIANCE</div>
      <div class="av-text">Every piece carries it. The decision to walk away from safe. The choice to live louder. Defiance isn't rebellion for its own sake — it's the refusal to let the world decide your ceiling.</div>
    </div>
    <div class="av">
      <span class="av-num">05</span>
      <div class="av-title">PRESSURE</div>
      <div class="av-text">Pressure creates diamonds. We were built from collapse — and what emerged from that collapse was a brand, an identity, a movement. Nothing here came easy. That's the point.</div>
    </div>
    <div class="av">
      <span class="av-num">06</span>
      <div class="av-title">IDENTITY</div>
      <div class="av-text">When you wear Kraz Kiwi, you're not just wearing clothes. You're declaring where you stand. You're announcing the version of yourself that refuses to be ordinary, unremarkable, or forgotten.</div>
    </div>
  </div>
</div>

<!-- ABOUT MARQUEE -->
<div class="marquee-sec">
  <div class="marquee-track">
    <div class="mq-item solid">Born Defiant<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Built From Collapse</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Risen From Pressure<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Refuse Limits</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Live Louder<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Move Bolder</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Born Defiant<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Built From Collapse</div>
    <div class="mq-item red">★</div>
    <div class="mq-item solid">Risen From Pressure<span class="mq-star">★</span></div>
    <div class="mq-item hollow">Refuse Limits</div>
    <div class="mq-item red">★</div>
  </div>
</div>

<!-- ABOUT STATEMENT -->
<div class="statement-sec">
  <div class="stmt-kicker">★ ★ ★ &nbsp; This Is What We Stand For &nbsp; ★ ★ ★</div>
  <div class="stmt-h">
    REFUSE<br>
    <span class="yellow">AVERAGE.</span><br>
    <span class="stroke">BECOME</span><br>
    LEGENDARY.
  </div>
  <p class="stmt-sub">
    This brand stands for confidence, superiority, and the freedom to become your highest form. Pursue something louder, bolder, and your own.
  </p>
  <div class="stmt-btns">
    <a href="#shop" onclick="showSection('shop')" class="btn-black">★ Shop The Drop</a>
    <a href="#contact" onclick="showSection('contact')" class="btn-outline-w">Get In Touch</a>
  </div>
</div>

</div><!-- END ABOUT -->


<!-- ═══════════════════════════════════════════════════
     CONTACT SECTION
═══════════════════════════════════════════════════ -->
<div id="section-contact" style="display:none;">

<!-- CONTACT HERO -->
<div style="padding:10rem 4rem 5rem;text-align:center;position:relative;overflow:hidden;border-bottom:1px solid #1c1c1c;">
  <div style="position:absolute;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(209,0,0,.04) 79px,rgba(209,0,0,.04) 80px);"></div>
  <div style="position:relative;z-index:2;">
    <div class="sec-eye" style="justify-content:center;">Contact</div>
    <h1 style="font-family:var(--A);font-size:clamp(5rem,10vw,9rem);line-height:.88;letter-spacing:.02em;text-transform:uppercase;">
      LET'S<br>
      <span style="color:var(--red)">TALK.</span><br>
      <span style="-webkit-text-stroke:2px var(--white);color:transparent;">★ NOW.</span>
    </h1>
    <p style="font-family:var(--I);font-style:italic;font-size:1.1rem;color:rgba(245,240,232,.4);margin-top:2rem;line-height:2;max-width:440px;margin-left:auto;margin-right:auto;">
      We move fast. Whether you're placing an order, asking a question, or just ready to go — reach out and we'll get back to you within 24 hours.
    </p>
  </div>
</div>

<!-- CONTACT SPLIT -->
<div class="contact-hero">
  <div class="contact-left">
    <div class="sec-eye">Direct Contact</div>
    <div class="contact-h">
      REACH<br>
      <span class="red">OUT.</span><br>
      <span class="stroke">NOW. ★</span>
    </div>
    <div class="contact-sub">
      You don't need a middleman. Hit us directly on WhatsApp or the form — fast, direct, no noise.
    </div>
    <div class="contact-items">
      <a href="tel:0766461594" class="ci">
        <div class="ci-icon">📞</div>
        <div><div class="ci-label">Phone</div><div class="ci-val">076 646 1594</div></div>
      </a>
      <a href="https://wa.me/27766461594" class="ci">
        <div class="ci-icon">💬</div>
        <div><div class="ci-label">WhatsApp</div><div class="ci-val">076 646 1594 — Message us directly</div></div>
      </a>
      <div class="ci" style="cursor:default;">
        <div class="ci-icon">📍</div>
        <div><div class="ci-label">Location</div><div class="ci-val">South Africa — Nationwide Delivery</div></div>
      </div>
      <div class="ci" style="cursor:default;">
        <div class="ci-icon">⚡</div>
        <div><div class="ci-label">Response Time</div><div class="ci-val">Within 24 hours — usually faster</div></div>
      </div>
      <div class="ci" style="cursor:default;">
        <div class="ci-icon">🕐</div>
        <div><div class="ci-label">Hours</div><div class="ci-val">Monday – Saturday, 9AM – 7PM</div></div>
      </div>
    </div>
  </div>

  <div class="contact-right">
    <div class="of-h">★ Place An Order</div>
    <div class="of-sub">Fill in your details below and we'll confirm your order via WhatsApp.</div>
    <div class="order-form">
      <div class="of-row">
        <input class="of-input" type="text" placeholder="Your name">
        <input class="of-input" type="tel" placeholder="WhatsApp number">
      </div>
      <select class="of-select of-input">
        <option value="" disabled selected>Select a piece</option>
        <option>Lost Souls Piece — R XXX</option>
        <option>High Roller Piece — R XXX</option>
        <option>Cold As Ice Piece — R XXX</option>
        <option>Moving On Piece — R XXX</option>
        <option>Stargazer Piece — R XXX</option>
        <option>Green Luck Piece — R XXX</option>
        <option>Lilith '26 Piece — R XXX</option>
        <option>Bleed Out Piece — R XXX</option>
        <option>Thorn Bloom Piece — R XXX</option>
      </select>
      <div class="of-row">
        <select class="of-select of-input">
          <option value="" disabled selected>Size</option>
          <option>XS</option>
          <option>S</option>
          <option>M</option>
          <option>L</option>
          <option>XL</option>
          <option>XXL</option>
        </select>
        <input class="of-input" type="text" placeholder="City / Town">
      </div>
      <textarea class="of-textarea of-input" placeholder="Any notes or questions..."></textarea>
      <a href="tel:0766461594" class="cta-primary" style="align-self:flex-start;"><span>★ Send Order via WhatsApp</span></a>
      <p style="font-family:var(--I);font-style:italic;font-size:.85rem;color:var(--muted);line-height:1.8;">After submitting, we'll confirm details and payment via WhatsApp. Orders are final once confirmed.</p>
    </div>
  </div>
</div>

<!-- CONTACT STATEMENT -->
<div class="statement-sec">
  <div class="stmt-kicker">★ ★ ★ &nbsp; No Waiting. No Excuses. &nbsp; ★ ★ ★</div>
  <div class="stmt-h">
    DON'T<br>
    <span class="yellow">HESITATE.</span><br>
    <span class="stroke">MAKE THE</span><br>
    MOVE.
  </div>
  <p class="stmt-sub">Every legend started with one decision. Place the order. Wear the proof.</p>
  <div class="stmt-btns">
    <a href="https://wa.me/27766461594" class="btn-black">★ WhatsApp Now</a>
    <a href="#shop" onclick="showSection('shop')" class="btn-outline-w">Browse The Catalog</a>
  </div>
</div>

</div><!-- END CONTACT -->


<!-- FOOTER (always visible) -->
<footer>
  <div class="foot-inner">
    <div>
      <div class="foot-logo">
        <!-- ═══ FOOTER LOGO ═══ -->
        <!-- src="photos/kraz-kiwi-logo.png" — update when you have local file -->
        <img src="https://krazkiwi.weebly.com/uploads/1/5/2/2/152248344/published/untitled707-20260224120111.png?1771927737" alt="Kraz Kiwi">
      </div>
      <p class="foot-bio">Born from the ashes of defiance. Built for those who refuse limits. Wear it like you mean it. ★</p>
    </div>
    <div>
      <div class="foot-col-title">Navigate</div>
      <div class="foot-links">
        <a href="#home" onclick="showSection('home')">Home</a>
        <a href="#shop" onclick="showSection('shop')">Shop</a>
        <a href="#about" onclick="showSection('about')">About</a>
        <a href="#contact" onclick="showSection('contact')">Contact</a>
      </div>
    </div>
    <div>
      <div class="foot-col-title">The Catalog</div>
      <div class="foot-links">
        <a href="#shop" onclick="showSection('shop')">Lost Souls Piece</a>
        <a href="#shop" onclick="showSection('shop')">High Roller Piece</a>
        <a href="#shop" onclick="showSection('shop')">Cold As Ice Piece</a>
        <a href="#shop" onclick="showSection('shop')">Moving On Piece</a>
        <a href="#shop" onclick="showSection('shop')">Stargazer Piece</a>
        <a href="#shop" onclick="showSection('shop')">Green Luck Piece</a>
        <a href="#shop" onclick="showSection('shop')">Lilith '26 Series</a>
      </div>
    </div>
    <div>
      <div class="foot-col-title">Contact</div>
      <div class="foot-links">
        <a href="tel:0766461594">076 646 1594</a>
        <a href="https://wa.me/27766461594">WhatsApp Us</a>
        <a href="#contact" onclick="showSection('contact')">Place an Order</a>
      </div>
    </div>
  </div>
  <div class="foot-bottom">
    <div class="foot-copy">© 2026 Kraz Kiwi ★ All rights reserved.</div>
    <div class="foot-tag">OUTWORK <span>YOUR PAST. ★</span></div>
  </div>
</footer>

<script>
// ─── Cursor ───
const cur = document.getElementById('kk-cursor');
document.addEventListener('mousemove', e => {
  cur.style.left = e.clientX + 'px';
  cur.style.top = e.clientY + 'px';
});

// ─── Loader ───
window.addEventListener('load', () => {
  setTimeout(() => {
    const l = document.getElementById('loader');
    l.style.transition = 'opacity .5s ease';
    l.style.opacity = '0';
    setTimeout(() => l.remove(), 500);
  }, 1600);
});

// ─── Nav pin ───
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('pinned', window.scrollY > 80);
});

// ─── Section switcher ───
const sections = ['home', 'shop', 'about', 'contact'];
function showSection(id) {
  sections.forEach(s => {
    const el = document.getElementById('section-' + s);
    if (el) el.style.display = s === id ? 'block' : 'none';
  });
  // Update active nav link
  document.querySelectorAll('.nav-link').forEach(a => {
    a.classList.toggle('active', a.dataset.section === id);
  });
  window.scrollTo({ top: 0, behavior: 'smooth' });
  // Re-trigger reveal animations
  setTimeout(() => {
    document.querySelectorAll('.rv').forEach(el => {
      if (!el.classList.contains('on')) observer.observe(el);
    });
  }, 100);
}

// ─── Scroll reveal ───
const rvEls = document.querySelectorAll('.rv');
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('on');
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.08 });
rvEls.forEach(el => observer.observe(el));

// ─── Hero parallax ───
window.addEventListener('scroll', () => {
  const img = document.querySelector('.hero-product-img');
  if (img) img.style.transform = `translateY(${scrollY * .1}px)`;
});

// ─── Shop filter buttons ───
document.querySelectorAll('.sf').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.sf').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
  });
});

// ─── Star field ───
(function(){
  const body = document.body;
  for(let i = 0; i < 55; i++){
    const s = document.createElement('div');
    const size = Math.random() * 2.5 + .8;
    const dur = Math.random() * 4 + 2;
    const delay = Math.random() * 8;
    s.style.cssText = `
      position:fixed;z-index:0;pointer-events:none;
      width:${size}px;height:${size}px;border-radius:50%;
      background:#D10000;opacity:0;
      left:${Math.random()*100}%;top:${Math.random()*100}%;
      animation:starTwink ${dur}s ${delay}s ease-in-out infinite;
    `;
    body.appendChild(s);
  }
  if(!document.getElementById('starStyle')){
    const st = document.createElement('style');
    st.id = 'starStyle';
    st.textContent = `@keyframes starTwink{0%,100%{opacity:0;transform:scale(.3)}50%{opacity:.5;transform:scale(1)}}`;
    document.head.appendChild(st);
  }
})();
</script>
</body>
</html>
