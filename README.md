        }

        /* Анимация фона */
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        body {
            background-size: 200% 200%;
            animation: gradientBG 10s ease infinite;
        }

        /* Контейнер */
        .container {
            max-width: 450px;
            margin: 0 auto;
        }

        /* Карточка статистики */
        .stats-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px);
            border-radius: 32px;
            padding: 20px;
            margin-bottom: 24px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
        }

        .stat-row {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 16px;
        }

        .stat-label {
            font-size: 14px;
            opacity: 0.7;
            letter-spacing: 0.5px;
        }

        .stat-value {
            font-size: 28px;
            font-weight: bold;
            background: linear-gradient(135deg, #ffd700, #ffaa00);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        /* Энергия */
        .energy-container {
            margin-top: 8px;
        }

        .energy-bar-bg {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            height: 12px;
            overflow: hidden;
        }

        .energy-bar-fill {
            background: linear-gradient(90deg, #00ff87, #60efff);
            width: 100%;
            height: 100%;
            border-radius: 20px;
            transition: width 0.3s ease;
            box-shadow: 0 0 10px rgba(0, 255, 135, 0.5);
        }

        /* Кнопка тапа */
        .tap-area {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }

        .tap-button {
            background: radial-gradient(circle at 30% 30%, #ffd700, #ff8c00);
            width: 220px;
            height: 220px;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), 0 0 0 8px rgba(255, 215, 0, 0.3), inset 0 2px 5px rgba(255, 255, 255, 0.5);
            transition: transform 0.05s linear, box-shadow 0.1s ease;
            position: relative;
        }

        .tap-button:active {
            transform: scale(0.96);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4), 0 0 0 8px rgba(255, 215, 0, 0.5);
        }

        .tap-emoji {
            font-size: 90px;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
        }

        .tap-text {
            font-size: 18px;
            font-weight: bold;
            margin-top: 10px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        /* Нижняя навигация */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(20px);
            display: flex;
            justify-content: space-around;
            padding: 12px 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            z-index: 100;
        }

        .nav-item {
            text-align: center;
            padding: 8px 16px;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.2s ease;
            flex: 1;
            max-width: 80px;
        }

        .nav-item.active {
            background: rgba(255, 215, 0, 0.2);
            transform: translateY(-2px);
        }

        .nav-icon {
            font-size: 28px;
            display: block;
        }

        .nav-label {
            font-size: 11px;
            margin-top: 4px;
            opacity: 0.7;
        }

        .nav-item.active .nav-label {
            opacity: 1;
            color: #ffd700;
        }

        /* Панели */
        .panel {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .panel.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Карточки бустов */
        .boost-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            padding: 16px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .boost-card:active {
            transform: scale(0.98);
            background: rgba(255, 255, 255, 0.15);
        }

        .boost-info h4 {
            font-size: 16px;
            margin-bottom: 4px;
        }

        .boost-info p {
            font-size: 12px;
            opacity: 0.6;
        }

        .boost-price {
            font-size: 18px;
            font-weight: bold;
            color: #ffd700;
        }

        /* Статистика */
        .stat-block {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 24px;
            padding: 16px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* Рейтинг */
        .rating-item {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 14px 16px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* Анимация бонуса */
        .floating-bonus {
            position: fixed;
            pointer-events: none;
            font-size: 28px;
            font-weight: bold;
            z-index: 1000;
            animation: floatUp 1s ease-out forwards;
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        @keyframes floatUp {
            0% {
                opacity: 1;
                transform: translateY(0) scale(0.8);
            }
            100% {
                opacity: 0;
                transform: translateY(-120px) scale(1.2);
            }
        }

        /* Заголовки */
        .section-title {
            font-size: 20px;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Кнопка быстрого тапа */
        .quick-tap {
            position: fixed;
            bottom: 100px;
            right: 20px;
            background: rgba(255, 215, 0, 0.9);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            z-index: 99;
            font-size: 24px;
        }
        
        .quick-tap:active {
            transform: scale(0.9);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Статистика -->
        <div class="stats-card">
            <div class="stat-row">
                <span class="stat-label">💰 МОНЕТЫ</span>
                <span class="stat-value" id="coins">0</span>
            </div>
            <div class="energy-container">
                <div class="stat-row" style="margin-bottom: 8px;">
                    <span class="stat-label">⚡ ЭНЕРГИЯ</span>
                    <span class="stat-value" id="energy" style="font-size: 20px;">100</span>
                </div>
                <div class="energy-bar-bg">
                    <div class="energy-bar-fill" id="energyFill" style="width: 100%"></div>
                </div>
            </div>
            <div class="stat-row" style="margin-top: 12px;">
                <span class="stat-label">💪 СИЛА ТАПА</span>
                <span class="stat-value" id="tapPower" style="font-size: 20px;">1</span>
            </div>
        </div>

        <!-- Панель игры -->
        <div id="gamePanel" class="panel active">
            <div class="tap-area">
                <div class="tap-button" id="tapButton">
                    <span class="tap-emoji">💎</span>
                    <span class="tap-text">ТАПАЙ!</span>
                </div>
            </div>
            <div style="text-align: center; margin-top: 10px;">
                <p style="opacity: 0.6; font-size: 14px;">За каждый тап +<span id="tapReward">1</span> монет</p>
            </div>
        </div>

        <!-- Панель бустов -->
        <div id="boostsPanel" class="panel">
            <div class="section-title">
                <span>📈</span>
                <span>УЛУЧШЕНИЯ</span>
            </div>
            <div id="boostsList"></div>
        </div>

        <!-- Панель статистики -->
        <div id="statsPanel" class="panel">
            <div class="section-title">
                <span>📊</span>
                <span>СТАТИСТИКА</span>
            </div>
            <div class="stat-block">
                <span>🔨 Всего тапов</span>
                <span id="totalTaps" style="font-weight: bold;">0</span>
            </div>
            <div class="stat-block">
                <span>💸 Всего заработано</span>
                <span id="totalEarned" style="font-weight: bold; color: #ffd700;">0</span>
            </div>
            <div class="stat-block">
                <span>🤖 Авто-тап/сек</span>
                <span id="autoTap" style="font-weight: bold;">0</span>
            </div>
            <div class="stat-block">
                <span>🎯 Шанс крита</span>
                <span id="critChance" style="font-weight: bold;">0%</span>
            </div>
        </div>

        <!-- Панель рейтинга -->
        <div id="ratingPanel" class="panel">
            <div class="section-title">
                <span>🏆</span>
                <span>ТОП ИГРОКОВ</span>
            </div>
            <div id="ratingList"></div>
        </div>
    </div>

    <!-- Нижняя навигация -->
    <div class="bottom-nav">
        <div class="nav-item active" data-panel="game">
            <span class="nav-icon">🔨</span>
            <span class="nav-label">Игра</span>
        </div>
        <div class="nav-item" data-panel="boosts">
            <span class="nav-icon">📈</span>
            <span class="nav-label">Бусты</span>
        </div>
        <div class="nav-item" data-panel="stats">
            <span class="nav-icon">📊</span>
            <span class="nav-label">Статистика</span>
        </div>
        <div class="nav-item" data-panel="rating">
            <span class="nav-icon">🏆</span>
            <span class="nav-label">Рейтинг</span>
        </div>
    </div>

    <!-- Быстрый тап -->
    <div class="quick-tap" id="quickTap">💎</div>

    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        // Инициализация Telegram WebApp
        const tg = window.Telegram.WebApp;
        tg.expand();
        tg.ready();
        tg.enableClosingConfirmation();

        // Данные игрока
        let player = {
            coins: 100,
            energy: 100,
            maxEnergy: 100,
            totalTaps: 0,
            totalEarned: 0,
            boosts: {
                tapPower: 0,
                energyLimit: 0,
                autoTap: 0,
                critChance: 0
            },
            lastEnergyUpdate: Date.now()
        };

        // Конфигурация бустов
        const BOOSTS = {
            tapPower: { name: "💪 Усиление тапа", baseCost: 100, effect: 1, max: 10, desc: "+1 монета за тап" },
            energyLimit: { name: "⚡ Лимит энергии", baseCost: 80, effect: 10, max: 20, desc: "+10 макс. энергии" },
            autoTap: { name: "🤖 Авто-тап", baseCost: 200, effect: 1, max: 5, desc: "+1 монета/сек" },
            critChance: { name: "🎯 Критический удар", baseCost: 150, effect: 5, max: 10, desc: "+5% шанс x2" }
        };

        // Загрузка данных
        function loadData() {
            const saved = localStorage.getItem('tapper_game');
            if (saved) {
                try {
                    const data = JSON.parse(saved);
                    player = { ...player, ...data };
                    player.lastEnergyUpdate = Date.now();
                } catch(e) {}
            }
            updateEnergy();
        }

        // Сохранение данных
        function saveData() {
            const toSave = {
                coins: player.coins,
                energy: player.energy,
                maxEnergy: player.maxEnergy,
                totalTaps: player.totalTaps,
                totalEarned: player.totalEarned,
                boosts: player.boosts,
                lastEnergyUpdate: player.lastEnergyUpdate
            };
            localStorage.setItem('tapper_game', JSON.stringify(toSave));
        }

        // Обновление энергии
        function updateEnergy() {
            const now = Date.now();
            const secondsPassed = (now - player.lastEnergyUpdate) / 1000;
            const maxEnergy = player.maxEnergy + (player.boosts.energyLimit * 10);
            let newEnergy = player.energy + secondsPassed;
            if (newEnergy > maxEnergy) newEnergy = maxEnergy;
            player.energy = Math.min(newEnergy, maxEnergy);
            player.maxEnergy = maxEnergy;
            player.lastEnergyUpdate = now;
            updateUI();
        }

        // Показать всплывающий бонус
        function showFloatingBonus(text, isCrit = false, x, y) {
            const bonus = document.createElement('div');
            bonus.className = 'floating-bonus';
            bonus.textContent = text;
            bonus.style.color = isCrit ? '#ff6666' : '#ffd700';
            bonus.style.left = (x || window.innerWidth / 2 - 40) + 'px';
            bonus.style.top = (y || window.innerHeight * 0.5) + 'px';
            document.body.appendChild(bonus);
            setTimeout(() => bonus.remove(), 1000);
        }

        // Тап
        function tap(event) {
            if (player.energy < 1) {
                showFloatingBonus('❌ Нет энергии!', false, event?.clientX, event?.clientY);
                return false;
            }
            
            let reward = 1 + player.boosts.tapPower;
            const critChance = player.boosts.critChance * 5;
            const isCrit = Math.random() * 100 < critChance;
            
            if (isCrit) {
                reward *= 2;
                showFloatingBonus(`КРИТ! +${reward}`, true, event?.clientX, event?.clientY);
            } else {
                showFloatingBonus(`+${reward}`, false, event?.clientX, event?.clientY);
            }
            
            player.energy -= 1;
            player.coins += reward;
            player.totalTaps++;
            player.totalEarned += reward;
            
            // Анимация кнопки
            const btn = document.getElementById('tapButton');
            btn.style.transform = 'scale(0.96)';
            setTimeout(() => btn.style.transform = '', 100);
            
            updateUI();
            saveData();
            
            // Вибрация (если доступно)
            if (navigator.vibrate) navigator.vibrate(50);
            
            return true;
        }

        // Покупка буста
        function buyBoost(boostId) {
            const boost = BOOSTS[boostId];
            const currentLevel = player.boosts[boostId];
            
            if (currentLevel >= boost.max) {
                tg.showAlert(`❌ ${boost.name} достиг максимального уровня!`);
                return;
            }
            
            const cost = boost.baseCost * (currentLevel + 1);
            
            if (player.coins < cost) {
                tg.showAlert(`❌ Недостаточно монет! Нужно ${cost} 💰`);
                return;
            }
            
            player.coins -= cost;
            player.boosts[boostId]++;
            
            updateUI();
            saveData();
            
            tg.showAlert(`✅ Куплен ${boost.name}!\nУровень: ${player.boosts[boostId]}/${boost.max}`);
        }

        // Авто-тап
        function autoTap() {
            if (player.boosts.autoTap > 0) {
                const reward = player.boosts.autoTap;
                player.coins += reward;
                player.totalEarned += reward;
                updateUI();
                saveData();
            }
        }

        // Обновление интерфейса
        function updateUI() {
            document.getElementById('coins').textContent = Math.floor(player.coins);
            document.getElementById('energy').textContent = Math.floor(player.energy);
            document.getElementById('tapPower').textContent = 1 + player.boosts.tapPower;
            document.getElementById('tapReward').textContent = 1 + player.boosts.tapPower;
            
            const energyPercent = (player.energy / player.maxEnergy) * 100;
            document.getElementById('energyFill').style.width = energyPercent + '%';
            
            document.getElementById('totalTaps').textContent = player.totalTaps;
            document.getElementById('totalEarned').textContent = Math.floor(player.totalEarned);
            document.getElementById('autoTap').textContent = player.boosts.autoTap;
            document.getElementById('critChance').textContent = (player.boosts.critChance * 5) + '%';
            
            updateBoostsList();
        }

        // Обновление списка бустов
        function updateBoostsList() {
            const container = document.getElementById('boostsList');
            if (!container) return;
            
            container.innerHTML = '';
            
            for (const [id, boost] of Object.entries(BOOSTS)) {
                const level = player.boosts[id];
                const maxLevel = boost.max;
                const cost = boost.baseCost * (level + 1);
                const isMax = level >= maxLevel;
                
                const div = document.createElement('div');
                div.className = 'boost-card';
                div.onclick = () => buyBoost(id);
                
                div.innerHTML = `
                    <div class="boost-info">
                        <h4>${boost.name} ${level}/${maxLevel}</h4>
                        <p>${boost.desc}</p>
                    </div>
                    <div class="boost-price">
                        ${isMax ? '🔒 MAX' : cost + '💰'}
                    </div>
                `;
                
                container.appendChild(div);
            }
        }

        // Обновление рейтинга
        function updateRating() {
            const players = [
             
