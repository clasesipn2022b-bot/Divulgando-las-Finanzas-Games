<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera </title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS TEMÁTICOS --- */
        :root {
            --primary-lucha: #ff4757; 
            --secondary-lucha: #ffa502; 
            --dark-lucha: #2f3542;
            --bg-color: #1e272e;
        }

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background-color: var(--bg-color);
            background-image: radial-gradient(#ffffff 1px, transparent 1px);
            background-size: 20px 20px;
            color: #333;
            min-height: 100vh;
            overflow: hidden; 
            user-select: none;
            touch-action: manipulation;
        }

        h1, h2, h3, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 1.5px;
            text-shadow: 2px 2px 0px #000;
        }

        /* --- BOTONES --- */
        .btn-lucha {
            font-family: 'Bangers', cursive;
            text-transform: uppercase;
            border: 3px solid #000;
            border-radius: 10px;
            box-shadow: 4px 4px 0px #000;
            transition: transform 0.1s, box-shadow 0.1s;
        }
        .btn-lucha:active { transform: translate(2px, 2px); box-shadow: 1px 1px 0px #000; }

        .btn-mega-academic {
            background: linear-gradient(45deg, #ffa502, #ffda79);
            color: #000 !important;
            border: 3px solid #fff;
            white-space: normal;
            box-shadow: 0 0 15px var(--secondary-lucha), 4px 4px 0 #000;
            animation: glowing 2s infinite;
        }
        @keyframes glowing { 50% { box-shadow: 0 0 25px #ff6b81, 4px 4px 0 #000; } }

        /* --- EL RING --- */
        #maze-wrapper {
            background: #dfe6e9;
            padding: 10px;
            border: 5px solid #ff4757;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            aspect-ratio: 1 / 1;
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
            position: relative; /* Referencia para posicionamiento si fuera necesario */
        }

        #maze-grid {
            display: grid;
            width: 100%;
            height: 100%;
        }

        .cell {
            display: flex; align-items: center; justify-content: center;
            background: #fff;
            border: 1px solid #ecf0f1;
            font-size: clamp(1rem, 2.5vw, 2rem); 
        }
        .wall { 
            background: #2f3542; 
            background-image: repeating-linear-gradient(45deg, #333 0, #333 2px, #222 2px, #222 5px); 
        }

        /* --- CONTROLES --- */
        .control-pad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            width: 180px; 
        }
        
        .c-btn {
            width: 100%; aspect-ratio: 1/1;
            border-radius: 15px;
            background: radial-gradient(#e74c3c, #c0392b);
            border: 3px solid #000;
            box-shadow: 0 4px 0 #000;
            color: white;
            font-size: 1.5rem;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer;
            transition: transform 0.05s;
        }
        .c-btn:active { transform: translateY(3px); box-shadow: 0 0 0 #000; }

        /* --- MENSAJES FLOTANTES MEJORADOS --- */
        .float-msg {
            position: absolute; 
            font-family: 'Bangers'; 
            font-size: 1.8rem; /* Tamaño base */
            font-weight: bold; 
            pointer-events: none; 
            animation: floatUp 2.5s forwards; /* AUMENTADO A 2.5 SEGUNDOS */
            z-index: 5000; 
            text-shadow: 2px 2px 0 #000, -1px -1px 0 #fff; /* Borde doble para lectura */
            white-space: nowrap;
            /* El left y top se definen en JS */
        }

        /* Animación más lenta y visible */
        @keyframes floatUp { 
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
            10% { transform: translate(-50%, -80%) scale(1.2); opacity: 1; } /* Pop in rápido */
            20% { transform: translate(-50%, -90%) scale(1); opacity: 1; }
            80% { transform: translate(-50%, -120px) scale(1); opacity: 1; } /* Se queda quieto un rato */
            100% { transform: translate(-50%, -150px) scale(0.8); opacity: 0; } /* Se va */
        }

        /* --- MODALES --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 9999; display: none;
            align-items: center; justify-content: center; backdrop-filter: blur(5px);
        }
        .modal-box {
            background: #fff; border: 5px solid #000; padding: 2rem;
            text-align: center; max-width: 500px; width: 90%; border-radius: 20px;
            animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        @keyframes popIn { from{transform: scale(0.5); opacity:0;} to{transform: scale(1); opacity:1;} }
    </style>
</head>
<body>

    <div id="screen-menu" class="container min-vh-100 d-flex align-items-center justify-content-center">
        <div class="row w-100 justify-content-center">
            <div class="col-12 col-md-10 col-lg-6">
                <div class="card p-4 border-0 shadow-lg rounded-4" style="border: 4px solid black !important;">
                    
                    <a href="https://www.researchgate.net/profile/A-Ortiz-Ramirez" target="_blank" class="btn btn-lucha btn-mega-academic w-100 mb-4 text-decoration-none">
                        <i class="fas fa-graduation-cap fa-lg"></i> CONOCE NUESTRO TRABAJO ACADEMICO Y REDES SOCIALES AQUÍ
                    </a>

                    <div class="text-center mb-4">
                        <h1 class="text-danger display-3 fw-bold lucha-font">LUCHA FINANCIERA</h1>
                        <span class="badge bg-dark fs-5">KIDS EDITION</span>
                    </div>

                    <div class="d-grid gap-3 mb-4">
                        <button class="btn btn-light btn-lg border border-3 border-dark d-flex justify-content-between align-items-center p-3 shadow-sm" onclick="initLevel(1)">
                            <span class="fs-1">🧸</span>
                            <div class="text-end lh-1">
                                <span class="h3 d-block lucha-font text-primary m-0">Juguete</span>
                                <small class="fw-bold text-muted">FÁCIL</small>
                            </div>
                        </button>
                        
                        <button class="btn btn-light btn-lg border border-3 border-dark d-flex justify-content-between align-items-center p-3 shadow-sm" onclick="initLevel(2)">
                            <span class="fs-1">🚲</span>
                            <div class="text-end lh-1">
                                <span class="h3 d-block lucha-font text-warning m-0" style="text-shadow:1px 1px 0 #000;">Bici</span>
                                <small class="fw-bold text-muted">MEDIO</small>
                            </div>
                        </button>

                        <button class="btn btn-light btn-lg border border-3 border-dark d-flex justify-content-between align-items-center p-3 shadow-sm" onclick="initLevel(3)">
                            <span class="fs-1">✈️</span>
                            <div class="text-end lh-1">
                                <span class="h3 d-block lucha-font text-danger m-0">Mundial</span>
                                <small class="fw-bold text-muted">DIFÍCIL</small>
                            </div>
                        </button>
                    </div>

                    <button class="btn btn-lucha w-100 py-3 btn-success" style="background-color: #7bed9f; color: black; border-color: black;" onclick="goToEconMaster()">
                        <i class="fas fa-gamepad fa-lg"></i> JUGAR ECONMASTER
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="screen-game" class="container-fluid min-vh-100 d-none flex-column p-0">
        
        <div class="row bg-dark text-white py-2 px-3 mx-0 border-bottom border-warning border-4 align-items-center shadow">
            <div class="col-4 d-flex align-items-center">
                <span id="ui-lives" class="fs-4 text-danger">❤️❤️❤️</span>
            </div>
            <div class="col-4 text-center">
                <span class="h2 m-0 text-warning lucha-font">VS</span>
            </div>
            <div class="col-4 text-end">
                <span id="ui-timer" class="h3 m-0 fw-bold"><i class="fas fa-clock"></i> 60</span>
            </div>
        </div>

        <div class="row flex-grow-1 align-items-center justify-content-center m-0 w-100 position-relative">
            
            <div class="col-12 col-lg-7 p-3 d-flex justify-content-center">
                <div id="maze-wrapper">
                    <div id="maze-grid"></div>
                </div>
            </div>

            <div class="col-12 col-lg-5 pb-4 pb-lg-0 d-flex flex-column align-items-center justify-content-center">
                
                <div class="control-pad mb-4">
                    <div></div> 
                    <div class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></div>
                    <div></div> 
                    
                    <div class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></div>
                    <div class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></div>
                    <div class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></div>
                </div>

                <div class="d-flex gap-3">
                    <button class="btn btn-warning border-3 border-dark rounded-circle shadow p-3" onclick="toggleMusic()" id="music-btn" style="width: 60px; height: 60px;">
                        <i class="fas fa-volume-up fa-lg"></i>
                    </button>
                    <button class="btn btn-danger border-3 border-dark rounded-pill shadow px-4 fw-bold font-monospace" onclick="exitToMenu()">
                        SALIR
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h1 class="lucha-font text-danger display-4 mb-3">¡EL RETO!</h1>
            <p class="fs-4">Estás en: <strong id="inst-goal" class="text-primary"></strong></p>
            <hr>
            <div class="row text-start fs-5 my-3">
                <div class="col-6 text-success fw-bold">
                    <i class="fas fa-check-circle"></i> DINERO <br>
                    <i class="fas fa-check-circle"></i> INVERSIÓN
                </div>
                <div class="col-6 text-danger fw-bold">
                    <i class="fas fa-times-circle"></i> GASTOS <br>
                    <i class="fas fa-times-circle"></i> RUDOS
                </div>
            </div>
            <button class="btn btn-lucha btn-success w-100 py-3 fs-3" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box bg-danger border-white">
            <div class="display-1 mb-2">🔔</div>
            <h2 class="lucha-font text-white display-3">¡TE RINDIERON!</h2>
            <p id="lose-msg" class="text-white h4 fw-bold mb-4">...</p>
            <button class="btn btn-lucha btn-dark w-100 fs-4" onclick="exitToMenu()">VOLVER A INTENTAR</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box bg-warning border-dark">
            <div class="display-1 mb-2">🏆</div>
            <h2 class="lucha-font text-danger display-3">¡CAMPEÓN!</h2>
            <p id="win-msg" class="text-dark h4 fw-bold mb-4">...</p>
            <button class="btn btn-lucha btn-primary w-100 fs-4" onclick="exitToMenu()">GENIAL</button>
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
                btn.innerHTML = '<i class="fas fa-volume-up fa-lg"></i>'; btn.classList.remove('btn-danger'); btn.classList.add('btn-warning');
                if(state.active && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute fa-lg"></i>'; btn.classList.remove('btn-warning'); btn.classList.add('btn-danger');
                sounds.bgm.pause();
            }
        }

        function playSfx(key) { if(musicOn && audioContextUnlocked) { try { const s = sounds[key].cloneNode(); s.volume = 0.6; s.play().catch(()=>{}); } catch(e) {} } }
        function goToEconMaster() { if(confirm("¿Ir a EconMaster?")) window.location.href = "https://econ-master-8w1z.vercel.app/"; }

        function showScreen(id) {
            document.getElementById('screen-menu').classList.remove('d-flex');
            document.getElementById('screen-menu').style.display = 'none';
            document.getElementById('screen-game').classList.remove('d-flex');
            
            if(id === 'screen-menu') {
                document.getElementById('screen-menu').style.display = 'flex';
                document.getElementById('screen-menu').classList.add('d-flex');
            }
            if(id === 'screen-game') {
                document.getElementById('screen-game').classList.remove('d-none');
                document.getElementById('screen-game').classList.add('d-flex');
            }
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
                
                // Get the DOM element for the cell to position the float text
                const cellIndex = ny * size + nx;
                const targetCell = document.getElementById('maze-grid').children[cellIndex];

                if(cell.item) {
                    floatText(cell.item.t, cell.item.type==='good'?'#2ed573':'#ff4757', targetCell);
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

        function floatText(txt, col, target) {
            const el = document.createElement('div');
            el.innerText = txt;
            el.className = 'float-msg';
            el.style.color = col;

            // Positioning logic relative to the cell
            if(target) {
                const rect = target.getBoundingClientRect();
                el.style.left = (rect.left + rect.width / 2) + 'px';
                el.style.top = (rect.top) + 'px';
            } else {
                el.style.left = '50%'; el.style.top = '50%';
            }

            document.body.appendChild(el);
            setTimeout(() => el.remove(), 2500); // 2.5 seconds to match animation
        }
    </script>
</body>
</html>
