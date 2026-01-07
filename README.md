<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ORCHESTRA</title>

  <style>
    :root{
      /* Pink/Black theme */
      --bg-dark:#0b0206;
      --bg-deep:#1a060d;
      --glow-pink:#ff3d6e;
      --pink:#ff4d73;
      --pink2:#ff6aa0;

      --card:rgba(25,7,13,0.82);
      --card2:rgba(25,7,13,0.92);
      --stroke:rgba(255,255,255,0.08);
      --text:#ffffff;
      --muted:rgba(255,255,255,0.72);

      --shadow:0 22px 60px rgba(0,0,0,0.55);
      --shadow2:0 12px 30px rgba(0,0,0,0.45);
      --radius:22px;
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: Inter, Segoe UI, -apple-system, Arial, sans-serif;
      color:var(--text);
      background:
        radial-gradient(900px 700px at 10% 20%, rgba(255,61,110,0.75), transparent 60%),
        radial-gradient(700px 600px at 85% 40%, rgba(255,77,115,0.15), transparent 55%),
        radial-gradient(900px 700px at 85% 85%, rgba(255,106,160,0.16), transparent 58%),
        linear-gradient(135deg, var(--bg-deep), var(--bg-dark));
      background-attachment: fixed;
      overflow-x:hidden;
    }

    /* subtle background icons */
    .bg-note{
      position:fixed;
      left:7%;
      bottom:12%;
      opacity:.08;
      font-size:140px;
      transform:rotate(-10deg);
      pointer-events:none;
      user-select:none;
      z-index:0;
    }
    .bg-disc{
      position:fixed;
      right:12%;
      top:40%;
      opacity:.08;
      width:140px;
      height:140px;
      border-radius:50%;
      border:10px solid rgba(255,255,255,0.35);
      box-shadow: inset 0 0 0 18px rgba(255,255,255,0.12);
      pointer-events:none;
      user-select:none;
      z-index:0;
    }
    .bg-disc::after{
      content:"";
      position:absolute;
      inset:50% auto auto 50%;
      transform:translate(-50%,-50%);
      width:18px;height:18px;border-radius:50%;
      background:rgba(255,255,255,0.45);
    }

    /* Top nav */
    .topbar{
      position:fixed;
      top:14px; left:50%;
      transform:translateX(-50%);
      z-index:1000;

      display:flex;
      align-items:center;
      gap:10px;
      padding:10px 14px;

      background:rgba(20,5,10,0.55);
      border:1px solid var(--stroke);
      backdrop-filter: blur(12px);
      border-radius:999px;
      box-shadow:var(--shadow2);
      max-width:calc(100% - 24px);
      overflow:auto;
      scrollbar-width:none;
    }
    .topbar::-webkit-scrollbar{display:none}

    .brand-mini{
      font-weight:900;
      letter-spacing:2px;
      color:var(--pink);
      margin-right:8px;
      white-space:nowrap;
    }
    .navlinks{display:flex;gap:8px;align-items:center}
    .navlinks a{
      text-decoration:none;
      color:rgba(255,255,255,0.92);
      font-weight:800;
      padding:10px 12px;
      border-radius:999px;
      transition:all .18s ease;
      white-space:nowrap;
    }
    .navlinks a:hover{
      background:rgba(255,77,115,0.14);
      box-shadow:0 0 0 1px rgba(255,77,115,0.25) inset;
    }

    .status{
      display:flex;align-items:center;gap:8px;
      padding:6px 10px;
      border-radius:999px;
      border:1px solid rgba(255,255,255,0.12);
      background:rgba(0,0,0,0.25);
      margin-left:6px;
      white-space:nowrap;
    }
    .dot{width:10px;height:10px;border-radius:50%;background:#ff6b6b;border:1px solid rgba(255,255,255,0.5)}
    .status span{font-weight:800;color:rgba(255,255,255,0.9);font-size:.92rem}

    /* Layout containers */
    .wrap{
      position:relative;
      z-index:2;
      max-width:1100px;
      margin:0 auto;
      padding:86px 16px 46px;
    }

    /* Home hero card */
    .hero{
      display:grid;
      grid-template-columns: 1.15fr .85fr;
      gap:18px;
      align-items:stretch;
    }
    @media (max-width: 900px){
      .hero{grid-template-columns:1fr}
    }

    .panel{
      background:var(--card);
      border:1px solid var(--stroke);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      backdrop-filter: blur(14px);
      overflow:hidden;
    }

    .hero-left{
      padding:26px 22px 20px;
      position:relative;
    }
    .title{
      margin:0;
      font-size:3.2rem;
      letter-spacing:3px;
      font-weight:900;
      color:var(--pink);
      text-transform:uppercase;
    }
    .tagline{
      margin:8px 0 0;
      color:var(--muted);
      font-weight:600;
      line-height:1.55;
      max-width:720px;
    }
    .intro{
      margin:14px 0 0;
      padding:14px 14px;
      border-radius:16px;
      background:rgba(0,0,0,0.22);
      border:1px solid rgba(255,255,255,0.08);
      color:rgba(255,255,255,0.86);
      line-height:1.65;
      font-weight:600;
    }
    .members{
      margin:10px 0 0;
      color:rgba(255,255,255,0.74);
      font-weight:700;
      font-size:.96rem;
    }
    .members strong{color:rgba(255,255,255,0.92)}
    .cta-row{
      display:flex;
      gap:12px;
      flex-wrap:wrap;
      margin-top:16px;
      align-items:center;
    }
    .btn{
      border:none;
      cursor:pointer;
      padding:13px 18px;
      border-radius:999px;
      font-weight:900;
      box-shadow:var(--shadow2);
      transition:transform .16s ease, filter .16s ease, box-shadow .16s ease;
    }
    .btn:active{transform:translateY(1px)}
    .btn.primary{
      background:linear-gradient(90deg, var(--pink), var(--pink2));
      color:#13040a;
    }
    .btn.ghost{
      background:transparent;
      color:rgba(255,255,255,0.9);
      border:1px solid rgba(255,77,115,0.55);
      box-shadow:none;
    }
    .btn.ghost:hover{background:rgba(255,77,115,0.14)}

    /* Hero right image panel */
    .hero-right{
      position:relative;
      min-height:260px;
      display:flex;
      align-items:stretch;
      justify-content:stretch;
    }
    .hero-img{
      width:100%;
      height:100%;
      object-fit:cover;
      filter:saturate(1.05) contrast(1.05);
      transform:scale(1.02);
    }
    .img-overlay{
      position:absolute; inset:0;
      background:
        radial-gradient(400px 300px at 20% 20%, rgba(255,77,115,0.35), transparent 60%),
        linear-gradient(180deg, rgba(0,0,0,0.05), rgba(10,2,6,0.65));
    }
    .hero-right .badge{
      position:absolute;
      left:16px; bottom:14px;
      padding:10px 12px;
      border-radius:16px;
      background:rgba(0,0,0,0.35);
      border:1px solid rgba(255,255,255,0.12);
      backdrop-filter: blur(10px);
      color:rgba(255,255,255,0.9);
      font-weight:800;
      box-shadow:var(--shadow2);
    }

    /* Artists grid */
    .section-title{
      margin:22px 0 12px;
      font-size:1.35rem;
      font-weight:900;
      letter-spacing:.3px;
      color:rgba(255,255,255,0.92);
    }
    .grid{
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(230px, 1fr));
      gap:16px;
    }
    .card{
      background:rgba(0,0,0,0.22);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:18px;
      overflow:hidden;
      box-shadow:var(--shadow2);
      cursor:pointer;
      transition:transform .18s ease, box-shadow .18s ease;
    }
    .card:hover{transform:translateY(-4px)}
    .cover{width:100%;height:160px;object-fit:cover}
    .card-body{padding:12px 12px 14px}
    .card-title{margin:0;font-weight:900}
    .card-sub{margin:6px 0 0;color:rgba(255,255,255,0.70);font-weight:600}

    /* Shared sections */
    .section{
      margin-top:18px;
      padding:20px;
      background:var(--card2);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      backdrop-filter: blur(14px);
    }
    .section h2{
      margin:0 0 8px;
      font-weight:900;
      color:rgba(255,255,255,0.95);
      letter-spacing:.2px;
    }
    .subtitle{
      margin:0;
      color:var(--muted);
      font-weight:600;
      line-height:1.55;
    }
    .hidden{display:none !important;}

    /* Mood cards */
    .mood-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px;margin-top:12px}
    .mood{
      background:rgba(0,0,0,0.22);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:16px;
      padding:14px;
      text-align:center;
      cursor:pointer;
      transition:transform .15s ease, box-shadow .15s ease;
    }
    .mood:hover{
      transform:translateY(-2px);
      box-shadow:0 0 0 1px rgba(255,77,115,0.22) inset;
    }
    .emoji{font-size:1.7rem;margin-bottom:8px}

    /* Playlist box */
    .playlist{
      margin-top:10px;
      background:rgba(0,0,0,0.22);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:16px;
      padding:14px;
    }
    .playlist h3{margin:4px 0 10px;font-weight:900;color:rgba(255,255,255,0.95)}
    .playlist ul{list-style:none;margin:0;padding:0}
    .playlist li{margin:8px 0}
    .playlist a{
      color:rgba(255,106,160,0.95);
      font-weight:800;
      text-decoration:none;
    }
    .playlist a:hover{text-decoration:underline}

    /* Login (styled like screenshot) */
    .auth-wrap{max-width:520px;margin:0 auto;}
    .auth-head{text-align:center;margin-bottom:14px;}
    .auth-title{
      margin:0;font-size:2.6rem;font-weight:900;color:var(--pink);
      letter-spacing:3px;text-transform:uppercase;
    }
    .auth-sub{margin:8px 0 0;color:rgba(255,255,255,0.75);font-weight:600;}

    .field{margin-top:12px;position:relative;}
    .input{
      width:100%;
      padding:14px 14px 14px 46px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,0.10);
      background:rgba(0,0,0,0.32);
      color:rgba(255,255,255,0.92);
      outline:none;
      font-weight:700;
      font-size:1rem;
    }
    .input::placeholder{color:rgba(255,255,255,0.45);font-weight:700}
    .icon{
      position:absolute;left:14px;top:50%;
      transform:translateY(-50%);
      opacity:.85;width:18px;height:18px;fill:rgba(255,255,255,0.78);
    }

    .auth-actions{
      display:flex;flex-direction:column;gap:10px;margin-top:14px;
    }
    .btn.full{width:100%}
    .divider{text-align:center;margin:10px 0 6px;color:rgba(255,255,255,0.55);font-weight:800;}
    .btn.outline{
      background:transparent;border:1px solid rgba(255,77,115,0.55);
      color:rgba(255,106,160,0.92);box-shadow:none;
    }
    .btn.outline:hover{background:rgba(255,77,115,0.12)}
    .note-error{margin:10px 0 0;color:#ff8a8a;font-weight:800;text-align:center;}

    /* Premium toggle UI */
    .premium-box{
      max-width:820px;
      margin:0 auto;
      background:rgba(0,0,0,0.22);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:18px;
      padding:16px;
    }
    .premium-row{
      display:flex;
      gap:14px;
      justify-content:space-between;
      align-items:center;
      flex-wrap:wrap;
    }
    .price{
      font-weight:900;
      color:rgba(255,255,255,0.92);
      margin-top:6px;
    }
    .price span{color:var(--pink2)}
    .toggle-wrap{
      display:flex;
      align-items:center;
      gap:10px;
      user-select:none;
    }
    .toggle-label{
      font-weight:900;
      color:rgba(255,255,255,0.88);
      letter-spacing:.2px;
    }
    .switch{
      position:relative;
      width:56px;height:32px;
      border-radius:999px;
      background:rgba(255,255,255,0.16);
      border:1px solid rgba(255,255,255,0.16);
      cursor:pointer;
      transition:background .2s ease, box-shadow .2s ease;
      box-shadow:0 0 0 1px rgba(255,77,115,0.0) inset;
    }
    .switch::after{
      content:"";
      position:absolute;
      top:4px; left:4px;
      width:24px; height:24px;
      border-radius:50%;
      background:rgba(255,255,255,0.75);
      transition:left .2s ease, background .2s ease;
      box-shadow:0 10px 20px rgba(0,0,0,0.4);
    }
    .switch.on{
      background:rgba(255,77,115,0.35);
      box-shadow:0 0 0 1px rgba(255,77,115,0.25) inset;
    }
    .switch.on::after{
      left:28px;
      background:linear-gradient(90deg, var(--pink), var(--pink2));
    }
    .premium-state{
      margin-top:14px;
      display:flex;
      gap:10px;
      align-items:center;
      flex-wrap:wrap;
      font-weight:900;
    }
    .pill{
      padding:8px 12px;
      border-radius:999px;
      border:1px solid rgba(255,255,255,0.14);
      background:rgba(0,0,0,0.20);
      color:rgba(255,255,255,0.85);
    }
    .pill.on{
      border-color:rgba(255,77,115,0.45);
      background:rgba(255,77,115,0.14);
      color:rgba(255,255,255,0.92);
    }
    .features{
      margin-top:14px;
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(220px, 1fr));
      gap:10px;
    }
    .feature{
      background:rgba(0,0,0,0.20);
      border:1px solid rgba(255,255,255,0.10);
      border-radius:16px;
      padding:12px;
      color:rgba(255,255,255,0.86);
      font-weight:800;
      line-height:1.4;
    }
    .feature small{
      display:block;
      margin-top:6px;
      color:rgba(255,255,255,0.62);
      font-weight:700;
    }

    footer{
      text-align:center;
      color:rgba(255,255,255,0.55);
      font-weight:700;
      margin:18px 0 6px;
    }
  </style>
</head>

<body>
  <div class="bg-note">♪</div>
  <div class="bg-disc" aria-hidden="true"></div>

  <!-- Navigation menu -->
  <nav class="topbar">
    <div class="brand-mini">ORCHESTRA</div>

    <div class="navlinks">
      <a href="#landing" onclick="navigate('landing')">Home</a>
      <a href="#about" onclick="navigate('about')">About us</a>
      <a href="#premium" onclick="navigate('premium')">Premium</a>
      <a href="#login" onclick="navigate('login')">Login</a>
    </div>

    <div class="status" title="Session status">
      <span id="statusDot" class="dot"></span>
      <span id="statusText">Guest</span>
    </div>
  </nav>

  <main class="wrap">
    <!-- HOME -->
    <section id="landing">
      <div class="hero">
        <div class="panel hero-left">
          <h1 class="title">ORCHESTRA</h1>
          <p class="tagline">Music that understands your mood 🎧</p>

          <div class="intro">
            Welcome to ORCHESTRA Where music meets your identity. Create your profile, build your playlists, and let every beat reflect your mood.
            At ORCHESTRA, you don’t just listen you lead the rhythm. Your music. Your orchestra.
          </div>

          <div class="members">
            <strong>Group members:</strong> Malaika Noor • Sultan Abdul Hadi • Javaria Naveed
          </div>

          <div class="cta-row">
            <button class="btn primary" onclick="scrollToArtists()">Explore artists</button>
            <button class="btn ghost" onclick="navigate('login')">Login</button>
          </div>
        </div>

        <div class="panel hero-right" aria-label="Music mood illustration">
          
          <div class="img-overlay"></div>
          <div class="badge">Pick an artist → Pick a mood → Get songs</div>
        </div>
      </div>

      <h3 class="section-title" id="artistsTitle">Artists</h3>

      <div class="grid">
        <!-- Existing -->
        <div class="card" onclick="selectArtist('Taylor Swift')">
         
          <div class="card-body">
            <h3 class="card-title">Taylor Swift</h3>
            <p class="card-sub">Pop • Storytelling • Anthems</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Kodaline')">
     
          <div class="card-body">
            <h3 class="card-title">Kodaline</h3>
            <p class="card-sub">Indie • Melodic • Emotion</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Coldplay')">
          
          <div class="card-body">
            <h3 class="card-title">Coldplay</h3>
            <p class="card-sub">Alt Rock • Uplifting • Classic</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Ed Sheeran')">
         
          <div class="card-body">
            <h3 class="card-title">Ed Sheeran</h3>
            <p class="card-sub">Pop • Acoustic • Heartfelt</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Talwiinder')">
         
          <div class="card-body">
            <h3 class="card-title">Talwiinder</h3>
            <p class="card-sub">Punjabi • Urban • Vibes</p>
          </div>
        </div>

        <!-- Added artists -->
        <div class="card" onclick="selectArtist('Radiohead')">
          
          <div class="card-body">
            <h3 class="card-title">Radiohead</h3>
            <p class="card-sub">Alt Rock • Experimental • Iconic</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('M83')">
         
          <div class="card-body">
            <h3 class="card-title">M83</h3>
            <p class="card-sub">Synth • Dreamy • Cinematic</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Bayaan')">
          
          <div class="card-body">
            <h3 class="card-title">Bayaan</h3>
            <p class="card-sub">Pakistani Rock • Poetry • Soul</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Hassan Raheem')">
          
          <div class="card-body">
            <h3 class="card-title">Hassan Raheem</h3>
            <p class="card-sub">Pop • Chill • Pakistani Vibes</p>
          </div>
        </div>

        <div class="card" onclick="selectArtist('Gracie Abrams')">
          
          <div class="card-body">
            <h3 class="card-title">Gracie Abrams</h3>
            <p class="card-sub">Indie Pop • Soft • Emotional</p>
          </div>
        </div>
      </div>

      <!-- Mood section -->
      <div class="section hidden" id="moodSection">
        <h2 id="moodTitle">Pick your mood</h2>
        <p class="subtitle" style="text-align:center;margin-top:6px;">
          Choose how you feel to tailor the playlist.
        </p>

        <div class="mood-grid">
          <div class="mood" onclick="chooseMood('Happy')">
            <div class="emoji">😄</div>
            <div><strong>Happy</strong><br/><small style="color:rgba(255,255,255,0.65);font-weight:700;">Bright, upbeat</small></div>
          </div>
          <div class="mood" onclick="chooseMood('Sad')">
            <div class="emoji">😢</div>
            <div><strong>Sad</strong><br/><small style="color:rgba(255,255,255,0.65);font-weight:700;">Soft, reflective</small></div>
          </div>
          <div class="mood" onclick="chooseMood('Excited')">
            <div class="emoji">🤩</div>
            <div><strong>Excited</strong><br/><small style="color:rgba(255,255,255,0.65);font-weight:700;">Energetic, high tempo</small></div>
          </div>
        </div>
      </div>

      <!-- Playlist section -->
      <div class="section hidden" id="playlistSection">
        <h2>Your playlist</h2>
        <p class="subtitle" id="playlistMeta" style="text-align:center;margin-top:6px;"></p>
        <div class="playlist" id="playlistBox"></div>
        <div style="text-align:center;margin-top:14px;">
          <button class="btn ghost" onclick="resetFlow()">Reset selection</button>
        </div>
      </div>
    </section>

    <!-- LOGIN -->
    <section id="login" class="section hidden">
      <div class="auth-wrap">
        <div class="auth-head">
          <h2 class="auth-title">ORCHESTRA</h2>
          <p class="auth-sub">Music that understands your mood 🎧</p>
        </div>

        <div class="field">
          <svg class="icon" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4-8 5-8-5V6l8 5 8-5v2z"/>
          </svg>
          <input id="loginUser" class="input" type="text" placeholder="Email / Username"/>
        </div>

        <div class="field">
          <svg class="icon" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M12 17a2 2 0 1 0 0-4 2 2 0 0 0 0 4zm6-7h-1V8a5 5 0 0 0-10 0v2H6c-1.1 0-2 .9-2 2v8c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2v-8c0-1.1-.9-2-2-2zm-3 0H9V8a3 3 0 0 1 6 0v2z"/>
          </svg>
          <input id="loginPass" class="input" type="password" placeholder="Password"/>
        </div>

        <div class="auth-actions">
          <button class="btn primary full" onclick="doLogin()">Log In</button>
          <div class="divider">or</div>
          <button class="btn outline full" onclick="continueGuest()">Continue without Login</button>
          <p id="loginNote" class="note-error"></p>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="section hidden">
      <h2>About us</h2>
      <p class="subtitle">
        ORCHESTRA is a first-semester ICT project that recommends songs based on the user’s chosen artist and mood.
        It showcases how simple web technologies can create a personalized experience.
      </p>

      <div style="height:1px;background:rgba(255,255,255,0.10);margin:14px 0;"></div>

      <p style="margin:0 0 6px;font-weight:900;color:rgba(255,255,255,0.92);">Team</p>
      <ul style="margin:8px 0 0;padding-left:18px;color:rgba(255,255,255,0.78);font-weight:700;line-height:1.7;">
        <li>Malaika Noor</li>
        <li>Sultan Abdul Hadi</li>
        <li>Javaria Naveed</li>
      </ul>
    </section>

    <!-- PREMIUM (updated with toggle) -->
    <section id="premium" class="section hidden">
      <h2>Premium</h2>
      <p class="subtitle">Unlock premium for <strong style="color:rgba(255,255,255,0.95)">500Rs / month</strong> and level up your listening.</p>

      <div class="premium-box" style="margin-top:14px;">
        <div class="premium-row">
          <div>
            <div style="font-weight:900;font-size:1.15rem;color:rgba(255,255,255,0.92);">
              Unlock Premium
            </div>
            <div class="price">Price: <span>500Rs</span> per month</div>
          </div>

          <div class="toggle-wrap">
            <div class="toggle-label" id="premiumLabel">Locked</div>
            <div class="switch" id="premiumSwitch" role="switch" aria-checked="false" tabindex="0"
                 onclick="togglePremium()" onkeydown="if(event.key==='Enter' || event.key===' '){event.preventDefault();togglePremium();}">
            </div>
          </div>
        </div>

        <div class="premium-state">
          <div class="pill" id="pillStatus">Premium: OFF</div>
          <div class="pill" id="pillAds">Ads: ON</div>
          <div class="pill" id="pillBg">Background Play: OFF</div>
          <div class="pill" id="pillLyrics">Lyrics: OFF</div>
        </div>

        <div class="features" style="margin-top:14px;">
          <div class="feature">
            🎤 Lyrics
            <small>See synced lyrics while listening.</small>
          </div>
          <div class="feature">
            🚫 Block Ads
            <small>Enjoy ad-free music sessions.</small>
          </div>
          <div class="feature">
            🌙 Play in Background
            <small>Keep music playing while using other apps.</small>
          </div>
          <div class="feature">
            🎉 Music Sharing (Live Party / Jam)
            <small>Listen together in real-time.</small>
          </div>
          <div class="feature">
            ✨ Magic Shuffle
            <small>Smart shuffle based on mood + taste.</small>
          </div>
          <div class="feature">
            🔥 Many more features
            <small>More upgrades coming soon.</small>
          </div>
        </div>

        <div style="text-align:center;margin-top:14px;">
          <button class="btn primary" onclick="togglePremium()">
            Toggle Premium
          </button>
        </div>
      </div>
    </section>

    <footer>© 2026 ORCHESTRA</footer>
  </main>

  <script>
    let isLogged = false;
    let chosenArtist = null;
    let chosenMood = null;

    // Premium state
    let premiumEnabled = false;

    function showOnly(idsToShow){
      const ids = ['landing','login','about','premium'];
      ids.forEach(id=>{
        const el = document.getElementById(id);
        if(!el) return;
        el.classList.toggle('hidden', !idsToShow.includes(id));
      });
    }

    function navigate(id){
      if(id === 'landing'){
        showOnly(['landing']);
        window.scrollTo({top:0, behavior:'smooth'});
        history.pushState(null, '', '#landing');
        return;
      }

      if(!isLogged && id !== 'login'){
        showOnly(['login']);
        document.getElementById('loginNote').textContent =
          'Please log in or continue without login to access other sections.';
        history.pushState(null, '', '#login');
        return;
      }

      showOnly([id]);
      history.pushState(null, '', '#' + id);
      window.scrollTo({top:0, behavior:'smooth'});
    }

    function scrollToArtists(){
      const el = document.getElementById('artistsTitle');
      if(el) el.scrollIntoView({behavior:'smooth', block:'start'});
    }

    function selectArtist(artist){
      chosenArtist = artist;
      chosenMood = null;

      document.getElementById('moodTitle').textContent = `Pick your mood for ${artist}`;
      document.getElementById('moodSection').classList.remove('hidden');

      document.getElementById('playlistSection').classList.add('hidden');
      document.getElementById('playlistBox').innerHTML = '';
      document.getElementById('playlistMeta').textContent = '';

      document.getElementById('moodSection').scrollIntoView({behavior:'smooth', block:'start'});
    }

    function chooseMood(mood){
      chosenMood = mood;
      generatePlaylist();
    }

    function resetFlow(){
      chosenArtist = null;
      chosenMood = null;
      document.getElementById('moodSection').classList.add('hidden');
      document.getElementById('playlistSection').classList.add('hidden');
      window.scrollTo({top:0, behavior:'smooth'});
    }

    function doLogin(){
      const u = document.getElementById('loginUser').value.trim();
      const p = document.getElementById('loginPass').value.trim();

      if(!u || !p){
        document.getElementById('loginNote').textContent = 'Enter both email/username and password.';
        return;
      }

      isLogged = true;
      document.getElementById('statusText').textContent = u;
      document.getElementById('statusDot').style.background = '#86efac';
      document.getElementById('loginNote').textContent = '';
      navigate('landing');
    }

    function continueGuest(){
      isLogged = true;
      document.getElementById('statusText').textContent = 'Guest';
      document.getElementById('statusDot').style.background = '#86efac';
      document.getElementById('loginNote').textContent = '';
      navigate('landing');
    }

    function togglePremium(){
      premiumEnabled = !premiumEnabled;

      const sw = document.getElementById('premiumSwitch');
      const lbl = document.getElementById('premiumLabel');

      const pillStatus = document.getElementById('pillStatus');
      const pillAds = document.getElementById('pillAds');
      const pillBg = document.getElementById('pillBg');
      const pillLyrics = document.getElementById('pillLyrics');

      if(premiumEnabled){
        sw.classList.add('on');
        sw.setAttribute('aria-checked','true');
        lbl.textContent = 'Unlocked';

        pillStatus.textContent = 'Premium: ON';
        pillStatus.classList.add('on');

        pillAds.textContent = 'Ads: OFF';
        pillAds.classList.add('on');

        pillBg.textContent = 'Background Play: ON';
        pillBg.classList.add('on');

        pillLyrics.textContent = 'Lyrics: ON';
        pillLyrics.classList.add('on');
      }else{
        sw.classList.remove('on');
        sw.setAttribute('aria-checked','false');
        lbl.textContent = 'Locked';

        pillStatus.textContent = 'Premium: OFF';
        pillStatus.classList.remove('on');

        pillAds.textContent = 'Ads: ON';
        pillAds.classList.remove('on');

        pillBg.textContent = 'Background Play: OFF';
        pillBg.classList.remove('on');

        pillLyrics.textContent = 'Lyrics: OFF';
        pillLyrics.classList.remove('on');
      }
    }

    const playlists = {
      "Taylor Swift": [
        { title: "Blank Space", url: "https://www.youtube.com/watch?v=e-ORhEE9VVg" },
        { title: "Shake It Off", url: "https://www.youtube.com/watch?v=nfWlot6h_JM" },
        { title: "Style", url: "https://www.youtube.com/watch?v=-CmadmM5cOk" },
        { title: "Love Story (Taylor’s Version)", url: "https://www.youtube.com/watch?v=sRxrwjOtIag" },
        { title: "You Belong With Me (Taylor’s Version)", url: "https://www.youtube.com/watch?v=8xg3vE8Ie_E" },
        { title: "ME! (feat. Brendon Urie)", url: "https://www.youtube.com/watch?v=FuXNumBwDOM" },
        { title: "The Man", url: "https://www.youtube.com/watch?v=AqAJLh9wuZ0" },
        { title: "willow", url: "https://www.youtube.com/watch?v=RsEZmictANA" },
        { title: "cardigan", url: "https://www.youtube.com/watch?v=b1kbLwvqugk" },
        { title: "Bejeweled", url: "https://www.youtube.com/watch?v=b7QlX3yR2xs" }
      ],
      "Kodaline": [
        { title: "All I Want", url: "https://www.youtube.com/watch?v=mtf7hC17IBM" },
        { title: "High Hopes", url: "https://www.youtube.com/watch?v=1yYV9-KoSUM" },
        { title: "Brother", url: "https://www.youtube.com/watch?v=VdA1c5mP9bg" },
        { title: "The One", url: "https://www.youtube.com/watch?v=cmjcYElJxBg" },
        { title: "Ready", url: "https://www.youtube.com/watch?v=RzWlU7K0wYg" },
        { title: "Love Like This", url: "https://www.youtube.com/watch?v=3yqM--IMkX4" },
        { title: "Follow Your Fire", url: "https://www.youtube.com/watch?v=zM3D3cGJ5kw" },
        { title: "One Day", url: "https://www.youtube.com/watch?v=3Xr1Gqzv0bY" },
        { title: "Honest", url: "https://www.youtube.com/watch?v=Rji0i6QFqkg" },
        { title: "Wherever You Are", url: "https://www.youtube.com/watch?v=V6QhC8kE4-4" }
      ],
      "Coldplay": [
        { title: "Yellow", url: "https://www.youtube.com/watch?v=yKNxeF4KMsY" },
        { title: "The Scientist", url: "https://www.youtube.com/watch?v=RB-RcX5DS5A" },
        { title: "Paradise", url: "https://www.youtube.com/watch?v=1G4isv_Fylg" },
        { title: "Viva La Vida", url: "https://www.youtube.com/watch?v=dvgZkm1xWPE" },
        { title: "Hymn for the Weekend", url: "https://www.youtube.com/watch?v=YykjpeuMNEk" },
        { title: "A Sky Full of Stars", url: "https://www.youtube.com/watch?v=VPRjCeoBqrI" },
        { title: "Clocks", url: "https://www.youtube.com/watch?v=d020hcWA_Wg" },
        { title: "Fix You", url: "https://www.youtube.com/watch?v=k4V3Mo61fJM" },
        { title: "Adventure of a Lifetime", url: "https://www.youtube.com/watch?v=QtXby3twMmI" },
        { title: "Something Just Like This", url: "https://www.youtube.com/watch?v=FM7MFYoylVs" }
      ],
      "Ed Sheeran": [
        { title: "Shape of You", url: "https://www.youtube.com/watch?v=JGwWNGJdvx8" },
        { title: "Perfect", url: "https://www.youtube.com/watch?v=2Vv-BfVoq4g" },
        { title: "Thinking Out Loud", url: "https://www.youtube.com/watch?v=lp-EO5I60KA" },
        { title: "Photograph", url: "https://www.youtube.com/watch?v=nSDgHBxUbVQ" },
        { title: "Give Me Love", url: "https://www.youtube.com/watch?v=FOjdXSrtUxA" },
        { title: "Lego House", url: "https://www.youtube.com/watch?v=c4BLVznuWnU" },
        { title: "The A Team", url: "https://www.youtube.com/watch?v=UAWcs5H-qgQ" },
        { title: "Castle on the Hill", url: "https://www.youtube.com/watch?v=7M7C3Y0l7bU" },
        { title: "Galway Girl", url: "https://www.youtube.com/watch?v=87gWaABqGYs" },
        { title: "Shivers", url: "https://www.youtube.com/watch?v=Il0S8BoucSA" }
      ],
      "Talwiinder": [
        { title: "Haseena", url: "https://www.youtube.com/watch?v=mr32Zp42oAo" },
        { title: "Samhaal", url: "https://www.youtube.com/watch?v=9Q0YE0rb9A8" },
        { title: "Jhanjar", url: "https://www.youtube.com/watch?v=1iCwqGZc3Jc" },
        { title: "Jatti Lover", url: "https://www.youtube.com/watch?v=9xHkJQFzD0w" },
        { title: "Adhiya", url: "https://www.youtube.com/watch?v=2vF4e3yq1aM" },
        { title: "Gedi Route", url: "https://www.youtube.com/watch?v=eLwFZJX5r7o" },
        { title: "Gusse", url: "https://www.youtube.com/watch?v=E5iQy5wJHcE" },
        { title: "Ki Hoye", url: "https://www.youtube.com/watch?v=R6p9bqYV6Rk" },
        { title: "Jaan", url: "https://www.youtube.com/watch?v=9Qk2RrT4cF8" },
        { title: "Nakhra", url: "https://www.youtube.com/watch?v=8f5bO8qCw5k" }
      ],

      /* Added artists with 10 songs each (YouTube search links) */
      "Radiohead": [
        { title: "Creep", url: "https://www.youtube.com/results?search_query=Radiohead+Creep" },
        { title: "No Surprises", url: "https://www.youtube.com/results?search_query=Radiohead+No+Surprises" },
        { title: "Karma Police", url: "https://www.youtube.com/results?search_query=Radiohead+Karma+Police" },
        { title: "High and Dry", url: "https://www.youtube.com/results?search_query=Radiohead+High+and+Dry" },
        { title: "Fake Plastic Trees", url: "https://www.youtube.com/results?search_query=Radiohead+Fake+Plastic+Trees" },
        { title: "Paranoid Android", url: "https://www.youtube.com/results?search_query=Radiohead+Paranoid+Android" },
        { title: "Everything In Its Right Place", url: "https://www.youtube.com/results?search_query=Radiohead+Everything+In+Its+Right+Place" },
        { title: "There There", url: "https://www.youtube.com/results?search_query=Radiohead+There+There" },
        { title: "Jigsaw Falling Into Place", url: "https://www.youtube.com/results?search_query=Radiohead+Jigsaw+Falling+Into+Place" },
        { title: "Weird Fishes / Arpeggi", url: "https://www.youtube.com/results?search_query=Radiohead+Weird+Fishes+Arpeggi" }
      ],
      "M83": [
        { title: "Midnight City", url: "https://www.youtube.com/results?search_query=M83+Midnight+City" },
        { title: "Wait", url: "https://www.youtube.com/results?search_query=M83+Wait" },
        { title: "Outro", url: "https://www.youtube.com/results?search_query=M83+Outro" },
        { title: "Reunion", url: "https://www.youtube.com/results?search_query=M83+Reunion" },
        { title: "Steve McQueen", url: "https://www.youtube.com/results?search_query=M83+Steve+McQueen" },
        { title: "Kim & Jessie", url: "https://www.youtube.com/results?search_query=M83+Kim+and+Jessie" },
        { title: "We Own the Sky", url: "https://www.youtube.com/results?search_query=M83+We+Own+the+Sky" },
        { title: "Oblivion (feat. Susanne Sundfør)", url: "https://www.youtube.com/results?search_query=M83+Oblivion+Susanne+Sundfor" },
        { title: "Teen Angst", url: "https://www.youtube.com/results?search_query=M83+Teen+Angst" },
        { title: "Go! (feat. Mai Lan)", url: "https://www.youtube.com/results?search_query=M83+Go+Mai+Lan" }
      ],
      "Bayaan": [
        { title: "Sapna", url: "https://www.youtube.com/results?search_query=Bayaan+Sapna" },
        { title: "Farda", url: "https://www.youtube.com/results?search_query=Bayaan+Farda" },
        { title: "Teri Tasveer", url: "https://www.youtube.com/results?search_query=Bayaan+Teri+Tasveer" },
        { title: "Nahin Milta", url: "https://www.youtube.com/results?search_query=Bayaan+Nahin+Milta" },
        { title: "Khel Tamasha", url: "https://www.youtube.com/results?search_query=Bayaan+Khel+Tamasha" },
        { title: "Ranjish Hi Sahi (Bayaan)", url: "https://www.youtube.com/results?search_query=Bayaan+Ranjish+Hi+Sahi" },
        { title: "Beparwah", url: "https://www.youtube.com/results?search_query=Bayaan+Beparwah" },
        { title: "Teri Meri", url: "https://www.youtube.com/results?search_query=Bayaan+Teri+Meri" },
        { title: "Dil", url: "https://www.youtube.com/results?search_query=Bayaan+Dil" },
        { title: "Mera Musafir", url: "https://www.youtube.com/results?search_query=Bayaan+Mera+Musafir" }
      ],
      "Hassan Raheem": [
        { title: "Pehle Bhi Main (Hassan Raheem)", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Pehle+Bhi+Main" },
        { title: "Aisay Kaisay", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Aisay+Kaisay" },
        { title: "Joona", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Joona" },
        { title: "Maybe It’s Love", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Maybe+It%27s+Love" },
        { title: "Bach Ke", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Bach+Ke" },
        { title: "Sun Le Na", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Sun+Le+Na" },
        { title: "Ulta", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Ulta" },
        { title: "Mood", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Mood+song" },
        { title: "Burey Din", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Burey+Din" },
        { title: "Mera Deewana", url: "https://www.youtube.com/results?search_query=Hassan+Raheem+Mera+Deewana" }
      ],
      "Gracie Abrams": [
        { title: "I miss you, I’m sorry", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+I+miss+you+I%E2%80%99m+sorry" },
        { title: "21", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+21" },
        { title: "Where do we go now?", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Where+do+we+go+now" },
        { title: "Feels Like", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Feels+Like" },
        { title: "Stay", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Stay" },
        { title: "The Bottom", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+The+Bottom" },
        { title: "Right Now", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Right+Now" },
        { title: "This Is What The Drugs Are For", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+This+Is+What+The+Drugs+Are+For" },
        { title: "Risk", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Risk" },
        { title: "Close To You", url: "https://www.youtube.com/results?search_query=Gracie+Abrams+Close+To+You" }
      ]
    };

    function buildList(items){
      return items.map(x =>
        `<li><a href="${x.url}" target="_blank" rel="noopener noreferrer">${x.title}</a></li>`
      ).join('');
    }

    function generatePlaylist(){
      if(!chosenArtist || !chosenMood) return;

      const base = playlists[chosenArtist] || [];
      const moodShift = { Happy: 0, Sad: 3, Excited: 6 }[chosenMood] || 0;

      const rotated = base.slice(moodShift).concat(base.slice(0, moodShift));
      const selected = rotated.slice(0,10);

      const emoji = chosenMood === 'Happy' ? '😄' : chosenMood === 'Sad' ? '😢' : '🤩';
      document.getElementById('playlistMeta').textContent =
        `${chosenArtist} • Mood: ${chosenMood} ${emoji}`;

      document.getElementById('playlistBox').innerHTML =
        `<h3>Top picks</h3><ul>${buildList(selected)}</ul>`;

      document.getElementById('playlistSection').classList.remove('hidden');
      document.getElementById('playlistSection').scrollIntoView({behavior:'smooth', block:'start'});
    }

    // Load correct section if user opens with a hash
    (function(){
      const hash = (location.hash || '#landing').replace('#','');
      if(['landing','login','about','premium'].includes(hash)){
        navigate(hash);
      }else{
        navigate('landing');
      }
    })();
  </script>
</body>
</html>
