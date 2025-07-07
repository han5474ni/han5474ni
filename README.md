<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code Quest Adventure - README Game</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
            font-family: 'Orbitron', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
        }

        .game-container {
            width: 800px;
            height: 600px;
            background: linear-gradient(45deg, #0f3460 0%, #16537e 100%);
            border: 4px solid #00ffff;
            border-radius: 20px;
            box-shadow: 0 0 50px rgba(0, 255, 255, 0.5);
            position: relative;
            overflow: hidden;
        }

        .game-header {
            background: linear-gradient(90deg, #1a1a2e, #16213e);
            color: #00ffff;
            padding: 15px;
            text-align: center;
            border-bottom: 2px solid #00ffff;
        }

        .game-title {
            font-size: 24px;
            font-weight: 900;
            margin-bottom: 5px;
            text-shadow: 0 0 20px rgba(0, 255, 255, 0.8);
        }

        .game-subtitle {
            font-size: 12px;
            color: #ff6b6b;
            animation: pulse 2s infinite;
        }

        .game-area {
            position: relative;
            width: 100%;
            height: 500px;
            background: linear-gradient(180deg, #0a0a23 0%, #1a1a40 100%);
            overflow: hidden;
        }

        .player {
            position: absolute;
            width: 40px;
            height: 40px;
            background: #00ffff;
            border-radius: 50%;
            bottom: 50px;
            left: 50px;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.8);
            transition: all 0.3s ease;
            z-index: 10;
        }

        .player::before {
            content: "🚀";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 20px;
        }

        .enemy {
            position: absolute;
            width: 35px;
            height: 35px;
            background: #ff6b6b;
            border-radius: 50%;
            box-shadow: 0 0 15px rgba(255, 107, 107, 0.8);
            animation: enemyMove 3s linear infinite;
        }

        .enemy::before {
            content: "🐛";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
        }

        .coin {
            position: absolute;
            width: 30px;
            height: 30px;
            background: #ffd700;
            border-radius: 50%;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.8);
            animation: coinFloat 2s ease-in-out infinite;
        }

        .coin::before {
            content: "💰";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 15px;
        }

        .powerup {
            position: absolute;
            width: 35px;
            height: 35px;
            background: #ff00ff;
            border-radius: 50%;
            box-shadow: 0 0 20px rgba(255, 0, 255, 0.8);
            animation: powerupPulse 1.5s ease-in-out infinite;
        }

        .powerup::before {
            content: "⚡";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 20px;
        }

        .stats {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.8);
            padding: 15px;
            border-radius: 10px;
            border: 2px solid #00ffff;
            color: #00ffff;
            font-size: 14px;
        }

        .controls {
            position: absolute;
            bottom: 20px;
            left: 20px;
            background: rgba(0, 0, 0, 0.8);
            padding: 15px;
            border-radius: 10px;
            border: 2px solid #00ffff;
            color: #00ffff;
            font-size: 12px;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #00ffff;
            border-radius: 50%;
            animation: particleFloat 4s linear infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        @keyframes enemyMove {
            0% { transform: translateX(0) rotate(0deg); }
            25% { transform: translateX(100px) rotate(90deg); }
            50% { transform: translateX(100px) translateY(-50px) rotate(180deg); }
            75% { transform: translateX(0) translateY(-50px) rotate(270deg); }
            100% { transform: translateX(0) rotate(360deg); }
        }

        @keyframes coinFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        @keyframes powerupPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }

        @keyframes particleFloat {
            0% { 
                transform: translateY(0px) translateX(0px);
                opacity: 1;
            }
            100% { 
                transform: translateY(-500px) translateX(100px);
                opacity: 0;
            }
        }

        .game-over {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.9);
            color: #00ffff;
            padding: 30px;
            border-radius: 20px;
            border: 3px solid #00ffff;
            text-align: center;
            display: none;
            z-index: 100;
        }

        .btn {
            background: linear-gradient(45deg, #00ffff, #0099cc);
            color: #000;
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            cursor: pointer;
            margin: 10px;
            transition: all 0.3s ease;
        }

        .btn:hover {
            transform: scale(1.1);
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.8);
        }

        .achievement {
            position: absolute;
            top: 100px;
            right: 20px;
            background: rgba(255, 215, 0, 0.9);
            color: #000;
            padding: 10px;
            border-radius: 10px;
            font-size: 12px;
            transform: translateX(300px);
            transition: all 0.5s ease;
        }

        .achievement.show {
            transform: translateX(0);
        }

        .stars {
            position: absolute;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="1" fill="white" opacity="0.8"/><circle cx="80" cy="30" r="1" fill="white" opacity="0.6"/><circle cx="40" cy="60" r="1" fill="white" opacity="0.9"/><circle cx="90" cy="70" r="1" fill="white" opacity="0.7"/><circle cx="10" cy="80" r="1" fill="white" opacity="0.5"/></svg>') repeat;
            animation: starMove 20s linear infinite;
        }

        @keyframes starMove {
            0% { transform: translateY(0px); }
            100% { transform: translateY(-100px); }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="game-header">
            <div class="game-title">🎮 CODE QUEST ADVENTURE</div>
            <div class="game-subtitle">Debug the bugs, collect the coins, level up your skills!</div>
        </div>
        
        <div class="game-area">
            <div class="stars"></div>
            <div class="player" id="player"></div>
            
            <div class="stats" id="stats">
                <div>💰 Coins: <span id="coins">0</span></div>
                <div>🐛 Bugs Fixed: <span id="bugs">0</span></div>
                <div>⚡ Power: <span id="power">0</span></div>
                <div>🎯 Level: <span id="level">1</span></div>
                <div>💚 Health: <span id="health">100</span></div>
            </div>
            
            <div class="controls">
                <div><strong>🎮 CONTROLS:</strong></div>
                <div>WASD or Arrow Keys - Move</div>
                <div>Space - Boost</div>
                <div>Click - Interact</div>
                <div><strong>🎯 GOAL:</strong> Collect coins & fix bugs!</div>
            </div>
            
            <div class="achievement" id="achievement">
                🏆 Achievement Unlocked!
            </div>
        </div>
        
        <div class="game-over" id="gameOver">
            <h2>🎉 GAME COMPLETE!</h2>
            <p>You've mastered the art of coding!</p>
            <button class="btn" onclick="resetGame()">🚀 Play Again</button>
            <button class="btn" onclick="window.open('https://github.com/yourusername', '_blank')">📱 Visit My GitHub</button>
        </div>
    </div>

    <script>
        const player = document.getElementById('player');
        const gameArea = document.querySelector('.game-area');
        const stats = {
            coins: 0,
            bugs: 0,
            power: 0,
            level: 1,
            health: 100
        };
        
        let playerPos = { x: 50, y: 450 };
        let gameObjects = [];
        let particles = [];
        let keys = {};
        let gameRunning = true;
        
        // Initialize game
        function init() {
            updatePlayerPosition();
            spawnObjects();
            createParticles();
            gameLoop();
            setupControls();
        }
        
        function updatePlayerPosition() {
            player.style.left = playerPos.x + 'px';
            player.style.bottom = (500 - playerPos.y) + 'px';
        }
        
        function spawnObjects() {
            // Spawn enemies (bugs)
            for (let i = 0; i < 3; i++) {
                setTimeout(() => {
                    createEnemy();
                }, i * 2000);
            }
            
            // Spawn coins
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    createCoin();
                }, i * 1500);
            }
            
            // Spawn power-ups
            setTimeout(() => {
                createPowerup();
            }, 3000);
        }
        
        function createEnemy() {
            const enemy = document.createElement('div');
            enemy.className = 'enemy';
            enemy.style.left = Math.random() * 700 + 'px';
            enemy.style.top = Math.random() * 400 + 'px';
            gameArea.appendChild(enemy);
            gameObjects.push({ element: enemy, type: 'enemy' });
            
            // Remove after animation
            setTimeout(() => {
                if (enemy.parentNode) {
                    enemy.parentNode.removeChild(enemy);
                    gameObjects = gameObjects.filter(obj => obj.element !== enemy);
                }
            }, 3000);
        }
        
        function createCoin() {
            const coin = document.createElement('div');
            coin.className = 'coin';
            coin.style.left = Math.random() * 700 + 'px';
            coin.style.top = Math.random() * 400 + 'px';
            gameArea.appendChild(coin);
            gameObjects.push({ element: coin, type: 'coin' });
        }
        
        function createPowerup() {
            const powerup = document.createElement('div');
            powerup.className = 'powerup';
            powerup.style.left = Math.random() * 700 + 'px';
            powerup.style.top = Math.random() * 400 + 'px';
            gameArea.appendChild(powerup);
            gameObjects.push({ element: powerup, type: 'powerup' });
            
            setTimeout(() => {
                if (powerup.parentNode) {
                    powerup.parentNode.removeChild(powerup);
                    gameObjects = gameObjects.filter(obj => obj.element !== powerup);
                }
            }, 5000);
        }
        
        function createParticles() {
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const particle = document.createElement('div');
                    particle.className = 'particle';
                    particle.style.left = Math.random() * 800 + 'px';
                    particle.style.top = '500px';
                    gameArea.appendChild(particle);
                    
                    setTimeout(() => {
                        if (particle.parentNode) {
                            particle.parentNode.removeChild(particle);
                        }
                    }, 4000);
                }, i * 200);
            }
        }
        
        function setupControls() {
            document.addEventListener('keydown', (e) => {
                keys[e.key.toLowerCase()] = true;
            });
            
            document.addEventListener('keyup', (e) => {
                keys[e.key.toLowerCase()] = false;
            });
            
            // Click to collect
            gameArea.addEventListener('click', (e) => {
                const rect = gameArea.getBoundingClientRect();
                const clickX = e.clientX - rect.left;
                const clickY = e.clientY - rect.top;
                
                gameObjects.forEach(obj => {
                    const objRect = obj.element.getBoundingClientRect();
                    const objX = objRect.left - rect.left;
                    const objY = objRect.top - rect.top;
                    
                    if (Math.abs(clickX - objX) < 50 && Math.abs(clickY - objY) < 50) {
                        collectObject(obj);
                    }
                });
            });
        }
        
        function gameLoop() {
            if (!gameRunning) return;
            
            // Handle movement
            let speed = 5;
            if (keys[' ']) speed = 10; // Boost
            
            if (keys['w'] || keys['arrowup']) {
                playerPos.y = Math.max(0, playerPos.y - speed);
            }
            if (keys['s'] || keys['arrowdown']) {
                playerPos.y = Math.min(450, playerPos.y + speed);
            }
            if (keys['a'] || keys['arrowleft']) {
                playerPos.x = Math.max(0, playerPos.x - speed);
            }
            if (keys['d'] || keys['arrowright']) {
                playerPos.x = Math.min(760, playerPos.x + speed);
            }
            
            updatePlayerPosition();
            checkCollisions();
            updateStats();
            
            // Spawn more objects
            if (Math.random() < 0.01) createEnemy();
            if (Math.random() < 0.008) createCoin();
            if (Math.random() < 0.003) createPowerup();
            if (Math.random() < 0.05) createParticles();
            
            requestAnimationFrame(gameLoop);
        }
        
        function checkCollisions() {
            gameObjects.forEach(obj => {
                const rect = obj.element.getBoundingClientRect();
                const playerRect = player.getBoundingClientRect();
                
                if (rect.left < playerRect.right && 
                    rect.right > playerRect.left && 
                    rect.top < playerRect.bottom && 
                    rect.bottom > playerRect.top) {
                    collectObject(obj);
                }
            });
        }
        
        function collectObject(obj) {
            if (obj.collected) return;
            obj.collected = true;
            
            switch(obj.type) {
                case 'coin':
                    stats.coins += 10;
                    showAchievement('💰 Coin Collected! +10 points');
                    break;
                case 'enemy':
                    stats.bugs += 1;
                    stats.coins += 5;
                    showAchievement('🐛 Bug Fixed! +5 points');
                    break;
                case 'powerup':
                    stats.power += 1;
                    stats.health = Math.min(100, stats.health + 20);
                    showAchievement('⚡ Power Up! Health restored!');
                    break;
            }
            
            // Level up logic
            if (stats.coins >= stats.level * 50) {
                stats.level++;
                showAchievement('🎉 Level Up! Welcome to Level ' + stats.level);
            }
            
            // Remove object
            if (obj.element.parentNode) {
                obj.element.style.transform = 'scale(0)';
                setTimeout(() => {
                    if (obj.element.parentNode) {
                        obj.element.parentNode.removeChild(obj.element);
                    }
                }, 300);
            }
            
            gameObjects = gameObjects.filter(o => o !== obj);
        }
        
        function updateStats() {
            document.getElementById('coins').textContent = stats.coins;
            document.getElementById('bugs').textContent = stats.bugs;
            document.getElementById('power').textContent = stats.power;
            document.getElementById('level').textContent = stats.level;
            document.getElementById('health').textContent = stats.health;
            
            // Win condition
            if (stats.level >= 5) {
                document.getElementById('gameOver').style.display = 'block';
                gameRunning = false;
            }
        }
        
        function showAchievement(message) {
            const achievement = document.getElementById('achievement');
            achievement.textContent = message;
            achievement.classList.add('show');
            
            setTimeout(() => {
                achievement.classList.remove('show');
            }, 3000);
        }
        
        function resetGame() {
            stats.coins = 0;
            stats.bugs = 0;
            stats.power = 0;
            stats.level = 1;
            stats.health = 100;
            playerPos = { x: 50, y: 450 };
            gameRunning = true;
            
            // Clear all objects
            gameObjects.forEach(obj => {
                if (obj.element.parentNode) {
                    obj.element.parentNode.removeChild(obj.element);
                }
            });
            gameObjects = [];
            
            document.getElementById('gameOver').style.display = 'none';
            init();
        }
        
        // Start the game
        init();
    </script>
</body>
</html>
