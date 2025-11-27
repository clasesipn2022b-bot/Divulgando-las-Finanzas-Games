<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Lucha Financiera Kids</title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">     
    <link href="https://fonts.googleapis.com/css2?family=Bangers&family=Roboto+Condensed:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- PALETA DE COLORES --- */
        :root {
            --azul-titulo: #0d47a1; 
            --rosa-mexicano: #E4007C;
            --amarillo-mx: #FFD700;
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
            letter-spacing: 1.5px;
            text-transform: uppercase;
        }

        /* --- WRAPPER GENERAL --- */
        #app-container {
            width: 100%; height: 100%;
            display: flex; justify-content: center; align-items: center;
            position: relative;
        }

        /* --- PANTALLA MENÚ --- */
        #screen-menu {
            width: 100%; height: 100%;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            overflow-y: auto; padding: 10px;
        }

        .menu-card {
            background: #fff;
            border: 5px solid #000;
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            max-width: 650px; width: 100%;
            box-shadow: 10px 10px 0 var(--morado-mx);
            margin: auto; position: relative;
        }

        /* Header con Avatar y Título */
        .title-container {
            display: flex; align-items: center; justify-content: center;
            gap: 15px; margin-bottom: 15px; flex-wrap: wrap;
            position: relative; z-index: 2;
        }

        .avatar-img {
            width: 70px; height: 70px;
            border: 3px solid #000; border-radius: 50%;
            box-shadow: 3px 3px 0 var(--amarillo-mx);
            background: white; object-fit: cover;
        }

        .wrestling-mask {
            width: 50px; height: auto;
            position: absolute; top: 10px; right: 10px;
            filter: drop-shadow(2px 2px 0 #000); z-index: 1;
        }

        .main-title {
            color: var(--azul-titulo);
            text-shadow: 2px 2px 0 #fff, 4px 4px 0 #000;
            font-size: clamp(1.8rem, 5vw, 3rem);
            margin: 0; line-height: 1; text-align: left;
        }

        /* Botones */
        .btn-lucha {
            font-family: 'Bangers', cursive;
            font-size: 1.2rem;
            border: 2px solid #000; border-radius: 12px;
            box-shadow: 3px 3px 0 #000;
            transition: transform 0.1s;
            background: white; color: black;
            padding: 10px 15px; cursor: pointer;
            text-decoration: none; display: inline-block;
        }
        .btn-lucha:active { transform: translate(2px, 2px); box-shadow: 1px 1px 0 #000; }

        .btn-bio { background: #fff; color: var(--azul-titulo); margin-bottom: 10px; width: 100%; }
        .btn-pinata { background: var(--morado-mx); color: white; margin-bottom: 20px; width: 100%; }
        .btn-pinata:hover { color: #fff; background: #4a148c; }
        
        .level-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 10px; margin-top: 10px;
        }
        .btn-nivel-1 { background: #81ecec; }
        .btn-nivel-2 { background: var(--amarillo-mx); }
        .btn-nivel-3 { background: var(--rosa-mexicano); color: white; }

        /* --- MODALES --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 9000; display: none;
            align-items: center; justify-content: center; backdrop-filter: blur(5px);
        }
        .modal-box {
            background: #fff; border: 5px solid #000; padding: 25px;
            text-align: center; width: 90%; max-width: 500px; border-radius: 20px;
            box-shadow: 0 0 30px var(--amarillo-mx); position: relative;
        }
        .modal-bio-text {
            font-size: 1rem; line-height: 1.5; text-align: justify;
            margin: 20px 0; border-left: 4px solid var(--azul-titulo);
            padding-left: 15px; background: #f8f9fa; padding: 10px;
        }
        .btn-salir {
            background: #d63031; color: white; border: 2px solid #000;
            padding: 5px 20px; border-radius: 20px; font-weight: bold; font-size: 1rem;
            box-shadow: 0 3px 0 #000;
        }

        /* Créditos pequeños */
        .footer-credits {
            font-size: 0.75rem; margin-top: 20px; color: #666;
            border-top: 1px dashed #ccc; padding-top: 10px;
        }
        .footer-credits a { color: var(--azul-titulo); text-decoration: none; font-weight: bold; }
        
    </style>
</head>
<body>

    <div id="app-container">
        
        <div id="screen-menu">
            <div class="menu-card">
                <img src="https://cdn-icons-png.flaticon.com/512/2319/2319856.png" class="wrestling-mask" alt="Máscara">

                <div class="title-container">
                    <img src="https://img.freepik.com/foto-gratis/renderizacion-3d-avatar-llamada-zoom_23-2149556776.jpg" class="avatar-img" alt="Avatar">
                    <div>
                        <h1 class="main-title">LUCHA<br>FINANCIERA</h1>
                        <span class="badge bg-danger lucha-font" style="font-size: 0.8rem;">Kids Edition</span>
                    </div>
                </div>

                <button class="btn-lucha btn-bio" onclick="toggleModal('modal-bio', true)">
                    <i class="fas fa-user-graduate"></i> Conoce al Autor
                </button>

                <a href="https://econ-master-8w1z.vercel.app/" class="btn-lucha btn-pinata">
                    <i class="fas fa-star"></i> Jugar Piñatas de la Economía
                </a>

                <h3 class="lucha-font text-start mt-2">Selecciona Arena:</h3>
                <div class="level-grid">
                    <button class="btn-lucha btn-nivel-1">🧸 Juguete</button>
                    <button class="btn-lucha btn-nivel-2">🚲 Bici</button>
                    <button class="btn-lucha btn-nivel-3">✈️ Mundial</button>
                </div>

                <div class="footer-credits">
                    Ambrosio Ortiz Ramírez &copy; 2025<br>
                    Recurso gráfico: <a href="https://www.freepik.es/icono/lucha_6769709" target="_blank">Icono de Freepik</a>
                </div>
            </div>
        </div>

        <div id="modal-bio" class="modal-overlay">
            <div class="modal-box">
                <h2 class="lucha-font" style="color: var(--azul-titulo);">👨‍🏫 El Profesor</h2>
                
                <div class="modal-bio-text">
                    Ambrosio Ortiz Ramírez es Profesor Investigador en el IPN y miembro del SNI Nivel 1. Especialista en Econometría Financiera y Riesgos, combina la investigación académica rigurosa con la divulgación accesible a través de su proyecto "Divulgando las Finanzas", enfocándose en modelos estocásticos y derivados.
                </div>

                <div class="d-flex justify-content-center gap-2">
                    <a href="https://www.researchgate.net/profile/A-Ortiz-Ramirez" target="_blank" class="btn-lucha" style="background:#00cc88; font-size:0.9rem">
                        <i class="fas fa-book"></i> ResearchGate
                    </a>
                    <button class="btn-lucha btn-salir" onclick="toggleModal('modal-bio', false)">CERRAR</button>
                </div>
            </div>
        </div>

    </div>

    <script>
        function toggleModal(modalId, show) {
            const modal = document.getElementById(modalId);
            if (modal) {
                modal.style.display = show ? 'flex' : 'none';
            }
        }
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
