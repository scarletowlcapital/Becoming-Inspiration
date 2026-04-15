# Becoming-Inspiration
New site
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Summer Rose-Thompson — Becoming Inspiration</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,900;1,400;1,700&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Outfit:wght@200;300;400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
:root{
  --gold:#C9A84C;
  --gold2:#F0D080;
  --charcoal:#1A1612;
  --dark:#0C0A08;
  --mid:#161210;
  --cream:#F5EDE0;
  --muted:rgba(245,237,224,0.45);
  --rose:#C4687A;
}
html{scroll-behavior:smooth;}
body{background:var(--dark);font-family:'Outfit',sans-serif;color:var(--cream);overflow-x:hidden;cursor:none;}

/* CURSOR */
.cur{position:fixed;width:6px;height:6px;background:var(–gold);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);}
.cur-ring{position:fixed;width:32px;height:32px;border:1px solid rgba(201,168,76,0.4);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:all .1s;}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:500;display:flex;align-items:center;justify-content:space-between;padding:24px 60px;background:linear-gradient(to bottom,rgba(12,10,8,.95),transparent);}
.logo{font-family:‘Playfair Display’,serif;font-size:1.1rem;font-weight:400;letter-spacing:.12em;color:var(–cream);text-transform:uppercase;}
.logo span{color:var(–gold);font-style:italic;}
.nav-r{display:flex;gap:40px;align-items:center;}
.nav-r a{font-size:.58rem;letter-spacing:.28em;text-transform:uppercase;color:var(–muted);text-decoration:none;transition:color .3s;}
.nav-r a:hover{color:var(–gold2);}
.nav-cta{border:1px solid rgba(201,168,76,.4);color:var(–gold)!important;padding:10px 28px;transition:all .3s!important;}
.nav-cta:hover{background:rgba(201,168,76,.1);border-color:var(–gold)!important;}

/* HERO */
#scroll-driver{height:600vh;position:relative;}
#sticky{position:sticky;top:0;height:100vh;overflow:hidden;display:flex;align-items:center;}
#book-canvas{position:absolute;inset:0;z-index:1;}

.hero-atmo{
position:absolute;inset:0;z-index:2;
background:
linear-gradient(110deg,rgba(12,10,8,.96) 0%,rgba(12,10,8,.85) 38%,rgba(12,10,8,.2) 62%,transparent 100%),
radial-gradient(ellipse 50% 60% at 68% 50%,rgba(100,50,20,.35) 0%,transparent 65%),
radial-gradient(ellipse 30% 40% at 75% 20%,rgba(201,168,76,.06) 0%,transparent 60%);
pointer-events:none;
}

/* diagonal gold line */
.hero-accent{position:absolute;top:0;right:35%;bottom:0;z-index:3;width:1px;background:linear-gradient(to bottom,transparent,rgba(201,168,76,.12) 30%,rgba(201,168,76,.2) 60%,transparent);pointer-events:none;}

.hero-text{position:relative;z-index:10;margin-left:7vw;max-width:520px;}
.hero-text > *{opacity:0;transform:translateY(24px);}
.loaded .t1{animation:fadeUp .9s ease .1s forwards;}
.loaded .t2{animation:fadeUp 1s ease .3s forwards;}
.loaded .t3{animation:fadeUp .9s ease .5s forwards;}
.loaded .t4{animation:fadeUp .9s ease .7s forwards;}
.loaded .t5{animation:fadeUp .9s ease .9s forwards;}
@keyframes fadeUp{to{opacity:1;transform:translateY(0);}}

.hero-kicker{font-size:.54rem;letter-spacing:.5em;text-transform:uppercase;color:var(–gold);margin-bottom:24px;display:flex;align-items:center;gap:14px;}
.hero-kicker::before{content:’’;width:32px;height:1px;background:var(–gold);}

.hero-h1{font-family:‘Playfair Display’,serif;font-size:clamp(3rem,6vw,6rem);font-weight:900;line-height:.95;color:var(–cream);margin-bottom:8px;letter-spacing:-.02em;}
.hero-h1 em{font-style:italic;font-weight:400;color:var(–gold);display:block;font-size:.8em;}

.hero-author{font-family:‘Cormorant Garamond’,serif;font-size:1.1rem;font-weight:300;font-style:italic;color:var(–muted);margin-bottom:32px;letter-spacing:.06em;}

.hero-p{font-size:.76rem;line-height:2;color:var(–muted);max-width:380px;margin-bottom:40px;font-weight:300;}

.hero-btns{display:flex;gap:20px;align-items:center;flex-wrap:wrap;}
.btn-gold{background:linear-gradient(135deg,rgba(201,168,76,.9),rgba(240,208,128,.9));color:var(–dark);padding:15px 40px;text-decoration:none;font-size:.64rem;letter-spacing:.28em;text-transform:uppercase;font-weight:600;border:none;cursor:none;font-family:‘Outfit’,sans-serif;transition:all .3s;display:inline-block;box-shadow:0 0 40px rgba(201,168,76,.25);}
.btn-gold:hover{box-shadow:0 0 60px rgba(201,168,76,.45);transform:translateY(-2px);}
.btn-ghost{color:var(–muted);font-size:.64rem;letter-spacing:.22em;text-transform:uppercase;text-decoration:none;display:flex;align-items:center;gap:10px;transition:color .3s;background:none;border:none;cursor:none;font-family:‘Outfit’,sans-serif;}
.btn-ghost::after{content:‘→’;font-size:1rem;transition:transform .3s;}
.btn-ghost:hover{color:var(–gold2);}
.btn-ghost:hover::after{transform:translateX(5px);}

/* book title reveal */
.book-title-display{
position:absolute;right:7vw;bottom:80px;z-index:10;
text-align:right;
opacity:0;transition:opacity 1s ease 1.5s;
}
.loaded .book-title-display{opacity:1;}
.btd-title{font-family:‘Playfair Display’,serif;font-size:clamp(1.2rem,2.5vw,2rem);font-weight:400;font-style:italic;color:var(–gold);letter-spacing:.06em;}
.btd-sub{font-size:.54rem;letter-spacing:.35em;text-transform:uppercase;color:var(–muted);margin-top:6px;}

/* scroll cue */
.scroll-cue{position:absolute;bottom:36px;left:7vw;z-index:10;display:flex;align-items:center;gap:14px;font-size:.5rem;letter-spacing:.4em;text-transform:uppercase;color:rgba(245,237,224,.2);}
.scroll-line{width:1px;height:44px;background:linear-gradient(to bottom,rgba(201,168,76,.4),transparent);animation:sdrop 2.5s ease-in-out infinite;}
@keyframes sdrop{0%{transform:scaleY(0);transform-origin:top;}50%{transform:scaleY(1);transform-origin:top;}51%{transform:scaleY(1);transform-origin:bottom;}100%{transform:scaleY(0);transform-origin:bottom;}}

/* MARQUEE */
.mwrap{overflow:hidden;border-top:1px solid rgba(201,168,76,.1);border-bottom:1px solid rgba(201,168,76,.1);padding:14px 0;background:rgba(201,168,76,.03);}
.mtrack{display:flex;gap:60px;animation:mq 25s linear infinite;white-space:nowrap;}
.mtrack span{font-size:.54rem;letter-spacing:.32em;text-transform:uppercase;color:var(–gold);opacity:.5;display:flex;align-items:center;gap:20px;}
.mtrack span::after{content:‘◆’;font-size:.32rem;}
@keyframes mq{from{transform:translateX(0);}to{transform:translateX(-50%);}}

/* BOOK SECTION */
.book-sec{padding:100px 60px;display:grid;grid-template-columns:1fr 1fr;gap:80px;align-items:center;position:relative;}
.book-sec::before{content:’’;position:absolute;top:0;left:60px;right:60px;height:1px;background:linear-gradient(90deg,transparent,rgba(201,168,76,.2),transparent);}

.book-img-wrap{position:relative;display:flex;align-items:center;justify-content:center;}
.book-glow{position:absolute;width:300px;height:300px;border-radius:50%;background:radial-gradient(circle,rgba(201,168,76,.15) 0%,transparent 70%);animation:glow 4s ease-in-out infinite;}
@keyframes glow{0%,100%{transform:scale(1);opacity:.6;}50%{transform:scale(1.2);opacity:1;}}
.book-3d-static{
width:280px;
filter:drop-shadow(0 30px 60px rgba(0,0,0,.8)) drop-shadow(0 0 40px rgba(201,168,76,.2));
animation:bookFloat 6s ease-in-out infinite;
border-radius:4px;
}
@keyframes bookFloat{0%,100%{transform:translateY(0) rotateY(-5deg);}50%{transform:translateY(-16px) rotateY(5deg);}}

.book-info{}
.sec-label{font-size:.54rem;letter-spacing:.45em;text-transform:uppercase;color:var(–gold);margin-bottom:14px;display:flex;align-items:center;gap:14px;}
.sec-label::before{content:’’;width:24px;height:1px;background:var(–gold);}
.sec-h{font-family:‘Playfair Display’,serif;font-size:clamp(2rem,4vw,3.2rem);font-weight:700;color:var(–cream);line-height:1.15;margin-bottom:16px;}
.sec-h em{font-style:italic;color:var(–gold);font-weight:400;}
.sec-p{font-size:.76rem;line-height:2;color:var(–muted);margin-bottom:32px;font-weight:300;}

/* book details */
.book-details{display:flex;gap:32px;margin-bottom:36px;flex-wrap:wrap;}
.bd-item{padding:16px 20px;border:1px solid rgba(201,168,76,.15);background:rgba(201,168,76,.03);}
.bd-n{font-family:‘Playfair Display’,serif;font-size:1.6rem;font-weight:400;color:var(–gold);line-height:1;}
.bd-l{font-size:.54rem;letter-spacing:.2em;text-transform:uppercase;color:var(–muted);margin-top:4px;}

/* AUTHOR SECTION */
.author-sec{
padding:100px 60px;
background:var(–mid);
position:relative;overflow:hidden;
}
.author-sec::before{
content:‘SUMMER’;
position:absolute;top:50%;left:50%;
transform:translate(-50%,-50%);
font-family:‘Playfair Display’,serif;
font-size:18vw;font-weight:900;
color:rgba(201,168,76,.02);
white-space:nowrap;pointer-events:none;
}
.author-inner{position:relative;z-index:2;max-width:700px;margin:0 auto;text-align:center;}
.author-img-placeholder{
width:180px;height:180px;border-radius:50%;
background:linear-gradient(135deg,rgba(201,168,76,.2),rgba(201,168,76,.05));
border:1px solid rgba(201,168,76,.2);
margin:0 auto 32px;
display:flex;align-items:center;justify-content:center;
font-size:4rem;
position:relative;
}
.author-img-placeholder::after{
content:’’;
position:absolute;inset:-8px;border-radius:50%;
border:1px solid rgba(201,168,76,.08);
}
.author-name{font-family:‘Playfair Display’,serif;font-size:clamp(2rem,4vw,3rem);font-weight:400;font-style:italic;color:var(–cream);margin-bottom:8px;}
.author-title{font-size:.58rem;letter-spacing:.38em;text-transform:uppercase;color:var(–gold);margin-bottom:28px;}
.author-bio{font-family:‘Cormorant Garamond’,serif;font-size:1.15rem;font-weight:300;font-style:italic;color:var(–muted);line-height:1.9;margin-bottom:40px;}

/* ANIMATION SECTION */
.anim-sec{padding:100px 60px;}
.anim-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:rgba(201,168,76,.06);margin-top:48px;}
.anim-card{
background:var(–charcoal);padding:48px 36px;
transition:background .4s;position:relative;overflow:hidden;
}
.anim-card:hover{background:#201A14;}
.anim-card::after{content:’’;position:absolute;bottom:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(–gold),transparent);transform:scaleX(0);transition:transform .5s;}
.anim-card:hover::after{transform:scaleX(1);}
.ac-num{font-family:‘Playfair Display’,serif;font-size:4rem;font-weight:900;color:var(–gold);opacity:.08;line-height:1;margin-bottom:20px;}
.ac-icon{font-size:2rem;margin-bottom:16px;display:block;}
.ac-title{font-family:‘Playfair Display’,serif;font-size:1.2rem;font-weight:400;color:var(–cream);margin-bottom:10px;}
.ac-p{font-size:.7rem;line-height:1.9;color:var(–muted);font-weight:300;}

/* NEWSLETTER */
.nl-sec{
padding:100px 60px;
background:radial-gradient(ellipse 70% 50% at 50% 50%,rgba(80,50,15,.3) 0%,transparent 70%),var(–mid);
text-align:center;position:relative;overflow:hidden;
}
.nl-sec::before{content:’’;position:absolute;inset:0;background:radial-gradient(ellipse 60% 60% at 50% 50%,rgba(201,168,76,.04) 0%,transparent 70%);}
.nl-inner{position:relative;z-index:2;max-width:560px;margin:0 auto;}
.nl-h{font-family:‘Playfair Display’,serif;font-size:clamp(2rem,4vw,3.2rem);font-weight:700;color:var(–cream);line-height:1.2;margin-bottom:14px;}
.nl-h em{font-style:italic;color:var(–gold);font-weight:400;}
.nl-p{font-size:.74rem;color:var(–muted);line-height:1.9;margin-bottom:36px;font-weight:300;}
.nl-form{display:flex;gap:0;max-width:440px;margin:0 auto;}
.nl-input{flex:1;padding:16px 20px;background:rgba(245,237,224,.05);border:1px solid rgba(201,168,76,.2);border-right:none;color:var(–cream);font-family:‘Outfit’,sans-serif;font-size:.74rem;outline:none;}
.nl-input::placeholder{color:rgba(245,237,224,.25);}
.nl-btn{padding:16px 28px;background:linear-gradient(135deg,var(–gold),var(–gold2));color:var(–dark);border:none;cursor:pointer;font-size:.6rem;letter-spacing:.2em;text-transform:uppercase;font-weight:600;font-family:‘Outfit’,sans-serif;transition:all .3s;}
.nl-btn:hover{box-shadow:0 0 30px rgba(201,168,76,.4);}

/* FOOTER */
footer{padding:70px 60px 36px;border-top:1px solid rgba(201,168,76,.08);}
.foot-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:48px;flex-wrap:wrap;gap:40px;}
.foot-brand-name{font-family:‘Playfair Display’,serif;font-size:1.6rem;font-weight:400;font-style:italic;color:var(–cream);margin-bottom:8px;}
.foot-brand-name span{color:var(–gold);}
.foot-tag{font-size:.68rem;color:var(–muted);line-height:1.8;max-width:240px;font-weight:300;}
.foot-links-wrap{display:flex;gap:60px;}
.foot-col-t{font-size:.54rem;letter-spacing:.3em;text-transform:uppercase;color:var(–gold);margin-bottom:16px;}
.foot-links{list-style:none;}
.foot-links li{margin-bottom:8px;}
.foot-links a{font-size:.68rem;color:var(–muted);text-decoration:none;transition:color .3s;}
.foot-links a:hover{color:var(–cream);}
.foot-bot{border-top:1px solid rgba(245,237,224,.04);padding-top:24px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:12px;}
.foot-copy{font-size:.56rem;letter-spacing:.1em;color:rgba(245,237,224,.2);}

/* RESPONSIVE */
@media(max-width:1024px){
nav{padding:18px 28px;}
.book-sec{grid-template-columns:1fr;padding:60px 28px;text-align:center;}
.book-img-wrap{order:-1;}
.sec-label{justify-content:center;}
.book-details{justify-content:center;}
.author-sec,.anim-sec,.nl-sec{padding:64px 28px;}
footer{padding:56px 28px 28px;}
.anim-grid{grid-template-columns:1fr;}
.foot-top{flex-direction:column;}
.cur,.cur-ring{display:none;}
body{cursor:auto;}
a,button{cursor:pointer;}
}
@media(max-width:640px){
.hero-h1{font-size:3rem;}
.nl-form{flex-direction:column;}
.nl-input{border-right:1px solid rgba(201,168,76,.2);border-bottom:none;}
nav{padding:14px 20px;}
.nav-r a:not(.nav-cta){display:none;}
}
</style>

</head>
<body>

<div class="cur" id="cur"></div>
<div class="cur-ring" id="curR"></div>

<nav>
  <div class="logo">Becoming <span>Inspiration</span></div>
  <div class="nav-r">
    <a href="#book">The Book</a>
    <a href="#author">About</a>
    <a href="#animate">Work</a>
    <a href="#newsletter" class="nav-cta">Stay Connected</a>
  </div>
</nav>

<!-- HERO -->

<div id="scroll-driver">
  <div id="sticky">
    <canvas id="book-canvas"></canvas>
    <div class="hero-atmo"></div>
    <div class="hero-accent"></div>

```
<div class="hero-text" id="ht">
  <div class="hero-kicker t1">Author · Animator · Visionary</div>
  <div id="pt">
    <h1 class="hero-h1 t2">
      Becoming<br>
      <em>Inspiration.</em>
    </h1>
  </div>
  <div class="hero-author t3">Summer Rose-Thompson</div>
  <p class="hero-p t4">Stories that move. Worlds that breathe. Words that set you free. Welcome to the beginning of your unbound path.</p>
  <div class="hero-btns t5">
    <a href="#book" class="btn-gold">Discover The Book</a>
    <button class="btn-ghost" onclick="document.getElementById('author').scrollIntoView({behavior:'smooth'})">Meet Summer</button>
  </div>
</div>

<div class="book-title-display">
  <div class="btd-title">The Unbound Path</div>
  <div class="btd-sub">Scroll to explore</div>
</div>

<div class="scroll-cue"><div class="scroll-line"></div>Journey begins below</div>
```

  </div>
</div>

<!-- MARQUEE -->

<div class="mwrap">
  <div class="mtrack">
    <span>Author</span><span>Animator</span><span>Storyteller</span><span>The Unbound Path</span><span>Becoming Inspiration</span><span>Summer Rose-Thompson</span><span>Words That Move</span><span>Worlds That Breathe</span>
    <span>Author</span><span>Animator</span><span>Storyteller</span><span>The Unbound Path</span><span>Becoming Inspiration</span><span>Summer Rose-Thompson</span><span>Words That Move</span><span>Worlds That Breathe</span>
  </div>
</div>

<!-- BOOK SECTION -->

<section class="book-sec" id="book">
  <div class="book-img-wrap">
    <div class="book-glow"></div>
    <!-- Book renders using CSS 3D — real image drops in here -->
    <div style="perspective:1200px;perspective-origin:50% 50%;">
      <div style="width:240px;transform-style:preserve-3d;animation:bookSpin 12s ease-in-out infinite;">
        <img id="bookImg"
          src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='240' height='320' viewBox='0 0 240 320'%3E%3Crect width='240' height='320' fill='%231A1612'/%3E%3Crect x='0' y='0' width='16' height='320' fill='%23C9A84C'/%3E%3Ctext x='120' y='130' text-anchor='middle' font-family='serif' font-size='22' fill='%23C9A84C' font-weight='bold'%3ETHE%3C/text%3E%3Ctext x='120' y='165' text-anchor='middle' font-family='serif' font-size='22' fill='%23C9A84C' font-weight='bold'%3EUNBOUND%3C/text%3E%3Ctext x='120' y='200' text-anchor='middle' font-family='serif' font-size='22' fill='%23C9A84C' font-weight='bold'%3EPATH%3C/text%3E%3Ctext x='120' y='280' text-anchor='middle' font-family='serif' font-size='12' fill='%23C9A84C'%3ESummer Rose-Thompson%3C/text%3E%3C/svg%3E"
          alt="The Unbound Path"
          class="book-3d-static"
          style="width:240px;display:block;">
      </div>
    </div>
  </div>

  <div class="book-info">
    <div class="sec-label">Debut Work</div>
    <h2 class="sec-h">The Unbound<br><em>Path</em></h2>
    <p class="sec-p">A journey into the uncharted. Summer Rose-Thompson's debut work weaves together breathtaking narrative and visual storytelling — a book that doesn't just tell a story, it makes you feel every word like a world coming alive around you.</p>
    <div class="book-details">
      <div class="bd-item"><div class="bd-n">2025</div><div class="bd-l">Year</div></div>
      <div class="bd-item"><div class="bd-n">∞</div><div class="bd-l">Pages of Wonder</div></div>
      <div class="bd-item"><div class="bd-n">01</div><div class="bd-l">Volume</div></div>
    </div>
    <a href="#newsletter" class="btn-gold">Get Notified on Release</a>
  </div>
</section>

<!-- AUTHOR SECTION -->

<section class="author-sec" id="author">
  <div class="author-inner">
    <div class="author-img-placeholder">✍️</div>
    <div class="author-name">Summer Rose-Thompson</div>
    <div class="author-title">Author · Animator · Creative Director</div>
    <p class="author-bio">"I don't just write stories — I build worlds. Every word is a brushstroke, every chapter a frame in an animation that plays inside your mind. My work exists at the intersection of literature and motion, where the page comes alive and inspiration finds its form."</p>
    <a href="#newsletter" class="btn-gold">Follow the Journey</a>
  </div>
</section>

<!-- ANIMATION WORK -->

<section class="anim-sec" id="animate">
  <div class="sec-label">Creative Work</div>
  <h2 class="sec-h" style="max-width:500px">Where Words<br><em>Meet Motion</em></h2>
  <div class="anim-grid">
    <div class="anim-card">
      <div class="ac-num">01</div>
      <span class="ac-icon">📖</span>
      <div class="ac-title">Literary Fiction</div>
      <p class="ac-p">Narratives that push beyond the page. Stories crafted to challenge, inspire, and move the reader through emotional landscapes unlike anything they've encountered.</p>
    </div>
    <div class="anim-card">
      <div class="ac-num">02</div>
      <span class="ac-icon">🎬</span>
      <div class="ac-title">Animation</div>
      <p class="ac-p">Visual worlds brought to life through the art of animation. Each frame is intentional, each movement purposeful — storytelling elevated into a visual language.</p>
    </div>
    <div class="anim-card">
      <div class="ac-num">03</div>
      <span class="ac-icon">✨</span>
      <div class="ac-title">Becoming Inspiration</div>
      <p class="ac-p">More than a brand — a movement. Dedicated to helping others find their unbound path through the power of creative expression, authentic storytelling, and fearless becoming.</p>
    </div>
  </div>
</section>

<!-- NEWSLETTER -->

<section class="nl-sec" id="newsletter">
  <div class="nl-inner">
    <div class="sec-label" style="justify-content:center">Stay Connected</div>
    <h2 class="nl-h">Begin Your<br><em>Unbound Path</em></h2>
    <p class="nl-p">Be the first to know when The Unbound Path releases, get exclusive behind-the-scenes content, and join a community of readers and creators on their own journeys.</p>
    <div class="nl-form">
      <input class="nl-input" type="email" placeholder="Your email address">
      <button class="nl-btn">Join</button>
    </div>
  </div>
</section>

<!-- FOOTER -->

<footer>
  <div class="foot-top">
    <div>
      <div class="foot-brand-name">Becoming <span>Inspiration</span></div>
      <p class="foot-tag">Stories that move. Worlds that breathe. The creative universe of Summer Rose-Thompson — author, animator, visionary.</p>
    </div>
    <div class="foot-links-wrap">
      <div>
        <div class="foot-col-t">Explore</div>
        <ul class="foot-links">
          <li><a href="#book">The Book</a></li>
          <li><a href="#author">About Summer</a></li>
          <li><a href="#animate">Creative Work</a></li>
          <li><a href="#newsletter">Newsletter</a></li>
        </ul>
      </div>
      <div>
        <div class="foot-col-t">Connect</div>
        <ul class="foot-links">
          <li><a href="#">Instagram</a></li>
          <li><a href="#">TikTok</a></li>
          <li><a href="#">YouTube</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>
    </div>
  </div>
  <div class="foot-bot">
    <div class="foot-copy">© 2025 Summer Rose-Thompson · Becoming Inspiration · All rights reserved.</div>
  </div>
</footer>

<script>
// CURSOR
const c=document.getElementById('cur'),cr=document.getElementById('curR');
document.addEventListener('mousemove',e=>{
  c.style.left=e.clientX+'px';c.style.top=e.clientY+'px';
  cr.style.left=e.clientX+'px';cr.style.top=e.clientY+'px';
});

// THREE.JS — Rotating 3D Book
const canvas=document.getElementById('book-canvas');
const renderer=new THREE.WebGLRenderer({canvas,antialias:true,alpha:true});
renderer.setPixelRatio(Math.min(devicePixelRatio,2));
renderer.toneMapping=THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure=1.4;
renderer.shadowMap.enabled=true;

const scene=new THREE.Scene();
const camera=new THREE.PerspectiveCamera(38,innerWidth/innerHeight,0.1,100);
camera.position.set(0,0,7);

function rsz(){renderer.setSize(innerWidth,innerHeight);camera.aspect=innerWidth/innerHeight;camera.updateProjectionMatrix();}
rsz();window.addEventListener('resize',rsz);

// CINEMATIC LIGHTS — matching the Stitch render
const amb=new THREE.AmbientLight(0x0A0806,3);
scene.add(amb);

// Key — warm gold from top right (matches book render lighting)
const key=new THREE.SpotLight(0xFFD080,25,20,Math.PI/5,.3);
key.position.set(4,5,5);
key.castShadow=true;
scene.add(key);

// Fill — cool dim from left
const fill=new THREE.PointLight(0x4060A0,4,16);
fill.position.set(-5,-1,3);
scene.add(fill);

// Rim — warm gold edge glow
const rim=new THREE.PointLight(0xC9A84C,8,12);
rim.position.set(2,-3,-3);
scene.add(rim);

// Ground bounce
const bounce=new THREE.PointLight(0x8B6020,5,10);
bounce.position.set(0,-4,2);
scene.add(bounce);

// BOOK GEOMETRY — realistic proportions
const bookW=1.6, bookH=2.2, bookD=0.28;

// Cover material — dark charcoal like the render
const coverM=new THREE.MeshStandardMaterial({
  color:0x1A1510,
  metalness:0.05,
  roughness:0.75,
});

// Spine material — gold
const spineM=new THREE.MeshStandardMaterial({
  color:0xC9A84C,
  metalness:0.7,
  roughness:0.25,
  emissive:0x3D2800,
  emissiveIntensity:0.2,
});

// Pages material — cream
const pagesM=new THREE.MeshStandardMaterial({
  color:0xF0E8D8,
  metalness:0,
  roughness:0.95,
});

// Gold text emboss material
const goldM=new THREE.MeshStandardMaterial({
  color:0xD4A843,
  metalness:0.85,
  roughness:0.2,
  emissive:0x3A2000,
  emissiveIntensity:0.15,
});

// BUILD BOOK GROUP
const book=new THREE.Group();

// Main cover body
const coverGeo=new THREE.BoxGeometry(bookW,bookH,bookD);
const coverMats=[
  spineM,  // right (spine side)
  pagesM,  // left (pages side)
  pagesM,  // top
  pagesM,  // bottom
  coverM,  // front cover
  coverM,  // back cover
];
const coverMesh=new THREE.Mesh(coverGeo,coverMats);
book.add(coverMesh);

// Gold spine accent
const spineGeo=new THREE.BoxGeometry(0.06,bookH,bookD+0.01);
const spineMesh=new THREE.Mesh(spineGeo,spineM);
spineMesh.position.x=-bookW/2+0.03;
book.add(spineMesh);

// Title text blocks (embossed gold rectangles)
const titleLine1=new THREE.Mesh(new THREE.BoxGeometry(0.9,0.08,0.01),goldM);
titleLine1.position.set(0.1,0.5,bookD/2+0.005);
book.add(titleLine1);

const titleLine2=new THREE.Mesh(new THREE.BoxGeometry(1.1,0.08,0.01),goldM);
titleLine2.position.set(0.1,0.35,bookD/2+0.005);
book.add(titleLine2);

const titleLine3=new THREE.Mesh(new THREE.BoxGeometry(0.7,0.08,0.01),goldM);
titleLine3.position.set(0.1,0.2,bookD/2+0.005);
book.add(titleLine3);

// Author name line
const authorLine=new THREE.Mesh(new THREE.BoxGeometry(0.8,0.04,0.01),goldM);
authorLine.position.set(0.1,-0.7,bookD/2+0.005);
book.add(authorLine);

// Decorative corner accents
const cornerGeo=new THREE.BoxGeometry(0.15,0.15,0.01);
[[-.65,.9],[.65,.9],[-.65,-.9],[.65,-.9]].forEach(([x,y])=>{
  const corner=new THREE.Mesh(cornerGeo,goldM);
  corner.position.set(x,y,bookD/2+0.005);
  book.add(corner);
});

// Shadow plane
const shadowGeo=new THREE.PlaneGeometry(4,4);
const shadowM=new THREE.MeshStandardMaterial({color:0x000000,transparent:true,opacity:0.4});
const shadow=new THREE.Mesh(shadowGeo,shadowM);
shadow.rotation.x=-Math.PI/2;
shadow.position.y=-1.5;
book.add(shadow);

scene.add(book);

// PARTICLES — dust motes
const pGeo=new THREE.BufferGeometry();
const pPos=new Float32Array(150*3);
for(let i=0;i<450;i++)pPos[i]=(Math.random()-.5)*(i%3===2?8:18);
pGeo.setAttribute('position',new THREE.BufferAttribute(pPos,3));
scene.add(new THREE.Points(pGeo,new THREE.PointsMaterial({
  color:0xC9A84C,size:0.025,transparent:true,opacity:0.2
})));

// SCROLL
let scrollP=0,targetP=0;
window.addEventListener('scroll',()=>{
  const el=document.getElementById('scroll-driver');
  const sc=-el.getBoundingClientRect().top;
  const tot=el.offsetHeight-innerHeight;
  targetP=Math.max(0,Math.min(1,sc/tot));
  // parallax title
  const p=Math.min(scrollY/(innerHeight*2),1);
  document.getElementById('pt').style.transform=`translateY(${p*-28}px)`;
});

// Mouse parallax on book
let mx=0,my=0;
document.addEventListener('mousemove',e=>{
  mx=(e.clientX/innerWidth-.5)*2;
  my=(e.clientY/innerHeight-.5)*2;
});

function lerp(a,b,t){return a+(b-a)*t;}

const clk=new THREE.Clock();
(function loop(){
  requestAnimationFrame(loop);
  const dt=clk.getDelta(),et=clk.getElapsedTime();

  scrollP+=(targetP-scrollP)*.05;

  // Book position — right side hero, moves forward on scroll
  book.position.x=lerp(2.2,0,scrollP);
  book.position.y=lerp(0,.3,scrollP)+Math.sin(et*.6)*.06;
  book.position.z=lerp(0,1.5,scrollP);

  // Gentle auto rotation + mouse parallax
  book.rotation.y=lerp(-.3,.3,scrollP)+Math.sin(et*.25)*.15+mx*.08;
  book.rotation.x=Math.sin(et*.18)*.04+my*.04;
  book.rotation.z=Math.sin(et*.12)*.02;

  // Key light pulse — like the golden hour light in the render
  key.intensity=25+Math.sin(et*.8)*4;
  rim.intensity=8+Math.sin(et*1.1)*2;

  renderer.render(scene,camera);
})();

// Hero load
setTimeout(()=>document.body.classList.add('loaded'),200);

// Book spin CSS
const style=document.createElement('style');
style.textContent=`@keyframes bookSpin{0%{transform:rotateY(-8deg);}50%{transform:rotateY(8deg);}100%{transform:rotateY(-8deg);}}`;
document.head.appendChild(style);
</script>

</body>
</html>