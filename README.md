# Divulgando-las-Finanzas-Games
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera Kids</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS LUCHA LIBRE --- */
        :root {
            --bg-color: #2c3e50;
            --primary: #e74c3c; /* Rojo Sangre */
            --secondary: #f1c40f; /* Amarillo Mostaza */
            --accent: #3498db; /* Azul Rey */
            --dark: #1a1a1a;
            --light: #ecf0f1;
            --rope: #c0392b;
        }

        * { box-sizing: border-box; }

        body {
            margin: 0; padding: 0;
            /* Fondo con patrón de semitono (estilo cómic) */
            background: radial-gradient(circle, #2c3e50 20%, #000000 100%);
            color: var(--text);
            font-family: 'Roboto Condensed', sans-serif;
            overflow: hidden;
            height: 100vh;
            display: flex; flex-direction: column;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        h1, h2, h3 {
            font-family: 'Bangers', cursive;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-align: center;
            color: var(--secondary);
            text-shadow: 3px 3px 0px var(--primary), 5px 5px 0px black;
            margin: 10px 0;
        }

        /* --- NAVEGACIÓN --- */
        .top-nav {
            display: flex; justify-content: space-between; align-items: center;
            padding: 10px 20px;
            background: var(--dark);
            border-bottom: 4px solid var(--secondary);
            z-index: 1000; height: 70px; flex-shrink: 0;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
        }

        .nav-btn {
            background: var(--primary); color: white;
            padding: 8px 16px; border: 2px solid black; 
            border-radius: 5px; text-decoration: none;
            font-family: 'Bangers', cursive; font-size: 1.1rem;
            cursor: pointer; display: flex; align-items: center; gap: 8px;
            transform: skew(-10deg); /* Estilo dinámico */
        }
        .nav-btn:active { transform: skew(-10deg) translateY(2px); }

        /* --- PANTALLAS --- */
        .screen {
            flex: 1; width: 100%; overflow-y: auto;
            display: flex; flex-direction: column; align-items: center;
            padding: 20px; transition: opacity 0.3s;
        }
        .hidden { display: none !important; }

        /* --- MENÚ PRINCIPAL (CARTELERA) --- */
        .hero-card {
            background: #fff;
            background-image: repeating-linear-gradient(45deg, #fff 0, #fff 10px, #f0f0f0 10px, #f0f0f0 20px);
            padding: 30px; border: 5px solid var(--dark);
            text-align: center;
            box-shadow: 10px 10px 0px var(--primary);
            max-width: 600px; width: 100%; margin-top: 20px;
            position: relative;
        }
        /* Tachuelas del cartel */
        .hero-card::before, .hero-card::after {
            content: ''; position: absolute; top: 10px; width: 15px; height: 15px;
            background: silver; border-radius: 50%; border: 2px solid black;
        }
        .hero-card::before { left: 10px; } .hero-card::after { right: 10px; }

        .level-grid {
            display: flex; flex-wrap: wrap; gap: 15px; justify-content: center;
            margin-top: 30px;
        }

        .level-btn {
            background: var(--accent); border: 3px solid black;
            color: white;
            padding: 15px; width: 140px;
            cursor: pointer; transition: transform 0.1s;
            box-shadow: 5px 5px 0 black;
            display: flex; flex-direction: column; align-items: center;
        }
        .level-btn:active { transform: translate(3px, 3px); box-shadow: 2px 2px 0 black; }
        
        .lvl-title { font-family: 'Bangers'; font-size: 1.2rem; margin-top: 5px; text-shadow: 1px 1px 0 black;}

        /* --- JUEGO (EL RING) --- */
        .game-header {
            width: 100%; max-width: 600px;
            background: var(--dark);
            border: 3px solid var(--secondary);
            padding: 10px 20px; 
            display: flex; justify-content: space-between; align-items: center;
            color: white; font-family: 'Bangers'; font-size: 1.5rem;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            margin-bottom: 20px;
        }

        #maze-wrapper {
            background: #eee; /* Lona del ring */
            padding: 15px; 
            border: 8px solid var(--rope); /* Cuerdas rojas */
            border-radius: 5px;
            box-shadow: 
                inset 0 0 20px rgba(0,0,0,0.3),
                0 0 0 4px white, /* Espacio entre cuerdas */
                0 0 0 8px var(--rope), /* Segunda cuerda */
                0 10px 20px rgba(0,0,0,0.5);
            position: relative;
        }
        /* Esquinas del ring */
        #maze-wrapper::after {
            content: 'ARENA MÉXICO';
            position: absolute; bottom: -25px; right: 0; left: 0;
            text-align: center; font-family: 'Bangers'; color: white; letter-spacing: 3px;
        }

        #maze-grid { display: grid; gap: 0; /* Sin espacio, lona continua */ }

        .cell {
            width: 35px; height: 35px;
            display: flex; align-items: center; justify-content: center;
            background: rgba(255,255,255,0.8); 
            font-size: 22px;
            border: 1px solid rgba(0,0,0,0.05); /* Textura lona */
        }
        /* Muros oscuros (El público/fuera del ring) */
        .wall { 
            background: #222; 
            background-image: radial-gradient(#333 15%, transparent 16%);
            background-size: 5px 5px;
        }

        /* Controles */
        .controls {
            margin-top: 30px;
            display: grid; grid-template-columns: 70px 70px 70px; gap: 10px;
        }
        .c-btn {
            width: 70px; height: 70px; 
            background: var(--primary); border: 3px solid black; border-radius: 50%;
            box-shadow: 0 6px 0 #800000; font-size: 2rem;
            color: white; cursor: pointer;
        }
        .c-btn:active { transform: translateY(6px); box-shadow: none; }
        .up { grid-column: 2; } .left { grid-column: 1; grid-row: 2; }
        .down { grid-column: 2; grid-row: 2; } .right { grid-column: 3; grid-row: 2; }

        /* --- MODALES --- */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 2000;
            display: none; align-items: center; justify-content: center; padding: 20px;
        }
        .modal-content {
            background: var(--secondary); /* Fondo amarillo cartel */
            padding: 30px; border: 5px solid black;
            text-align: center; max-width: 400px; width: 100%;
            transform: rotate(-2deg); /* Estilo desenfadado */
            animation: popIn 0.4s;
            box-shadow: 15px 15px 0 rgba(255,0,0,0.5);
        }
        .modal-content h2 { 
            color: black; text-shadow: 2px 2px 0 white; font-size: 2.5rem;
        }
        .modal-content p { 
            color: black; font-size: 1.2rem; font-weight: bold; margin-bottom: 20px; 
        }

        /* RESUMEN ESTADÍSTICO */
        .summary-stats {
            display: grid; grid-template-columns: 1fr 1fr; gap: 10px;
            background: white; padding: 15px; border: 3px solid black;
            margin-bottom: 20px;
        }
        .stat-box {
            padding: 5px; 
            font-weight: bold; font-size: 1rem;
            text-transform: uppercase;
        }
        .stat-good { color: #27ae60; border-right: 2px dashed black; }
        .stat-bad { color: #c0392b; }
        .stat-num { font-family: 'Bangers'; font-size: 2rem; display: block; color: black;}

        .big-btn {
            background: var(--accent); color: white; border: 3px solid black;
            padding: 10px 30px; font-size: 1.5rem; 
            font-family: 'Bangers'; width: 100%; cursor: pointer;
            box-shadow: 5px 5px 0 black; text-transform: uppercase;
        }
        .big-btn:active { transform: translate(3px, 3px); box-shadow: 2px 2px 0 black; }

        @keyframes popIn { 0% {transform: scale(0) rotate(0deg);} 80% {transform: scale(1.1) rotate(-3deg);} 100% {transform: scale(1) rotate(-2deg);} }
        
        .float-msg {
            position: absolute; font-family: 'Bangers'; 
            font-size: 2rem; z-index: 3000; color: var(--secondary);
            text-shadow: 2px 2px 0 black;
            pointer-events: none; animation: floatUp 1s forwards;
        }
        @keyframes floatUp { to { transform: translate(-50%, -80px) scale(1.5); opacity: 0; } }

    </style>
</head>
<body>

    <div class="top-nav">
        <a href="https://ambrosioortizramirez.link" class="nav-btn">
            <i class="fas fa-home"></i> SALIR
        </a>
        <button class="nav-btn" onclick="toggleMusic()" id="music-btn">
            <i class="fas fa-volume-mute"></i> SONIDO
        </button>
    </div>

    <div id="screen-menu" class="screen">
        <div class="hero-card">
            <div style="font-size: 4rem;">👺</div>
            <h1>LUCHA FINANCIERA</h1>
            <p style="font-weight:bold; text-transform:uppercase;">¡Vence a los Rudos y Gana el Campeonato!</p>

            <div style="background:black; color:white; padding:5px; font-family:'Bangers'; font-size:1.2rem; margin:15px 0;">
                ELIGE TU ARENA:
            </div>

            <div class="level-grid">
                <button class="level-btn" onclick="initLevel(1)" style="background:#ff9ff3; color:black;">
                    <span style="font-size: 2.5rem;">🧸</span>
                    <span class="lvl-title">Arena<br>Juguete</span>
                    <span style="font-size:0.8rem">(Corto Plazo)</span>
                </button>
                <button class="level-btn" onclick="initLevel(2)" style="background:#54a0ff; color:black;">
                    <span style="font-size: 2.5rem;">🚲</span>
                    <span class="lvl-title">Coliseo<br>Bici</span>
                    <span style="font-size:0.8rem">(Mediano)</span>
                </button>
                <button class="level-btn" onclick="initLevel(3)" style="background:#ff6b6b; color:black;">
                    <span style="font-size: 2.5rem;">✈️</span>
                    <span class="lvl-title">Arena<br>Mundial</span>
                    <span style="font-size:0.8rem">(Largo Plazo)</span>
                </button>
            </div>
        </div>
    </div>

    <div id="screen-game" class="screen hidden">
        <div class="game-header">
            <div id="ui-lives">❤️❤️❤️</div>
            <div style="color:var(--secondary)">VS</div>
            <div id="ui-timer"><i class="fas fa-clock"></i> 60</div>
            <button onclick="exitToMenu()" style="background:none; border:none; color:white; font-size:1.5rem; cursor:pointer;">
                <i class="fas fa-sign-out-alt"></i>
            </button>
        </div>

        <div id="maze-wrapper">
            <div id="maze-grid"></div>
        </div>

        <div class="controls">
            <button class="c-btn up" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></button>
            <button class="c-btn left" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></button>
            <button class="c-btn down" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></button>
            <button class="c-btn right" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></button>
        </div>
    </div>

    <div id="modal-inst" class="modal">
        <div class="modal-content">
            <h2>¡EL RETO!</h2>
            <div style="text-align: left; margin: 20px; font-size: 1.1rem; line-height: 1.5; background:white; padding:10px; border:2px solid black;">
                📍 <strong>Sede:</strong> <span id="inst-goal" style="color:red; font-weight:bold;">...</span><br>
                🤼 <strong>Técnico:</strong> Recoge <span style="color:green">Dinero</span>.<br>
                👹 <strong>Rudos:</strong> Evita <span style="color:red">Gastos Hormiga</span>.<br>
                🏆 <strong>Meta:</strong> Llega al <span style="color:#f1c40f; background:black; padding:0 5px;">Cinturón</span>.
            </div>
            <button class="big-btn" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal">
        <div class="modal-content" style="background:#e74c3c; color:white;">
            <div style="font-size: 4rem;">🔔</div>
            <h2 style="color:white; text-shadow:3px 3px 0 black;">¡TE RINDIERON!</h2>
            <p id="lose-msg" style="color:white;">Perdiste la máscara.</p>
            
            <div class="summary-stats">
                <div class="stat-box stat-good">Ganancias <span class="stat-num" id="lose-good">0</span></div>
                <div class="stat-box stat-bad">Pérdidas <span class="stat-num" id="lose-bad">0</span></div>
            </div>

            <button class="big-btn" style="background:black;" onclick="exitToMenu()">REVANCHA</button>
        </div>
    </div>

    <div id="modal-win" class="modal">
        <div class="modal-content" style="background:#f1c40f;">
            <div style="font-size: 4rem;">🏆</div>
            <h2 style="color:#c0392b;">¡CAMPEÓN!</h2>
            <p id="win-msg">¡El público enloquece!</p>

            <div class="summary-stats">
                <div class="stat-box stat-good">Ganancias <span class="stat-num" id="win-good">0</span></div>
                <div class="stat-box stat-bad">Pérdidas <span class="stat-num" id="win-bad">0</span></div>
            </div>

            <button class="big-btn" style="background:#3498db;" onclick="exitToMenu()">¡VICTORIA!</button>
        </div>
    </div>

    <script>
        /* --- CONFIGURACIÓN --- */
        const levels = {
            1: { name: "ARENA JUGUETE", size: 8, badRate: 0.2 },
            2: { name: "COLISEO BICI", size: 10, badRate: 0.25 },
            3: { name: "ARENA MUNDIAL", size: 12, badRate: 0.3 }
        };
        
        const items = {
            // Iconos temáticos: Dinero/Inversión vs Gastos/Rudos
            good: [{t:"¡DINERO!", i:"💵"}, {t:"¡AHORRO!", i:"💰"}, {t:"¡LLAVE!", i:"🗝️"}],
            bad: [{t:"¡SILLAZO!", i:"🪑"}, {t:"¡RUDO!", i:"👹"}, {t:"¡GASTO!", i:"💸"}]
        };

        /* --- ESTADO DEL JUEGO --- */
        let state = {
            lvl: 1,
            lives: 3,
            time: 60,
            active: false,
            canMove: true,
            collectedGood: 0,
            collectedBad: 0
        };
        let player = {x:0, y:0};
        let grid = [];
        let timerInt;
        let musicOn = false;

        /* --- AUDIO --- */
        const sounds = {
            bgm: new Audio('https://cdn.pixabay.com/audio/2022/03/15/audio_7764920df3.mp3'), // Algo más rock/acción
            coin: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_9704e4b8d2.mp3'),
            hurt: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_c642338665.mp3'), // Golpe seco
            win: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_0625c153e1.mp3'),
            lose: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_88447e769f.mp3')
        };
        sounds.bgm.loop = true;
        sounds.bgm.volume = 0.3;

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            musicOn = !musicOn;
            if(musicOn) {
                btn.innerHTML = '<i class="fas fa-volume-up"></i> SONIDO';
                btn.style.background = "#2ecc71";
                btn.style.color = "black";
                if(state.active) sounds.bgm.play().catch(()=>{});
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute"></i> MUTE';
                btn.style.background = "#e74c3c";
                btn.style.color = "white";
                sounds.bgm.pause();
            }
        }

        function playSfx(key) {
            if(musicOn) {
                try { const s = sounds[key].cloneNode(); s.volume = 0.5; s.play().catch(()=>{}); } catch(e) {}
            }
        }

        /* --- NAVEGACIÓN --- */
        function showScreen(id) {
            document.querySelectorAll('.screen').forEach(el => el.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
        }
        
        function showModal(id) {
            document.querySelectorAll('.modal').forEach(el => el.style.display = 'none');
            if(id) document.getElementById(id).style.display = 'flex';
        }

        function initLevel(lvl) {
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
            
            // Reset
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
            div.style.gridTemplateColumns = `repeat(${size}, 35px)`;

            for(let y=0; y<size; y++) {
                for(let x=0; x<size; x++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    const data = grid[y][x];
                    
                    if(data.wall) cell.classList.add('wall');
                    else if(data.item) cell.innerText = data.item.i;

                    // Renderizar Jugador (Luchador)
                    if(x===player.x && y===player.y) {
                        cell.innerHTML = '🤼‍♂️'; 
                        cell.style.zIndex = 10;
                    }
                    // Renderizar Meta (Cinturón)
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';
                    
                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e) e.preventDefault(); 
            if(!state.active || !state.canMove) return;

            state.canMove = false;
            setTimeout(() => state.canMove = true, 150); // Freno de velocidad

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
                        // Efecto de golpe en pantalla
                        document.getElementById('maze-wrapper').style.borderColor = "white";
                        setTimeout(()=>document.getElementById('maze-wrapper').style.borderColor = "#c0392b", 100);
                        
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
            if(state.time < 10) document.getElementById('ui-timer').style.color = "red";
            else document.getElementById('ui-timer').style.color = "white";

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
            // Posicionar en el centro de la pantalla para mejor visibilidad
            el.style.left = '50%'; el.style.top = '50%'; 
            el.style.transform = 'translate(-50%, -50%)';
            el.style.color = col;
            if(col === 'red') el.style.fontSize = "3rem"; // Golpes más grandes
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 1000);
        }

    </script>
</body>
