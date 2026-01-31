<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Espace Privé - Manon ❤️</title>
    <style>
        :root {
            --accent: #ff4785;
            --info-blue: #4facfe;
            --glass: rgba(255, 255, 255, 0.95);
            --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #ff4785 100%);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif; }

        body, html { height: 100%; width: 100%; background: var(--bg-gradient); overflow: hidden; display: flex; align-items: center; justify-content: center; }

        /* --- ÉCRAN DE VERROUILLAGE --- */
        #lock-screen { position: absolute; width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; z-index: 100; background: var(--bg-gradient); transition: 0.6s ease-in-out; }
        .login-card { background: var(--glass); padding: 35px 25px; border-radius: 30px; box-shadow: 0 15px 35px rgba(0,0,0,0.2); width: 85%; max-width: 320px; text-align: center; }
        input { width: 100%; padding: 15px; border: 2px solid #eee; border-radius: 15px; outline: none; text-align: center; font-size: 16px; margin-bottom: 15px; transition: 0.3s; }
        input:focus { border-color: var(--accent); }
        .btn-confirm { background: var(--accent); color: white; border: none; padding: 14px; border-radius: 50px; font-weight: bold; cursor: pointer; width: 100%; font-size: 1rem; box-shadow: 0 5px 15px rgba(255, 71, 133, 0.3); }

        /* --- BUREAU --- */
        #desktop { display: none; width: 100%; height: 100%; position: relative; flex-direction: column; animation: fadeIn 0.8s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .desktop-icons { padding: 25px; display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
        .app-icon { text-align: center; color: white; font-size: 0.7rem; font-weight: 600; text-shadow: 0 2px 4px rgba(0,0,0,0.3); }
        .icon-box { width: 65px; height: 65px; background: white; border-radius: 20px; display: flex; align-items: center; justify-content: center; font-size: 32px; margin: 0 auto 8px; box-shadow: 0 8px 20px rgba(0,0,0,0.15); transition: 0.2s; }
        .icon-box:active { transform: scale(0.9); }

        /* --- FENÊTRE --- */
        .window { position: absolute; top: 5%; left: 5%; width: 90%; height: 85%; background: #f0f2f5; border-radius: 25px; display: none; flex-direction: column; box-shadow: 0 25px 60px rgba(0,0,0,0.4); z-index: 50; overflow: hidden; animation: slideUp 0.4s cubic-bezier(0.18, 0.89, 0.32, 1.28); }
        @keyframes slideUp { from { transform: translateY(50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        .window-header { background: white; padding: 15px; display: flex; align-items: center; border-bottom: 1px solid #ddd; }
        .tabs { display: flex; gap: 10px; }
        .tab { padding: 8px 16px; background: #eee; border-radius: 12px; font-size: 0.85rem; color: #666; font-weight: 600; transition: 0.3s; }
        .tab.active { background: var(--accent); color: white; }
        .close-btn { position: absolute; right: 15px; font-size: 24px; color: #999; cursor: pointer; }

        .window-body { padding: 20px; flex: 1; overflow-y: auto; -webkit-overflow-scrolling: touch; display: none; }
        .window-body.active { display: block; }

        /* --- AMÉLIORATION INFOS PERSO --- */
        .profile-header { text-align: center; margin-bottom: 20px; }
        .profile-pic { width: 80px; height: 80px; background: var(--info-blue); color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 40px; margin: 0 auto 10px; border: 4px solid white; box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        
        .info-card { background: white; border-radius: 20px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
        .info-row { display: flex; align-items: center; padding: 10px 0; border-bottom: 1px solid #f5f5f5; }
        .info-row:last-child { border-bottom: none; }
        .info-icon { font-size: 20px; margin-right: 15px; width: 30px; text-align: center; }
        .info-content { flex: 1; }
        .info-label { font-size: 0.75rem; color: #999; text-transform: uppercase; font-weight: 700; letter-spacing: 0.5px; }
        .info-value { font-size: 1rem; color: #333; font-weight: 600; }

        .skill-bar { height: 8px; background: #eee; border-radius: 10px; margin-top: 5px; overflow: hidden; }
        .skill-progress { height: 100%; background: var(--info-blue); border-radius: 10px; }

        /* BARRE DES TÂCHES */
        .taskbar { position: absolute; bottom: 15px; align-self: center; height: 65px; background: rgba(255, 255, 255, 0.2); backdrop-filter: blur(20px); border-radius: 25px; display: flex; align-items: center; padding: 0 20px; gap: 25px; border: 1px solid rgba(255,255,255,0.3); }
        .task-item { font-size: 30px; transition: 0.3s; }
        .task-item:active { transform: scale(0.8); }

    </style>
</head>
<body>

    <div id="lock-screen">
        <div class="login-card">
            <h2 style="color: var(--accent); margin-bottom: 5px;">Hello Manon ❤️</h2>
            <p style="font-size: 0.8rem; color: #888; margin-bottom: 20px;">Accès sécurisé - Alexandre D.</p>
            <input type="password" id="passInput" placeholder="Ton mot de passe préféré...">
            <button class="btn-confirm" onclick="checkPassword()">Confirmer</button>
            <p id="error" style="color: #ff4785; font-size: 0.75rem; margin-top: 10px; display: none; font-weight: 600;">Ce n'est pas le bon code, mon ange...</p>
        </div>
    </div>

    <div id="desktop">
        <div class="desktop-icons">
            <div class="app-icon" onclick="openWindow('tab-lettre')">
                <div class="icon-box" style="background: #fff0f5;">💌</div>
                <span>MA LETTRE</span>
            </div>
            <div class="app-icon" onclick="openWindow('tab-info')">
                <div class="icon-box" style="background: #e0f7fa;">🤵</div>
                <span>ALEXANDRE</span>
            </div>
        </div>

        <div id="mainWindow" class="window">
            <div class="close-btn" onclick="closeWindow()">×</div>
            <div class="window-header">
                <div class="tabs">
                    <div id="btn-lettre" class="tab active" onclick="switchTab('tab-lettre')">Lettre</div>
                    <div id="btn-info" class="tab" onclick="switchTab('tab-info')">Mon Amoureux</div>
                </div>
            </div>
            
            <div id="tab-lettre" class="window-body active">
                <h3 style="color: var(--accent); margin-bottom: 15px; font-family: 'Georgia', serif;">Ma très chère Manon,</h3>
                <div style="font-family: 'Georgia', serif; line-height: 1.8; color: #444;">
                    <p>Je voulais créer ce petit espace rien que pour toi. Tu es la personne qui illumine mes journées et je voulais te dire à quel point tu comptes pour moi.</p>
                    <br>
                    <p>Depuis que tu fais partie de mon quotidien, tout est devenu plus beau. Je ne savais pas qu'il était possible de s'attacher autant à quelqu'un. Tu es ma force quand je doute, et ma plus belle récompense quand tout va bien.</p>
                    <br>
                    <p>Ce simulateur, c'est ma façon de te montrer que je pense à toi, même à travers les lignes de code.</p>
                    <br>
                    <p>Je t'aime, plus que les mots ne peuvent l'écrire.</p>
                    <p style="margin-top: 25px; text-align: right; font-weight: bold; color: var(--accent); font-size: 1.2rem;">Ton Alexandre ❤️</p>
                </div>
            </div>

            <div id="tab-info" class="window-body">
                <div class="profile-header">
                    <div class="profile-pic">A</div>
                    <h2 style="color: #333;">Alexandre Draux</h2>
                    <p style="color: var(--accent); font-weight: 600; font-size: 0.9rem;">Reine : Manon ❤️</p>
                </div>

                <div class="info-card">
                    <div class="info-row">
                        <div class="info-icon">🎂</div>
                        <div class="info-content">
                            <div class="info-label">Âge & Taille</div>
                            <div class="info-value">18 ans — 1m81</div>
                        </div>
                    </div>
                    <div class="info-row">
                        <div class="info-icon">🇮🇹</div>
                        <div class="info-content">
                            <div class="info-label">Nationalité & Origines</div>
                            <div class="info-value">Français (Italien/Français)</div>
                        </div>
                    </div>
                    <div class="info-row">
                        <div class="info-icon">📍</div>
                        <div class="info-content">
                            <div class="info-label">Résidence</div>
                            <div class="info-value">Maignelay-Montigny (Né à Creil)</div>
                        </div>
                    </div>
                    <div class="info-row">
                        <div class="info-icon">🏠</div>
                        <div class="info-content">
                            <div class="info-label">Adresse Précise</div>
                            <div class="info-value">1 rue des tieule, 60420</div>
                        </div>
                    </div>
                </div>

                <h3 style="margin: 10px 5px; font-size: 0.9rem; color: #666;">PASSIONS & SKILLS</h3>
                <div class="info-card">
                    <div style="margin-bottom: 15px;">
                        <div style="display: flex; justify-content: space-between; font-size: 0.9rem;">
                            <span>🎹 Piano</span><span style="color: var(--info-blue);">90%</span>
                        </div>
                        <div class="skill-bar"><div class="skill-progress" style="width: 90%;"></div></div>
                    </div>
                    <div style="margin-bottom: 15px;">
                        <div style="display: flex; justify-content: space-between; font-size: 0.9rem;">
                            <span>💻 Codage</span><span style="color: var(--info-blue);">85%</span>
                        </div>
                        <div class="skill-bar"><div class="skill-progress" style="width: 85%;"></div></div>
                    </div>
                    <div>
                        <div style="display: flex; justify-content: space-between; font-size: 0.9rem;">
                            <span>🎨 Dessin</span><span style="color: var(--info-blue);">75%</span>
                        </div>
                        <div class="skill-bar"><div class="skill-progress" style="width: 75%;"></div></div>
                    </div>
                </div>

                <div class="info-card" style="background: #f0f7ff; border: 1px dashed #4facfe; display: flex; align-items: center;">
                    <span style="font-size: 25px; margin-right: 15px;">🐱</span>
                    <div>
                        <div class="info-label">Compagnon</div>
                        <div class="info-value">1 Chat adorable</div>
                    </div>
                </div>
                <div style="height: 20px;"></div>
            </div>
        </div>

        <div class="taskbar">
            <div class="task-item" onclick="openWindow('tab-lettre')">💖</div>
            <div class="task-item" onclick="openWindow('tab-info')">📂</div>
            <div class="task-item" onclick="location.reload()">🔒</div>
        </div>
    </div>

    <script>
        function checkPassword() {
            const val = document.getElementById('passInput').value.toLowerCase();
            if (val === 'mon coeur' || val === 'mon cœur') {
                document.getElementById('lock-screen').style.opacity = '0';
                document.getElementById('lock-screen').style.transform = 'scale(1.2)';
                setTimeout(() => {
                    document.getElementById('lock-screen').style.display = 'none';
                    document.getElementById('desktop').style.display = 'flex';
                }, 500);
            } else {
                document.getElementById('error').style.display = 'block';
                document.getElementById('passInput').style.borderColor = '#ff4785';
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
            document.getElementById('btn-' + tabId.split('-')[1]).classList.add('active');
        }

        document.getElementById('passInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') checkPassword();
        });
    </script>
</body>
</html>
