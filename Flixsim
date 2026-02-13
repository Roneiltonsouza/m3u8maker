<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FLIXSIM | IPTV & Cinema</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
    <style>
        :root {
            --preto: #0e0e0e;
            --branco: #ffffff;
            --vermelho: #ff0000;
            --laranja: #ff4500;
            --cinza: #2a2a2a;
        }

        body {
            background-color: var(--preto);
            color: var(--branco);
            font-family: 'Arial Black', sans-serif;
            margin: 0;
            padding-bottom: 50px;
        }

        header { padding: 40px 20px; text-align: center; position: relative; }

        .flixsim-logo {
            font-size: 3.5rem;
            font-weight: 900;
            text-transform: uppercase;
            background: linear-gradient(to right, var(--vermelho), var(--laranja));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0px 4px 10px rgba(255, 0, 0, 0.5));
            display: inline-block;
            font-style: italic;
        }

        .container { padding: 0 20px; font-family: 'Arial', sans-serif; }

        /* Abas Estilizadas */
        .tabs { display: flex; justify-content: center; gap: 8px; margin-bottom: 20px; flex-wrap: wrap; }
        .tab-btn { 
            background: #1a1a1a; border: 1px solid #333; color: white; 
            padding: 12px 15px; cursor: pointer; border-radius: 8px;
            transition: 0.3s; font-weight: bold; font-size: 13px;
        }
        .tab-btn.active { background: var(--vermelho); border-color: var(--vermelho); box-shadow: 0 0 15px rgba(255,0,0,0.4); }

        .content { display: none; padding: 20px; background: #1a1a1a; border-radius: 15px; animation: fadeIn 0.4s; }
        .content.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Configurações IPTV */
        .iptv-form { background: var(--cinza); padding: 20px; border-radius: 10px; margin-bottom: 20px; }
        .iptv-form input { width: 100%; padding: 15px; margin-bottom: 10px; border-radius: 5px; border: none; background: #000; color: #fff; }
        .iptv-form button { width: 100%; padding: 15px; background: #25d366; color: white; border: none; border-radius: 5px; font-weight: bold; cursor: pointer; }

        /* Player de Vídeo Estilo Netflix */
        #videoContainer { width: 100%; max-width: 800px; margin: 20px auto; background: #000; border-radius: 10px; overflow: hidden; border: 2px solid var(--vermelho); display: none; }
        video { width: 100%; display: block; }

        /* Grid de Postagem */
        .post-form { background: var(--cinza); padding: 20px; border-radius: 10px; margin-bottom: 20px; }
        .post-form input, .post-form button { width: 100%; padding: 12px; margin: 8px 0; border-radius: 5px; border: none; }
        .post-form button { background: var(--vermelho); color: white; font-weight: bold; }
        
        .feed { display: grid; grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); gap: 15px; }
        .movie-card { background: #000; border-radius: 8px; overflow: hidden; border: 1px solid #333; }
        .movie-card img { width: 100%; height: 200px; object-fit: cover; }
        .movie-card h4 { font-size: 0.8em; padding: 8px; text-align: center; margin: 0; }
    </style>
</head>
<body>

    <header>
        <h1 class="flixsim-logo">Flixsim</h1>
    </header>

    <div class="container">
        <div class="tabs">
            <button class="tab-btn active" onclick="openTab(event, 'comunidade')"><i class="fas fa-users"></i> Feed</button>
            <button class="tab-btn" onclick="openTab(event, 'iptv_tab')"><i class="fas fa-tv"></i> Configurar IPTV</button>
            <button class="tab-btn" onclick="openTab(event, 'suporte')"><i class="fab fa-whatsapp"></i> Suporte</button>
        </div>

        <div id="iptv_tab" class="content">
            <div class="iptv-form">
                <h3><i class="fas fa-signal"></i> Adicionar Lista/Filme</h3>
                <p style="font-size: 12px; color: #bbb;">Cole abaixo a URL do canal ou filme (m3u8, mp4)</p>
                <input type="text" id="iptvUrl" placeholder="Ex: https://servidor.com/filme.m3u8">
                <button onclick="playIPTV()">CARREGAR NO PLAYER</button>
            </div>

            <div id="videoContainer">
                <video id="videoPlayer" controls></video>
                <div style="padding: 10px; font-size: 12px; text-align: center; background: #111;">
                    Modo Ultra-Smooth Ativado (Software HLS)
                </div>
            </div>
        </div>

        <div id="comunidade" class="content active">
            <div class="post-form">
                <input type="text" id="movieTitle" placeholder="Título do Filme">
                <input type="file" id="movieImage" accept="image/*">
                <button onclick="addPost()">PUBLICAR NA GALERIA</button>
            </div>
            <div id="movieFeed" class="feed"></div>
        </div>

        <div id="suporte" class="content">
            <div style="text-align: center;">
                <h2>Precisa de ajuda?</h2>
                <a href="https://whatz.app/rdg" style="background:#25d366; color:white; padding:15px 30px; text-decoration:none; border-radius:30px; display:inline-block; font-weight:bold;">
                    CHAMAR NO WHATSAPP
                </a>
            </div>
        </div>
    </div>

    <script>
        // Função para alternar abas
        function openTab(evt, tabName) {
            var i, content, tabbtn;
            content = document.getElementsByClassName("content");
            for (i = 0; i < content.length; i++) content[i].style.display = "none";
            tabbtn = document.getElementsByClassName("tab-btn");
            for (i = 0; i < tabbtn.length; i++) tabbtn[i].classList.remove("active");
            document.getElementById(tabName).style.display = "block";
            evt.currentTarget.classList.add("active");
        }

        // Software de Reprodução (HLS) para não travar
        function playIPTV() {
            const url = document.getElementById('iptvUrl').value;
            const video = document.getElementById('videoPlayer');
            const container = document.getElementById('videoContainer');

            if (!url) return alert("Insira uma URL válida!");
            
            container.style.display = "block";

            if (Hls.isSupported()) {
                const hls = new Hls({
                    capLevelToPlayerSize: true,
                    progressive: true,
                });
                hls.loadSource(url);
                hls.attachMedia(video);
                hls.on(Hls.Events.MANIFEST_PARSED, function() {
                    video.play();
                });
            } 
            else if (video.canPlayType('application/vnd.apple.mpegurl')) {
                video.src = url;
                video.addEventListener('loadedmetadata', function() {
                    video.play();
                });
            }
        }

        // Postagem na Galeria
        function addPost() {
            const title = document.getElementById('movieTitle').value;
            const imageInput = document.getElementById('movieImage');
            const feed = document.getElementById('movieFeed');

            if (!title || imageInput.files.length === 0) return alert("Preencha tudo!");

            const reader = new FileReader();
            reader.onload = function(e) {
                const card = document.createElement('div');
                card.className = 'movie-card';
                card.innerHTML = `<img src="${e.target.result}"><h4>${title}</h4>`;
                feed.prepend(card);
            };
            reader.readAsDataURL(imageInput.files[0]);
        }
    </script>
</body>
</html>
