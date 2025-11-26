<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera Kids</title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS TEMÁTICOS MEJORADOS --- */
        :root {
            --primary-lucha: #ff4757; /* Rojo vibrante */
            --secondary-lucha: #ffa502; /* Dorado intenso */
            --accent-lucha: #3742fa; /* Azul eléctrico */
            --dark-lucha: #2f3542;
            --bg-gradient: radial-gradient(circle at center, #2f3542 0%, #000000 100%);
        }

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background: #2c3e50;
            /* Patrón de puntos estilo cómic sobre el fondo oscuro */
            background-image: radial-gradient(#ffffff 1px, transparent 1px), radial-gradient(#ffffff 1px, transparent 1px);
            background-size: 20px 20px;
            background-position: 0 0, 10px 10px;
            background-color: #1e272e;
            color: #333;
            min-height: 100vh;
            overflow-x: hidden;
            user-select: none;
            padding-bottom: 50px;
            touch-action: manipulation;
        }

        h1, h2, h3, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 2px;
            text-shadow: 2px 2px 0px #000; /* Sombra dura al texto */
        }

        /* Navbar más llamativa */
        .navbar-custom {
            background: linear-gradient(90deg, #000 0%, #2f3542 100%);
            border-bottom: 5px solid var(--secondary-lucha);
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            z-index: 1000;
        }

        /* Tarjetas con estilo Pop-Art */
        .card-lucha {
            background: #fff;
            border: 4px solid #000;
            border-radius: 15px;
            box-shadow: 10px 10px 0px rgba(0,0,0,0.5); /* Sombra dura */
            position: relative;
            overflow: hidden;
        }
        
        /* Botones Generales Estilo Cómic */
        .btn-lucha {
            font-family: 'Bangers', cursive;
            font-size: 1.3rem;
            text-transform: uppercase;
            border: 3px solid #000;
            border-radius: 10px;
            box-shadow: 4px 4px 0px #000; /* Efecto 3D */
            transition: all 0.1s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            margin-bottom: 5px;
        }
        .btn-lucha:active {
            transform: translate(4px, 4px); /* Efecto de presionar */
            box-shadow: 0px 0px 0px #000;
        }

        /* Botón Específico EconMaster */
        .btn-econmaster {
            background-color: #7bed9f;
            color: #000;
        }
        .btn-econmaster:hover {
            background-color: #2ed573;
            transform: scale(1.02);
        }

        /* --- EL BOTÓN MEGA LLAMATIVO (ACADÉMICO) --- */
        .btn-mega-academic {
            background: linear-gradient(45deg, #ffa502, #ffda79, #ffa502);
            background-size: 200% 200%;
            color: #000 !important;
            border: 4px solid #fff;
            font-size: 1.4rem;
            line-height: 1.2;
            padding: 15px;
            white-space: normal; /* Permite varias líneas */
            box-shadow: 0 0 15px var(--secondary-lucha), 4px 4px 0 #000;
            animation: glowing 2s ease-in-out infinite, gradientMove 3s ease infinite;
            text-shadow: none;
        }
        
        @keyframes glowing {
            0% { box-shadow: 0 0 5px #ffa502, 4px 4px 0 #000; transform: scale(1); }
            50% { box-shadow: 0 0 25px #ff6b81, 4px 4px 0 #000; transform: scale(1.03); }
            100% { box-shadow: 0 0 5px #ffa502, 4px 4px 0 #000; transform: scale(1); }
        }
        @keyframes gradientMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* EL RING (Grid) */
        #maze-wrapper {
            background: #dfe6e9;
            padding: 8px;
            border: 6px solid #ff4757;
            border-radius: 8px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.6);
            display: inline-block;
            max-width: 100%;
            position: relative;
        }
        /* Cuerdas del Ring */
        #maze-wrapper::after {
            content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            border: 2px dashed rgba(0,0,0,0.1);
            pointer-events: none;
        }

        #maze-grid {
            display: grid;
            margin: 0 auto;
            background: #fff;
        }

        .cell {
            width: 35px; height: 35px; 
            display: flex; align-items: center; justify-content: center;
            background: #fff;
            font-size: 1.4rem;
            border: 1px solid #f1f2f6;
        }
        
        @media (max-width: 450px) {
            .cell { width: 29px; height: 29px; font-size: 1.1rem; }
        }

        .wall {
            background-color: #2f3542;
            background-image: repeating-linear-gradient(45deg, #2f3542 25%, #57606f 25%, #57606f 50%, #2f3542 50%, #2f3542 75%, #57606f 75%, #57606f 100%);
            background-size: 10px 10px;
        }

        /* Controles */
        .c-btn {
            height: 65px; width: 65px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #ff6b81, #c0392b);
            color: white;
            border: 4px solid #000;
            box-shadow: 0 5px 10px rgba(0,0,0,0.5);
            font-size: 1.8rem;
            display: flex; align-items: center; justify-content: center;
            touch-action: manipulation;
        }
        .c-btn:active { background: #c0392b; transform: scale(0.9); box-shadow: inset 0 0 10px #000; }

        /* Modales */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.95);
            z-index: 2000;
            display: none;
            align-items: center; justify-content: center;
            backdrop-filter: blur(5px);
        }
        .modal-box {
            background: #fff;
            border: 6px solid #000;
            border-radius: 20px;
            padding: 25px;
            text-align: center;
            width: 90%; max-width: 400px;
            box-shadow: 0 0 50px rgba(255, 165, 2, 0.6);
            animation: bounceIn 0.5s;
        }
        @keyframes bounceIn {
            0% { transform: scale(0.3); opacity: 0; }
            50% { transform: scale(1.05); opacity: 1; }
            70% { transform: scale(0.9); }
            100% { transform: scale(1); }
        }

        .float-msg {
            position: absolute; font-family: 'Bangers'; font-size: 2rem; 
            font-weight: bold; pointer-events: none; 
            animation: floatUp 1s forwards; z-index: 100;
            text-shadow: 2px 2px 0 #000, -1px -1px 0 #fff;
        }
        @keyframes floatUp { 
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
            20% { transform: translate(-50%, -50%) scale(1.2); opacity: 1; }
            100% { transform: translate(-50%, -100px) scale(1); opacity: 0; } 
        }

        /* Marca de Agua */
        .brand-watermark {
            position: fixed;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 3000; 
            pointer-events: none;
            width: 100%;
            text-align: center;
        }
        .brand-badge {
            background-color: #000;
            color: #f1c40f;
            font-family: 'Bangers', cursive;
            padding: 8px 20px;
            border: 2px solid #fff;
            border-radius: 25px;
            font-size: 1.2rem;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.6);
            text-transform: uppercase;
            letter-spacing: 2px;
        }
    </style>
</head>
<body>

    <div class="brand-watermark">
        <span class="brand-badge">DIVULGANDO LAS FINANZAS GAMES</span>
    </div>

    <nav class="navbar navbar-expand navbar-dark navbar-custom sticky-top">
        <div class="container-fluid px-3">
            <span class="navbar-brand lucha-font text-warning m-0" style="font-size: 1.5rem;">
                🕹️ 🤼‍♂️LUCHAS FINANCIERAS
            </span>
            
            <div class="d-flex gap-2 align-items-center">
                <button class="btn btn-sm btn-warning btn-lucha" onclick="toggleMusic()" id="music-btn" style="font-size: 1rem; padding: 5px 10px;">
                    <i class="fas fa-volume-up"></i>
                </button>
            </div>
        </div>
    </nav>

    <div class="container py-4">
        
        <div id="screen-menu" class="row justify-content-center">
            <div class="col-12 col-md-10 col-lg-6">
                <a href="https://www.researchgate.net/profile/A-Ortiz-Ramirez" target="_blank" class="btn btn-lucha btn-mega-academic w-100 mb-4 text-decoration-none">
                    <i class="fas fa-graduation-cap fa-lg mb-1 d-block"></i>
                    CONOCE NUESTRO TRABAJO ACADEMICO Y REDES SOCIALES AQUÍ
                </a>

                <div class="card card-lucha p-4 text-center">
                    <div class="display-1 mb-0 animate__animated animate__tada">🤼‍♂️</div>
                    <h1 class="text-danger mb-2 display-4 fw-bold" style="-webkit-text-stroke: 1px black;">LUCHA FINANCIERA</h1>
                    <p class="lead fw-bold small text-muted text-uppercase mb-4">¡Aprende Finanzas en el Ring!</p>
                    
                    <div class="alert alert-dark p-2 fw-bold lucha-font mb-3 text-uppercase border-3 border-dark">👇 Elige tu Nivel 👇</div>

                    <div class="d-grid gap-3">
                        <button class="btn btn-light border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow bg-white" onclick="initLevel(1)">
                            <span class="h1 m-0">🧸</span>
                            <div class="text-end lh-1">
                                <div class="h4 m-0 lucha-font text-primary">Arena Juguete</div>
                                <small class="text-muted fw-bold">Nivel Principiante</small>
                            </div>
                        </button>
                        
                        <button class="btn btn-light border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow bg-white" onclick="initLevel(2)">
                            <span class="h1 m-0">🚲</span>
                            <div class="text-end lh-1">
                                <div class="h4 m-0 lucha-font text-warning" style="text-shadow: 1px 1px 0 #000;">Coliseo Bici</div>
                                <small class="text-muted fw-bold">Nivel Intermedio</small>
                            </div>
                        </button>

                        <button class="btn btn-light border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow bg-white" onclick="initLevel(3)">
                            <span class="h1 m-0">✈️</span>
                            <div class="text-end lh-1">
                                <div class="h4 m-0 lucha-font text-danger">Arena Mundial</div>
                                <small class="text-muted fw-bold">Nivel Experto</small>
                            </div>
                        </button>
                    </div>

                    <hr class="border-3 border-dark my-4">
                    
                    <button class="btn btn-lucha btn-econmaster w-100 py-3" onclick="goToEconMaster()">
                        <i class="fas fa-gamepad fa-lg"></i> JUGAR ECONMASTER
                    </button>
                </div>
            </div>
        </div>

        <div id="screen-game" class="d-none flex-column align-items-center">
            
            <div class="bg-dark text-white p-3 rounded-pill border-4 border-warning mb-4 d-flex justify-content-between align-items-center w-100 shadow" style="max-width: 400px;">
                <div id="ui-lives" class="h4 m-0 text-danger" style="letter-spacing: 2px;">❤️❤️❤️</div>
                <div class="h3 m-0 lucha-font text-warning">VS</div>
                <div id="ui-timer" class="h4 m-0"><i class="fas fa-clock"></i> 60</div>
            </div>

            <div id="maze-wrapper">
                <div id="maze-grid"></div>
            </div>

            <div class="control-pad mt-4">
                <div></div> 
                <button class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></button>
                <div></div> 
                
                <button class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></button>
                <button class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></button>
                <button class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></button>
            </div>

            <button class="btn btn-outline-light btn-sm mt-4 text-uppercase fw-bold" onclick="exitToMenu()">
                <i class="fas fa-flag"></i> Rendirse / Salir
            </button>
        </div>
    </div>

    <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h2 class="text-uppercase display-5 fw-bold text-danger mb-3" style="text-shadow: 2px 2px 0 #000;">¡El Reto!</h2>
            <div class="bg-light border border-2 border-dark p-3 text-start mb-4 rounded shadow-sm">
                <p class="mb-2 h5">📍 <strong>Arena:</strong> <span id="inst-goal" class="text-primary fw-bold">...</span></p>
                <hr>
                <p class="mb-1">✅ <strong>Busca:</strong> <span class="badge bg-success">Dinero</span> <span class="badge bg-success">Inversión</span></p>
                <p class="mb-1">❌ <strong>Evita:</strong> <span class="badge bg-danger">Gastos</span> <span class="badge bg-danger">Rudos</span></p>
            </div>
            <button class="btn btn-lucha btn-success w-100 py-3" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box bg-danger">
            <div class="display-1 mb-2">🔔</div>
            <h2 class="lucha-font text-white display-4">¡TE RINDIERON!</h2>
            <p id="lose-msg" class="fw-bold text-white mb-3">Perdiste la máscara.</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-2 border-2 border-dark rounded">
                <div class="col-6 border-end">Ganado: <br><span id="lose-good" class="h3 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="lose-bad" class="h3 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-dark text-white w-100" onclick="exitToMenu()">INTENTAR DE NUEVO</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box bg-warning">
            <div class="display-1 mb-2">🏆</div>
            <h2 class="lucha-font text-danger display-4">¡CAMPEÓN!</h2>
            <p id="win-msg" class="text-dark fw-bold mb-3">¡El público enloquece!</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-2 border-2 border-dark rounded">
                <div class="col-6 border-end">Ganado: <br><span id="win-good" class="h3 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="win-bad" class="h3 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-primary w-100" onclick="exitToMenu()">¡EXCELENTE!</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        const levels = {
            1: { name: "ARENA JUGUETE", size: 8, badRate: 0.2 },
            2: { name: "COLISEO BICI", size: 10, badRate: 0.25 },
            3: { name: "ARENA MUNDIAL", size: 12, badRate: 0.3 }
        };
        
        const items = {
            good: [
                {t:"¡DINERO!", i:"💵"}, 
                {t:"¡AHORRO!", i:"🐖"}, 
                {t:"¡LLAVE!", i:"🤼‍♂️"},
                {t:"¡INVERSIÓN!", i:"📈"}, 
                {t:"¡BONO!", i:"💰"}, 
                {t:"¡CRÉDITO!", i:"🏦"}, 
                {t:"¡PRESTAMO SIN INTERESES!", i:"🤝"}
            ],
            bad: [
                {t:"¡SILLAZO!", i:"🪑"}, 
                {t:"¡RUDO!", i:"👹"}, 
                {t:"¡GASTO HORMIGA!", i:"💸🐜"}, 
                {t:"¡INTERESES MORATORIOS!", i:"💸💸"},
                {t:"¡PAGO MINIMO!", i:"⚠️"},
                {t:"¡FONDOS INSUFICIENTES!", i:"💔"}
            ]
        };

        let state = {
            lvl: 1, lives: 3, time: 60, active: false, canMove: true,
            collectedGood: 0, collectedBad: 0
        };
        let player = {x:0, y:0};
        let grid = [];
        let timerInt;
        
        // MÚSICA Y AUDIO
        let musicOn = true; 
        let audioContextUnlocked = false;

        const sounds = {
            bgm: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/theme_01.mp3'), 
            coin: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/pickup.ogg'),
            hurt: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_01.ogg'),
            win: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/bonus.wav'),
            lose: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_02.ogg')
        };
        sounds.bgm.loop = true;
        sounds.bgm.volume = 0.3;

        function unlockAudio() {
            if(audioContextUnlocked) return;
            Object.values(sounds).forEach(s => {
                s.play().then(() => {
                    s.pause();
                    if(s !== sounds.bgm) s.currentTime = 0;
                }).catch(e => console.log("Esperando interacción..."));
            });
            audioContextUnlocked = true;
            if(musicOn && state.active) sounds.bgm.play();

            document.removeEventListener('click', unlockAudio);
            document.removeEventListener('touchstart', unlockAudio);
            document.removeEventListener('keydown', unlockAudio);
        }

        document.addEventListener('click', unlockAudio);
        document.addEventListener('touchstart', unlockAudio);
        document.addEventListener('keydown', unlockAudio);

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            musicOn = !musicOn;
            
            if(musicOn) {
                btn.innerHTML = '<i class="fas fa-volume-up"></i>';
                btn.classList.remove('btn-danger');
                btn.classList.add('btn-warning');
                if(state.active && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute"></i>';
                btn.classList.remove('btn-warning');
                btn.classList.add('btn-danger');
                sounds.bgm.pause();
            }
        }

        function playSfx(key) {
            if(musicOn && audioContextUnlocked) {
                try { 
                    const s = sounds[key].cloneNode(); 
                    s.volume = 0.6; 
                    s.play().catch(()=>{}); 
                } catch(e) {}
            }
        }

        function goToEconMaster() {
            if(confirm("¿Quieres ir a EconMaster?")) {
                window.location.href = "https://econ-master-8w1z.vercel.app/"; 
            }
        }

        function showScreen(id) {
            document.getElementById('screen-menu').classList.add('d-none');
            document.getElementById('screen-game').classList.add('d-none');
            document.getElementById('screen-game').classList.remove('d-flex');
            
            const el = document.getElementById(id);
            el.classList.remove('d-none');
            if(id === 'screen-game') el.classList.add('d-flex');
        }
        
        function showModal(id) {
            document.querySelectorAll('.modal-overlay').forEach(el => el.style.display = 'none');
            if(id) document.getElementById(id).style.display = 'flex';
        }

        function initLevel(lvl) {
            unlockAudio();
            state.lvl = lvl;
            document.getElementById('inst-goal').innerText = levels[lvl].name;
            showModal('modal-inst');
        }

        function exitToMenu() {
            state.active = false;
            clearInterval(timerInt);
            sounds.bgm.pause();
            sounds.bgm.currentTime = 0;
            showModal(null);
            showScreen('screen-menu');
        }

        function startGame() {
            showModal(null);
            showScreen('screen-game');
            
            state.lives = 3;
            state.time = 60;
            state.collectedGood = 0;
            state.collectedBad = 0;
            state.active = true;
            state.canMove = true;
            
            updateUI();
            
            const size = levels[state.lvl].size;
            generateGrid(size);
            renderGrid();
            
            clearInterval(timerInt);
            timerInt = setInterval(() => {
                state.time--;
                updateUI();
                if(state.time <= 0) gameOver("time");
            }, 1000);

            if(musicOn && audioContextUnlocked) sounds.bgm.play().catch(()=>{});

            window.onkeydown = (e) => {
                if(e.key === 'ArrowUp') move(0,-1);
                if(e.key === 'ArrowDown') move(0,1);
                if(e.key === 'ArrowLeft') move(-1,0);
                if(e.key === 'ArrowRight') move(1,0);
            };
        }

        function generateGrid(size) {
            grid = [];
            const badRate = levels[state.lvl].badRate;

            for(let y=0; y<size; y++) {
                let row = [];
                for(let x=0; x<size; x++) {
                    let isWall = Math.random() < 0.3;
                    if((x<2 && y<2) || (x>size-3 && y>size-3)) isWall = false;
                    
                    let item = null;
                    if(!isWall && Math.random() < 0.3 && !(x===0 && y===0)) {
                        const list = Math.random() < badRate ? items.bad : items.good;
                        const type = list === items.bad ? 'bad' : 'good';
                        const randItem = list[Math.floor(Math.random()*list.length)];
                        item = { ...randItem, type: type };
                    }
                    row.push({ wall: isWall, item: item });
                }
                grid.push(row);
            }
            let cx=0, cy=0;
            while(cx < size-1 || cy < size-1) {
                grid[cy][cx].wall = false;
                if(grid[cy][cx].item?.type === 'bad') grid[cy][cx].item = null;
                if(cx < size-1 && (Math.random()>0.5 || cy === size-1)) cx++; else cy++;
            }
            grid[size-1][size-1].wall = false; 
            player = {x:0, y:0};
        }

        function renderGrid() {
            const div = document.getElementById('maze-grid');
            div.innerHTML = '';
            const size = levels[state.lvl].size;
            
            div.style.gridTemplateColumns = `repeat(${size}, auto)`;

            for(let y=0; y<size; y++) {
                for(let x=0; x<size; x++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    const data = grid[y][x];
                    
                    if(data.wall) cell.classList.add('wall');
                    else if(data.item) cell.innerText = data.item.i;

                    if(x===player.x && y===player.y) {
                        cell.innerHTML = '🤼‍♂️'; 
                        cell.style.zIndex = 10;
                    }
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';
                    
                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e && e.cancelable) e.preventDefault();
            if(!state.active || !state.canMove) return;

            if(musicOn && sounds.bgm.paused && audioContextUnlocked) sounds.bgm.play();

            state.canMove = false;
            setTimeout(() => state.canMove = true, 120); 

            const size = levels[state.lvl].size;
            let nx = player.x + dx;
            let ny = player.y + dy;

            if(nx>=0 && nx<size && ny>=0 && ny<size && !grid[ny][nx].wall) {
                player = {x:nx, y:ny};
                
                const cell = grid[ny][nx];
                if(cell.item) {
                    floatText(cell.item.t, cell.item.type==='good'?'#2ed573':'#ff4757');
                    
                    if(cell.item.type === 'good') {
                        playSfx('coin');
                        state.collectedGood++;
                    } else {
                        playSfx('hurt');
                        state.collectedBad++;
                        state.lives--;
                        updateUI();
                        
                        const wrap = document.getElementById('maze-wrapper');
                        wrap.style.borderColor = "white";
                        setTimeout(()=>wrap.style.borderColor = "#ff4757", 100);
                        
                        if(state.lives <= 0) gameOver('lives');
                    }
                    cell.item = null; 
                }

                renderGrid();
                if(nx === size-1 && ny === size-1) gameWin();
            }
        }

        function updateUI() {
            document.getElementById('ui-timer').innerHTML = `<i class="fas fa-clock"></i> ${state.time}`;
            document.getElementById('ui-timer').className = state.time < 10 ? "h4 m-0 text-danger fw-bold" : "h4 m-0 text-white";
            
            let h = ""; for(let i=0;i<state.lives;i++) h+="❤️";
            document.getElementById('ui-lives').innerText = h;
        }

        function gameOver(reason) {
            state.active = false;
            playSfx('lose');
            const msg = reason === 'time' ? "¡SE ACABÓ EL TIEMPO!" : "¡TE QUEDASTE SIN VIDA!";
            document.getElementById('lose-msg').innerText = msg;
            document.getElementById('lose-good').innerText = state.collectedGood;
            document.getElementById('lose-bad').innerText = state.collectedBad;
            showModal('modal-lose');
        }

        function gameWin() {
            state.active = false;
            playSfx('win');
            document.getElementById('win-msg').innerText = "¡CONQUISTASTE LA " + levels[state.lvl].name + "!";
            document.getElementById('win-good').innerText = state.collectedGood;
            document.getElementById('win-bad').innerText = state.collectedBad;
            showModal('modal-win');
        }

        function floatText(txt, col) {
            const el = document.createElement('div');
            el.innerText = txt; 
            el.className = 'float-msg'; 
            el.style.left = '50%'; el.style.top = '50%'; 
            el.style.transform = 'translate(-50%, -50%)';
            el.style.color = col;
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 1000);
        }
    </script>
</body>
</html>
