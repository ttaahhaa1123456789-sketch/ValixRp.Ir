<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VALIX Role Play | نسل بعدی گیمینگ</title>
    
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
            --primary: #ff0000;
            --primary-dark: #990000;
            --primary-glow: #ff3300;
            --secondary: #0066ff;
            --secondary-glow: #0099ff;
            --accent: #aa00ff;
            --accent-glow: #cc33ff;
            --dark: #030014;
            --darker: #000000;
            --neon-red: 255, 0, 0;
            --neon-blue: 0, 102, 255;
            --neon-purple: 170, 0, 255;
            
            /* انیمیشن‌های سه‌بعدی */
            --perspective: 1000px;
            --rotation: 5deg;
        }

        /* ===== BASE STYLES ===== */
        body {
            font-family: 'Exo 2', 'Rajdhani', 'Orbitron', sans-serif;
            color: #fff;
            background: var(--darker);
            overflow-x: hidden;
            line-height: 1.6;
            min-height: 100vh;
            position: relative;
        }

        /* پس زمینه سایبرپانک */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(125deg, #000000 0%, #0a0015 40%, #15000a 80%, #000000 100%),
                repeating-linear-gradient(45deg, 
                    rgba(255, 0, 0, 0.02) 0px, 
                    rgba(255, 0, 0, 0.02) 2px,
                    rgba(0, 102, 255, 0.02) 2px, 
                    rgba(0, 102, 255, 0.02) 4px,
                    rgba(170, 0, 255, 0.02) 4px,
                    rgba(170, 0, 255, 0.02) 6px,
                    transparent 6px,
                    transparent 12px
                );
            pointer-events: none;
            z-index: 0;
            animation: matrix 20s linear infinite;
        }

        @keyframes matrix {
            0% { background-position: 0 0, 0 0; }
            100% { background-position: 100% 100%, 100% 100%; }
        }

        /* ذرات سه‌بعدی */
        .cyber-particle {
            position: fixed;
            width: 4px;
            height: 4px;
            background: linear-gradient(45deg, var(--primary), var(--secondary), var(--accent));
            border-radius: 50%;
            filter: blur(1px);
            pointer-events: none;
            z-index: 1;
            animation: float3D 15s linear infinite;
            transform-style: preserve-3d;
        }

        @keyframes float3D {
            0% {
                transform: translateZ(-500px) translateY(100vh) translateX(0) rotateX(0deg) rotateY(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.8;
            }
            90% {
                opacity: 0.8;
            }
            100% {
                transform: translateZ(500px) translateY(-100vh) translateX(100px) rotateX(360deg) rotateY(360deg);
                opacity: 0;
            }
        }

        /* خطوط سایبرپانک */
        .cyber-line {
            position: fixed;
            background: linear-gradient(90deg, transparent, var(--primary), var(--secondary), var(--accent), transparent);
            height: 2px;
            width: 100%;
            z-index: 1;
            animation: scan 8s linear infinite;
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
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s;
        }

        .cyber-loader {
            position: relative;
            width: 120px;
            height: 120px;
            perspective: 1000px;
        }

        .cube {
            width: 100%;
            height: 100%;
            position: absolute;
            transform-style: preserve-3d;
            animation: cubeRotate 5s infinite linear;
        }

        .cube div {
            position: absolute;
            width: 100%;
            height: 100%;
            border: 3px solid;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 900;
            font-size: 24px;
            text-shadow: 0 0 20px currentColor;
        }

        .cube .front { transform: translateZ(60px); border-color: var(--primary); color: var(--primary); }
        .cube .back { transform: rotateY(180deg) translateZ(60px); border-color: var(--secondary); color: var(--secondary); }
        .cube .right { transform: rotateY(90deg) translateZ(60px); border-color: var(--accent); color: var(--accent); }
        .cube .left { transform: rotateY(-90deg) translateZ(60px); border-color: var(--primary-glow); color: var(--primary-glow); }
        .cube .top { transform: rotateX(90deg) translateZ(60px); border-color: var(--secondary-glow); color: var(--secondary-glow); }
        .cube .bottom { transform: rotateX(-90deg) translateZ(60px); border-color: var(--accent-glow); color: var(--accent-glow); }

        @keyframes cubeRotate {
            from { transform: rotateX(0deg) rotateY(0deg); }
            to { transform: rotateX(360deg) rotateY(360deg); }
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
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(20px);
            z-index: 1000;
            border: 2px solid transparent;
            border-radius: 60px;
            background-clip: padding-box;
            animation: borderGlow 3s infinite;
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.3);
        }

        @keyframes borderGlow {
            0%, 100% { border-color: var(--primary); box-shadow: 0 0 30px rgba(255, 0, 0, 0.3); }
            33% { border-color: var(--secondary); box-shadow: 0 0 30px rgba(0, 102, 255, 0.3); }
            66% { border-color: var(--accent); box-shadow: 0 0 30px rgba(170, 0, 255, 0.3); }
        }

        .logo {
            font-size: 32px;
            font-weight: 900;
            background: linear-gradient(45deg, var(--primary), var(--secondary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 4px;
            position: relative;
            animation: logoPulse 2s infinite;
        }

        @keyframes logoPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .logo::before {
            content: '⚡';
            position: absolute;
            left: -30px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--primary);
            text-shadow: 0 0 20px var(--primary);
            animation: spin 3s linear infinite;
        }

        .logo::after {
            content: '⚡';
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--accent);
            text-shadow: 0 0 20px var(--accent);
            animation: spin 3s linear infinite reverse;
        }

        @keyframes spin {
            from { transform: translateY(-50%) rotate(0deg); }
            to { transform: translateY(-50%) rotate(360deg); }
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
            position: relative;
            overflow: hidden;
            font-size: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            border: 1px solid transparent;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
            cursor: pointer;
        }

        .navbar a::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
        }

        .navbar a:hover::before {
            left: 100%;
        }

        .navbar a:hover {
            background: linear-gradient(45deg, var(--primary), var(--accent));
            transform: scale(1.05) translateY(-2px);
            box-shadow: 0 0 20px var(--primary), 0 0 40px var(--accent);
            border-color: #fff;
        }

        /* لینک شاپ ویژه - بدون لینک */
        .navbar a.shop-link {
            background: linear-gradient(45deg, #ff0000, #ff0066, #ff00cc);
            color: #fff;
            font-weight: 900;
            border: 2px solid #fff;
            animation: shopPulse 1.5s infinite;
            position: relative;
            pointer-events: none;
            opacity: 0.9;
        }

        @keyframes shopPulse {
            0%, 100% { 
                box-shadow: 0 0 20px #ff0000, 0 0 40px #ff0066, 0 0 60px #ff00cc;
                transform: scale(1);
            }
            50% { 
                box-shadow: 0 0 30px #ff00cc, 0 0 60px #ff0000, 0 0 90px #ff0066;
                transform: scale(1.05);
            }
        }

        /* لینک انجمن - بدون لینک */
        .navbar a.forum-link {
            pointer-events: none;
            opacity: 0.9;
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
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 4px;
            transition: all 0.3s;
            box-shadow: 0 0 10px var(--primary);
        }

        .menu-toggle.active div:nth-child(1) {
            transform: rotate(45deg) translate(10px, 10px);
            background: var(--secondary);
        }

        .menu-toggle.active div:nth-child(2) {
            opacity: 0;
            transform: translateX(-20px);
        }

        .menu-toggle.active div:nth-child(3) {
            transform: rotate(-45deg) translate(8px, -8px);
            background: var(--accent);
        }

        @media (max-width: 1000px) {
            .navbar ul {
                display: none;
                flex-direction: column;
                background: rgba(0, 0, 0, 0.95);
                backdrop-filter: blur(20px);
                position: absolute;
                top: 80px;
                left: 20px;
                right: 20px;
                padding: 25px;
                border-radius: 40px;
                border: 2px solid var(--primary);
                box-shadow: 0 0 40px rgba(255, 0, 0, 0.5);
            }

            .navbar ul.show {
                display: flex;
                animation: slideDown 0.3s ease;
            }

            @keyframes slideDown {
                from {
                    opacity: 0;
                    transform: translateY(-30px) scale(0.9);
                }
                to {
                    opacity: 1;
                    transform: translateY(0) scale(1);
                }
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
            perspective: 1000px;
        }

        .hero h1 {
            font-size: clamp(60px, 12vw, 120px);
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            background: linear-gradient(45deg, 
                var(--primary), 
                var(--secondary), 
                var(--accent), 
                var(--primary-glow), 
                var(--secondary-glow)
            );
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 
                0 0 30px rgba(255, 0, 0, 0.7),
                0 0 60px rgba(0, 102, 255, 0.5),
                0 0 90px rgba(170, 0, 255, 0.3);
            margin-bottom: 20px;
            letter-spacing: 8px;
            animation: titleRotate 5s infinite;
            transform-style: preserve-3d;
        }

        @keyframes titleRotate {
            0%, 100% { transform: rotateX(0deg) rotateY(0deg); }
            25% { transform: rotateX(5deg) rotateY(-5deg); }
            75% { transform: rotateX(-5deg) rotateY(5deg); }
        }

        .hero h2 {
            font-size: clamp(24px, 5vw, 32px);
            margin-bottom: 40px;
            color: transparent;
            background: linear-gradient(135deg, #fff, #ccc);
            -webkit-background-clip: text;
            position: relative;
        }

        #typing {
            color: #fff;
            text-shadow: 0 0 10px var(--primary), 0 0 20px var(--secondary);
            border-left: 4px solid var(--primary);
            padding-left: 20px;
            margin-left: 20px;
        }

        .glitch {
            position: relative;
        }

        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #ff0000;
            animation: glitch-1 2s infinite linear alternate-reverse;
        }

        .glitch::after {
            left: -2px;
            text-shadow: 2px 0 #0000ff;
            animation: glitch-2 2s infinite linear alternate-reverse;
        }

        @keyframes glitch-1 {
            0% { clip-path: inset(20% 0 30% 0); }
            20% { clip-path: inset(60% 0 10% 0); }
            40% { clip-path: inset(10% 0 80% 0); }
            60% { clip-path: inset(40% 0 50% 0); }
            80% { clip-path: inset(90% 0 5% 0); }
            100% { clip-path: inset(15% 0 70% 0); }
        }

        @keyframes glitch-2 {
            0% { clip-path: inset(30% 0 20% 0); }
            20% { clip-path: inset(80% 0 10% 0); }
            40% { clip-path: inset(5% 0 60% 0); }
            60% { clip-path: inset(20% 0 40% 0); }
            80% { clip-path: inset(50% 0 30% 0); }
            100% { clip-path: inset(70% 0 15% 0); }
        }

        .hero .btn {
            display: inline-block;
            padding: 20px 60px;
            background: linear-gradient(45deg, #ff0000, #ff6600, #ff00ff);
            color: #fff;
            text-decoration: none;
            border-radius: 60px;
            font-weight: 900;
            font-size: 22px;
            border: 3px solid #fff;
            box-shadow: 0 0 30px #ff0000, 0 0 60px #ff00ff;
            transition: all 0.3s;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 3px;
            transform-style: preserve-3d;
            animation: btnFloat 3s infinite;
        }

        @keyframes btnFloat {
            0%, 100% { transform: translateZ(0) scale(1); }
            50% { transform: translateZ(20px) scale(1.05); }
        }

        .hero .btn:hover {
            transform: translateZ(40px) scale(1.1);
            box-shadow: 0 0 40px #ff0000, 0 0 80px #ff00ff, 0 0 120px #0000ff;
        }

        /* ===== SECTIONS ===== */
        .section {
            padding: 120px 20px;
            text-align: center;
            position: relative;
            z-index: 2;
            perspective: 1000px;
        }

        .section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: repeating-linear-gradient(45deg, 
                rgba(255, 0, 0, 0.02) 0px,
                rgba(255, 0, 0, 0.02) 20px,
                rgba(0, 102, 255, 0.02) 20px,
                rgba(0, 102, 255, 0.02) 40px,
                rgba(170, 0, 255, 0.02) 40px,
                rgba(170, 0, 255, 0.02) 60px
            );
            pointer-events: none;
        }

        .section h2 {
            font-size: 56px;
            font-weight: 900;
            margin-bottom: 70px;
            position: relative;
            display: inline-block;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            background: linear-gradient(135deg, #fff, #ff0000, #0066ff, #aa00ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
            animation: sectionTitle 4s infinite;
            transform-style: preserve-3d;
        }

        @keyframes sectionTitle {
            0%, 100% { transform: rotateY(0deg) scale(1); }
            50% { transform: rotateY(10deg) scale(1.1); }
        }

        .section h2::before,
        .section h2::after {
            content: '⚡';
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            font-size: 40px;
            animation: spark 1.5s infinite;
        }

        .section h2::before {
            left: -70px;
            color: var(--primary);
            text-shadow: 0 0 20px var(--primary);
        }

        .section h2::after {
            right: -70px;
            color: var(--accent);
            text-shadow: 0 0 20px var(--accent);
        }

        @keyframes spark {
            0%, 100% { opacity: 1; transform: translateY(-50%) scale(1); }
            50% { opacity: 0.5; transform: translateY(-50%) scale(1.5); }
        }

        /* ===== CARDS ===== */
        .cards {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 40px;
            max-width: 1400px;
            margin: 0 auto;
            perspective: 1000px;
        }

        .card {
            padding: 40px 30px;
            border-radius: 50px;
            width: 280px;
            font-weight: 700;
            font-size: 18px;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(10px);
            border: 2px solid transparent;
            transition: all 0.4s;
            cursor: default;
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
            animation: cardFloat 6s infinite;
        }

        .card:nth-child(1) { animation-delay: 0s; }
        .card:nth-child(2) { animation-delay: 1s; }
        .card:nth-child(3) { animation-delay: 2s; }
        .card:nth-child(4) { animation-delay: 3s; }

        @keyframes cardFloat {
            0%, 100% { transform: translateY(0) rotateX(0deg); }
            50% { transform: translateY(-20px) rotateX(5deg); }
        }

        .card::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, 
                var(--primary), 
                var(--secondary), 
                var(--accent), 
                var(--primary-glow), 
                var(--secondary-glow)
            );
            border-radius: 50px;
            z-index: -1;
            opacity: 0;
            transition: opacity 0.4s;
            animation: borderRotate 3s linear infinite;
        }

        @keyframes borderRotate {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        .card:hover::before {
            opacity: 1;
        }

        .card:hover {
            transform: translateY(-30px) scale(1.05) rotateX(10deg);
            box-shadow: 0 0 50px rgba(255, 0, 0, 0.5);
        }

        .card.founder {
            background: linear-gradient(135deg, rgba(0, 0, 0, 0.9), rgba(255, 0, 0, 0.2));
        }

        .card.owner {
            background: linear-gradient(135deg, rgba(0, 0, 0, 0.9), rgba(255, 215, 0, 0.2));
        }

        .card.scripter {
            background: linear-gradient(135deg, rgba(0, 0, 0, 0.9), rgba(0, 255, 0, 0.2));
        }

        /* ===== SERVER IP ===== */
        .server-ip-section {
            padding: 100px 20px;
            perspective: 1000px;
        }

        #server-ip {
            cursor: pointer;
            padding: 50px 100px;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(15px);
            border: 4px solid transparent;
            border-radius: 100px;
            display: inline-block;
            box-shadow: 0 0 50px rgba(255, 0, 0, 0.5);
            position: relative;
            transition: all 0.4s;
            transform-style: preserve-3d;
            animation: ipFloat 5s infinite;
        }

        @keyframes ipFloat {
            0%, 100% { transform: translateZ(0) rotateY(0deg); }
            50% { transform: translateZ(30px) rotateY(5deg); }
        }

        #server-ip:hover {
            transform: translateZ(50px) scale(1.05);
            border-color: var(--primary);
            box-shadow: 0 0 70px var(--primary), 0 0 140px var(--accent);
        }

        #server-ip h2 {
            color: #fff;
            margin-bottom: 25px;
            font-size: 36px;
            text-shadow: 0 0 20px var(--primary), 0 0 40px var(--secondary);
            letter-spacing: 3px;
        }

        #ip-text {
            font-size: 56px;
            font-weight: 900;
            background: linear-gradient(45deg, #ff0000, #0066ff, #aa00ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
            letter-spacing: 6px;
            font-family: 'Orbitron', monospace;
        }

        #copy-msg {
            position: absolute;
            bottom: -50px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(45deg, var(--primary), var(--accent));
            color: #fff;
            padding: 10px 40px;
            border-radius: 50px;
            font-weight: 700;
            opacity: 0;
            transition: opacity 0.3s;
            white-space: nowrap;
            border: 2px solid #fff;
            font-size: 18px;
        }

        /* ===== FOOTER ===== */
        footer {
            background: linear-gradient(135deg, #000, #0a000a, #000a0a);
            padding: 50px;
            text-align: center;
            font-weight: 700;
            color: #fff;
            border-top: 3px solid transparent;
            position: relative;
            z-index: 2;
            animation: footerGlow 4s infinite;
            font-size: 20px;
        }

        @keyframes footerGlow {
            0%, 100% { border-color: var(--primary); box-shadow: 0 -5px 30px rgba(255, 0, 0, 0.5); }
            33% { border-color: var(--secondary); box-shadow: 0 -5px 30px rgba(0, 102, 255, 0.5); }
            66% { border-color: var(--accent); box-shadow: 0 -5px 30px rgba(170, 0, 255, 0.5); }
        }

        footer p {
            font-size: 20px;
            text-shadow: 0 0 15px currentColor;
        }

        footer span {
            background: linear-gradient(45deg, var(--primary), var(--secondary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: 900;
            font-size: 22px;
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 768px) {
            .section h2 {
                font-size: 40px;
            }

            .section h2::before,
            .section h2::after {
                display: none;
            }

            #server-ip {
                padding: 30px 50px;
            }

            #ip-text {
                font-size: 32px;
                letter-spacing: 3px;
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

            .logo::before,
            .logo::after {
                display: none;
            }

            #ip-text {
                font-size: 24px;
            }

            .btn {
                padding: 15px 40px;
                font-size: 18px;
            }
        }
    </style>
</head>
<body>

    <!-- ذرات سایبرپانک -->
    <script>
        (function() {
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'cyber-particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 10 + 's';
                particle.style.width = Math.random() * 6 + 2 + 'px';
                particle.style.height = particle.style.width;
                document.body.appendChild(particle);
            }

            for (let i = 0; i < 5; i++) {
                const line = document.createElement('div');
                line.className = 'cyber-line';
                line.style.top = Math.random() * 100 + '%';
                line.style.animationDelay = Math.random() * 5 + 's';
                document.body.appendChild(line);
            }
        })();
    </script>

    <!-- ===== PRELOADER ===== -->
    <div id="preloader">
        <div class="cyber-loader">
            <div class="cube">
                <div class="front">V</div>
                <div class="back">A</div>
                <div class="right">L</div>
                <div class="left">I</div>
                <div class="top">X</div>
                <div class="bottom">⚡</div>
            </div>
        </div>
    </div>

    <!-- ===== NAVBAR ===== -->
    <nav class="navbar">
        <div class="logo">VALIX Role Play</div>
        <div class="menu-toggle" id="menu-toggle">
            <div></div>
            <div></div>
            <div></div>
        </div>
        <ul id="nav-links">
            <li><a href="#home" class="glitch" data-text="خانه">🏠 خانه</a></li>
            <li><a href="#features" class="glitch" data-text="ویژگی‌ها">✨ ویژگی‌ها</a></li>
            <li><a href="#team" class="glitch" data-text="تیم">👥 تیم</a></li>
            <li><a href="#server-ip" class="glitch" data-text="آیپی">🌐 آیپی</a></li>
            <li><a class="shop-link">⚡ فروشگاه ویژه ⚡</a></li>
            <li><a class="glitch forum-link" data-text="انجمن">📋 انجمن</a></li>
        </ul>
    </nav>

    <!-- ===== HERO SECTION ===== -->
    <section id="home" class="hero">
        <h1 class="glitch" data-text="VALIX RP">VALIX Role Play</h1>
        <h2><span id="typing"></span></h2>
        <a href="mtasa://5.57.35.52:7777" class="btn">🎮 ورود به بازی</a>
    </section>

    <!-- ===== FEATURES SECTION ===== -->
    <section id="features" class="section">
        <h2 class="glitch" data-text="ویژگی‌های سرور">ویژگی‌های سرور</h2>
        <div class="cards">
            <div class="card">🚓 سیستم پلیس پیشرفته</div>
            <div class="card">🏢 گتو و مافیای قدرتمند</div>
            <div class="card">💰 اقتصاد پویا</div>
            <div class="card">🏎 ماشین‌های سوپراسپرت</div>
        </div>
    </section>

    <!-- ===== TEAM SECTION ===== -->
    <section id="team" class="section">
        <h2 class="glitch" data-text="تیم مدیریت">تیم مدیریت</h2>
        <div class="cards">
            <div class="card founder">👑 Founder: <span style="color: #ff5555; text-shadow: 0 0 20px #ff0000;">Abolfazl</span></div>
            <div class="card owner">👑 Owner: <span style="color: #ffaa00; text-shadow: 0 0 20px #ffaa00;">Hosein</span></div>
            <div class="card scripter">⚡ Scripter: <span style="color: #00ff00; text-shadow: 0 0 20px #00ff00;">Amirreza</span></div>
        </div>
    </section>

    <!-- ===== SERVER IP SECTION ===== -->
    <section class="server-ip-section">
        <div id="server-ip" onclick="copyIP()">
            <h2>🌐 آیپی سرور</h2>
            <span id="ip-text">5.57.35.52:7777</span>
            <div id="copy-msg">✅ کپی شد</div>
        </div>
    </section>

    <!-- ===== FOOTER ===== -->
    <footer>
        <p>⚡ <span>VALIX ROLEPLAY</span> | تمامی حقوق محفوظ است © 2026</p>
        <p style="font-size: 18px; margin-top: 20px;">طراحی شده با ❤️ برای گیمرهای حرفه‌ای</p>
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

        if (menuToggle && navLinks) {
            menuToggle.addEventListener('click', function(e) {
                e.stopPropagation();
                this.classList.toggle('active');
                navLinks.classList.toggle('show');
            });

            // بستن منو با کلیک روی لینک‌ها
            document.querySelectorAll('.navbar a').forEach(link => {
                link.addEventListener('click', function() {
                    menuToggle.classList.remove('active');
                    navLinks.classList.remove('show');
                });
            });

            // بستن منو با کلیک بیرون
            document.addEventListener('click', function(e) {
                if (!menuToggle.contains(e.target) && !navLinks.contains(e.target)) {
                    menuToggle.classList.remove('active');
                    navLinks.classList.remove('show');
                }
            });
        }

        // ===== TYPING EFFECT =====
        const text = "به سرور Valix Role Play خوش آمدید، سروری جذاب و پر چالش با ایونت های هیجان انگیز";
        let i = 0;
        const typingElement = document.getElementById('typing');

        if (typingElement) {
            function typeWriter() {
                if (i < text.length) {
                    typingElement.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(typeWriter, 50);
                }
            }
            typeWriter();
        }

        // ===== COPY IP =====
        function copyIP() {
            const ipElement = document.getElementById('ip-text');
            if (!ipElement) return;
            
            const ip = ipElement.innerText;
            navigator.clipboard.writeText(ip).then(() => {
                const msg = document.getElementById('copy-msg');
                if (msg) {
                    msg.style.opacity = '1';
                    setTimeout(() => {
                        msg.style.opacity = '0';
                    }, 2000);
                }
            }).catch(err => {
                console.error('خطا در کپی کردن:', err);
                alert('خطا در کپی آیپی! لطفاً دستی کپی کنید.');
            });
        }

        // ===== SMOOTH SCROLL =====
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>
