<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مفاجأة خاصة جداً! 🎁✨</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            color: #fff;
            position: relative;
            padding: 20px 0;
        }

        .stars { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        .star { position: absolute; background: #ffffff; border-radius: 50%; animation: twinkle var(--duration) infinite ease-in-out; }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(0.8); }
            50% { opacity: 1; transform: scale(1.4); box-shadow: 0 0 10px #fff; }
        }

        .container { display: flex; flex-direction: column; align-items: center; justify-content: center; z-index: 10; width: 90%; max-width: 500px; }

        /* 🎁 الهدية */
        .gift-container { perspective: 1000px; cursor: pointer; margin-bottom: 20px; }
        .gift-box {
            position: relative; width: 140px; height: 140px;
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border-radius: 15px; box-shadow: 0 15px 35px rgba(255, 65, 108, 0.5);
            transform-style: preserve-3d; transition: transform 0.5s ease;
            animation: float 3s ease-in-out infinite;
        }
        .gift-box:hover { transform: scale(1.08) rotateY(10deg); }

        .gift-lid {
            position: absolute; top: -15px; left: -10px; width: 160px; height: 40px;
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border-radius: 8px; box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transition: transform 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55); z-index: 2;
        }

        .ribbon-v { position: absolute; width: 25px; height: 100%; background: linear-gradient(to right, #ffd700, #fff8dc, #ffd700); left: 50%; transform: translateX(-50%); }
        .ribbon-h { position: absolute; width: 100%; height: 25px; background: linear-gradient(to bottom, #ffd700, #fff8dc, #ffd700); top: 50%; transform: translateY(-50%); }

        .gift-container.open .gift-lid { transform: translateY(-120px) rotate(-25deg) scale(0.8); opacity: 0; }
        .gift-container.open .gift-box { animation: none; transform: scale(0); opacity: 0; transition: all 0.5s ease 0.3s; }

        .hint-text { font-size: 1.15rem; color: #ffd700; font-weight: 600; text-shadow: 0 0 10px rgba(255, 215, 0, 0.6); animation: pulse 1.5s infinite; text-align: center; }

        /* 🎂 الكيكة والشمعة */
        .cake-container {
            display: none;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
            margin-bottom: 20px;
            animation: popup 0.8s ease forwards;
        }

        .cake {
            font-size: 80px;
            position: relative;
            user-select: none;
        }

        .flame {
            position: absolute;
            top: 5px;
            left: 50%;
            transform: translateX(-50%);
            width: 16px;
            height: 26px;
            background: radial-gradient(ellipse at bottom, #ffea00 0%, #ff4500 100%);
            border-radius: 50% 50% 20% 20%;
            box-shadow: 0 0 15px #ff4500, 0 0 25px #ffea00;
            animation: flicker 0.1s infinite alternate;
        }

        .flame.off {
            display: none;
        }

        @keyframes flicker {
            0% { transform: translateX(-50%) scale(1) rotate(-2deg); }
            100% { transform: translateX(-50%) scale(1.1) rotate(2deg); }
        }

        /* 📜 البطاقة والمعرض */
        .card {
            display: none; background: rgba(255, 255, 255, 0.08); backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px); border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 30px 20px; border-radius: 24px; box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
            text-align: center; width: 100%; animation: popup 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        .card h1 { font-size: 2rem; background: linear-gradient(45deg, #ff758c, #ff7eb3, #ffd700); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 15px; }
        .typed-text { font-size: 1.1rem; line-height: 1.8; color: #f0f0f0; margin-bottom: 25px; }

        /* 📸 ألبوم الصور التفاعلي */
        .gallery-container {
            margin-top: 15px;
            position: relative;
            width: 100%;
            max-width: 320px;
            margin-left: auto;
            margin-right: auto;
        }

        .slider {
            width: 100%;
            height: 220px;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            border: 2px solid rgba(255,255,255,0.2);
            position: relative;
        }

        .slider img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
            animation: fadeIn 0.8s ease;
        }

        .slider img.active { display: block; }

        .slider-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            font-size: 1.2rem;
            padding: 8px 12px;
            border-radius: 50%;
            cursor: pointer;
            backdrop-filter: blur(4px);
            z-index: 5;
        }

        .prev-btn { left: 8px; }
        .next-btn { right: 8px; }

        .floating-element { position: absolute; top: -10%; user-select: none; pointer-events: none; animation: fall linear infinite; }

        .music-btn {
            position: fixed; top: 15px; right: 15px; z-index: 99;
            background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.3);
            color: #fff; padding: 8px 15px; border-radius: 20px; cursor: pointer;
            backdrop-filter: blur(5px); font-size: 0.9rem; display: none;
        }

        @keyframes float { 0%, 100% { transform: translateY(0) rotate(0deg); } 50% { transform: translateY(-15px) rotate(3deg); } }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
        @keyframes popup { 0% { transform: scale(0.5); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }
        @keyframes fall { to { transform: translateY(115vh) rotate(360deg); } }
    </style>
</head>
<body>

    <button id="musicToggle" class="music-btn" onclick="toggleMusic()">🎵 تشغيل/إيقاف الموسيقى</button>

    <div class="stars" id="starsContainer"></div>

    <audio id="bgMusic" loop playsinline preload="auto">
        <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=happy-birthday-112328.mp3" type="audio/mp3">
        <source src="https://actions.google.com/sounds/v1/holidays/happy_birthday.ogg" type="audio/ogg">
    </audio>

    <div class="container">
        <!-- 🎁 الهدية -->
        <div id="giftContainer" class="gift-container" onclick="openSurprise()">
            <div class="gift-box">
                <div class="gift-lid"><div class="ribbon-v"></div></div>
                <div class="ribbon-v"></div><div class="ribbon-h"></div>
            </div>
        </div>
        <p id="hint" class="hint-text">✨ إلمس الهدية لاكتشاف المفاجأة ✨</p>

        <!-- 🎂 الكيكة والتمني -->
        <div id="cakeContainer" class="cake-container" onclick="blowCandle()">
            <div class="cake">
                <div id="flame" class="flame"></div>
                🎂
            </div>
            <p id="cakeHint" class="hint-text" style="margin-top: 15px;">🕯️ تمنّ أمنية وإلمس الشمعة لإطفائها! 🕯️</p>
        </div>

        <!-- 📜 البطاقة والمعرض -->
        <div id="card" class="card">
            <h1>🌸 عيد ميلاد سعيد! 🌸</h1>
            <p id="typedText" class="typed-text"></p>

            <!-- 📸 معرض الصور (يمكنك استبدال الروابط بصورك الخاصة) -->
            <div class="gallery-container">
                <div class="slider">
                    <button class="slider-btn prev-btn" onclick="changeSlide(-1)">❮</button>
                    <!-- يمكنك تغيير روابط الصور التالية لروابط صورك الخاصة -->
                    <img src="https://images.unsplash.com/photo-1513151233558-d860c5398176?w=500" class="active" alt="صورة 1">
                    <img src="https://images.unsplash.com/photo-1464349095431-e9a21285b5f3?w=500" alt="صورة 2">
                    <img src="https://images.unsplash.com/photo-1530103862676-de8c9debad1d?w=500" alt="صورة 3">
                    <button class="slider-btn next-btn" onclick="changeSlide(1)">❯</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        function createStars() {
            const starsContainer = document.getElementById('starsContainer');
            for (let i = 0; i < 100; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 3 + 1;
                star.style.width = size + 'px'; star.style.height = size + 'px';
                star.style.top = Math.random() * 100 + '%'; star.style.left = Math.random() * 100 + '%';
                star.style.setProperty('--duration', (Math.random() * 3 + 1.5) + 's');
                starsContainer.appendChild(star);
            }
        }
        createStars();

        const messageText = "في هذا اليوم المميز جداً، أتمنى لك سنة جديدة مليئة بالسعادة والنجاحات واللحظات الجميلة التي تشبه قلبك. 💖\n\nكل عام وأنت بألف خير وصحة وأمل! 🎆✨";

        function openSurprise() {
            const giftContainer = document.getElementById('giftContainer');
            const hint = document.getElementById('hint');
            const cakeContainer = document.getElementById('cakeContainer');
            const music = document.getElementById('bgMusic');
            const musicBtn = document.getElementById('musicToggle');

            music.play().then(() => { musicBtn.style.display = 'block'; }).catch(e => { musicBtn.style.display = 'block'; });

            giftContainer.classList.add('open');
            hint.style.display = 'none';

            setTimeout(() => {
                giftContainer.style.display = 'none';
                cakeContainer.style.display = 'flex';
                launchFireworks();
            }, 800);
        }

        // إطفاء الشمعة
        function blowCandle() {
            const flame = document.getElementById('flame');
            const cakeContainer = document.getElementById('cakeContainer');
            const card = document.getElementById('card');

            flame.classList.add('off');
            launchFireworks();
            startFloatingElements();

            setTimeout(() => {
                cakeContainer.style.display = 'none';
                card.style.display = 'block';
                typeWriter(messageText, 'typedText', 50);
            }, 1000);
        }

        // تحريك معرض الصور
        let currentSlide = 0;
        function changeSlide(direction) {
            const slides = document.querySelectorAll('.slider img');
            slides[currentSlide].classList.remove('active');
            currentSlide = (currentSlide + direction + slides.length) % slides.length;
            slides[currentSlide].classList.add('active');
        }

        function toggleMusic() {
            const music = document.getElementById('bgMusic');
            if (music.paused) { music.play(); } else { music.pause(); }
        }

        function typeWriter(text, elementId, speed) {
            let i = 0;
            const elem = document.getElementById(elementId);
            elem.innerHTML = '';
            function type() {
                if (i < text.length) {
                    if (text.charAt(i) === '\n') { elem.innerHTML += '<br>'; } else { elem.innerHTML += text.charAt(i); }
                    i++; setTimeout(type, speed);
                }
            }
            type();
        }

        function launchFireworks() {
            var duration = 2.5 * 1000; var end = Date.now() + duration;
            (function frame() {
                confetti({ particleCount: 5, angle: 60, spread: 55, origin: { x: 0 }, colors: ['#ff416c', '#ffd700', '#ffffff'] });
                confetti({ particleCount: 5, angle: 120, spread: 55, origin: { x: 1 }, colors: ['#ff416c', '#ffd700', '#ffffff'] });
                if (Date.now() < end) { requestAnimationFrame(frame); }
            })();
        }

        function startFloatingElements() {
            const elements = ['🌸', '🌹', '💖', '✨', '🌷', '🎈', '⭐'];
            setInterval(() => {
                const el = document.createElement('div');
                el.classList.add('floating-element');
                el.innerText = elements[Math.floor(Math.random() * elements.length)];
                el.style.left = Math.random() * 100 + 'vw';
                el.style.animationDuration = Math.random() * 3 + 3 + 's';
                el.style.fontSize = Math.random() * 15 + 20 + 'px';
                el.style.opacity = Math.random();
                document.body.appendChild(el);
                setTimeout(() => { el.remove(); }, 6000);
            }, 300);
        }
    </script>
</body>
</html>
