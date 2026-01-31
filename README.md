<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Espace Manon ❤️</title>
    <style>
        :root {
            --accent: #ff4785;
            --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #ff4785 100%);
            --glass: rgba(255, 255, 255, 0.95);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }

        body { 
            background: var(--bg-gradient); 
            height: 100vh; 
            display: flex; 
            align-items: center; 
            justify-content: center;
            overflow: hidden;
        }

        /* --- ÉCRAN DE VERROUILLAGE --- */
        #lock-screen {
            text-align: center;
            z-index: 100;
            transition: 0.6s all ease-in-out;
        }

        .login-card {
            background: var(--glass);
            padding: 40px 30px;
            border-radius: 30px;
            backdrop-filter: blur(15px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            width: 320px;
        }

        input {
            width: 100%;
            padding: 15px;
            border: 2px solid #eee;
            border-radius: 15px;
            outline: none;
            text-align: center;
            font-size: 1rem;
            margin-bottom: 15px;
        }

        .btn-confirm {
            background: var(--accent);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
        }

        /* --- BUREAU --- */
        #desktop {
            display: none;
            width: 100%;
            height: 100%;
            position: relative;
            flex-direction: column;
            animation: zoomIn 0.8s ease forwards;
        }

        @keyframes zoomIn { from { opacity: 0; transform: scale(1.1); } to { opacity: 1; transform: scale(1); } }

        .desktop-icons { padding: 30px; display: flex; flex-direction: column; gap: 25px; }

        .app-icon {
            width: 75px;
            text-align: center;
            cursor: pointer;
            color: white;
            font-size: 0.85rem;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }

        .icon-box {
            width: 65px; height: 65px;
            background: white;
            border-radius: 20px;
            display: flex; align-items: center; justify-content: center;
            font-size: 35px; margin: 0 auto 8px;
            box-shadow: 0 8px 15px rgba(0,0,0,0.1);
        }

        /* --- FENÊTRE --- */
        .window {
            position: absolute;
            top: 45%; left: 50%;
            transform: translate(-50%, -50%);
            width: 95%; max-width: 600px;
            height: 80vh;
            background: white;
            border-radius: 25px;
            display: none;
            flex-direction: column;
            box-shadow: 0 30px 60px rgba(0,0,0,0.4);
            overflow: hidden;
            z-index: 50;
        }

        .window-header {
            background: #f8f9fa;
            padding: 10px 20px;
            display: flex; align-items: flex-end;
            border-bottom: 1px solid #eee;
        }

        .tabs { display: flex; gap: 10px; }
        .tab { 
            padding: 10px 20px; 
            background: #e9ecef; 
            border-radius: 12px 12px 0 0; 
            font-size: 0.9rem; 
            cursor: pointer; 
            color: #777;
        }
        .tab.active { background: white; color: var(--accent); font-weight: bold; }

        .window-body { padding: 30px; flex: 1; overflow-y: auto; color: #333; display: none; }
        .window-body.active { display: block; }

        .close-circle {
            width: 15px; height: 15px; background: #ff5f56; border-radius: 50%;
            position: absolute; right: 20px; top: 15px; cursor: pointer;
        }

        /* --- STYLE LETTRE LONGUE --- */
        .lettre-container {
            font-family: 'Georgia', serif;
            line-height: 1.8;
            color: #444;
            max-width: 500px;
            margin: 0 auto;
        }

        .lettre-titre {
            font-size: 1.8rem;
            color: var(--accent);
            text-align: center;
            margin-bottom: 30px;
        }

        .lettre-section {
            margin-bottom: 25px;
        }

        .lettre-coeur {
            text-align: center;
            font-size: 2rem;
            margin: 40px 0;
            color: var(--accent);
        }

        /* --- INFOS STYLE --- */
        .info-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            background: #fdf2f5;
            padding: 20px;
            border-radius: 15px;
        }
        .info-label { font-weight: bold; color: var(--accent); display: block; font-size: 0.8rem; text-transform: uppercase; }
        .info-val { font-size: 1rem; color: #333; }

        /* BARRE DES TÂCHES */
        .taskbar {
            position: absolute; bottom: 20px; align-self: center;
            height: 65px; background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(20px); border-radius: 22px;
            display: flex; align-items: center; padding: 0 25px; gap: 25px;
            border: 1px solid rgba(255,255,255,0.3);
        }

        .task-item { font-size: 30px; cursor: pointer; }

    </style>
</head>
<body>

    <div id="lock-screen">
        <div class="login-card">
            <h2 style="color: var(--accent);">Coucou Manon ❤️</h2>
            <p style="margin-bottom: 20px; color: #666;">Code requis : Mon coeur</p>
            <input type="password" id="passInput" placeholder="Tape ici...">
            <button class="btn-confirm" onclick="checkPassword()">Accéder à mon univers</button>
            <p id="error" style="color: #ff5f56; font-size: 0.8rem; margin-top: 15px; display: none;">Oups, ce n'est pas le bon code...</p>
        </div>
    </div>

    <div id="desktop">
        <div class="desktop-icons">
            <div class="app-icon" onclick="openWindow('tab-lettre')">
                <div class="icon-box">✉️</div>
                <span>Ma Lettre</span>
            </div>
            <div class="app-icon" onclick="openWindow('tab-info')">
                <div class="icon-box">🤵</div>
                <span>Alexandre</span>
            </div>
        </div>

        <div id="mainWindow" class="window">
            <div class="close-circle" onclick="closeWindow()"></div>
            <div class="window-header">
                <div class="tabs">
                    <div id="tab-btn-lettre" class="tab active" onclick="switchTab('tab-lettre')">Lettre ❤️</div>
                    <div id="tab-btn-info" class="tab" onclick="switchTab('tab-info')">Fiche Info</div>
                </div>
            </div>
            
            <div id="tab-lettre" class="window-body active">
                <div class="lettre-container">
                    <h1 class="lettre-titre">Ma Chère Manon,</h1>
                    
                    <div class="lettre-section">
                        <p>Je voulais prendre le temps de t'écrire quelque chose qui reste, un petit coin numérique qui t'appartient autant qu'à moi. Ce code, c'est un peu comme nous : des heures de travail, de la patience, mais surtout beaucoup de passion.</p>
                    </div>

                    <div class="lettre-section">
                        <p>Depuis que tu fais partie de mon quotidien, chaque petite chose a pris une saveur différente. Je ne savais pas qu'il était possible de s'attacher autant à quelqu'un, de vouloir partager chaque pensée, chaque rire et chaque projet. Tu es devenue ma priorité, celle qui occupe mes pensées dès que je me réveille et la dernière à qui je pense avant de m'endormir.</p>
                    </div>

                    <div class="lettre-section">
                        <p>J'aime ta façon d'être, ta présence qui me rassure et cette étincelle que tu as. Avec toi, j'ai l'impression de pouvoir être moi-même sans filtre, sans peur d'être jugé. Tu es ma force quand je doute, et ma plus belle récompense quand tout va bien.</p>
                    </div>

                    <div class="lettre-section">
                        <p>Je sais que la vie peut parfois être compliquée, mais je veux que tu puisses toujours ouvrir ce petit simulateur et te rappeler que, quelque part à Maignelay-Montigny, il y a un garçon qui pense à toi plus que tout. Un garçon qui est fier de dire que tu es sa Manon.</p>
                    </div>

                    <div class="lettre-section">
                        <p>Je te promets d'être là pour tes moments de joie comme pour tes moments de peine. Je veux apprendre à te connaître encore davantage, découvrir chacun de tes rêves et t'aider à les réaliser. Mon cœur t'est ouvert, tout comme ce programme l'a été pour toi aujourd'hui.</p>
                    </div>

                    <p>Merci d'être qui tu es, merci de m'avoir choisi. Je t'aime d'un amour sincère et profond.</p>

                    <div class="lettre-coeur">❤️</div>
                    
                    <p style="text-align: right; font-weight: bold; font-style: italic; color: var(--accent);">Ton Alexandre, pour toujours.</p>
                    <div style="height: 50px;"></div> </div>
            </div>

            <div id="tab-info" class="window-body">
                <h2 style="margin-bottom: 20px; color: #333;">À propos de moi</h2>
                <div class="info-grid">
                    <div class="info-item"><span class="info-label">Prénom</span><span class="info-val">Alexandre</span></div>
                    <div class="info-item"><span class="info-label">Nom</span><span class="info-val">Draux</span></div>
                    <div class="info-item"><span class="info-label">Âge</span><span class="info-val">18 ans</span></div>
                    <div class="info-item"><span class="info-label">Taille</span><span class="info-val">1m81</span></div>
                    <div class="info-item"><span class="info-label">Nationalité</span><span class="info-val">Français</span></div>
                    <div class="info-item"><span class="info-label">Origines</span><span class="info-val">Italiens/Français</span></div>
                </div>
                
                <div style="margin-top: 20px; background: #fff; padding: 15px; border-radius: 15px; border: 1px dashed var(--accent);">
                    <span class="info-label">Ma Ville & Pays Natal</span>
                    <p class="info-val">Maignelay-Montigny (Né à Creil)</p>
                    <span class="info-label" style="margin-top: 10px;">Adresse précise</span>
                    <p class="info-val">1 rue des tieule, 60420</p>
                </div>

                <div style="margin-top: 20px;">
                    <h3 style="color: #555; font-size: 1rem; margin-bottom: 10px;">Mes Passions & Vie</h3>
                    <p>🎹 <strong>Piano :</strong> Ma part de sensibilité.</p>
                    <p>🎨 <strong>Dessin :</strong> Mon imagination sur papier.</p>
                    <p>💻 <strong>Codage :</strong> Ce que j'ai utilisé pour créer cet espace pour toi.</p>
                    <p>🐱 <strong>Mon Chat :</strong> Mon petit compagnon de tous les jours.</p>
                </div>
            </div>
        </div>

        <div class="taskbar">
            <div class="task-item" onclick="openWindow('tab-lettre')">💖</div>
            <div class="task-item" onclick="openWindow('tab-info')">📋</div>
            <div class="task-item" onclick="location.reload()">🔒</div>
        </div>
    </div>

    <script>
        function checkPassword() {
            const pass = document.getElementById('passInput').value.toLowerCase();
            if (pass === 'mon coeur' || pass === 'mon cœur') {
                document.getElementById('lock-screen').style.display = 'none';
                document.getElementById('desktop').style.display = 'flex';
            } else {
                document.getElementById('error').style.display = 'block';
            }
        }

        function openWindow(tabId) {
            document.getElementById('mainWindow').style.display = 'flex';
            switchTab(tabId);
        }

        function closeWindow() { document.getElementById('mainWindow').style.display = 'none'; }

        function switchTab(tabId) {
            document.querySelectorAll('.window-body').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            if(tabId === 'tab-lettre') document.getElementById('tab-btn-lettre').classList.add('active');
            if(tabId === 'tab-info') document.getElementById('tab-btn-info').classList.add('active');
        }

        document.getElementById('passInput').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') checkPassword();
        });
    </script>
</body>
</html>
