# Divulgando-las-Finanzas-Games
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Aventura Financiera Kids | Dr. Ambrosio</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Varela+Round&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- ESTILOS GENERALES --- */
        :root {
            --bg-gradient: linear-gradient(180deg, #a18cd1 0%, #fbc2eb 100%);
            --primary-color: #ff6b6b;
            --secondary-color: #48dbfb;
            --accent-color: #feca57;
            --text-color: #2d3436;
            --card-bg: #ffffff;
        }

        body {
            margin: 0; padding: 0;
            background-image: var(--bg-gradient);
            color: var(--text-color);
            font-family: 'Varela Round', sans-serif;
            /* Permitir scroll en el menú, pero bloquearlo en el juego */
            overflow-x: hidden;
            min-height: 100vh;
            -webkit-tap-highlight-color: transparent;
        }

        h1, h2, h3 {
            font-family: 'Fredoka One', cursive;
            text-transform: uppercase;
            text-align: center;
            color: white;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.1);
        }

        /* --- UI SUPERIOR --- */
        .top-nav {
            display: flex; justify-content: space-between; align-items: center;
            padding: 15px;
            background: rgba(255,255,255,0.2);
            backdrop-filter: blur(5px);
            position: sticky; top: 0; z-index: 50;
        }

        .nav-btn {
            background: white; color: var(--primary-color);
            padding: 8px 15px; border-radius: 30px; text-decoration: none;
            font-weight: bold; box-shadow: 0 4px 0 rgba(0,0,0,0.1);
            font-size: 0.9rem; border: none; cursor: pointer;
            display: flex; align-items: center; gap: 5px;
        }
        .nav-btn:active { transform: translateY(4px); box-shadow: none; }

        /* --- MENÚ PRINCIPAL --- */
        #main-container {
            padding: 20px;
            max-width: 800px; margin: 0 auto;
            text-align: center;
        }

        .hero-section {
            background: rgba(255,255,255,0.9);
            padding: 30px 20px; border-radius: 25px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 40px;
            border-bottom: 8px solid #e0e0e0;
        }

        .level-grid {
            display: flex; flex-wrap: wrap; gap: 15px; justify-content: center;
            margin-top: 20px;
        }

        .level-card {
            background: #fff; border: 2px solid #eee;
            border-radius: 20px; padding: 15px; width: 130px;
            cursor: pointer; transition: transform 0.2s;
            box-shadow: 0 5px 0 #ddd;
        }
        .level-card:active { transform: translateY(5px); box-shadow: none; }
        
        /* Colores de niveles */
        .lvl-1 { border-top: 10px solid var(--secondary-color); }
        .lvl-2 { border-top: 10px solid var(--accent-color); }
        .lvl-3 { border-top: 10px solid var(--primary-color); }

        /* --- SECCIÓN "MÁS JUEGOS" (PLACEHOLDERS) --- */
        .more-games-section {
            margin-top: 50px;
            padding-bottom: 50px;
        }
        .more-games-title { font-size: 1.5rem; margin-bottom: 20px; color: white; }
        
        .games-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 20px;
        }

        .game-placeholder {
            background: rgba(255,255,255,0.6);
            border-radius: 15px; padding: 20px;
            color: #666; font-size: 0.9rem;
            display: flex; flex-direction: column; align-items: center; gap: 10px;
        }
        .game-placeholder i { font-size: 2rem; opacity: 0.5; }

        /* --- PANTALLA DE JUEGO (MODAL) --- */
        #game-ui {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #fff3cd; z-index: 100;
            flex-direction: column; align-items: center;
        }

        .game-header {
            width: 100%; padding: 10px 20px; background: var(--accent-color);
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* LABERINTO */
        #maze-area {
            flex: 1; display: flex; align-items: center; justify-content: center;
            width: 100%; overflow: hidden; position: relative;
        }

        #maze-container {
            display: grid; gap: 1px; 
            background: #8d6e63; padding: 5px; border-radius: 10px;
            border: 4px solid #5d4037;
        }

        .cell {
            width: 32px; height: 32px;
            display: flex; align-items: center; justify-content: center;
            font-size: 20px; background: #ffe0b2;
        }
        .wall { background: #6d4c41; border-radius: 4px; }
        
        /* CONTROLES TÁCTILES */
        .controls-area {
            padding: 20px; background: rgba(255,255,255,0.9);
            width: 100%; border-top-left-radius: 25px; border-top-right-radius: 25px;
            display: flex; justify-content: center;
            box-shadow: 0 -5px 20px rgba(0,0,0,0.1);
        }
        .d-pad {
            display: grid; grid-template-columns: 70px 70px 70px; gap: 10px;
        }
        .c-btn {
            width: 70px; height: 70px; background: white; border-radius: 50%;
            border: none; box-shadow: 0 6px 0 #bdc3c7; font-size: 2rem;
            color: var(--text-color); cursor: pointer; touch-action: manipulation;
        }
        .c-btn:active { transform: translateY(6px); box-shadow: none; background: #f0f0f0; }
        .up { grid-column: 2; } .left { grid-column: 1; grid-row: 2; }
        .down { grid-column: 2; grid-row: 2; } .right { grid-column: 3; grid-row: 2; }

        /* MODALES (Instrucciones, Win, Lose) */
        .modal-overlay {
            display: none; position: fixed; top:0; left:0; width:100%; height:100%;
            background: rgba(0,0,0,0.85); z-index: 200;
            align-items: center; justify-content: center; padding: 20px;
        }
        .modal-box {
            background: white; padding: 30px; border-radius: 25px;
            text-align: center; max-width: 400px; width: 100%;
            border: 8px solid var(--secondary-color);
            animation: popIn 0.4s;
        }
        @keyframes popIn { 0% {transform: scale(0);} 80% {transform: scale(1.1);} 100% {transform: scale(1);} }

        .big-btn {
            background: var(--secondary-color); color: white; border: none;
            padding: 15px 40px; font-size: 1.2rem; border-radius: 40px;
            font-family: 'Fredoka One'; margin-top: 20px; cursor: pointer;
            box-shadow: 0 6px 0 rgba(0,0,0,0.2); width: 100%;
        }
        .big-btn:active { transform: translateY(6px); box-shadow: none; }

        /* MENSAJES FLOTANTES */
        .float-txt {
            position: absolute; font-weight: bold; font-size: 1.2rem; z-index: 10;
            animation: floatUp 0.8s forwards; text-shadow: 1px 1px 0 #fff;
        }
        @keyframes floatUp { to { transform: translateY(-40px); opacity: 0; } }

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

    <div id="main-container">
        
        <section class="hero-section">
            <div style="font-size: 4rem; margin-bottom: 10px;">🐷</div>
            <h1 style="color: var(--primary-color);">El Laberinto del Ahorro</h1>
            <p>Ayuda al cerdito a cumplir sus metas. ¡Cuidado con los gastos hormiga!</p>

            <h3 style="color: #666; margin-top: 20px; font-size: 1rem;">Elige tu meta:</h3>
            
            <div class="level-grid">
                <div class="level-card lvl-1" onclick="initGame(1)">
                    <div style="font-size: 2.5rem;">🧸</div>
                    <strong>Corto Plazo</strong>
                    <div style="font-size: 0.8rem; color:#888;">Juguetes</div>
                </div>
                <div class="level-card lvl-2" onclick="initGame(2)">
                    <div style="font-size: 2.5rem;">🚲</div>
                    <strong>Mediano</strong>
                    <div style="font-size: 0.8rem; color:#888;">Bicicleta</div>
                </div>
                <div class="level-card lvl-3" onclick="initGame(3)">
                    <div style="font-size: 2.5rem;">✈️</div>
                    <strong>Largo Plazo</strong>
                    <div style="font-size: 0.8rem; color:#888;">Viaje</div>
                </div>
            </div>
        </section>

        <section class="more-games-section">
            <h2 class="more-games-title">Próximamente más juegos</h2>
            <div class="games-grid">
                <div class="game-placeholder">
                    <i class="fas fa-brain"></i>
                    <strong>Memorama de Monedas</strong>
                    <span>(En construcción)</span>
                </div>
                <div class="game-placeholder">
                    <i class="fas fa-balance-scale"></i>
                    <strong>Balanza de Precios</strong>
                    <span>(En construcción)</span>
                </div>
                <div class="game-placeholder">
                    <i class="fas fa-calculator"></i>
                    <strong>Calculadora Mágica</strong>
                    <span>(En construcción)</span>
                </div>
            </div>
        </section>
    </div>

    <div id="inst-modal" class="modal-overlay">
        <div class="modal-box">
            <h2 style="color: var(--secondary-color);">¿Cómo jugar?</h2>
            <div style="text-align: left; margin: 20px 0; font-size: 1rem; line-height: 2;">
                ✅ Come <strong>Ahorro</strong> y <strong>Sueldo</strong>.<br>
                ❌ Evita <strong>Gastos Hormiga</strong> (Quitan ❤️).<br>
                🏁 Llega a la <strong>Meta</strong> final.
            </div>
            <button class="big-btn" onclick="startGame()">¡JUGAR!</button>
        </div>
    </div>

    <div id="game-ui">
        <div class="game-header">
            <div style="color:white; font-weight:bold;" id="goal-title">Meta: Juguete</div>
            <div style="color:white; font-size: 1.5rem;" id="lives-display">❤️❤️❤️</div>
            <button onclick="quitGame()" style="background:none; border:none; color:white; font-size:1.5rem;"><i class="fas fa-times"></i></button>
        </div>

        <div id="maze-area">
            <div id="maze-container"></div>
        </div>

        <div class="controls-area">
            <div class="d-pad">
                <button class="c-btn up" ontouchstart="movePlayer(0,-1)" onmousedown="movePlayer(0,-1)"><i class="fas fa-arrow-up"></i></button>
                <button class="c-btn left" ontouchstart="movePlayer(-1,0)" onmousedown="movePlayer(-1,0)"><i class="fas fa-arrow-left"></i></button>
                <button class="c-btn down" ontouchstart="movePlayer(0,1)" onmousedown="movePlayer(0,1)"><i class="fas fa-arrow-down"></i></button>
                <button class="c-btn right" ontouchstart="movePlayer(1,0)" onmousedown="movePlayer(1,0)"><i class="fas fa-arrow-right"></i></button>
            </div>
        </div>
    </div>

    <div id="lose-modal" class="modal-overlay">
        <div class="modal-box">
            <div style="font-size: 4rem;">💸</div>
            <h2 style="color: var(--primary-color);">¡Sin dinero!</h2>
            <p>Los gastos hormiga se comieron tus ahorros.</p>
            <button class="big-btn" style="background: var(--primary-color);" onclick="quitGame()">Salir</button>
        </div>
    </div>

    <div id="win-modal" class="modal-overlay">
        <div class="modal-box" style="border-color: var(--accent-color);">
            <div style="font-size: 4rem;">🏆</div>
            <h2 style="color: var(--accent-color);">¡LO LOGRASTE!</h2>
            <p id="win-msg">¡Compraste tu juguete!</p>
            <button class="big-btn" style="background: var(--accent-color);" onclick="quitGame()">¡Genial!</button>
        </div>
    </div>

    <script>
        /* --- SISTEMA DE AUDIO --- */
        // Usamos MP3s libres de derechos (Pixabay)
        const audio = {
            bgm: new Audio('https://cdn.pixabay.com/audio/2022/01/18/audio_d0a13f69d2.mp3'), // Música infantil feliz
            coin: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_9704e4b8d2.mp3'), // Sonido bueno
            hurt: new Audio('https://cdn.pixabay.com/audio/2022/03/10/audio_c628727358.mp3'), // Sonido malo (boing)
            win: new Audio('https://cdn.pixabay.com/audio/2021/08/04/audio_0625c153e1.mp3'),  // Victoria
            lose: new Audio('https://cdn.pixabay.com/audio/2021/08/09/audio_88447e769f.mp3') // Derrota
        };
        
        audio.bgm.loop = true;
        audio.bgm.volume = 0.3;
        let musicEnabled = false;

        function toggleMusic() {
            const btn = document.getElementById('music-btn');
            if(!musicEnabled) {
                musicEnabled = true;
                btn.innerHTML = '<i class="fas fa-volume-up"></i> Música';
                btn.style.color = "#48dbfb";
                audio.bgm.play().catch(e => console.log("Interacción requerida"));
            } else {
                musicEnabled = false;
                btn.innerHTML = '<i class="fas fa-volume-mute"></i> Música';
                btn.style.color = "#ff6b6b";
                audio.bgm.pause();
            }
        }

        function playSfx(name) {
            if(musicEnabled) {
                // Clonamos el audio para permitir sonidos simultáneos rápidos
                const sound = audio[name].cloneNode();
                sound.volume = 0.5;
                sound.play();
            }
        }

        /* --- DATOS DEL JUEGO --- */
        const levels = {
            1: { name: "Juguete Nuevo", size: 8, badRate: 0.15 },
            2: { name: "Bicicleta Roja", size: 10, badRate: 0.25 },
            3: { name: "Viaje a la Playa", size: 12, badRate: 0.35 }
        };
        
        const items = {
            good: [ {t:"Ahorro", i:"💰"}, {t:"Sueldo", i:"💵"}, {t:"Bono", i:"💎"} ],
            bad:  [ {t:"Gasto Hormiga", i:"🐜"}, {t:"Dulces", i:"🍭"}, {t:"Compra", i:"🛒"} ]
        };

        let currentLvl = 1;
        let lives = 3;
        let rows, cols;
        let maze = [], gridItems = [];
        let player = {x:0, y:0};

        /* --- CONTROL DE FLUJO --- */
        function initGame(lvl) {
            currentLvl = lvl;
            document.getElementById('inst-modal').style.display = 'flex';
        }

        function startGame() {
            document.getElementById('inst-modal').style.display = 'none';
            document.getElementById('main-container').style.display = 'none';
            document.getElementById('game-ui').style.display = 'flex';
            
            // Si el usuario ya activó música antes, asegurar que suene
            if(musicEnabled) audio.bgm.play();

            lives = 3;
            updateLives();
            document.getElementById('goal-title').innerText = "Meta: " + levels[currentLvl].name;
            
            rows = levels[currentLvl].size;
            cols = levels[currentLvl].size;
            
            generateMaze();
            renderMaze();
            
            window.addEventListener('keydown', handleKey);
        }

        function quitGame() {
            document.getElementById('game-ui').style.display = 'none';
            document.getElementById('win-modal').style.display = 'none';
            document.getElementById('lose-modal').style.display = 'none';
            document.getElementById('main-container').style.display = 'block';
            window.removeEventListener('keydown', handleKey);
        }

        function updateLives() {
            let h = "";
            for(let i=0; i<lives; i++) h += "❤️";
            document.getElementById('lives-display').innerText = h;
        }

        /* --- LÓGICA DEL LABERINTO --- */
        function generateMaze() {
            maze = []; gridItems = [];
            const badChance = levels[currentLvl].badRate;

            for(let y=0; y<rows; y++) {
                let row = [], iRow = [];
                for(let x=0; x<cols; x++) {
                    // Paredes aleatorias
                    let isWall = Math.random() < 0.3 ? 1 : 0;
                    if((x<2 && y<2) || (x>cols-3 && y>rows-3)) isWall = 0; // Limpiar esquinas
                    row.push(isWall);

                    // Items
                    let it = null;
                    if(isWall === 0 && Math.random() < 0.3 && !(x===0 && y===0)) {
                        if(Math.random() < badChance) {
                            it = {...items.bad[Math.floor(Math.random()*items.bad.length)], type:'bad'};
                        } else {
                            it = {...items.good[Math.floor(Math.random()*items.good.length)], type:'good'};
                        }
                    }
                    iRow.push(it);
                }
                maze.push(row); gridItems.push(iRow);
            }

            // Camino garantizado (Excavadora)
            let cx=0, cy=0;
            while(cx < cols-1 || cy < rows-1) {
                maze[cy][cx] = 0;
                if(gridItems[cy][cx]?.type === 'bad') gridItems[cy][cx] = null; // Quitar malos del camino principal
                
                if(cx < cols-1 && (Math.random()>0.5 || cy === rows-1)) cx++;
                else cy++;
            }
            maze[rows-1][cols-1] = 0; // Meta
        }

        function renderMaze() {
            const cont = document.getElementById('maze-container');
            cont.innerHTML = '';
            cont.style.gridTemplateColumns = `repeat(${cols}, 32px)`;

            for(let y=0; y<rows; y++) {
                for(let x=0; x<cols; x++) {
                    const d = document.createElement('div');
                    d.className = 'cell';
                    if(maze[y][x]===1) d.classList.add('wall');
                    else {
                        // Item
                        if(gridItems[y][x]) d.innerText = gridItems[y][x].i;
                    }
                    
                    // Jugador
                    if(x===player.x && y===player.y) {
                        d.innerHTML = '🐷'; d.style.zIndex=5;
                    }
                    // Meta
                    if(x===cols-1 && y===rows-1) d.innerHTML = '🏆';

                    cont.appendChild(d);
                }
            }
        }

        /* --- MOVIMIENTO --- */
        function handleKey(e) {
            if(e.key==='ArrowUp') movePlayer(0,-1);
            if(e.key==='ArrowDown') movePlayer(0,1);
            if(e.key==='ArrowLeft') movePlayer(-1,0);
            if(e.key==='ArrowRight') movePlayer(1,0);
        }

        function movePlayer(dx, dy) {
            if(lives <= 0) return;
            
            let nx = player.x + dx;
            let ny = player.y + dy;

            if(nx>=0 && nx<cols && ny>=0 && ny<rows && maze[ny][nx]!==1) {
                player = {x:nx, y:ny};
                
                // Item check
                const it = gridItems[ny][nx];
                if(it) {
                    showFloatText(it.t, it.type==='good'?'#48dbfb':'#ff6b6b', nx, ny);
                    if(it.type === 'good') playSfx('coin');
                    else {
                        playSfx('hurt');
                        lives--;
                        updateLives();
                        document.getElementById('game-ui').style.backgroundColor = "#ffcccb";
                        setTimeout(()=>document.getElementById('game-ui').style.backgroundColor = "#fff3cd", 200);
                        
                        if(lives<=0) {
                            playSfx('lose');
                            document.getElementById('lose-modal').style.display = 'flex';
                        }
                    }
                    gridItems[ny][nx] = null;
                }

                renderMaze();

                // Win check
                if(nx===cols-1 && ny===rows-1) {
                    playSfx('win');
                    document.getElementById('win-msg').innerText = "¡Conseguiste: " + levels[currentLvl].name + "!";
                    document.getElementById('win-modal').style.display = 'flex';
                }
            }
        }

        function showFloatText(txt, col, x, y) {
            // Posición aproximada basada en celda
            // Simplemente lo mostramos en el centro para facilitar
            const el = document.createElement('div');
            el.innerText = txt;
            el.className = 'float-txt';
            el.style.color = col;
            el.style.left = '50%';
            el.style.top = '40%';
            document.body.appendChild(el);
            setTimeout(()=>el.remove(), 800);
        }

    </script>
</body>
</html>
