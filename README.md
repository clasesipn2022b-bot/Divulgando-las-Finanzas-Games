# Divulgando-las-Finanzas-Games
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Aventura Financiera Kids</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Varela+Round&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS BASE --- */
        :root {
            --bg-gradient: linear-gradient(180deg, #a18cd1 0%, #fbc2eb 100%);
            --primary: #ff6b6b;
            --secondary: #48dbfb;
            --accent: #feca57;
            --text: #2d3436;
        }

        * { box-sizing: border-box; }

        body {
            margin: 0; padding: 0;
            background-image: var(--bg-gradient);
            color: var(--text);
            font-family: 'Varela Round', sans-serif;
            overflow: hidden; /* Evitar scroll durante el juego */
            height: 100vh;
            display: flex;
            flex-direction: column;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        h1, h2, h3 {
            font-family: 'Fredoka One', cursive;
            text-transform: uppercase;
            color: white;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.1);
            margin: 10px 0;
        }

        /* --- NAVEGACIÓN --- */
        .top-nav {
            display: flex; justify-content: space-between; align-items: center;
            padding: 10px 20px;
            background: rgba(255,255,255,0.3);
            backdrop-filter: blur(5px);
            z-index: 1000;
            height: 60px;
            flex-shrink: 0;
        }

        .nav-btn {
            background: white; color: var(--primary);
            padding: 8px 16px; border-radius: 30px; text-decoration: none;
            font-weight: bold; box-shadow: 0 4px 0 rgba(0,0,0,0.1);
            font-size: 0.9rem; border: none; cursor: pointer;
            display: flex; align-items: center; gap: 8px;
        }
        .nav-btn:active { transform: translateY(2px); box-shadow: none; }

        /* --- PANTALLAS (Menú y Juego) --- */
        .screen {
            flex: 1;
            width: 100%;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            transition: opacity 0.3s;
        }

        /* Ocultar pantallas inactivas */
        .hidden { display: none !important; }

        /* --- MENÚ PRINCIPAL --- */
        .hero-card {
            background: rgba(255,255,255,0.9);
            padding: 30px; border-radius: 25px;
            text-align: center;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            max-width: 600px;
            width: 100%;
            margin-top: 20px;
        }

        .level-grid {
            display: flex; flex-wrap: wrap; gap: 15px; justify-content: center;
            margin-top: 30px;
        }

        .level-btn {
            background: white; border: 2px solid #eee;
            border-radius: 20px; padding: 15px; width: 140px;
            cursor: pointer; transition: transform 0.1s;
            box-shadow: 0 6px 0 #ddd;
            display: flex; flex-direction: column; align-items: center;
        }
        .level-btn:active { transform: translateY(6px); box-shadow: none; }
        
        .lvl-1 { border-top: 8px solid var(--secondary); }
        .lvl-2 { border-top: 8px solid var(--accent); }
        .lvl-3 { border-top: 8px solid var(--primary); }

        /* --- JUEGO --- */
        .game-header {
            width: 100%; max-width: 600px;
            background: var(--accent);
            padding: 10px 20px; border-radius: 15px;
            display: flex; justify-content: space-between; align-items: center;
            color: white; font-weight: bold;
            box-shadow: 0 5px 0 rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        #maze-wrapper {
            background: #8d6e63;
            padding: 10px; border-radius: 10px;
            border: 4px solid #5d4037;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        #maze-grid {
            display: grid; gap: 1px;
        }

        .cell {
            width: 35px; height: 35px;
            display: flex; align-items: center; justify-content: center;
            background: #ffe0b2; font-size: 20px;
        }
        .wall { background: #5d4037; border-radius: 4px; }

        /* Controles */
        .controls {
            margin-top: 20px;
            display: grid; grid-template-columns: 70px 70px 70px; gap: 10px;
        }
        .c-btn {
            width: 70px; height: 70px; background: white; border-radius: 50%;
            border: none; box-shadow: 0 6px 0 #bdc3c7; font-size: 2rem;
            color: var(--text); cursor: pointer;
        }
        .c-btn:active { transform: translateY(6px); box-shadow: none; background: #f0f0f0; }
        .up { grid-column: 2; } .left { grid-column: 1; grid-row: 2; }
        .down { grid-column: 2; grid-row: 2; } .right { grid-column: 3; grid-row: 2; }

        /* --- MODALES --- */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85); z-index: 2000;
            display: none; align-items: center; justify-content: center;
            padding: 20px;
        }
        .modal-content {
            background: white; padding: 30px; border-radius: 25px;
            text-align: center; max-width: 400px; width: 100%;
            border: 6px solid var(--secondary);
            animation: popIn 0.4s;
        }
        .modal-content h2 { color: var(--primary); text-shadow: none; }
        .modal-content p { color: #555; font-size: 1.1rem; margin-bottom: 20px; }

        .big-btn {
            background: var(--secondary); color: white; border: none;
            padding: 15px 40px; font-size: 1.2rem; border-radius: 40px;
            font-family: 'Fredoka One'; width: 100%; cursor: pointer;
            box-shadow: 0 6px 0 rgba(0,0,0,0.2);
        }
        .big-btn:active { transform: translateY(4px); box-shadow: none; }

        @keyframes popIn { 0% {transform: scale(0);} 90% {transform: scale(1.05);} 100% {transform: scale(1);} }
        
        /* Flotantes */
        .float-msg {
            position: absolute; font-weight: bold; font-size: 1.5rem; z-index: 3000;
            pointer-events: none; animation: floatUp 1s forwards; text-shadow: 1px 1px 0 white;
        }
        @keyframes floatUp { to { transform: translateY(-50px); opacity: 0; } }

    </style>
</head>
<body>

    <div class="top-nav">
        <a href="https://ambrosioortizramirez.link" class="nav-btn">
            <i class="fas fa-home"></i> Salir
        </a>
        <button class="nav-btn" onclick="toggleMusic()" id="music-btn">
            <i class="fas fa-volume-mute"></i> Música
        </button>
    </div>

    <div id="screen-menu" class="screen">
        <div class="hero-card">
            <div style="font-size: 4rem;">🐷</div>
            <h1 style="color: var(--primary); text-shadow: none;">Laberinto Financiero</h1>
            <p style="color: #666;">¡Ahorra para comprar tus sueños!</p>

            <div class="level-grid">
                <button class="level-btn lvl-1" onclick="initLevel(1)">
                    <span style="font-size: 2.5rem;">🧸</span>
                    <strong>Corto Plazo</strong>
                </button>
                <button class="level-btn lvl-2" onclick="initLevel(2)">
                    <span style="font-size: 2.5rem;">🚲</span>
                    <strong>Mediano</strong>
                </button>
                <button class="level-btn lvl-3" onclick="initLevel(3)">
                    <span style="font-size: 2.5rem;">✈️</span>
                    <strong>Largo Plazo</strong>
                </button>
            </div>
        </div>
        
        <div style="margin-top: 40px; opacity: 0.7; color: white;">
            <i class="fas fa-gamepad"></i> Más juegos próximamente...
        </div>
    </div>

    <div id="screen-game" class="screen hidden">
        <div class="game-header">
            <div id="ui-lives">❤️❤️❤️</div>
            <div id="ui-timer"><i class="fas fa-stopwatch"></i> 60s</div>
            <button onclick="exitToMenu()" style="background:none; border:none; color:white; font-size:1.5rem; cursor:pointer;">
                <i class="fas fa-times-circle"></i>
            </button>
        </div>

        <div id="maze-wrapper">
            <div id="maze-grid"></div>
        </div>

        <div class="controls">
            <button class="c-btn up" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-arrow-up"></i></button>
            <button class="c-btn left" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-arrow-left"></i></button>
            <button class="c-btn down" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-arrow-down"></i></button>
            <button class="c-btn right" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-arrow-right"></i></button>
        </div>
    </div>

    <div id="modal-inst" class="modal">
        <div class="modal-content">
            <h2>¡Tu Misión!</h2>
            <div style="text-align: left; margin: 20px; font-size: 1.1rem; line-height: 1.8;">
                🎯 <strong>Meta:</strong> <span id="inst-goal">...</span><br>
                🐷 <strong>Muévete:</strong> Usa las flechas.<br>
                💰 <strong>Recoge:</strong> Dinero y Ahorro.<br>
                ❌ <strong>Evita:</strong> Gastos Hormiga.<br>
                ⏱️ <strong>Tiempo:</strong> 60 Segundos.
            </div>
            <button class="big-btn" onclick="startGame()">¡JUGAR AHORA!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal">
        <div class="modal-content" style="border-color: var(--primary);">
            <div style="font-size: 4rem;">💸</div>
            <h2 style="color: var(--primary);">¡Oh no!</h2>
            <p id="lose-msg">Se acabó el dinero.</p>
            <button class="big-btn" style="background: var(--primary);" onclick="exitToMenu()">Intentar de Nuevo</button>
        </div>
    </div>

    <div id="modal-win" class="modal">
        <div class="modal-content" style="border-color: var(--accent);">
            <div style="font-size: 4rem;">🏆</div>
            <h2 style="color: var(--accent);">¡LO LOGRASTE!</h2>
            <p id="win-msg">Meta Cumplida</p>
            <button class="big-btn" style="background: var(--accent);" onclick="exitToMenu()">¡Genial!</button>
        </div>
    </div>

    <script>
        /* --- CONFIGURACIÓN --- */
        const levels = {
            1: { name: "Juguete Nuevo", size: 8, badRate: 0.2 },
            2: { name: "Bicicleta Roja", size: 10, badRate: 0.25 },
            3: { name: "Viaje a la Playa", size: 12, badRate: 0.3 }
        };
        
        const items = {
            good: [{t:"¡Ahorro!", i:"💰"}, {t:"¡Sueldo!", i:"💵"}],
            bad: [{t:"¡Gasto!", i:"🐜"}, {t:"¡Dulces!", i:"🍭"}]
        };

        /* --- ESTADO --- */
        let state = {
            lvl: 1,
            lives: 3,
            time: 60,
            active: false,
            canMove: true
        };
        let player = {x:0, y:0};
        let grid = [];
        let timerInt;
        let musicOn = false;

        /* --- AUDIO --- */
        // Definición segura de audios
        const sounds = {
            bgm: new Audio('https://cdn.pixabay.com/audio/2022/01/18/audio_d0a13f69d2.mp3'),
            coin: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_9704e4b8d2.mp3'),
            hurt: new Audio('https://cdn.pixabay.com/audio/2022/03/10/audio_c628727358.mp3'),
            win: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_0625c153e1.mp3'),
            lose: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_88447e769f.mp3')
        };
        sounds.bgm.loop = true;
        sounds.bgm.volume = 0.3;

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            musicOn = !musicOn;
            
            if(musicOn) {
                btn.innerHTML = '<i class="fas fa-volume-up"></i> Música';
                btn.style.color = "#48dbfb";
                // Solo reproducir si estamos en juego, para no molestar en menú
                if(state.active) sounds.bgm.play().catch(()=>{});
            } else {
                btn.innerHTML = '<i class="fas fa-volume-mute"></i> Música';
                btn.style.color = "#ff6b6b";
                sounds.bgm.pause();
            }
        }

        function playSfx(key) {
            if(musicOn) {
                // Clonar para permitir sonidos rápidos superpuestos
                try {
                    const s = sounds[key].cloneNode();
                    s.volume = 0.5;
                    s.play().catch(()=>{});
                } catch(e) {}
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
            
            // Reset Estado
            state.lives = 3;
            state.time = 60;
            state.active = true;
            state.canMove = true;
            
            updateUI();
            
            // Generar Laberinto
            const size = levels[state.lvl].size;
            generateGrid(size);
            renderGrid();
            
            // Iniciar Timer
            clearInterval(timerInt);
            timerInt = setInterval(() => {
                state.time--;
                updateUI();
                if(state.time <= 0) gameOver("time");
            }, 1000);

            // Música de fondo (si está activada)
            if(musicOn) sounds.bgm.play().catch(()=>{});

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
                    // Paredes aleatorias (30% prob)
                    let isWall = Math.random() < 0.3;
                    // Asegurar esquinas libres
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

            // Garantizar camino (Algoritmo simple de excavadora)
            let cx=0, cy=0;
            while(cx < size-1 || cy < size-1) {
                grid[cy][cx].wall = false;
                // Quitar items malos del camino principal para que sea posible pasar
                if(grid[cy][cx].item?.type === 'bad') grid[cy][cx].item = null;

                if(cx < size-1 && (Math.random()>0.5 || cy === size-1)) cx++;
                else cy++;
            }
            grid[size-1][size-1].wall = false; // Meta
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

                    if(x===player.x && y===player.y) {
                        cell.innerHTML = '🐷';
                        cell.style.zIndex = 10;
                    }
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';

                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e) e.preventDefault(); // Prevenir doble toque en móvil
            if(!state.active || !state.canMove) return;

            // Cooldown de movimiento (freno)
            state.canMove = false;
            setTimeout(() => state.canMove = true, 150);

            const size = levels[state.lvl].size;
            let nx = player.x + dx;
            let ny = player.y + dy;

            if(nx>=0 && nx<size && ny>=0 && ny<size && !grid[ny][nx].wall) {
                player = {x:nx, y:ny};
                
                // Lógica Items
                const cell = grid[ny][nx];
                if(cell.item) {
                    floatText(cell.item.t, cell.item.type==='good'?'#48dbfb':'#ff6b6b');
                    if(cell.item.type === 'good') {
                        playSfx('coin');
                    } else {
                        playSfx('hurt');
                        state.lives--;
                        updateUI();
                        document.body.style.backgroundColor = "#ff7675";
                        setTimeout(()=>document.body.style.backgroundImage = "var(--bg-gradient)", 150);
                        if(state.lives <= 0) gameOver('lives');
                    }
                    cell.item = null; // Consumir item
                }

                renderGrid();

                // Meta
                if(nx === size-1 && ny === size-1) {
                    gameWin();
                }
            }
        }

        function updateUI() {
            document.getElementById('ui-timer').innerText = state.time + "s";
            let h = ""; for(let i=0;i<state.lives;i++) h+="❤️";
            document.getElementById('ui-lives').innerText = h;
        }

        function gameOver(reason) {
            state.active = false;
            playSfx('lose');
            const msg = reason === 'time' ? "¡Se acabó el tiempo!" : "¡Gastaste todos tus ahorros!";
            document.getElementById('lose-msg').innerText = msg;
            showModal('modal-lose');
        }

        function gameWin() {
            state.active = false;
            playSfx('win');
            document.getElementById('win-msg').innerText = "¡Conseguiste: " + levels[state.lvl].name + "!";
            showModal('modal-win');
        }

        function floatText(txt, col) {
            const el = document.createElement('div');
            el.innerText = txt;
            el.className = 'float-msg';
            el.style.color = col;
            // Centrar en pantalla
            el.style.left = '50%'; 
            el.style.top = '40%';
            el.style.transform = 'translate(-50%, -50%)';
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 1000);
        }

    </script>
</body>
