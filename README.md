<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صانع المفاجآت والبطاقات التفاعلية 🎁✨</title>
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
            padding: 20px;
        }

        .stars { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        .star { position: absolute; background: #ffffff; border-radius: 50%; animation: twinkle var(--duration) infinite ease-in-out; }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(0.8); }
            50% { opacity: 1; transform: scale(1.4); box-shadow: 0 0 10px #fff; }
        }

        .container { display: flex; flex-direction: column; align-items: center; justify-content: center; z-index: 10; width: 100%; max-width: 500px; }

        .card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 30px 20px;
            border-radius: 24px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
            text-align: center;
            width: 100%;
            animation: popup 0.6s ease forwards;
        }

        h1 { font-size: 1.8rem; background: linear-gradient(45deg, #ff758c, #ff7eb3, #ffd700); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 20px; }
        p { margin-bottom: 15px; color: #e0e0e0; font-size: 1rem; line-height: 1.6; }

        /* أزرار الخيارات */
        .btn-group { display: flex; flex-direction: column; gap: 15px; margin-top: 15px; width: 100%; }

        .main-btn {
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            color: white; border: none; padding: 14px 20px; font-size: 1.05rem; font-weight: bold;
            border-radius: 30px; cursor: pointer; transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 5px 15px rgba(255, 65, 108, 0.4);
        }
        .main-btn:active { transform: scale(0.96); }

        .sec-btn {
            background: linear-gradient(135deg, #8a2be2, #4a00e0);
            box-shadow: 0 5px 15px rgba(138, 43, 226, 0.4);
        }

        /* المدخلات */
        input, textarea {
            width: 100%; padding: 12px 15px; border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.3);
            background: rgba(0, 0, 0, 0.4); color: #fff; font-size: 1rem; margin-bottom: 15px; outline: none;
            font-family: inherit;
        }

        /* 🎁 الهدية */
        .gift-container { perspective: 1000px; cursor: pointer; margin: 20px 0; }
        .gift-box {
            position: relative; width: 130px; height: 130px;
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border-radius: 15px; box-shadow: 0 15px 35px rgba(255, 65, 108, 0.5);
            transform-style: preserve-3d; animation: float 3s ease-in-out infinite; margin: 0 auto;
        }

        .gift-lid {
            position: absolute; top: -15px; left: -10px; width: 150px; height: 40px;
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border-radius: 8px; box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transition: transform 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55); z-index: 2;
        }

        .ribbon-v { position: absolute; width: 22px; height: 100%; background: linear-gradient(to right, #ffd700, #fff8dc, #ffd700); left: 50%; transform: translateX(-50%); }
        .ribbon-h { position: absolute; width: 100%; height: 22px; background: linear-gradient(to bottom, #ffd700, #fff8dc, #ffd700); top: 50%; transform: translateY(-50%); }

        .gift-container.open .gift-lid { transform: translateY(-120px) rotate(-25deg) scale(0.8); opacity: 0; }
        .gift-container.open .gift-box { animation: none; transform: scale(0); opacity: 0; transition: all 0.5s ease 0.3s; }

        /* 🎂 الكيكة */
        .cake { font-size: 85px; position: relative; user-select: none; cursor: pointer; margin: 15px 0; }
        .flame {
            position: absolute; top: 6px; left: 50%; transform: translateX(-50%); width: 16px; height: 26px;
            background: radial-gradient(ellipse at bottom, #ffea00 0%, #ff4500 100%);
            border-radius: 50% 50% 20% 20%; box-shadow: 0 0 15px #ff4500, 0 0 25px #ffea00;
            animation: flicker 0.1s infinite alternate;
        }
        .flame.off { display: none; }

        .hint-text { font-size: 1.1rem; color: #ffd700; font-weight: 600; text-shadow: 0 0 10px rgba(255, 215, 0, 0.6); animation: pulse 1.5s infinite; }
        .typed-text { font-size: 1.15rem; line-height: 1.8; color: #f0f0f0; margin-bottom: 20px; white-space: pre-line; }

        .floating-element { position: absolute; top: -10%; user-select: none; pointer-events: none; animation: fall linear infinite; }

        .music-btn {
            position: fixed; top: 15px; right: 15px; z-index: 99;
            background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.3);
            color: #fff; padding: 8px 15px; border-radius: 20px; cursor: pointer;
            backdrop-filter: blur(5px); font-size: 0.9rem; display: none;
        }

        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-15px); } }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
        @keyframes popup { 0% { transform: scale(0.6); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }
        @keyframes flicker { 0% { transform: translateX(-50%) scale(1); } 100% { transform: translateX(-50%) scale(1.1); } }
        @keyframes fall { to { transform: translateY(115vh) rotate(360deg); } }
    </style>
</head>
<body>

    <button id="musicToggle" class="music-btn" onclick="toggleMusic()">🎵 الموسيقى</button>
    <div class="stars" id="starsContainer"></div>

    <audio id="bgMusic" loop playsinline preload="auto">
        <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=happy-birthday-112328.mp3" type="audio/mp3">
    </audio>

    <div class="container">

        <!-- 1️⃣ شاشة الاختيارات الرئيسية (لصانع الرابط) -->
        <div id="makerView" class="card" style="display: none;">
            <h1>🎁 اصنع مفاجأتك الخاصة 🌸</h1>
            <p>اختر نوع المفاجأة التي تريد إرسالها لرابطك الخاص:</p>

            <div class="btn-group">
                <button class="main-btn" onclick="showForm('birthday')">🎂 مفاجأة عيد ميلاد</button>
                <button class="main-btn sec-btn" onclick="showForm('message')">💌 رسالة خاصة / تهنئة</button>
            </div>
        </div>

        <!-- 2️⃣ نموذج كتابة البيانات -->
        <div id="formView" class="card" style="display: none;">
            <h1 id="formTitle">تعبئة المفاجأة</h1>
            <input type="text" id="recipientName" placeholder="اسم الشخص (مثلاً: سارة)">
            <textarea id="customMessage" rows="4" placeholder="اكتب رسالتك الخاصة هنا..."></textarea>
            
            <button class="main-btn" onclick="generateLink()">✨ إنشاء الرابط الخاص</button>
        </div>

        <!-- 3️⃣ شاشة نسخ الرابط -->
        <div id="linkResultView" class="card" style="display: none;">
            <h1>تم إنشاء الرابط بنجاح! 🎉</h1>
            <p>انسخ الرابط وأرسله للشخص المطلوب ليشاهد المفاجأة:</p>
            <input type="text" id="finalLink" readonly>
            <button class="main-btn" onclick="copyGeneratedLink()">📋 نسخ الرابط</button>
        </div>

        <!-- ---------------- 4️⃣ شاشات المستلم (الشخص الذي يفتح الرابط) ---------------- -->

        <!-- أ) هدية عيد الميلاد للمستلم -->
        <div id="receiverGiftView" style="display: none; text-align: center;">
            <div id="giftContainer" class="gift-container" onclick="openReceiverSurprise()">
                <div class="gift-box">
                    <div class="gift-lid"><div class="ribbon-v"></div></div>
                    <div class="ribbon-v"></div><div class="ribbon-h"></div>
                </div>
            </div>
            <p id="giftHint" class="hint-text">✨ إلمس الهدية لاكتشاف المفاجأة ✨</p>

            <div id="cakeContainer" style="display: none; flex-direction: column; align-items: center; cursor: pointer;" onclick="blowCandle()">
                <div class="cake"><div id="flame" class="flame"></div>🎂</div>
                <p class="hint-text">🕯️ تمنّ أمنية وإلمس الشمعة لإطفائها! 🕯️</p>
            </div>
        </div>

        <!-- ب) العرض النهائي للرسالة للمستلم -->
        <div id="receiverCardView" class="card" style="display: none;">
            <h1 id="cardTitle">🌸 مفاجأة خاصة 🌸</h1>
            <p id="typedText" class="typed-text"></p>
            <button class="main-btn" onclick="location.href=window.location.pathname" style="margin-top: 10px;">✨ اصنع مفاجأة لشخص آخر</button>
        </div>

    </div>

    <script>
        // إنشاء النجوم
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

        let currentType = '';

        // قراءة الـ URL للتأكد هل المستخدم "صانع" أم "مستلم"
        const urlParams = new URLSearchParams(window.location.search);
        const mode = urlParams.get('type');
        const nameParam = urlParams.get('name') || '';
        const msgParam = urlParams.get('msg') || '';

        if (mode) {
            // الشاشة للمستلم
            if (mode === 'birthday') {
                document.getElementById('receiverGiftView').style.display = 'block';
            } else {
                document.getElementById('receiverCardView').style.display = 'block';
                document.getElementById('cardTitle').innerText = nameParam ? `🌸 إلى ${nameParam} 🌸` : "🌸 رسالة خاصة 🌸";
                typeWriter(msgParam || "أتمنى لك يوماً جميلاً ومميزاً! 💖", 'typedText', 50);
                startFloatingElements();
            }
        } else {
            // الشاشة للصانع
            document.getElementById('makerView').style.display = 'block';
        }

        function showForm(type) {
            currentType = type;
            document.getElementById('makerView').style.display = 'none';
            document.getElementById('formView').style.display = 'block';
            document.getElementById('formTitle').innerText = type === 'birthday' ? "🎂 مفاجأة عيد الميلاد" : "💌 رسالة خاصة";
            
            if(type === 'birthday' && !document.getElementById('customMessage').value) {
                document.getElementById('customMessage').value = "كل عام وأنت بألف خير وصحة وسعادة! 💖✨\nأتمنى لك سنة جديدة مليئة بالنجاحات والأيام الجميلة.";
            }
        }

        function generateLink() {
            const name = encodeURIComponent(document.getElementById('recipientName').value);
            const msg = encodeURIComponent(document.getElementById('customMessage').value);
            
            const baseUrl = window.location.origin + window.location.pathname;
            const fullUrl = `${baseUrl}?type=${currentType}&name=${name}&msg=${msg}`;

            document.getElementById('formView').style.display = 'none';
            document.getElementById('linkResultView').style.display = 'block';
            document.getElementById('finalLink').value = fullUrl;
        }

        function copyGeneratedLink() {
            const linkInput = document.getElementById('finalLink');
            linkInput.select();
            navigator.clipboard.writeText(linkInput.value);
            alert("تم نسخ الرابط بنجاح! أرسله الآن 🚀");
        }

        // تفاعلات المستلم (فتح الهدية والشمعة)
        function openReceiverSurprise() {
            document.getElementById('giftContainer').classList.add('open');
            document.getElementById('giftHint').style.display = 'none';
            
            const music = document.getElementById('bgMusic');
            music.play().then(() => { document.getElementById('musicToggle').style.display = 'block'; }).catch(() => {});

            setTimeout(() => {
                document.getElementById('giftContainer').style.display = 'none';
                const cake = document.getElementById('cakeContainer');
                cake.style.display = 'flex';
                launchFireworks();
            }, 800);
        }

        function blowCandle() {
            document.getElementById('flame').classList.add('off');
            launchFireworks();
            startFloatingElements();

            setTimeout(() => {
                document.getElementById('receiverGiftView').style.display = 'none';
                document.getElementById('receiverCardView').style.display = 'block';
                document.getElementById('cardTitle').innerText = nameParam ? `🎉 عيد ميلاد سعيد يا ${nameParam}! 🌸` : "🌸 عيد ميلاد سعيد! 🌸";
                typeWriter(msgParam, 'typedText', 50);
            }, 1000);
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
