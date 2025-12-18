<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chargement...</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1d35 50%, #0f1729 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            text-align: center;
            width: 90%;
            max-width: 600px;
        }

        .logo-section {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            margin-bottom: 50px;
        }

        .logo {
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .logo img {
            width: 100%;
            height: 100%;
            object-fit: contain;
            filter: brightness(1.1);
        }
        
        .logo img[alt]::before {
            content: '';
            display: block;
        }

        .server-name {
            font-size: 32px;
            font-weight: 700;
            color: white;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }

        .server-subtitle {
            font-size: 14px;
            color: rgba(255, 255, 255, 0.8);
            margin-top: 5px;
        }

        .progress-container {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50px;
            height: 12px;
            overflow: hidden;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #4facfe 0%, #00f2fe 100%);
            border-radius: 50px;
            width: 0%;
            transition: width 0.3s ease;
            box-shadow: 0 0 20px rgba(79, 172, 254, 0.6);
        }

        .loading-info {
            margin-top: 30px;
            color: white;
        }

        .loading-text {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .loading-details {
            font-size: 14px;
            color: rgba(255, 255, 255, 0.8);
            margin-top: 5px;
        }

        .percentage {
            position: absolute;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 14px;
            font-weight: 600;
            color: white;
        }

        .progress-wrapper {
            position: relative;
            margin-bottom: 20px;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .loading-text::after {
            content: '...';
            animation: pulse 1.5s infinite;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="logo-section">
            <div class="logo">
                <img src="https://i.imgur.com/1K2VOcg.png" alt="ALTÉA Logo">
            </div>
            <div>
                <div class="server-name">ALTÉA</div>
                <div class="server-subtitle">RolePlay • FR</div>
            </div>
        </div>

        <div class="progress-wrapper">
            <div class="progress-container">
                <div class="progress-bar" id="progressBar"></div>
            </div>
            <div class="percentage" id="percentage">0%</div>
        </div>

        <div class="loading-info">
            <div class="loading-text" id="loadingText">Chargement en cours</div>
            <div class="loading-details" id="loadingDetails">Initialisation...</div>
        </div>
    </div>

    <script>
        let progress = 0;
        const progressBar = document.getElementById('progressBar');
        const percentage = document.getElementById('percentage');
        const loadingText = document.getElementById('loadingText');
        const loadingDetails = document.getElementById('loadingDetails');

        const loadingStages = [
            { text: 'Chargement en cours', detail: 'Initialisation...', min: 0, max: 15 },
            { text: 'Connexion au serveur', detail: 'Établissement de la connexion...', min: 15, max: 30 },
            { text: 'Téléchargement des ressources', detail: 'Récupération des fichiers...', min: 30, max: 60 },
            { text: 'Chargement de la carte', detail: 'Génération du monde...', min: 60, max: 80 },
            { text: 'Finalisation', detail: 'Presque prêt...', min: 80, max: 100 }
        ];

        function updateProgress() {
            if (progress < 100) {
                progress += Math.random() * 2;
                if (progress > 100) progress = 100;

                progressBar.style.width = progress + '%';
                percentage.textContent = Math.floor(progress) + '%';

                // Mise à jour du texte de chargement
                for (let stage of loadingStages) {
                    if (progress >= stage.min && progress < stage.max) {
                        loadingText.textContent = stage.text;
                        loadingDetails.textContent = stage.detail;
                        break;
                    }
                }

                setTimeout(updateProgress, 100);
            } else {
                loadingText.textContent = 'Chargement terminé';
                loadingDetails.textContent = 'Bienvenue sur le serveur !';
            }
        }

        updateProgress();
    </script>
</body>
</html>
