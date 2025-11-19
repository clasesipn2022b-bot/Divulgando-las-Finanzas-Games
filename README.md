# Divulgando-las-Finanzas-Games
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera Kids</title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- PERSONALIZACIÓN TEMÁTICA SOBRE BOOTSTRAP --- */
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
            overflow-x: hidden; /* Evitar scroll horizontal en móvil */
        }

        h1, h2, h3, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 1px;
        }

        /* Navbar personalizada */
        .navbar-custom {
            background-color: var(--dark-lucha);
            border-bottom: 4px solid var(--secondary-lucha);
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
        }

        /* Tarjetas estilo Lucha */
        .card-lucha {
            border: 4px solid #000;
            box-shadow: 8px 8px 0px var(--primary-lucha);
            transition: transform 0.2s;
        }
        
        /* Botones personalizados */
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
        .btn-piñata {
            background-color: #9b59b6; /* Morado */
            color: white;
        }
        .btn-piñata:hover { background-color: #8e44ad; color: white;}

        /* EL RING (Grid del juego) */
        #maze-wrapper {
            background: #eee;
            padding: 5px;
            border: 5px solid #c0392b; /* Cuerdas */
            border-radius: 5px;
            box-shadow: 0 0 15px rgba(0,0,0,0.5);
            display: inline-block;
            max-width: 100%; /* Responsivo */
            overflow: hidden;
        }

        #maze-grid {
            display: grid;
            margin: 0 auto;
        }

        .cell {
            /* Tamaño dinámico para móviles */
            width: 35px; 
            height: 35px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255,255,255,0.8);
            font-size: 1.3rem;
            border: 1px solid rgba(0,0,0,0.1);
        }
        
        /* Ajuste para pantallas muy pequeñas (celulares) */
        @media (max-width: 400px) {
            .cell { width: 28px; height: 28px; font-size: 1rem; }
        }

        .wall {
            background: #222;
            background-image: radial-gradient(#444 15%, transparent 16%);
            background-size: 4px 4px;
        }

        /* Controles Móviles */
        .control-pad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 5px;
            max-width: 200px;
            margin: 20px auto;
        }
        .c-btn {
            height: 60px;
            border-radius: 50%;
            background: var(--primary-lucha);
            color: white;
            border: 3px solid black;
            font-size: 1.5rem;
            display: flex; align-items: center; justify-content: center;
            touch-action: manipulation; /* Mejora respuesta táctil */
        }
        .c-btn:active { background: #c0392b; transform: scale(0.95); }

        /* Modales superpuestos */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85);
            z-index: 2000;
            display: none;
            align-items: center; justify-content: center;
        }
        .modal-box {
            background: var(--secondary-lucha);
            border: 5px solid black;
            padding: 2rem;
            text-align: center;
            max-width: 90%;
            width: 400px;
            animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        @keyframes popIn { from {transform: scale(0.5);} to {transform: scale(1);} }

        /* Animación flotante de puntos */
        .float-msg {
            position: absolute; font-family: 'Bangers'; font-size: 1.5rem; 
            font-weight: bold; pointer-events: none; 
            animation: floatUp 0.8s forwards; z-index: 100;
            text-shadow: 1px 1px 0 white;
        }
        @keyframes floatUp { to { transform: translate(-50%, -50px); opacity: 0; } }

    </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg navbar-dark navbar-custom sticky-top">
        <div class="container-fluid">
            <span class="navbar-brand lucha-font text-warning" style="font-size: 1.5rem;">
                👺 LUCHA FINANCIERA
            </span>
            
            <div class="d-flex gap-2">
                <button class="btn btn-sm btn-warning btn-lucha" onclick="toggleMusic()" id="music-btn">
                    <i class="fas fa-volume-up"></i>
                </button>
                <button class="btn btn-sm btn-lucha btn-piñata" onclick="goToPinatas()">
                    <i class="fas fa-star"></i> Piñatas
                </button>
                <a href="https://ambrosioortizramirez.link" class="btn btn-sm btn-danger btn-lucha">
                    <i class="fas fa-sign-out-alt"></i> Salir
                </a>
            </div>
        </div>
    </nav>

    <div class="container py-4">
        
        <div id="screen-menu" class="row justify-content-center">
            <div class="col-12 col-md-8 col-lg-6">
                <div class="card card-lucha bg-white p-4 text-center">
                    <div class="display-1 mb-2">👺</div>
                    <h1 class="text-danger mb-3 display-4">LUCHA FINANCIERA</h1>
                    <p class="lead fw-bold">¡Vence a los Rudos y Gana el Campeonato!</p>
                    
                    <div class="alert alert-dark text-uppercase fw-bold lucha-font">Elige tu Arena</div>

                    <div class="d-grid gap-3">
                        <button class="btn btn-light border border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(1)">
                            <span class="h1 m-0">🧸</span>
                            <div class="text-end">
                                <div class="h4 m-0 lucha-font">Arena Juguete</div>
                                <small class="text-muted">Corto Plazo (Fácil)</small>
                            </div>
                        </button>
                        
                        <button class="btn btn-light border border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(2)">
                            <span class="h1 m-0">🚲</span>
                            <div class="text-end">
                                <div class="h4 m-0 lucha-font">Coliseo Bici</div>
                                <small class="text-muted">Mediano Plazo (Normal)</small>
                            </div>
                        </button>

                        <button class="btn btn-light border border-3 border-dark py-3 d-flex align-items-center justify-content-between shadow-sm" onclick="initLevel(3)">
                            <span class="h1 m-0">✈️</span>
                            <div class="text-end">
                                <div class="h4 m-0 lucha-font">Arena Mundial</div>
                                <small class="text-muted">Largo Plazo (Difícil)</small>
                            </div>
                        </button>
                    </div>

                    <hr>
                    <button class="btn btn-lucha btn-piñata w-100 py-2" onclick="goToPinatas()">
                        <i class="fas fa-gamepad"></i> Jugar Piñatas de la Economía
                    </button>
                </div>
            </div>
        </div>

        <div id="screen-game" class="d-none flex-column align-items-center">
            
            <div class="bg-dark text-white p-2 rounded border border-warning mb-3 d-flex justify-content-between align-items-center w-100" style="max-width: 500px;">
                <div id="ui-lives" class="h4 m-0 text-danger">❤️❤️❤️</div>
                <div class="h2 m-0 lucha-font text-warning">VS</div>
                <div id="ui-timer" class="h4 m-0"><i class="fas fa-clock"></i> 60</div>
            </div>

            <div id="maze-wrapper">
                <div id="maze-grid"></div>
            </div>

            <div class="control-pad">
                <div></div> <button class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></button>
                <div></div> <button class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></button>
                <button class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></button>
                <button class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></button>
            </div>

            <button class="btn btn-outline-light mt-3" onclick="exitToMenu()">
                <i class="fas fa-flag"></i> Rendirse (Volver al Menú)
            </button>
        </div>

    </div> <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h2 class="text-uppercase display-5 fw-bold">¡El Reto!</h2>
            <div class="bg-white border border-dark p-3 text-start mb-3">
                <p class="mb-1">📍 <strong>Sede:</strong> <span id="inst-goal" class="text-danger fw-bold">...</span></p>
                <p class="mb-1">🤼 <strong>Técnico:</strong> Recoge <span class="text-success">Dinero</span>.</p>
                <p class="mb-1">👹 <strong>Rudos:</strong> Evita <span class="text-danger">Gastos</span>.</p>
                <p class="mb-0">🏆 <strong>Meta:</strong> Llega al Cinturón.</p>
            </div>
            <button class="btn btn-lucha btn-success w-100 py-3" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box bg-danger text-white">
            <div class="display-1">🔔</div>
            <h2 class="lucha-font">¡TE RINDIERON!</h2>
            <p id="lose-msg" class="fw-bold">Perdiste la máscara.</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-2 border border-dark">
                <div class="col-6 border-end">Ganado: <br><span id="lose-good" class="h3 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="lose-bad" class="h3 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-dark w-100" onclick="exitToMenu()">REVANCHA</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box bg-warning">
            <div class="display-1">🏆</div>
            <h2 class="lucha-font text-danger">¡CAMPEÓN!</h2>
            <p id="win-msg" class="text-dark fw-bold">¡El público enloquece!</p>
            <div class="row bg-white text-dark mx-0 mb-3 p-2 border border-dark">
                <div class="col-6 border-end">Ganado: <br><span id="win-good" class="h3 text-success fw-bold">0</span></div>
                <div class="col-6">Perdido: <br><span id="win-bad" class="h3 text-danger fw-bold">0</span></div>
            </div>
            <button class="btn btn-lucha btn-primary w-100" onclick="exitToMenu()">¡VICTORIA!</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        /* --- CONFIGURACIÓN --- */
        const levels = {
            1: { name: "ARENA JUGUETE", size: 8, badRate: 0.2 },
            2: { name: "COLISEO BICI", size: 10, badRate: 0.25 },
            3: { name: "ARENA MUNDIAL", size: 12, badRate: 0.3 }
        };
        
        const items = {
            good: [{t:"¡DINERO!", i:"💵"}, {t:"¡AHORRO!", i:"💰"}, {t:"¡LLAVE!", i:"🗝️"}],
            bad: [{t:"¡SILLAZO!", i:"🪑"}, {t:"¡RUDO!", i:"👹"}, {t:"¡GASTO!", i:"💸"}]
        };

        /* --- ESTADO --- */
        let state = {
            lvl: 1, lives: 3, time: 60, active: false, canMove: true,
            collectedGood: 0, collectedBad: 0
        };
        let player = {x:0, y:0};
        let grid = [];
        let timerInt;
        
        // MÚSICA: Por defecto prendida
        let musicOn = true; 

        /* --- AUDIO --- */
        const sounds = {
            bgm: new Audio('https://cdn.pixabay.com/audio/2022/03/15/audio_7764920df3.mp3'), 
            coin: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_9704e4b8d2.mp3'),
            hurt: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_c642338665.mp3'),
            win: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_0625c153e1.mp3'),
            lose: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_88447e769f.mp3')
        };
        sounds.bgm.loop = true;
        sounds.bgm.volume = 0.3;

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            musicOn = !musicOn;
            
            if(musicOn) {
                btn.innerHTML = '<i class="fas fa-volume-up"></i>';
                btn.classList.remove('btn-danger');
                btn.classList.add('btn-warning');
                // Intentar reproducir si el juego está activo
                if(state.active) sounds.bgm.play().catch(e => console.log("Esperando interacción user"));
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute"></i>';
                btn.classList.remove('btn-warning');
                btn.classList.add('btn-danger');
                sounds.bgm.pause();
            }
        }

        function playSfx(key) {
            if(musicOn) {
                try { 
                    const s = sounds[key].cloneNode(); 
                    s.volume = 0.5; 
                    s.play().catch(()=>{}); 
                } catch(e) {}
            }
        }

        /* --- REDIRECCIÓN --- */
        function goToPinatas() {
            if(confirm("¿Quieres ir a 'Piñatas de la Economía'?")) {
                // Aquí pones tu URL real
                window.location.href = "https://tu-sitio-web.com/pinatas"; 
            }
        }

        /* --- NAVEGACIÓN Y PANTALLAS --- */
        function showScreen(id) {
            document.getElementById('screen-menu').classList.add('d-none');
            document.getElementById('screen-game').classList.add('d-none');
            document.getElementById('screen-game').classList.remove('d-flex'); // Quitar flex
            
            const el = document.getElementById(id);
            el.classList.remove('d-none');
            if(id === 'screen-game') el.classList.add('d-flex');
        }
        
        function showModal(id) {
            document.querySelectorAll('.modal-overlay').forEach(el => el.style.display = 'none');
            if(id) document.getElementById(id).style.display = 'flex';
        }

        function initLevel(lvl) {
            // Hack de Audio: Los navegadores bloquean audio hasta que el usuario interactúa.
            // Al hacer click en seleccionar nivel, desbloqueamos el contexto de audio.
            if(musicOn && sounds.bgm.paused) {
                sounds.bgm.play().then(() => sounds.bgm.pause()).catch(()=>{});
            }

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

        /* --- MOTOR DEL JUEGO --- */
        function startGame() {
            showModal(null);
            showScreen('screen-game');
            
            // Reinicio variables
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

            if(musicOn) sounds.bgm.play().catch(()=>{});

            // Teclado PC
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
            // Asegurar camino viable (simple walk)
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
            
            // CSS Grid dinámico
            div.style.gridTemplateColumns = `repeat(${size}, auto)`;

            for(let y=0; y<size; y++) {
                for(let x=0; x<size; x++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    const data = grid[y][x];
                    
                    if(data.wall) cell.classList.add('wall');
                    else if(data.item) cell.innerText = data.item.i;

                    // Jugador
                    if(x===player.x && y===player.y) {
                        cell.innerHTML = '🤼‍♂️'; 
                        cell.style.zIndex = 10;
                    }
                    // Meta
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';
                    
                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e) e.preventDefault(); 
            if(!state.active || !state.canMove) return;

            state.canMove = false;
            setTimeout(() => state.canMove = true, 100); // Freno leve

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
            document.getElementById('ui-timer').className = state.time < 10 ? "h4 m-0 text-danger fw-bold" : "h4 m-0 text-white";
            
            let h = ""; for(let i=0;i<state.lives;i++) h+="❤️";
            document.getElementById('ui-lives').innerText = h;
        }

        function updateSummaryUI(prefix) {
            document.getElementById(prefix + '-good').innerText = state.collectedGood;
            document.getElementById(prefix + '-bad').innerText = state.collectedBad;
        }

        function gameOver(reason) {
            state.active = false;
            playSfx('lose');
            const msg = reason === 'time' ? "¡SE ACABÓ EL TIEMPO!" : "¡TE QUEDASTE SIN VIDA!";
            document.getElementById('lose-msg').innerText = msg;
            updateSummaryUI('lose');
            showModal('modal-lose');
        }

        function gameWin() {
            state.active = false;
            playSfx('win');
            document.getElementById('win-msg').innerText = "¡CONQUISTASTE LA " + levels[state.lvl].name + "!";
            updateSummaryUI('win');
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
