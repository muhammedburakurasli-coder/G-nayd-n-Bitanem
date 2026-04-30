<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Bir Sürprizim Var</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background-color: #fdfbf7;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            touch-action: manipulation;
        }

        #giris-ekrani {
            text-align: center;
            z-index: 100;
        }

        .baslat-btn {
            padding: 15px 30px;
            font-size: 20px;
            background-color: #ff69b4;
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 105, 180, 0.4);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        #oyun-alani {
            display: none;
            flex-direction: column;
            align-items: center;
        }

        #mesaj {
            font-size: 26px;
            color: #5d4037;
            margin-bottom: 40px;
            height: 35px;
            font-weight: bold;
            text-align: center;
        }

        .papatya-konteynir {
            position: relative;
            width: 250px;
            height: 250px;
        }

        .orta-kisim {
            position: absolute;
            width: 70px;
            height: 70px;
            background: radial-gradient(circle, #ffd700 0%, #fbc02d 100%);
            border-radius: 50%;
            top: 90px;
            left: 90px;
            z-index: 10;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: transform 0.3s;
        }

        .yaprak {
            position: absolute;
            width: 50px;
            height: 110px;
            background-color: #ffffff;
            border-radius: 50%;
            left: 100px;
            top: 10px;
            transform-origin: bottom center;
            cursor: pointer;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid #f0f0f0;
        }

        .y1 { transform: rotate(0deg); }
        .y2 { transform: rotate(72deg); }
        .y3 { transform: rotate(144deg); }
        .y4 { transform: rotate(216deg); }
        .y5 { transform: rotate(288deg); }

        .gizle {
            opacity: 0;
            transform: translateY(-150px) rotate(90deg) scale(0.5);
            pointer-events: none;
        }

        #final {
            display: none;
            font-size: 24px;
            color: #d81b60;
            text-align: center;
            padding: 20px;
            line-height: 1.5;
            animation: popIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body>

    <div id="giris-ekrani">
        <h2 style="color: #5d4037;">Senin için küçük bir sürprizim var...</h2>
        <button class="baslat-btn" onclick="baslat()">Sürprizi Gör ✨</button>
    </div>

    <div id="oyun-alani">
        <div id="mesaj">Papatyaya tıkla...</div>
        <div class="papatya-konteynir">
            <div class="orta-kisim" id="gobek"></div>
            <div class="yaprak y1" onclick="kopar(this)"></div>
            <div class="yaprak y2" onclick="kopar(this)"></div>
            <div class="yaprak y3" onclick="kopar(this)"></div>
            <div class="yaprak y4" onclick="kopar(this)"></div>
            <div class="yaprak y5" onclick="kopar(this)"></div>
        </div>
        <div id="final">
            🌸 <br>
            <strong>Güne başlamak için en güzel sebebimmm <br> Günaydınnnn</strong>
        </div>
    </div>

    <!-- YouTube üzerinden müzik (gizli iframe) -->
    <div id="player" style="display:none"></div>

    <script>
        var player;
        // YouTube IFrame API'sini yükle
        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

        function onYouTubeIframeAPIReady() {
            player = new YT.Player('player', {
                height: '0',
                width: '0',
                videoId: 'gvcr98QJuFU',
                playerVars: {
                    'start': 51, // 51. saniyeden başlat (Öyle de güzeldi gözleri...)
                    'autoplay': 0,
                    'controls': 0
                }
            });
        }

        function baslat() {
            document.getElementById('giris-ekrani').style.display = 'none';
            document.getElementById('oyun-alani').style.display = 'flex';
            if (player && player.playVideo) {
                player.playVideo();
            }
        }

        let sira = 0;
        const mesajlar = ["Seviyor...", "Sevmiyor...", "Seviyor...", "Sevmiyor...", "Seviyor!"];
        const mesajElement = document.getElementById('mesaj');
        const gobek = document.getElementById('gobek');

        function kopar(element) {
            element.classList.add('gizle');
            mesajElement.innerText = mesajlar[sira];
            sira++;

            if (sira === 5) {
                gobek.style.cursor = 'pointer';
                gobek.onclick = function() {
                    document.querySelector('.papatya-konteynir').style.display = 'none';
                    mesajElement.style.display = 'none';
                    document.getElementById('final').style.display = 'block';
                    document.body.style.backgroundColor = "#fff0f5";
                };
            }
        }
    </script>
</body>
</html>