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
        /* --- ESTILOS GENERALES --- */
        :root {
            --primary-lucha: #ff4757; 
            --secondary-lucha: #ffa502; 
            --dark-lucha: #2f3542;
        }

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background: #1e272e;
            background-image: radial-gradient(#ffffff 1px, transparent 1px);
            background-size: 20px 20px;
            color: #333;
            height: 100vh;
            overflow: hidden; 
            user-select: none;
            touch-action: none;
        }

        h1, h2, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 1.5px;
            text-shadow: 2px 2px 0px #000;
        }

        /* --- PANTALLA DE MENÚ (REDIMENSIONADA) --- */
        #screen-menu {
            height: 100vh;
            overflow-y: auto; /* Permite scroll si la pantalla es muy bajita */
            padding: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(30, 39, 46, 0.95);
        }

        .card-lucha {
            background: #fff;
            border: 5px solid #000;
            border-radius: 20px;
            box-shadow: 10px 10px 0px rgba(0,0,0,0.5);
            /* CAMBIO: AHORA ES MÁS ANCHA */
            max-width: 800px; 
            width: 100%;
            position: relative;
        }

        /* Botones del Menú - MÁS GRANDES */
        .btn-lucha {
            font-family: 'Bangers', cursive;
            font-size: 1.5rem; /* Texto más grande */
            text-transform: uppercase;
            border: 4px solid #000;
            border-radius: 12px;
            box-shadow: 5px 5px 0px #000;
            transition: transform 0.1s;
        }
        .btn-lucha:active { transform: translate(3px, 3px); box-shadow: 2px 2px 0px #000; }

        .btn-mega-academic {
            background: linear-gradient(45deg, #ffa502, #ffda79);
            color: #000 !important;
            border: 4px solid #fff;
            font-size: 1.3rem; /* Más grande */
            padding: 15px;
            white-space: normal;
            box-shadow: 0 0 20px var(--secondary-lucha), 5px 5px 0 #000;
            animation: glowing 2s infinite;
        }
        @keyframes glowing { 50% { box-shadow: 0 0 30px #ff6b81, 5px 5px 0 #000; } }

        /* Estilo para los botones de nivel */
        .level-btn {
            font-size: 1.2rem;
            padding: 15px 20px; /* Más gorditos */
        }
        .level-icon { font-size: 2.5rem; } /* Iconos gigantes */

        /* --- PANTALLA DE JUEGO --- */
        #screen-game {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #2f3542;
            display: none; 
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 10px;
            gap: 10px;
        }

        .game-header {
            width: 100%;
            max-width: 700px; /* Cabecera un poco más ancha */
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #000;
            color: #f1c40f;
            padding: 5px 20px;
            border-radius: 20px;
            border: 2px solid #fff;
            height: 50px;
            flex-shrink: 0;
            font-size: 1.2rem;
        }

        .game-body {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            overflow: hidden;
            gap: 15px;
        }

        #maze-wrapper {
            background: #dfe6e9;
            padding: 8px;
            border: 5px solid #ff4757;
            border-radius: 10px;
            box-shadow: 0 0 25px rgba(0,0,0,0.6);
            aspect-ratio: 1 / 1;
            height: auto;
            width: 100%;
            max-height: 60vh; /* Un poco más alto */
            max-width: 95vw;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #maze-grid {
            display: grid;
            width: 100%;
            height: 100%;
        }

        .cell {
            display: flex; align-items: center; justify-content: center;
            background: #fff;
            border: 1px solid #eee;
            font-size: clamp(12px, 5vw, 35px); /* Fuente adaptable */
        }
        .wall { background: #2f3542; background-image: repeating-linear-gradient(45deg, #333 0, #333 1px, #222 1px, #222 4px); }

        .controls-area {
            display: flex;
            flex-direction: row;
            gap: 20px;
            align-items: center;
        }

        .control-pad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px; /* Botones más separados */
        }
        
        .c-btn {
            width: 65px; height: 65px; /* Botones táctiles más grandes */
            border-radius: 15px;
            background: radial-gradient(#e74c3c, #c0392b);
            border: 3px solid #000;
            box-shadow: 0 4px 0 #000;
            color: white;
            font-size: 1.8rem;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer;
        }
        .c-btn:active { transform: translateY(3px); box-shadow: 0 0 0 #000; }

        /* Media Query para Pantallas Grandes (Laptop) */
        @media (min-width: 992px) {
            .card-lucha { padding: 40px; } /* Más aire en el menú */
            .btn-lucha { font-size: 1.8rem; } /* Botones enormes en PC */
            
            .game-body { flex-direction: row; gap: 50px; }
            #maze-wrapper { max-height: 85vh; max-width: 85vh; }
            .controls-area { flex-direction: column; }
            .c-btn { width: 80px; height: 80px; font-size: 2rem; } /* Controles gigantes en PC */
        }

        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.95); z-index: 2000; display: none;
            align-items: center; justify-content: center;
        }
        .modal-box {
            background: #fff; border: 5px solid #000; padding: 30px;
            text-align: center; width: 90%; max-width: 450px; border-radius: 20px;
            box-shadow: 0 0 40px rgba(0,0,0,0.5);
        }
        .float-msg {
            position: absolute; font-family: 'Bangers'; font-size: 2.5rem; font-weight: bold; 
            pointer-events: none; animation: floatUp 0.8s forwards; z-index: 3000; text-shadow: 3px 3px 0 #000;
            white-space: nowrap; 
        }
        @keyframes floatUp { to { transform: translate(-50%, -150px); opacity: 0; } }
    </style>
</head>
<body>

    <div id="screen-menu">
        <div class="card-lucha p-3 p-md-5 text-center">
            
            <a href="https://www.researchgate.net/profile/A-Ortiz-Ramirez" target="_blank" class="btn btn-lucha btn-mega-academic w-100 mb-4 text-decoration-none">
                <i class="fas fa-graduation-cap"></i> CONOCE NUESTRO TRABAJO ACADEMICO Y REDES SOCIALES AQUÍ
            </a>

            <h1 class="text-danger mb-0 display-3 display-md-1 fw-bold" style="-webkit-text-stroke: 2px black;">LUCHA FINANCIERA</h1>
            <p class="mb-4 text-muted fw-bold h4">KIDS EDITION</p>
            
            <div class="d-grid gap-3">
                <button class="btn btn-light border-3 border-dark level-btn shadow-sm d-flex justify-content-between px-4 align-items-center" onclick="initLevel(1)">
                    <span class="level-icon m-0">🧸</span> 
                    <div class="text-end">
                        <span class="h3 m-0 lucha-font d-block text-primary">Juguete</span>
                        <small class="text-muted fw-bold">FÁCIL</small>
                    </div>
                </button>
                
                <button class="btn btn-light border-3 border-dark level-btn shadow-sm d-flex justify-content-between px-4 align-items-center" onclick="initLevel(2)">
                    <span class="level-icon m-0">🚲</span> 
                    <div class="text-end">
                        <span class="h3 m-0 lucha-font d-block text-warning" style="text-shadow: 1px 1px 0 #000;">Bici</span>
                        <small class="text-muted fw-bold">MEDIO</small>
                    </div>
                </button>

                <button class="btn btn-light border-3 border-dark level-btn shadow-sm d-flex justify-content-between px-4 align-items-center" onclick="initLevel(3)">
                    <span class="level-icon m-0">✈️</span> 
                    <div class="text-end">
                        <span class="h3 m-0 lucha-font d-block text-danger">Mundial</span>
                        <small class="text-muted fw-bold">DIFÍCIL</small>
                    </div>
                </button>
            </div>

            <hr class="border-3 border-dark my-4">
            
            <button class="btn btn-lucha w-100 py-3" style="background-color: #7bed9f;" onclick="goToEconMaster()">
                <i class="fas fa-gamepad fa-lg"></i> JUGAR ECONMASTER
            </button>
        </div>
    </div>

    <div id="screen-game">
        
        <div class="game-header">
            <div class="d-flex align-items-center gap-2">
                <span id="ui-lives" class="text-danger">❤️❤️❤️</span>
            </div>
            <div class="h3 m-0 text-warning lucha-font">VS</div>
            <div id="ui-timer" class="h3 m-0 fw-bold"><i class="fas fa-clock"></i> 60</div>
        </div>

        <div class="game-body">
            <div id="maze-wrapper">
                <div id="maze-grid"></div>
            </div>

            <div class="controls-area">
                <div class="control-pad">
                    <div></div> 
                    <div class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></div>
                    <div></div> 
                    
                    <div class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></div>
                    <div class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></div>
                    <div class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></div>
                </div>
                
                <div class="d-flex flex-column gap-3">
                     <button class="btn btn-warning border-2 border-dark rounded-circle shadow" style="width:60px; height:60px; font-size: 1.5rem;" onclick="toggleMusic()" id="music-btn">
                        <i class="fas fa-volume-up"></i>
                    </button>
                    <button class="btn btn-outline-light border-2 rounded-circle shadow" style="width:60px; height:60px; font-size: 1.5rem;" onclick="exitToMenu()">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h1 class="lucha-font text-danger display-4">¡EL RETO!</h1>
            <p class="mb-2 h4">📍 Arena: <strong id="inst-goal"></strong></p>
            <div class="row text-start mb-4 mt-3">
                <div class="col-6 text-success h5">✅ DINERO <br>✅ INVERSIÓN</div>
                <div class="col-6 text-danger h5">❌ GASTOS <br>❌ RUDOS</div>
            </div>
            <button class="btn btn-lucha btn-success w-100 py-3" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box bg-danger">
            <h1 class="display-1">🔔</h1>
            <h2 class="lucha-font text-white display-3">¡RINDIERON!</h2>
            <p id="lose-msg" class="text-white fw-bold h4">...</p>
            <button class="btn btn-lucha btn-dark w-100 mt-3" onclick="exitToMenu()">SALIR</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box bg-warning">
            <h1 class="display-1">🏆</h1>
            <h2 class="lucha-font text-danger display-3">¡CAMPEÓN!</h2>
            <p id="win-msg" class="text-dark fw-bold h4">...</p>
            <button class="btn btn-lucha btn-primary w-100 mt-3" onclick="exitToMenu()">GENIAL</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        const levels = {
            1: { name: "ARENA JUGUETE", size: 8, badRate: 0.25 },
            2: { name: "COLISEO BICI", size: 10, badRate: 0.30 },
            3: { name: "ARENA MUNDIAL", size: 12, badRate: 0.35 }
        };
        
        const items = {
            good: [
                {t:"¡RECIBIR LA TANDA!", i:"💰🤝"}, {t:"¡AGUINALDO!", i:"🎄🎁"},
                {t:"¡MESES SIN INTERESES!", i:"🗓️✨"}, {t:"¡SIN PAGO COMISIONES!", i:"🚫💸"},
                {t:"¡NO ANUALIDAD TDC!", i:"💳🆓"}, {t:"¡DEDUCCIÓN IMPUESTOS!", i:"📝✅"},
                {t:"¡PAGO ANTICIPADO!", i:"⏱️👍"}, {t:"¡CARGO AUTOMÁTICO!", i:"🔄"},
                {t:"¡PAGO CON PUNTOS!", i:"🌟"}, {t:"¡CUPONES!", i:"🎟️"},
                {t:"¡PENSIÓN DE VEJEZ!", i:"👴👵"}, {t:"¡PAGO DE CONTADO!", i:"💵💨"},
                {t:"¡COMPRA CON DESCUENTO!", i:"🏷️%"}, {t:"¡VENTAS JUSTAS!", i:"⚖️"},
                {t:"¡UTILIDADES!", i:"💰🚀"}, {t:"¡SUPERÁVIT!", i:"➕💵"},
                {t:"¡FONDO DE EMERGENCIA!", i:"🚨💰"}
            ],
            bad: [
                {t:"¡MULTAS!", i:"👮‍♂️"}, {t:"¡RECARGOS!", i:"📈😡"},
                {t:"¡FRAUDE!", i:"👺"}, {t:"¡BANCARROTA!", i:"🏳️"},
                {t:"¡DÉFICIT!", i:"📉😫"}, {t:"¡PAGO DE COMISIONES!", i:"💸🤏"},
                {t:"¡PAGOS SIN REGISTRO!", i:"❓📝"}, {t:"¡NO SEGUIR PRESUPUESTO!", i:"🙈"},
                {t:"¡LESIONES!", i:"🤕"}, {t:"¡ENFERMEDAD!", i:"🤒"},
                {t:"¡SOBREENDEUDAMIENTO!", i:"💣💳"}
            ]
        };

        let state = { lvl: 1, lives: 3, time: 60, active: false, canMove: true, collectedGood: 0, collectedBad: 0 };
        let player = {x:0, y:0};
        let grid = [];
        let timerInt;
        let musicOn = true; 
        let audioContextUnlocked = false;

        const sounds = {
            bgm: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/theme_01.mp3'), 
            coin: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/pickup.ogg'),
            hurt: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_01.ogg'),
            win: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/GalaxyInvaders/bonus.wav'),
            lose: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/assets/sound/explosion_02.ogg')
        };
        sounds.bgm.loop = true; sounds.bgm.volume = 0.3;

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function unlockAudio() {
            if(audioContextUnlocked) return;
            Object.values(sounds).forEach(s => {
                s.play().then(() => { s.pause(); if(s !== sounds.bgm) s.currentTime = 0; }).catch(()=>{});
            });
            audioContextUnlocked = true;
            if(musicOn && state.active) sounds.bgm.play();
            document.removeEventListener('click', unlockAudio); document.removeEventListener('touchstart', unlockAudio); document.removeEventListener('keydown', unlockAudio);
        }
        document.addEventListener('click', unlockAudio); document.addEventListener('touchstart', unlockAudio); document.addEventListener('keydown', unlockAudio);

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            musicOn = !musicOn;
            if(musicOn) {
                btn.innerHTML = '<i class="fas fa-volume-up"></i>'; btn.classList.remove('btn-danger'); btn.classList.add('btn-warning');
                if(state.active && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute"></i>'; btn.classList.remove('btn-warning'); btn.classList.add('btn-danger');
                sounds.bgm.pause();
            }
        }

        function playSfx(key) { if(musicOn && audioContextUnlocked) { try { const s = sounds[key].cloneNode(); s.volume = 0.6; s.play().catch(()=>{}); } catch(e) {} } }
        function goToEconMaster() { if(confirm("¿Ir a EconMaster?")) window.location.href = "https://econ-master-8w1z.vercel.app/"; }

        function showScreen(id) {
            document.getElementById('screen-menu').style.display = 'none';
            document.getElementById('screen-game').style.display = 'none';
            if(id === 'screen-menu') document.getElementById('screen-menu').style.display = 'flex';
            if(id === 'screen-game') document.getElementById('screen-game').style.display = 'flex';
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
            state.active = false; clearInterval(timerInt);
            sounds.bgm.pause(); sounds.bgm.currentTime = 0;
            showModal(null); showScreen('screen-menu');
        }

        function startGame() {
            showModal(null); showScreen('screen-game');
            state.lives = 3; state.time = 60; state.collectedGood = 0; state.collectedBad = 0;
            state.active = true; state.canMove = true;
            updateUI();
            generateGrid(levels[state.lvl].size);
            renderGrid();
            clearInterval(timerInt);
            timerInt = setInterval(() => { state.time--; updateUI(); if(state.time <= 0) gameOver("time"); }, 1000);
            if(musicOn && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            window.onkeydown = (e) => {
                if(e.key === 'ArrowUp') move(0,-1); if(e.key === 'ArrowDown') move(0,1);
                if(e.key === 'ArrowLeft') move(-1,0); if(e.key === 'ArrowRight') move(1,0);
            };
        }

        function generateGrid(size) {
            grid = []; 
            const badRate = levels[state.lvl].badRate;
            let goodPool = shuffleArray([...items.good]);
            let badPool = shuffleArray([...items.bad]);

            for(let y=0; y<size; y++) {
                let row = [];
                for(let x=0; x<size; x++) {
                    let isWall = Math.random() < 0.3;
                    if((x<2 && y<2) || (x>size-3 && y>size-3)) isWall = false;
                    let item = null;
                    if(!isWall && Math.random() < 0.3 && !(x===0 && y===0)) {
                        const isBad = Math.random() < badRate;
                        if(isBad) {
                            if(badPool.length === 0) badPool = shuffleArray([...items.bad]);
                            item = { ...badPool.pop(), type: 'bad' };
                        } else {
                            if(goodPool.length === 0) goodPool = shuffleArray([...items.good]);
                            item = { ...goodPool.pop(), type: 'good' };
                        }
                    }
                    row.push({ wall: isWall, item: item });
                }
                grid.push(row);
            }
            let cx=0, cy=0;
            while(cx < size-1 || cy < size-1) {
                grid[cy][cx].wall = false; if(grid[cy][cx].item?.type === 'bad') grid[cy][cx].item = null;
                if(cx < size-1 && (Math.random()>0.5 || cy === size-1)) cx++; else cy++;
            }
            grid[size-1][size-1].wall = false; player = {x:0, y:0};
        }

        function renderGrid() {
            const div = document.getElementById('maze-grid');
            div.innerHTML = ''; const size = levels[state.lvl].size;
            div.style.gridTemplateColumns = `repeat(${size}, 1fr)`; 
            div.style.gridTemplateRows = `repeat(${size}, 1fr)`; 
            for(let y=0; y<size; y++) {
                for(let x=0; x<size; x++) {
                    const cell = document.createElement('div'); cell.className = 'cell';
                    const data = grid[y][x];
                    if(data.wall) cell.classList.add('wall'); else if(data.item) cell.innerText = data.item.i;
                    if(x===player.x && y===player.y) { cell.innerHTML = '🤼‍♂️'; cell.style.zIndex = 10; }
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';
                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e && e.cancelable) e.preventDefault();
            if(!state.active || !state.canMove) return;
            if(musicOn && sounds.bgm.paused && audioContextUnlocked) sounds.bgm.play();
            state.canMove = false; setTimeout(() => state.canMove = true, 120); 
            const size = levels[state.lvl].size; let nx = player.x + dx; let ny = player.y + dy;
            if(nx>=0 && nx<size && ny>=0 && ny<size && !grid[ny][nx].wall) {
                player = {x:nx, y:ny};
                const cell = grid[ny][nx];
                if(cell.item) {
                    floatText(cell.item.t, cell.item.type==='good'?'#2ed573':'#ff4757');
                    if(cell.item.type === 'good') { playSfx('coin'); state.collectedGood++; } 
                    else { playSfx('hurt'); state.collectedBad++; state.lives--; updateUI(); 
                        const wrap = document.getElementById('maze-wrapper'); wrap.style.borderColor = "white"; 
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
            document.getElementById('ui-timer').className = state.time < 10 ? "h3 m-0 text-danger fw-bold" : "h3 m-0 text-white";
            let h = ""; for(let i=0;i<state.lives;i++) h+="❤️";
            document.getElementById('ui-lives').innerText = h;
        }

        function gameOver(reason) {
            state.active = false; playSfx('lose');
            document.getElementById('lose-msg').innerText = reason === 'time' ? "¡TIEMPO AGOTADO!" : "¡SIN VIDA!";
            showModal('modal-lose');
        }

        function gameWin() {
            state.active = false; playSfx('win');
            document.getElementById('win-msg').innerText = "¡GANASTE EN " + levels[state.lvl].name + "!";
            showModal('modal-win');
        }

        function floatText(txt, col) {
            const el = document.createElement('div'); el.innerText = txt; el.className = 'float-msg'; 
            el.style.left = '50%'; el.style.top = '50%'; el.style.transform = 'translate(-50%, -50%)'; el.style.color = col;
            document.body.appendChild(el); setTimeout(() => el.remove(), 1000);
        }
    </script>
</body>
</html>
