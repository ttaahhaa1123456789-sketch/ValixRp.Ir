<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Valix Role Play | نسل بعدی گیمینگ</title>
    
    <!-- فونت‌های خفن -->
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;700;900&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Exo+2:wght@400;700;900&display=swap" rel="stylesheet">
    
    <style>
        /* ===== RESET & VARIABLES ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            /* آبی ثابت */
            --primary: #0066ff;
            --primary-dark: #0044cc;
            --primary-light: #3385ff;
            --secondary: #003399;
            --accent: #0000ff;
            
            /* رنگ‌های جدید */
            --gold: #ffd700;
            --orange: #ff6600;
            --red: #ff0000;
            --teal: #00cc99; /* رنگ سبز-آبی برای ویژگی‌ها */
            
            /* پس زمینه خاکستری تیره */
            --bg-color: #111111;
            
            /* انیمیشن‌های ساده */
            --perspective: 1000px;
            --rotation: 5deg;
        }

        /* ===== BASE STYLES ===== */
        body {
            font-family: 'Exo 2', 'Rajdhani', 'Orbitron', sans-serif;
            color: #fff;
            background: var(--bg-color);
            overflow-x: hidden;
            line-height: 1.6;
            min-height: 100vh;
            position: relative;
        }

        /* پس زمینه خاکستری تیره */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--bg-color);
            pointer-events: none;
            z-index: 0;
        }

        /* ذرات ساده - بدون سایه */
        .cyber-particle {
            position: fixed;
            width: 2px;
            height: 2px;
            background: var(--primary);
            border-radius: 50%;
            pointer-events: none;
            z-index: 1;
            animation: float 20s linear infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) translateX(0);
                opacity: 0;
            }
            10% {
                opacity: 0.5;
            }
            90% {
                opacity: 0.5;
            }
            100% {
                transform: translateY(-100vh) translateX(100px);
                opacity: 0;
            }
        }

        /* خطوط ساده - بدون سایه */
        .cyber-line {
            position: fixed;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
            height: 1px;
            width: 100%;
            z-index: 1;
            animation: scan 10s linear infinite;
            opacity: 0.3;
        }

        @keyframes scan {
            0% { transform: translateY(-50%) translateX(-100%); }
            100% { transform: translateY(-50%) translateX(100%); }
        }

        /* ===== PRELOADER ===== */
        #preloader {
            position: fixed;
            width: 100%;
            height: 100%;
            background: var(--bg-color);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s;
        }

        .cyber-loader {
            position: relative;
            width: 80px;
            height: 80px;
        }

        .loader {
            width: 80px;
            height: 80px;
            border: 5px solid #333;
            border-top-color: var(--primary);
            border-radius: 50%;
            animation: loaderRotate 1s linear infinite;
        }

        @keyframes loaderRotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* ===== NAVBAR ===== */
        .navbar {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 95%;
            max-width: 1300px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 35px;
            background: rgba(17, 17, 17, 0.9);
            backdrop-filter: blur(10px);
            z-index: 1000;
            border: 2px solid var(--primary);
            border-radius: 60px;
        }

        .logo {
            font-size: 32px;
            font-weight: 900;
            color: var(--red); /* تغییر به قرمز */
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 4px;
            position: relative;
        }

        .navbar ul {
            display: flex;
            gap: 15px;
            list-style: none;
        }

        .navbar a {
            color: #fff;
            text-decoration: none;
            font-weight: 700;
            padding: 10px 22px;
            border-radius: 40px;
            transition: all 0.3s;
            font-size: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            background: rgba(0, 102, 255, 0.2);
            border: 2px solid transparent;
        }

        .navbar a:hover {
            background: var(--red);
            border-color: var(--red);
            transform: scale(1.05);
        }

        /* لینک شاپ ویژه */
        .navbar a.shop-link {
            background: var(--primary);
            color: #fff;
            font-weight: 900;
            border: 2px solid #fff;
        }

        .navbar a.shop-link:hover {
            background: var(--red);
        }

        /* لینک انجمن */
        .navbar a.forum-link {
            background: rgba(0, 102, 255, 0.2);
        }

        .navbar a.forum-link:hover {
            background: var(--red);
        }

        /* ===== HAMBURGER MENU ===== */
        .menu-toggle {
            display: none;
            flex-direction: column;
            gap: 8px;
            cursor: pointer;
            z-index: 1001;
        }

        .menu-toggle div {
            width: 35px;
            height: 4px;
            background: var(--primary);
            border-radius: 4px;
            transition: all 0.3s;
        }

        .menu-toggle.active div:nth-child(1) {
            transform: rotate(45deg) translate(10px, 10px);
        }

        .menu-toggle.active div:nth-child(2) {
            opacity: 0;
        }

        .menu-toggle.active div:nth-child(3) {
            transform: rotate(-45deg) translate(8px, -8px);
        }

        @media (max-width: 1000px) {
            .navbar ul {
                display: none;
                flex-direction: column;
                background: rgba(17, 17, 17, 0.95);
                position: absolute;
                top: 80px;
                left: 20px;
                right: 20px;
                padding: 25px;
                border-radius: 40px;
                border: 2px solid var(--primary);
            }

            .navbar ul.show {
                display: flex;
            }

            .menu-toggle {
                display: flex;
            }
        }

        /* ===== HERO SECTION ===== */
        .hero {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
            position: relative;
            z-index: 2;
        }

        .stars-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
            direction: ltr;
        }

        .star {
            font-size: 60px;
            color: #444;
            transition: all 0.3s;
        }

        .star.active {
            color: var(--gold);
            transform: scale(1.2);
        }

        .hero h1 {
            font-size: clamp(60px, 12vw, 120px);
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            color: var(--red); /* تغییر به قرمز */
            margin-bottom: 20px;
            letter-spacing: 8px;
        }

        .hero h2 {
            font-size: clamp(24px, 5vw, 32px);
            margin-bottom: 40px;
            color: #fff;
        }

        #typing {
            color: var(--primary);
            border-left: 4px solid var(--primary);
            padding-left: 20px;
            margin-left: 20px;
        }

        .hero .btn {
            display: inline-block;
            padding: 20px 60px;
            background: var(--primary);
            color: #fff;
            text-decoration: none;
            border-radius: 60px;
            font-weight: 900;
            font-size: 22px;
            border: 2px solid #fff;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 3px;
        }

        .hero .btn:hover {
            transform: scale(1.1);
            background: var(--primary-light);
        }

        /* ===== SECTIONS ===== */
        .section {
            padding: 120px 20px;
            text-align: center;
            position: relative;
            z-index: 2;
        }

        .section h2 {
            font-size: 56px;
            font-weight: 900;
            margin-bottom: 70px;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            color: var(--primary);
        }

        /* ===== CARDS ===== */
        .cards {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 40px;
            max-width: 1400px;
            margin: 0 auto;
        }

        .card {
            padding: 40px 30px;
            border-radius: 50px;
            width: 280px;
            font-weight: 700;
            font-size: 18px;
            background: rgba(0, 102, 255, 0.1);
            border: 2px solid var(--primary);
            transition: all 0.3s;
            cursor: default;
        }

        .card:hover {
            transform: translateY(-10px);
            background: rgba(0, 102, 255, 0.2);
            border-color: var(--red);
        }

        .card.founder {
            border-color: var(--primary);
        }

        .card.owner {
            border-color: #ffaa00;
        }

        .card.scripter {
            border-color: #00ff00;
        }

        .card span {
            font-size: 24px;
            font-weight: 900;
        }

        /* تنظیم رنگ کارت‌های ویژگی‌ها به سبز-آبی */
        #features .card {
            border-color: var(--teal);
            background: rgba(0, 204, 153, 0.1);
        }

        #features .card:hover {
            background: rgba(0, 204, 153, 0.2);
            border-color: var(--teal);
        }

        /* ===== SERVER IP ===== */
        .server-ip-section {
            padding: 80px 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .ip-container {
            position: relative;
            display: inline-block;
        }

        #server-ip {
            cursor: pointer;
            padding: 50px 100px;
            background: rgba(255, 102, 0, 0.1);
            border: 4px solid var(--orange);
            border-radius: 100px;
            display: inline-block;
            transition: all 0.3s;
            text-align: center;
        }

        #server-ip:hover {
            transform: scale(1.05);
            background: rgba(255, 102, 0, 0.2);
        }

        #server-ip h2 {
            color: #fff;
            margin-bottom: 20px;
            font-size: 36px;
        }

        #ip-text {
            font-size: 56px;
            font-weight: 900;
            color: var(--orange);
            letter-spacing: 6px;
            font-family: 'Orbitron', monospace;
        }

        #copy-msg {
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--orange);
            color: #fff;
            padding: 10px 40px;
            border-radius: 50px;
            font-weight: 700;
            opacity: 0;
            transition: opacity 0.3s;
            white-space: nowrap;
            border: 2px solid #fff;
            font-size: 18px;
            pointer-events: none;
            z-index: 10;
        }

        /* ===== FOOTER ===== */
        footer {
            background: var(--bg-color);
            padding: 50px;
            text-align: center;
            font-weight: 700;
            color: #fff;
            border-top: 3px solid var(--primary);
            font-size: 20px;
            margin-top: 50px;
        }

        footer span {
            color: #00ff00; /* تغییر به سبز */
            font-weight: 900;
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 768px) {
            .section h2 {
                font-size: 40px;
            }

            #server-ip {
                padding: 30px 50px;
            }

            #ip-text {
                font-size: 32px;
            }

            .card {
                width: 100%;
                max-width: 350px;
            }
        }

        @media (max-width: 480px) {
            .navbar {
                padding: 12px 20px;
            }

            .logo {
                font-size: 24px;
            }

            #server-ip {
                padding: 20px 30px;
            }

            #ip-text {
                font-size: 24px;
                letter-spacing: 3px;
            }

            .btn {
                padding: 15px 40px;
                font-size: 18px;
            }
        }
    </style>
</head>
<body>

    <!-- ذرات ساده -->
    <script>
        for (let i = 0; i < 30; i++) {
            const particle = document.createElement('div');
            particle.className = 'cyber-particle';
            particle.style.left = Math.random() * 100 + '%';
            particle.style.animationDelay = Math.random() * 10 + 's';
            document.body.appendChild(particle);
        }

        for (let i = 0; i < 3; i++) {
            const line = document.createElement('div');
            line.className = 'cyber-line';
            line.style.top = Math.random() * 100 + '%';
            document.body.appendChild(line);
        }
    </script>

    <!-- ===== PRELOADER ===== -->
    <div id="preloader">
        <div class="cyber-loader">
            <div class="loader"></div>
        </div>
    </div>

    <!-- ===== NAVBAR ===== -->
    <nav class="navbar">
        <div class="logo">Valix Role Play</div>
        <div class="menu-toggle" id="menu-toggle">
            <div></div>
            <div></div>
            <div></div>
        </div>
        <ul id="nav-links">
            <li><a href="#home">🏠 خانه</a></li>
            <li><a href="#features">✨ ویژگی‌ها</a></li>
            <li><a href="#team">👥 تیم</a></li>
            <li><a href="#server-ip">🌐 آیپی</a></li>
            <li><a class="shop-link">⚡ فروشگاه ویژه ⚡</a></li>
            <li><a class="forum-link">📋 انجمن</a></li>
        </ul>
    </nav>

    <!-- ===== HERO SECTION با ۵ ستاره طلایی ===== -->
    <section id="home" class="hero">
        <div class="stars-container" id="starsContainer">
            <span class="star" id="star1">★</span>
            <span class="star" id="star2">★</span>
            <span class="star" id="star3">★</span>
            <span class="star" id="star4">★</span>
            <span class="star" id="star5">★</span>
        </div>
        
        <h1>والیکس رول پلی</h1>
        <h2><span id="typing"></span></h2>
        <a href="mtasa:5.57.39.165:6666" class="btn">🎮 ورود به بازی</a>
    </section>

    <!-- ===== FEATURES SECTION ===== -->
    <section id="features" class="section">
        <h2>ویژگی‌های سرور</h2>
        <div class="cards">
            <div class="card">🚓 سیستم پلیس پیشرفته</div>
            <div class="card">🏢 گتو و مافیای قدرتمند</div>
            <div class="card">💰 اقتصاد پویا</div>
            <div class="card">🏎 ماشین‌های سوپراسپرت</div>
        </div>
    </section>

    <!-- ===== TEAM SECTION ===== -->
    <section id="team" class="section">
        <h2>تیم مدیریت</h2>
        <div class="cards">
            <div class="card founder">👑 Founder: <span style="color: #ff5555;">Abolfazl</span></div>
            <div class="card owner">👑 Owner: <span style="color: #ffaa00;">Hosein</span></div>
            <div class="card scripter">⚡ Scripter: <span style="color: #00ff00;">Amirreza</span></div>
        </div>
    </section>

    <!-- ===== SERVER IP SECTION با رنگ نارنجی ===== -->
    <section class="server-ip-section">
        <div class="ip-container">
            <div id="server-ip" onclick="copyIP()">
                <h2>🌐 آیپی سرور</h2>
                <span id="ip-text">5.57.39.165:6666</span>
            </div>
            <div id="copy-msg">✅ آیپی کپی شد</div>
        </div>
    </section>

    <!-- ===== FOOTER ===== -->
    <footer>
        <p>⚡ <span>Valix ROLEPLAY</span> | تمامی حقوق محفوظ است © 2026</p>
    </footer>

    <!-- ===== SCRIPTS ===== -->
    <script>
        // ===== PRELOADER =====
        window.addEventListener('load', function() {
            setTimeout(function() {
                document.getElementById('preloader').style.opacity = '0';
                setTimeout(function() {
                    document.getElementById('preloader').style.display = 'none';
                }, 500);
            }, 1000);
        });

        // ===== HAMBURGER MENU =====
        const menuToggle = document.getElementById('menu-toggle');
        const navLinks = document.getElementById('nav-links');

        menuToggle.addEventListener('click', function() {
            this.classList.toggle('active');
            navLinks.classList.toggle('show');
        });

        document.querySelectorAll('.navbar a').forEach(link => {
            link.addEventListener('click', function() {
                menuToggle.classList.remove('active');
                navLinks.classList.remove('show');
            });
        });

        // ===== TYPING EFFECT =====
        const text = "به سرور Valix Role Play خوش آمدید، سروری جذاب و پر چالش با ایونت های هیجان انگیز";
        let i = 0;
        const typingElement = document.getElementById('typing');

        function typeWriter() {
            if (i < text.length) {
                typingElement.innerHTML += text.charAt(i);
                i++;
                setTimeout(typeWriter, 50);
            }
        }
        typeWriter();

        // ===== COPY IP =====
        function copyIP() {
            const ip = document.getElementById('ip-text').innerText;
            navigator.clipboard.writeText(ip).then(() => {
                const msg = document.getElementById('copy-msg');
                msg.style.opacity = '1';
                setTimeout(() => {
                    msg.style.opacity = '0';
                }, 2000);
            }).catch(() => {
                alert('خطا در کپی آیپی');
            });
        }

        // ===== ۵ ستاره طلایی که هر ۳ ثانیه یکی روشن می‌شه =====
        const stars = [
            document.getElementById('star1'),
            document.getElementById('star2'),
            document.getElementById('star3'),
            document.getElementById('star4'),
            document.getElementById('star5')
        ];
        
        let currentStar = 0;
        
        function lightNextStar() {
            stars.forEach(star => star.classList.remove('active'));
            stars[currentStar].classList.add('active');
            currentStar = (currentStar + 1) % stars.length;
        }
        
        setInterval(lightNextStar, 3000);
        setTimeout(lightNextStar, 100);

        // ===== اسکرول نرم =====
        document.querySelectorAll('.navbar a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth' });
                }
            });
        });

        // ===== بستن منو با کلیک بیرون =====
        document.addEventListener('click', (e) => {
            if (!menuToggle.contains(e.target) && !navLinks.contains(e.target)) {
                menuToggle.classList.remove('active');
                navLinks.classList.remove('show');
            }
        });
    </script>
</body>
</html>
