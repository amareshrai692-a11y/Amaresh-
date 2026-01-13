<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy 15th Birthday Navya!</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;500;700&family=Parisienne&display=swap" rel="stylesheet">
    <style>
        /* --- CSS VARIABLES & RESET --- */
        :root {
            --primary: #ff4d6d;
            --secondary: #ff8fa3;
            --gold: #ffb703;
            --glass: rgba(255, 255, 255, 0.65);
            --glass-border: rgba(255, 255, 255, 0.8);
            --text-dark: #590d22;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ffc3a0 0%, #ffafbd 100%);
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
            padding-bottom: 50px;
        }

        /* --- BACKGROUND CANVAS --- */
        #canvas {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            z-index: -1;
        }

        /* --- MAIN CONTAINER --- */
        .container {
            width: 90%;
            max-width: 700px;
            margin-top: 20px;
            z-index: 10;
        }

        /* --- GLASS CARD --- */
        .card {
            background: var(--glass);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 2px solid var(--glass-border);
            border-radius: 30px;
            padding: 40px;
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.2);
            text-align: center;
            animation: floatUp 1.2s ease-out;
            position: relative;
        }

        /* --- TYPOGRAPHY --- */
        h1 {
            font-family: 'Great Vibes', cursive;
            font-size: 3.8rem;
            color: var(--primary);
            line-height: 1.1;
            text-shadow: 2px 2px 4px rgba(255, 255, 255, 0.5);
        }

        .subtitle {
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 3px;
            color: #888;
            margin: 10px 0 20px 0;
        }

        /* --- COUNTDOWN --- */
        .countdown-box {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 25px 0;
        }
        .time-unit {
            background: rgba(255, 255, 255, 0.8);
            padding: 10px;
            border-radius: 10px;
            min-width: 60px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        .time-unit span {
            display: block;
            font-weight: 700;
            font-size: 1.5rem;
            color: var(--primary);
        }
        .time-unit label {
            font-size: 0.7rem;
            text-transform: uppercase;
        }

        /* --- SURPRISE GRID --- */
        .gift-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 30px;
        }

        .gift-box {
            background: linear-gradient(45deg, #ff9a9e 0%, #fad0c4 99%, #fad0c4 100%);
            border-radius: 20px;
            padding: 20px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 5px 15px rgba(255, 77, 109, 0.3);
            border: 1px solid white;
        }

        .gift-box:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 10px 25px rgba(255, 77, 109, 0.5);
        }

        .gift-emoji { font-size: 3rem; }
        .gift-text { font-size: 0.9rem; font-weight: 600; color: white; margin-top: 5px;}

        /* --- MODAL (POPUP) --- */
        .modal {
            display: none; 
            position: fixed; 
            z-index: 1000; 
            left: 0; top: 0;
            width: 100%; height: 100%; 
            background-color: rgba(0,0,0,0.6); 
            backdrop-filter: blur(5px);
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 20px;
            width: 80%;
            max-width: 400px;
            text-align: center;
            position: relative;
            animation: popIn 0.4s ease;
            border: 4px solid var(--secondary);
        }

        .close-btn {
            position: absolute;
            top: 10px; right: 15px;
            font-size: 24px;
            font-weight: bold;
            color: #aaa;
            cursor: pointer;
        }
        .close-btn:hover { color: var(--primary); }

        /* --- MODAL SPECIFIC CONTENT STYLES --- */
        .quote-text { font-family: 'Parisienne', cursive; font-size: 1.8rem; color: var(--text-dark); }
        .bouquet-img { font-size: 5rem; animation: wobble 2s infinite; }
        .love-anim { font-size: 2.5rem; color: red; font-weight: bold; animation: heartbeat 1.5s infinite; }
        
        /* --- FOOTER --- */
        .footer {
            margin-top: 30px;
            font-size: 1rem;
            color: var(--text-dark);
            font-weight: 500;
        }
        .signature {
            font-family: 'Great Vibes', cursive;
            font-size: 2rem;
            color: var(--primary);
        }

        /* --- HIDDEN YOUTUBE PLAYER --- */
        #youtube-audio {
            display: none; 
            /* height:0; width:0; visibility:hidden; -- Keeping it in DOM but invisible */
        }

        /* --- ANIMATIONS --- */
        @keyframes floatUp { from { opacity: 0; transform: translateY(50px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes popIn { from { transform: scale(0.5); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        @keyframes heartbeat { 0% { transform: scale(1); } 15% { transform: scale(1.3); } 30% { transform: scale(1); } 45% { transform: scale(1.15); } 60% { transform: scale(1); } }
        @keyframes wobble { 0% { transform: rotate(0deg); } 25% { transform: rotate(-10deg); } 75% { transform: rotate(10deg); } 100% { transform: rotate(0deg); } }
        
        /* Flying Butterfly Class */
        .butterfly {
            position: fixed;
            font-size: 2rem;
            z-index: 2000;
            pointer-events: none;
            animation: flyAcross 6s linear forwards;
        }
        @keyframes flyAcross {
            0% { transform: translate(-100px, 100vh) rotate(0deg); opacity: 1; }
            25% { transform: translate(25vw, 70vh) rotate(15deg); }
            50% { transform: translate(50vw, 40vh) rotate(-15deg); }
            75% { transform: translate(75vw, 10vh) rotate(10deg); }
            100% { transform: translate(110vw, -100px) rotate(0deg); opacity: 0; }
        }

        /* Mobile Adjustments */
        @media(max-width: 480px) {
            h1 { font-size: 2.8rem; }
            .time-unit { min-width: 50px; }
            .time-unit span { font-size: 1.2rem; }
        }
    </style>
</head>
<body>

    <div id="youtube-player"></div>

    <canvas id="canvas"></canvas>

    <div class="container">
        <div class="card">
            <div style="font-size: 3rem;">👸</div>
            <h1>Happy 15th Birthday<br>Navya</h1>
            <p class="subtitle">14th January • My Love</p>

            <div class="countdown-box" id="countdown">
                <div class="time-unit"><span id="days">00</span><label>Days</label></div>
                <div class="time-unit"><span id="hours">00</span><label>Hrs</label></div>
                <div class="time-unit"><span id="minutes">00</span><label>Mins</label></div>
                <div class="time-unit"><span id="seconds">00</span><label>Secs</label></div>
            </div>

            <p style="margin: 20px 0;">Tap the boxes for your surprises! 🎁</p>

            <div class="gift-grid">
                <div class="gift-box" onclick="openModal('modal1')">
                    <div class="gift-emoji">💌</div>
                    <div class="gift-text">Wishes</div>
                </div>
                <div class="gift-box" onclick="triggerButterflies()">
                    <div class="gift-emoji">🦋</div>
                    <div class="gift-text">Magic</div>
                </div>
                <div class="gift-box" onclick="openModal('modal3')">
                    <div class="gift-emoji">💐</div>
                    <div class="gift-text">For You</div>
                </div>
                <div class="gift-box" onclick="openModal('modal4')">
                    <div class="gift-emoji">❤️</div>
                    <div class="gift-text">My Heart</div>
                </div>
            </div>

            <div class="footer">
                <p>Forever yours,</p>
                <div class="signature">Amaresh Rai</div>
            </div>
            
            <br>
            <button id="musicBtn" onclick="toggleMusic()" style="background:none; border:none; color: #888; text-decoration: underline; cursor:pointer;">
                🎵 Play Music
            </button>
        </div>
    </div>

    <div id="modal1" class="modal" onclick="closeModal('modal1')">
        <div class="modal-content">
            <span class="close-btn">&times;</span>
            <p class="quote-text">"In all the world, there is no heart for me like yours. In all the world, there is no love for you like mine."</p>
            <br>
            <p style="color:var(--primary)">Happy Birthday Princess! 👑</p>
        </div>
    </div>

    <div id="modal3" class="modal" onclick="closeModal('modal3')">
        <div class="modal-content">
            <span class="close-btn">&times;</span>
            <div class="bouquet-img">💐🍫</div>
            <h3>Sweets for the Sweetest!</h3>
            <p>Sending you virtual flowers and chocolates because you deserve the world.</p>
        </div>
    </div>

    <div id="modal4" class="modal" onclick="closeModal('modal4')">
        <div class="modal-content">
            <span class="close-btn">&times;</span>
            <div class="love-anim">I LOVE YOU<br>NAVYA</div>
            <p>Always & Forever.</p>
        </div>
    </div>

    <script>
        // --- 1. YOUTUBE MUSIC PLAYER ---
        var player;
        var isPlaying = false;

        function onYouTubeIframeAPIReady() {
            player = new YT.Player('youtube-player', {
                height: '0',
                width: '0',
                videoId: 'nAw2ooeubSQ', // Piano Birthday Song
                playerVars: {
                    'autoplay': 1,
                    'loop': 1,
                    'controls': 0,
                    'showinfo': 0,
                    'playlist': 'nAw2ooeubSQ' // Required for loop to work
                },
                events: {
                    'onReady': onPlayerReady
                }
            });
        }

        function onPlayerReady(event) {
            // Attempt to play automatically (might be blocked by browser)
            event.target.playVideo();
        }

        function toggleMusic() {
            if (player && typeof player.playVideo === 'function') {
                if (isPlaying) {
                    player.pauseVideo();
                    document.getElementById('musicBtn').innerText = "🎵 Play Music";
                    isPlaying = false;
                } else {
                    player.playVideo();
                    document.getElementById('musicBtn').innerText = "⏸ Pause Music";
                    isPlaying = true;
                }
            }
        }

        // Load YouTube API
        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);


        // --- 2. COUNTDOWN LOGIC ---
        function updateCountdown() {
            const now = new Date();
            const currentYear = now.getFullYear();
            let birthday = new Date(`January 14, ${currentYear} 00:00:00`);
            if (now > birthday) {
                birthday = new Date(`January 14, ${currentYear + 1} 00:00:00`);
            }
            const diff = birthday - now;
            const d = Math.floor(diff / (1000 * 60 * 60 * 24));
            const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const s = Math.floor((diff % (1000 * 60)) / 1000);
            document.getElementById('days').innerText = d < 10 ? '0'+d : d;
            document.getElementById('hours').innerText = h < 10 ? '0'+h : h;
            document.getElementById('minutes').innerText = m < 10 ? '0'+m : m;
            document.getElementById('seconds').innerText = s < 10 ? '0'+s : s;
        }
        setInterval(updateCountdown, 1000);
        updateCountdown();

        // --- 3. MODAL LOGIC ---
        function openModal(id) {
            document.getElementById(id).style.display = 'flex';
            // Try to play music if user hasn't started it yet
            if(!isPlaying) toggleMusic();
            triggerFireworks(); 
        }

        function closeModal(id) {
            document.getElementById(id).style.display = 'none';
        }

        // --- 4. BUTTERFLY ANIMATION ---
        function triggerButterflies() {
            if(!isPlaying) toggleMusic();
            const emojis = ['🦋', '✨', '🧚‍♀️'];
            for(let i=0; i<20; i++) {
                let b = document.createElement('div');
                b.className = 'butterfly';
                b.innerText = emojis[Math.floor(Math.random()*emojis.length)];
                b.style.left = Math.random() * 100 + 'vw';
                b.style.top = '100vh';
                b.style.animationDuration = (Math.random() * 3 + 3) + 's';
                document.body.appendChild(b);
                setTimeout(() => { b.remove(); }, 6000);
            }
        }

        // --- 5. FIREWORKS BACKGROUND ---
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        let particles = [];

        function triggerFireworks() {
            for(let i=0; i<5; i++) {
                createFirework(Math.random()*canvas.width, Math.random()*canvas.height/2);
            }
        }

        function createFirework(x, y) {
            const colors = ['#ff4d6d', '#ffb703', '#ffffff', '#80ffdb'];
            for (let i = 0; i < 30; i++) {
                particles.push({
                    x: x, y: y,
                    color: colors[Math.floor(Math.random() * colors.length)],
                    radius: Math.random() * 3,
                    velocity: { x: (Math.random() - 0.5) * 6, y: (Math.random() - 0.5) * 6 },
                    alpha: 1
                });
            }
        }

        function animate() {
            requestAnimationFrame(animate);
            ctx.fillStyle = 'rgba(255, 228, 230, 0.2)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            particles.forEach((p, index) => {
                if (p.alpha > 0) {
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                    ctx.fillStyle = p.color;
                    ctx.globalAlpha = p.alpha;
                    ctx.fill();
                    p.x += p.velocity.x;
                    p.y += p.velocity.y;
                    p.alpha -= 0.02;
                } else {
                    particles.splice(index, 1);
                }
            });
            ctx.globalAlpha = 1;
        }
        animate();
        window.addEventListener('resize', () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; });
    </script>
</body>
</html>
