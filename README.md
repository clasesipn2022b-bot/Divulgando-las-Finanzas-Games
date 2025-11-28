<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    
    <title>Luchas por las Finanzas de México</title>
    <meta name="description" content="Juego educativo financiero del Dr. Ambrosio Ortiz. Aprende sobre ingresos, gastos y riesgos en el ring de la economía.">
    <meta property="og:title" content="Luchas por las Finanzas de México">
    <meta property="og:description" content="¡Súbete al ring y defiende tu dinero! Un juego educativo del IPN.">
    <meta property="og:image" content="wrestling_6769709.png">
    <meta property="og:url" content="https://ambrosioortizramirez.link">
    <meta name="theme-color" content="#E4007C">
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- PALETA DE COLORES --- */
        :root {
            --azul-titulo: #0d47a1; 
            --rosa-mexicano: #E4007C;
            --amarillo-mx: #FFD700; /* Amarillo intenso para botones/títulos */
            --amarillo-tenue: #fff9c4; /* Amarillo MUY suave para el jugador (casi pastel) */
            --verde-mx: #009c3b;
            --morado-mx: #6A1B9A;
            --fondo-oscuro: #121212;
        }

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background-color: var(--fondo-oscuro);
            background-image: radial-gradient(#333 1px, transparent 1px);
            background-size: 20px 20px;
            color: #333;
            height: 100dvh; 
            width: 100vw;
            overflow: hidden; 
            user-select: none;
            touch-action: manipulation;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        h1, h2, h3, .lucha-font {
            font-family: 'Bangers', cursive;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        /* --- PANTALLA DE CARGA (Preloader) --- */
        #preloader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--fondo-oscuro); z-index: 9999;
            display: flex; justify-content: center; align-items: center;
            color: var(--rosa-mexicano); font-size: 2rem;
            transition: opacity 0.5s;
        }

        /* --- AVISO DE ROTACIÓN (Mejora UX) --- */
        #rotation-warning {
            display: none;
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.95); z-index: 9998;
            color: white; flex-direction: column;
            justify-content: center; align-items: center; text-align: center;
        }
        @media screen and (orientation: landscape) and (max-height: 500px) {
            #rotation-warning { display: flex !important; }
        }

        /* --- WRAPPER GENERAL --- */
        #app-container {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* --- PANTALLA MENÚ --- */
        #screen-menu {
            width: 100%; height: 100%;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            padding: 10px;
        }

        .menu-card {
            background: #fff;
            border: 4px solid #000;
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            max-width: 650px;
            width: 100%;
            box-shadow: 8px 8px 0 var(--morado-mx);
            margin: auto;
            position: relative;
            max-height: 98vh;
            overflow-y: auto;
            display: flex; flex-direction: column; justify-content: center;
        }

        /* Header Compacto */
        .title-container {
            display: flex; align-items: center; justify-content: center;
            gap: 10px; margin-bottom: 5px; position: relative; z-index: 2;
        }

        .avatar-img {
            width: 60px; height: 60px;
            border: 2px solid #000; border-radius: 50%;
            box-shadow: 2px 2px 0 var(--amarillo-mx);
            background: white; object-fit: cover; flex-shrink: 0;
            cursor: pointer; transition: transform 0.2s;
        }
        .avatar-img:hover { transform: scale(1.1); }

        .wrestling-mask {
            width: 40px; height: auto; position: absolute;
            top: 5px; right: 5px; filter: drop-shadow(1px 1px 0 #000);
            z-index: 1; opacity: 0.9;
        }

        .main-title {
            color: var(--azul-titulo);
            text-shadow: 1px 1px 0 #fff, 3px 3px 0 #000;
            font-size: 1.6rem; margin: 0; line-height: 1.1; text-align: left;
        }

        .social-links {
            font-size: 0.8rem; color: #444; background: #f8f9fa;
            padding: 5px; border-radius: 8px; border: 1px solid #eee; margin-bottom: 5px;
        }
        .social-links a { color: var(--morado-mx); text-decoration: none; font-weight: bold; margin: 0 5px; }

        .btn-lucha {
            font-family: 'Bangers', cursive; font-size: 1.1rem;
            border: 2px solid #000; border-radius: 8px;
            box-shadow: 3px 3px 0 #000; transition: transform 0.1s;
            background: white; color: black; padding: 8px 10px;
        }
        .btn-lucha:active { transform: translate(2px, 2px); box-shadow: 1px 1px 0 #000; }

        .btn-nivel-1 { background: #81ecec; }
        .btn-nivel-2 { background: var(--amarillo-mx); }
        .btn-nivel-3 { background: var(--rosa-mexicano); color: white; }

        /* Media Query PC */
        @media (min-width: 768px) {
            .menu-card { padding: 30px; overflow-y: visible; max-height: none; }
            .avatar-img { width: 90px; height: 90px; border-width: 3px; }
            .wrestling-mask { width: 60px; top: 15px; right: 15px; }
            .main-title { font-size: 3rem; text-shadow: 2px 2px 0 #fff, 4px 4px 0 #000; }
            .btn-lucha { font-size: 1.4rem; padding: 12px 20px; border-width: 3px; }
        }

        /* --- PANTALLA JUEGO --- */
        #screen-game {
            width: 100%; height: 100%; display: none;
            flex-direction: column; justify-content: space-between; align-items: center;
            padding: 10px 10px 20px 10px;
        }

        @media (min-width: 992px) {
            #screen-game { flex-direction: row; justify-content: center; gap: 50px; }
            #maze-container { max-height: 80vh !important; max-width: 80vh !important; }
            .controls-panel { width: auto !important; }
            .control-pad { width: 180px !important; gap: 10px !important; }
            .c-btn { height: 70px !important; width: 70px !important; font-size: 2rem !important; }
        }

        #maze-container {
            flex-grow: 1; display: flex; justify-content: center; align-items: center;
            width: 100%; max-height: 45vh; aspect-ratio: 1 / 1; position: relative;
        }

        #maze-wrapper {
            background: #eee; padding: 5px; border: 5px solid var(--rosa-mexicano);
            border-radius: 10px; box-shadow: 0 0 0 4px #000, 5px 5px 20px rgba(0,0,0,0.8);
            width: 100%; height: 100%;
        }

        #maze-grid { display: grid; width: 100%; height: 100%; border: 2px solid #000; }

        .cell {
            display: flex; align-items: center; justify-content: center;
            background: #fff; border: 1px solid rgba(0,0,0,0.1);
            font-size: clamp(14px, 4vw, 30px);
            transition: background-color 0.1s;
            overflow: hidden; 
        }
        .wall { 
            background: #2d3436; 
            background-image: repeating-linear-gradient(45deg, #000 0, #000 2px, #2d3436 2px, #2d3436 6px);
        }

        /* CLASE NUEVA: LUZ DEL LUCHADOR (Color Tenue) */
        .player-active {
            background-color: var(--amarillo-tenue) !important; /* Uso del amarillo suave */
            box-shadow: inset 0 0 15px #fff59d; /* Brillo interno más suave */
            animation: pulsePlayer 1s infinite alternate;
            border: 2px solid #000 !important;
        }
        @keyframes pulsePlayer {
            0% { background-color: var(--amarillo-tenue); transform: scale(0.95); }
            100% { background-color: #ffffff; transform: scale(1); }
        }

        .controls-panel {
            width: 100%; display: flex; flex-direction: column;
            align-items: center; justify-content: center; gap: 8px; flex-shrink: 0;
        }

        .hud-bar {
            background: #000; color: white; padding: 5px 15px;
            border-radius: 15px; border: 2px solid var(--amarillo-mx);
            display: flex; justify-content: space-between; align-items: center;
            width: 100%; max-width: 400px; font-size: 1rem; margin-bottom: 5px;
        }

        .control-pad {
            display: grid; grid-template-columns: repeat(3, 1fr); gap: 5px; width: 150px;
        }

        .c-btn {
            width: 100%; aspect-ratio: 1/1; border-radius: 10px;
            background: var(--rosa-mexicano); border: 2px solid #000;
            box-shadow: 0 3px 0 #000; color: white; font-size: 1.4rem;
            display: flex; align-items: center; justify-content: center; cursor: pointer;
        }
        .c-btn:active { transform: translateY(2px); box-shadow: 0 0 0 #000; background: #c20066; }

        .btn-salir {
            background: #d63031; color: white; border: 2px solid #000;
            padding: 4px 15px; border-radius: 15px; font-weight: bold; font-size: 0.9rem;
        }

        /* --- MODALES --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 9000; display: none;
            align-items: center; justify-content: center; backdrop-filter: blur(5px);
        }
        .modal-box {
            background: #fff; border: 5px solid #000; padding: 20px;
            text-align: center; width: 90%; max-width: 400px; border-radius: 20px;
            box-shadow: 0 0 30px var(--amarillo-mx);
        }

        /* Texto flotante */
        .float-msg {
            position: absolute; font-family: 'Bangers'; font-size: 1.5rem; 
            pointer-events: none; animation: floatUp 2.5s forwards; z-index: 5000; 
            text-shadow: 2px 2px 0 #000; white-space: nowrap; font-weight: normal;
        }
        @keyframes floatUp { 
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
            10% { transform: translate(-50%, -80%) scale(1.1); opacity: 1; }
            80% { transform: translate(-50%, -100px) scale(1); opacity: 1; }
            100% { transform: translate(-50%, -120px) scale(0.8); opacity: 0; }
        }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="spinner-border text-warning" role="status"></div>
    </div>

    <div id="rotation-warning">
        <i class="fas fa-mobile-alt fa-3x mb-3" style="transform: rotate(90deg);"></i>
        <h3>Por favor, gira tu dispositivo</h3>
        <p>Este juego está optimizado para modo vertical en móviles.</p>
    </div>

    <div id="app-container">
        
        <div id="screen-menu">
            <div class="menu-card animate__animated animate__fadeIn position-relative">
                
                <img src="wrestling_6769709.png" alt="Lucha" class="wrestling-mask">

                <div class="title-container">
                    <img src="ambro ortiz avatar.png" alt="Avatar" class="avatar-img" onclick="showBio()" title="Clic para Biografía">
                    <h1 class="main-title lucha-font">LUCHAS POR LAS<br>FINANZAS DE MÉXICO</h1>
                </div>

                <div class="social-links">
                    <p class="mb-1"><strong>Dr. Ambrosio Ortiz Ramírez</strong></p>
                    <a href="https://www.researchgate.net/profile/A-Ortiz-Ramirez" target="_blank"><i class="fas fa-graduation-cap"></i> ResearchGate</a> | 
                    <a href="https://orcid.org/0000-0002-3698-2873" target="_blank"><i class="fab fa-orcid"></i> ORCID</a>
                </div>
                
                <div style="font-size: 0.6rem; color: #777; margin-bottom: 10px;">
                    <a href="https://www.flaticon.es/iconos-gratis/luchador" title="luchador iconos" target="_blank" style="color: #777; text-decoration: none;">Luchador iconos creados por Freepik - Flaticon</a>
                </div>

                <div id="highscore-display" class="alert alert-warning py-1 small fw-bold mb-2">
                    🏆 Tu Récord: <span id="menu-highscore">0</span>
                </div>

                <p class="h6 mb-2 lucha-font text-muted">elige tu cuadrilátero:</p>

                <div class="d-grid gap-2 mb-2 px-md-4">
                    <button class="btn btn-lucha btn-nivel-1 d-flex justify-content-between px-3 align-items-center" onclick="initLevel(1)">
                        <span class="fw-bold">🪙 TANDA</span> <small>Corto Plazo</small>
                    </button>
                    <button class="btn btn-lucha btn-nivel-2 d-flex justify-content-between px-3 align-items-center" onclick="initLevel(2)">
                        <span class="fw-bold">🚲 BICI</span> <small>Mediano Plazo</small>
                    </button>
                    <button class="btn btn-lucha btn-nivel-3 d-flex justify-content-between px-3 align-items-center" onclick="initLevel(3)">
                        <span class="fw-bold">✈️ VIAJE</span> <small>Largo Plazo</small>
                    </button>
                </div>

                <a href="https://econ-master-8w1z.vercel.app/" target="_blank" class="btn btn-lucha w-100 py-2 text-white fw-bold text-decoration-none d-block mb-2" style="background: var(--morado-mx); border-color: black; display: none;">
                    <span class="me-2">🪅</span> JUGAR PIÑATAS DE LA ECONOMÍA
                </a>

                <button class="btn btn-lucha w-100 py-2 btn-success text-white fw-bold" style="background: var(--verde-mx); border-color: black;" onclick="confirmEconMaster()">
                    <i class="fas fa-gamepad me-2"></i> JUGAR ECONMASTER
                </button>
            </div>
        </div>

        <div id="screen-game">
            <div id="maze-container">
                <div id="maze-wrapper">
                    <div id="maze-grid"></div>
                </div>
            </div>

            <div class="controls-panel">
                <div class="hud-bar">
                    <span id="ui-lives" class="text-danger">❤️❤️❤️</span>
                    <span class="text-success fw-bold" title="Aciertos"><i class="fas fa-check-circle"></i> <span id="ui-good">0</span></span>
                    <span class="text-danger fw-bold" title="Errores"><i class="fas fa-times-circle"></i> <span id="ui-bad">0</span></span>
                    <span id="ui-timer" class="fw-bold text-white"><i class="fas fa-clock"></i> 60</span>
                </div>

                <div class="control-pad">
                    <div></div> 
                    <div class="c-btn" onmousedown="move(0,-1)" ontouchstart="move(0,-1, event)"><i class="fas fa-chevron-up"></i></div>
                    <div></div> 
                    <div class="c-btn" onmousedown="move(-1,0)" ontouchstart="move(-1,0, event)"><i class="fas fa-chevron-left"></i></div>
                    <div class="c-btn" onmousedown="move(0,1)" ontouchstart="move(0,1, event)"><i class="fas fa-chevron-down"></i></div>
                    <div class="c-btn" onmousedown="move(1,0)" ontouchstart="move(1,0, event)"><i class="fas fa-chevron-right"></i></div>
                </div>

                <div class="d-flex gap-3 mt-3">
                    <button class="btn btn-warning rounded-circle border-2 border-dark shadow-sm" style="width:45px; height:45px" onclick="toggleMusic()" id="music-btn"><i class="fas fa-volume-up"></i></button>
                    <button class="btn-salir" onclick="exitToMenu()">SALIR</button>
                </div>
            </div>
        </div>
    </div>

    <div id="modal-bio" class="modal-overlay">
        <div class="modal-box text-start">
            <div class="text-center mb-3">
                <img src="ambro ortiz avatar.png" class="avatar-img mb-2" style="width: 100px; height: 100px;">
                <h3 class="lucha-font" style="color: var(--azul-titulo);">Ambrosio Ortiz Ramírez</h3>
            </div>
            <div class="px-2 small" style="line-height: 1.4;">
                <p><strong>Ambrosio Ortiz Ramírez</strong> es Profesor Investigador en el <strong>IPN</strong> y miembro del <strong>SNI Nivel 1</strong>.</p>
                <p>Especialista en <strong>Econometría Financiera y Riesgos</strong>, combina la investigación académica rigurosa con la divulgación accesible a través de su proyecto <em>"Divulgando las Finanzas"</em>.</p>
            </div>
            <button class="btn btn-lucha w-100 mt-3 btn-success text-white" onclick="showModal(null)">CERRAR</button>
        </div>
    </div>

    <div id="modal-confirm" class="modal-overlay">
        <div class="modal-box">
            <h2 class="lucha-font text-success">¿Ir a EconMaster?</h2>
            <p>Saldrás de este juego para ir a otro sitio educativo.</p>
            <div class="d-flex gap-2">
                <button class="btn btn-secondary w-50" onclick="showModal(null)">Cancelar</button>
                <button class="btn btn-success w-50 fw-bold" onclick="goToEconMasterReal()">¡VAMOS!</button>
            </div>
        </div>
    </div>

    <div id="modal-inst" class="modal-overlay">
        <div class="modal-box">
            <h2 class="lucha-font text-danger">¡EL RETO!</h2>
            <p class="mb-2">Nivel: <strong id="inst-goal" style="color:var(--morado-mx)"></strong></p>
            <div class="alert alert-info py-2 small">
                Recolecta <strong>Activos</strong> y evita los <strong>Pasivos</strong> para llegar al trofeo.
            </div>
            <div class="row text-start small my-3">
                <div class="col-6 text-success fw-bold">✅ BUENO<br><span style="font-weight:normal; font-size:0.8rem">Inversión, Ahorro, Cetes, Seguro.</span></div>
                <div class="col-6 text-danger fw-bold">❌ MALO<br><span style="font-weight:normal; font-size:0.8rem">Inflación, Deuda, Fraudes, Gasto Vampiro.</span></div>
            </div>
            <button class="btn btn-lucha w-100 py-2 fs-4 fw-bold" style="background:var(--verde-mx); color:white;" onclick="startGame()">¡A LUCHAR!</button>
        </div>
    </div>

    <div id="modal-lose" class="modal-overlay">
        <div class="modal-box" style="border-color: red;">
            <div class="display-1 mb-2">🔔</div>
            <h2 class="lucha-font text-danger">¡TE RINDIERON!</h2>
            <p id="lose-msg" class="fw-bold">...</p>
            <div class="alert alert-light border border-dark p-2 small mt-2 text-start">
                <strong>💡 El Experto dice:</strong><br>
                <span id="lose-tip" class="fst-italic">...</span>
            </div>
            <button class="btn btn-lucha btn-dark w-100 mt-2" onclick="exitToMenu()">REINTENTAR</button>
        </div>
    </div>

    <div id="modal-win" class="modal-overlay">
        <div class="modal-box" style="border-color: gold;">
            <div class="display-1 mb-2">🏆</div>
            <h2 class="lucha-font text-success">¡CAMPEÓN!</h2>
            <p id="win-msg" class="fw-bold">...</p>
            <div class="alert alert-success border border-dark p-2 small mt-2 text-start">
                <strong>💡 Consejo de Oro:</strong><br>
                <span id="win-tip" class="fst-italic">...</span>
            </div>
            <button class="btn btn-lucha w-100 mt-2" style="background:var(--amarillo-mx)" onclick="exitToMenu()">GENIAL</button>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // --- PRELOADER ---
        window.onload = function() {
            document.getElementById('preloader').style.opacity = '0';
            setTimeout(() => document.getElementById('preloader').style.display = 'none', 500);
            updateHighScoreDisplay();
        };

        const levels = {
            1: { name: "TANDA (Corto Plazo)", size: 8, badRate: 0.25 },
            2: { name: "BICI (Mediano Plazo)", size: 10, badRate: 0.30 },
            3: { name: "VIAJE MUNDIAL (Largo Plazo)", size: 12, badRate: 0.35 }
        };
        
        // Items actualizados con más términos financieros relevantes
        const items = {
            good: [
                {t:"¡CETES DIRECTO!", i:"📈"}, {t:"¡FONDO EMERGENCIA!", i:"💰"},
                {t:"¡INTERÉS COMPUESTO!", i:"🚀"}, {t:"¡DIVERSIFICACIÓN!", i:"📊"},
                {t:"¡SEGURO GASTOS MÉDICOS!", i:"🛡️"}, {t:"¡APORTACIÓN AFORE!", i:"👵"},
                {t:"¡PRESUPUESTO!", i:"📝"}, {t:"¡CASHBACK!", i:"💸"},
                {t:"¡INGRESOS PASIVOS!", i:"🛌"}, {t:"¡EDUCACIÓN FINANCIERA!", i:"🎓"},
                {t:"¡PAGAR TOTAL TARJETA!", i:"💳"}, {t:"¡DESCUENTO PRONTO PAGO!", i:"🏷️"},
                {t:"¡BONO PRODUCTIVIDAD!", i:"🏆"}, {t:"¡DIVIDENDOS!", i:"💵"}
            ],
            bad: [
                {t:"¡INFLACIÓN!", i:"🎈"}, {t:"¡GASTO HORMIGA!", i:"☕"},
                {t:"¡GASTO VAMPIRO!", i:"🧛"}, {t:"¡ESTAFA PIRAMIDAL!", i:"🔺"},
                {t:"¡INTERESES MORATORIOS!", i:"🤬"}, {t:"¡TARJETAZO!", i:"💳"},
                {t:"¡SIN SEGURO!", i:"🤕"}, {t:"¡DEVALUACIÓN!", i:"📉"},
                {t:"¡COMPRA IMPULSIVA!", i:"🛍️"}, {t:"¡USURA!", i:"🦈"},
                {t:"¡ROBO IDENTIDAD!", i:"🎭"}, {t:"¡CLONACIÓN!", i:"📵"},
                {t:"¡SIN CONTRATO!", i:"🚫"}, {t:"¡MULTA SAT!", i:"👮"}
            ]
        };

        // TIPS MEJORADOS Y AMPLIADOS
        const tips = [
            "La Tanda no le gana a la inflación. ¡Mejor abre tu cuenta en CETES Directo desde $100 pesos!",
            "Evita los 'Gastos Vampiro': Esas suscripciones que pagas mensualmente y nunca usas.",
            "Paga el total de tu tarjeta de crédito (Totalero) para no regalar dinero en intereses.",
            "El Interés Compuesto es tu mejor aliado: reinvierte tus ganancias para crecer exponencialmente.",
            "Diversificar es la clave: 'No pongas todos los huevos en la misma canasta'.",
            "Tu AFORE es vital. Hacer aportaciones voluntarias hoy, te salvará mañana.",
            "El Fondo de Emergencia debe cubrir al menos 3 meses de tus gastos fijos.",
            "La tarjeta de crédito no es dinero extra, es deuda que debes pagar.",
            "Diferencia entre Deseo y Necesidad antes de comprar algo caro.",
            "La inflación hace que tu dinero guardado bajo el colchón valga menos cada año.",
            "Un seguro no es un gasto, es una inversión que protege tu patrimonio ante desgracias.",
            "Invierte a largo plazo en instrumentos regulados para reducir el riesgo."
        ];

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
        sounds.bgm.loop = true; sounds.bgm.volume = 0.5;

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // --- MANEJO DE RÉCORDS ---
        function saveHighScore(score) {
            const currentHigh = localStorage.getItem('lucha_highscore') || 0;
            if (score > currentHigh) {
                localStorage.setItem('lucha_highscore', score);
            }
        }
        function updateHighScoreDisplay() {
            const high = localStorage.getItem('lucha_highscore') || 0;
            document.getElementById('menu-highscore').innerText = high;
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
        
        function confirmEconMaster() { showModal('modal-confirm'); }
        function goToEconMasterReal() { window.location.href = "https://econ-master-8w1z.vercel.app/"; }
        function goToEconMaster() { confirmEconMaster(); } 

        function showBio() { showModal('modal-bio'); }

        function showScreen(id) {
            document.getElementById('screen-menu').classList.remove('d-flex');
            document.getElementById('screen-menu').style.display = 'none';
            document.getElementById('screen-game').classList.remove('d-flex');
            document.getElementById('screen-game').classList.add('d-none');
            
            if(id === 'screen-menu') {
                document.getElementById('screen-menu').style.display = 'flex';
                document.getElementById('screen-menu').classList.add('d-flex');
                updateHighScoreDisplay();
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
            state.lives = 3; 
            state.time = state.lvl === 1 ? 45 : (state.lvl === 2 ? 60 : 80); 
            state.collectedGood = 0; state.collectedBad = 0;
            state.active = true; state.canMove = true;
            updateUI();
            generateGrid(levels[state.lvl].size);
            renderGrid();
            clearInterval(timerInt);
            timerInt = setInterval(() => { state.time--; updateUI(); if(state.time <= 0) gameOver("time"); }, 1000);
            if(musicOn && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            
            window.onkeydown = (e) => {
                if(!state.active) return;
                if(['ArrowUp','ArrowDown','ArrowLeft','ArrowRight'].includes(e.key)) e.preventDefault();
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
                    if(!isWall && Math.random() < 0.35 && !(x===0 && y===0)) {
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
            grid[size-1][size-1].wall = false; 
            if(grid[size-1][size-1].item) grid[size-1][size-1].item = null;
            player = {x:0, y:0};
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
                    
                    // --- JUGADOR CON IMAGEN Y LUZ TENUE (CORREGIDO) ---
                    if(x===player.x && y===player.y) { 
                        // Usamos display:block y dimensiones relativas al padre flex para asegurar visualización
                        cell.innerHTML = '<img src="image_0.png" alt="Luchador" style="display: block; width: 85%; height: 85%; object-fit: contain;">'; 
                        cell.style.zIndex = 10; 
                        cell.classList.add('player-active'); // Clase CSS brillante tenue
                    }
                    
                    if(x===size-1 && y===size-1) cell.innerHTML = '🏆';
                    div.appendChild(cell);
                }
            }
        }

        function move(dx, dy, e) {
            if(e && e.cancelable) e.preventDefault();
            if(!state.active || !state.canMove) return;
            
            if(musicOn && sounds.bgm.paused && audioContextUnlocked) sounds.bgm.play().catch(()=>{});
            
            state.canMove = false; setTimeout(() => state.canMove = true, 100); 
            const size = levels[state.lvl].size; let nx = player.x + dx; let ny = player.y + dy;
            
            if(nx>=0 && nx<size && ny>=0 && ny<size && !grid[ny][nx].wall) {
                player = {x:nx, y:ny};
                const cell = grid[ny][nx];
                const cellIndex = ny * size + nx;
                const targetCell = document.getElementById('maze-grid').children[cellIndex];

                if(cell.item) {
                    floatText(cell.item.t, cell.item.type==='good'?'#00b894':'#d63031', targetCell);
                    if(cell.item.type === 'good') { 
                        playSfx('coin'); state.collectedGood++; 
                    } else { 
                        playSfx('hurt'); state.collectedBad++; state.lives--; updateUI(); 
                        const wrap = document.getElementById('maze-wrapper'); wrap.style.borderColor = "white"; 
                        setTimeout(()=>wrap.style.borderColor = "#E4007C", 100);
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
            document.getElementById('ui-timer').className = state.time < 10 ? "fw-bold text-danger" : "fw-bold text-white";
            let h = ""; for(let i=0;i<state.lives;i++) h+="❤️";
            document.getElementById('ui-lives').innerText = h;
            
            document.getElementById('ui-good').innerText = state.collectedGood;
            document.getElementById('ui-bad').innerText = state.collectedBad;
        }

        function gameOver(reason) {
            state.active = false; playSfx('lose');
            saveHighScore(state.collectedGood);
            const tip = tips[Math.floor(Math.random() * tips.length)];
            document.getElementById('lose-msg').innerText = reason === 'time' ? "¡SE ACABÓ EL TIEMPO!" : "¡TE QUEDASTE SIN VIDA!";
            document.getElementById('lose-tip').innerText = tip;
            showModal('modal-lose');
        }

        function gameWin() {
            state.active = false; playSfx('win');
            saveHighScore(state.collectedGood);
            const tip = tips[Math.floor(Math.random() * tips.length)];
            document.getElementById('win-msg').innerText = "¡GANASTE EN " + levels[state.lvl].name + "!";
            document.getElementById('win-tip').innerText = tip;
            showModal('modal-win');
        }

        function floatText(txt, col, target) {
            const el = document.createElement('div');
            el.innerText = txt;
            el.className = 'float-msg';
            el.style.color = col;
            if(target) {
                const rect = target.getBoundingClientRect();
                el.style.left = (rect.left + rect.width / 2) + 'px';
                el.style.top = (rect.top) + 'px';
            } else {
                el.style.left = '50%'; el.style.top = '50%';
            }
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 2500);
        }
    </script>
</body>
</html>
