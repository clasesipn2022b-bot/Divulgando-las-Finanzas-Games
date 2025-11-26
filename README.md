# Divulgando-las-Finanzas-Games
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera Kids</title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS TEMÁTICOS --- */
        :root {
            --primary-lucha: #e74c3c; /* Rojo */
            --secondary-lucha: #f1c40f; /* Amarillo */
            --accent-lucha: #3498db; /* Azul */
            --dark-lucha: #2c3e50;
        }

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background: radial-gradient(circle, #2c3e50 20%, #000000 100%);
            color: #333;
            min-height: 100vh;
            overflow-x: hidden;
            user-select: none; /* Evitar selección de texto al jugar */
            padding-bottom: 40px; /* Espacio para la marca de agua */
        }

        h1, h2, h3, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 1px;
        }

        /* Navbar */
        .navbar-custom {
            background-color: var(--dark-lucha);
            border-bottom: 4px solid var(--secondary-lucha);
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
            z-index: 1000;
        }

        /* Tarjetas */
        .card-lucha {
            border: 4px solid #000;
            box-shadow: 8px 8px 0px var(--primary-lucha);
            position: relative;
        }
        
        /* Botones */
        .btn-lucha {
            font-family: 'Bangers', cursive;
            font-size: 1.2rem;
            text-transform: uppercase;
            border: 2px solid black;
            box-shadow: 3px 3px 0 black;
            transition: all 0.1s;
        }
        .btn-lucha:active {
            transform: translate(2px, 2px);
            box-shadow: 1px 1px 0 black;
        }
        .btn-pinata {
            background-color: #9b59b6; 
            color: white;
        }
        .btn-pinata:hover { background-color: #8e44ad; color: white; }

        /* EL RING (Grid) */
        #maze-wrapper {
            background: #eee;
            padding: 5px;
            border: 5px solid #c0392b;
            border-radius: 5px;
            box-shadow: 0 0 15px rgba(0,0,0,0.5);
            display: inline-block;
            max-width: 100%;
            overflow: hidden;
            position: relative;
        }
        /* Esquinas del ring decorativas */
        #maze-wrapper::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            pointer-events: none;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.2);
        }

        #maze-grid {
            display: grid;
            margin: 0 auto;
        }

        .cell {
            width: 35px; height: 35px; /* Desktop base */
            display: flex; align-items: center; justify-content: center;
            background: rgba(255,255,255,0.8);
            font-size: 1.3rem;
            border: 1px solid rgba(0,0,0,0.05);
        }
        
        /* Ajuste responsive para celulares */
        @media (max-width: 450px) {
            .cell { width: 29px; height: 29px; font-size: 1.1rem; }
        }

        .wall {
            background: #222;
            background-image: radial-gradient(#444 15%, transparent 16%);
            background-size: 4px 4px;
        }

        /* Controles Táctiles */
        .control-pad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            max-width: 180px;
            margin: 15px auto;
        }
        .c-btn {
            height: 60px;
            border-radius: 50%;
            background: var(--primary-lucha);
            color: white;
            border: 3px solid black;
            font-size: 1.5rem;
            display: flex; align-items: center; justify-content: center;
            touch-action: manipulation;
        }
        .c-btn:active { background: #c0392b; transform: scale(0.95); }

        /* Modales */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9);
            z-index: 2000;
            display: none;
            align-items: center; justify-content: center;
        }
        .modal-box {
            background: var(--secondary-lucha);
            border: 5px solid black;
            padding: 20px;
            text-align: center;
            width: 90%; max-width: 400px;
            box-shadow: 0 0 20px rgba(255,255,255,0.2);
            animation: popIn 0.3s;
        }
        @keyframes popIn { from {transform: scale(0.5);} to {transform: scale(1);} }

        .float-msg {
            position: absolute; font-family: 'Bangers'; font-size: 1.5rem; 
            font-weight: bold; pointer-events: none; 
            animation: floatUp 0.8s forwards; z-index: 100;
            text-shadow: 1px 1px 0 white;
        }
        @keyframes floatUp { to { transform: translate(-50%, -60px); opacity: 0; } }

        /* NUEVO: Marca de Agua Divulgando las Finanzas */
        .brand-watermark {
            position: fixed;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 3000; /* Muy alto para estar al frente */
            pointer-events: none; /* Permite hacer click a través de él si fuera necesario */
            width: 100%;
            text-align: center;
        }
        .brand-badge {
            background-color: #000;
            color: #f1c40f;
            font-family: 'Bangers', cursive;
            padding: 5px 15px;
            border: 2px solid #fff;
            border-radius: 20px;
            font-size: 1.1rem;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
            text-transform: uppercase;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

    <div class="brand-watermark">
        <span class="brand-badge">DIVULGANDO LAS FINANZAS GAMES</span>
    </div>

    <nav class="navbar navbar-expand navbar-dark navbar-custom sticky-top">
        <div class="container-fluid px-2">
            <span class="navbar-brand lucha-font text-warning m-0" style="font-size: 1.2rem;">
                🕹️🪅 LUCHA KIDS
            </span>
            
            <div class="d-flex gap-2 align-items-center">
                <button class="btn btn-sm btn-warning btn-lucha" onclick="toggleMusic()" id="music-btn">
                    <i class="fas fa-volume-up"></i>
                </button>
                <button class="btn btn-sm btn-lucha btn-pinata" onclick="goToPinatas()" title="Ir a Piñatas">
                    <i class="fas fa-star"></i>
                </button>
                <a href="https://ambrosioortizramirez.link" class="btn btn-sm btn-danger btn-lucha">
                    <i class="fas fa-door-open"></i>
                </a>
            </div>
        </div>
    </nav>

    <div class="container py-3">
        
        <div id="screen-menu" class="row justify-content-center">
            <div class="col-12 col-md-8 col-lg-6">
                <div class="card card-lucha bg-white p-3 text-center">
                    <div class="display-1 mb-0">🕹️🪅</div>
                    <h1 class="text-danger mb-2 display-5">LUCHA FINANCIERA</h1>
                    <p class="lead fw-bold small text-muted text-uppercase">¡Vence a los Rudos y Gana el Campeonato!</p>
                    
                    <div class="alert alert-dark p-2 fw-bold lucha-font mb-3">Elige tu Arena</div>

                    <div class="d-grid gap-2">
                        <button class="btn btn-light border border-2 border-dark py-2 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(1)">
                            <span class="h2 m-0">🧸</span>
                            <div class="text-end lh-1">
                                <div class="h5 m-0 lucha-font">Arena Juguete</div>
                                <small class="text-muted" style="font-size:0.7rem">Corto Plazo</small>
                            </div>
                        </button>
                        
                        <button class="btn btn-light border border-2 border-dark py-2 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(2)">
                            <span class="h2 m-0">🚲</span>
                            <div class="text-end lh-1">
                                <div class="h5 m-0 lucha-font">Coliseo Bici</div>
                                <small class="text-muted" style="font-size:0.7rem">Mediano Plazo</small>
                            </div>
                        </button>

                        <button class="btn btn-light border border-2 border-dark py-2 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(3)">
                            <span class="h2 m-0">✈️</span>
                            <div class="text-end lh-1">
                                <div class="h5 m-0 lucha-font">Arena Mundial</div>
                                <small class="text-muted" style="font-size:0.7rem">Largo Plazo</small>
                            </div>
                        </button>
                    </div>

                    <hr>
                    <button class="btn btn-lucha btn-pinata w-100 py-2" onclick="goToPinatas()">
                        <i class="fas fa-gamepad"></i> Jugar Piñatas de la Economía
                    </button>
                </div>
            </div>
        </div>

        <div id="screen-game" class="d-none flex-column align-items-center">
            
            <div class="bg-dark text-white p-2 rounded border border-warning mb-3 d-flex justify-content-between align-items-center w-100" style="max-width: 400px;">
                <div id="ui-lives" class="h5 m-0 text-danger">❤️❤️❤️</div>
                <div class="h4 m-0 lucha-font text-warning">VS</div>
                <div id="ui-timer" class="h5 m-0"><i class="fas fa-clock"></i> 60</div>
            </div>

            <div id="maze-wrapper">
                <div id="maze-grid"></div>
            </div>

            <div class="control-pad">
                <div></div> 
                <button class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></button>
                <div></div> 
                
                <button class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></button>
                <button class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></button>
                <button class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></button>
            </div>

            <button class="btn btn-outline-light btn-sm mt-2" onclick="exitToMenu()">
                <i class="fas fa-flag"></i> Rendirse
            </button>
        </div>
    </div>

    <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h2 class="text-uppercase display-6 fw-bold">¡El Reto!</h2>
            <div class="bg-white border border-dark p-2 text-start mb-3 small">
                <p class="mb-1">📍 <strong>Sede:</strong> <span id="inst-goal" class="text-danger fw-bold">...</span></p>
                <p class="mb-1">✅ <strong>Recoge:</strong> <span class="text-success">Dinero/Ahorro</span>.</p>
                <p class="mb-1">❌ <strong>Evita:</strong> <span class="text-danger">Gastos/Rudos</span>.</p>
                <p class="mb-0">🏆 <strong>Meta:</strong> Llega al final.</p>
            </div>
            <button class="btn btn-lucha btn-success w-100 py-2" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box bg-danger text-white">
            <div class="display-1">🔔</div>
            <h2 class="lucha-font">¡TE RINDIERON!</h2>
            <p id="lose-msg" class="fw-bold small">Perdiste la máscara.</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-1 border border-dark small">
                <div class="col-6 border-end">Ganado: <br><span id="lose-good" class="h4 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="lose-bad" class="h4 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-dark w-100" onclick="exitToMenu()">REVANCHA</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box bg-warning">
            <div class="display-1">🏆</div>
            <h2 class="lucha-font text-danger">¡CAMPEÓN!</h2>
            <p id="win-msg" class="text-dark fw-bold small">¡El público enloquece!</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-1 border border-dark small">
                <div class="col-6 border-end">Ganado: <br><span id="win-good" class="h4 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="win-bad" class="h4 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-primary w-100" onclick="exitToMenu()">¡VICTORIA!</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        const levels = {
            1: { name: "ARENA JUGUETE", size: 8, badRate: 0.2 },
            2: { name: "COLISEO BICI", size: 10, badRate: 0.25 },
            3: { name: "ARENA MUNDIAL", size: 12, badRate: 0.3 }
        };
        
        // CORRECCIÓN APLICADA AQUÍ: Se arreglaron los corchetes y llaves faltantes
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
                {t:"¡INTERESES MORATORIOS!", i:"💸💸"}
                {t:"¡PAGO MINIMO!", i:"⚠️"}
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
            // Enlaces de audio más fiables (CodeSkulptor/Google CDN)
            bgm: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/theme_01.mp3'), 
            coin: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/pickup.ogg'),
            hurt: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_01.ogg'),
            win: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/bonus.wav'),
            lose: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_02.ogg')
        };
        sounds.bgm.loop = true;
        sounds.bgm.volume = 0.3;

        // Lógica de desbloqueo de audio (Critico para móviles)
        function unlockAudio() {
            if(audioContextUnlocked) return;
            
            Object.values(sounds).forEach(s => {
                s.play().then(() => {
                    s.pause();
                    if(s !== sounds.bgm) s.currentTime = 0;
                }).catch(e => console.log("Esperando interacción..."));
            });
            
            audioContextUnlocked = true;
            
            // Actualizar botón si estaba en "muted" visualmente pero quería sonar
            if(musicOn && state.active) sounds.bgm.play();

            // Quitar listeners
            document.removeEventListener('click', unlockAudio);
            document.removeEventListener('touchstart', unlockAudio);
            document.removeEventListener('keydown', unlockAudio);
        }

        // Detectores de primera interacción
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

        function goToPinatas() {
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
            unlockAudio(); // Asegurar desbloqueo
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

            // Teclado
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
            // Camino garantizado
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

            // Asegurar audio si estaba en pausa
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
                    floatText(cell.item.t, cell.item.type==='good'?'green':'red');
                    
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
                        setTimeout(()=>wrap.style.borderColor = "#c0392b", 100);
                        
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
            document.getElementById('ui-timer').className = state.time < 10 ? "h5 m-0 text-danger fw-bold" : "h5 m-0 text-white";
            
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
            if(col === 'red') el.style.fontSize = "2rem";
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 1000);
        }
    </script>
</body>
