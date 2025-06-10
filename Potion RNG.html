# Potion-RNG
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>El Caldero del Azar</title>
    <style>
        /* --- CSS (Estilos Visuales) --- */
        @import url('https://fonts.googleapis.com/css2?family=VT323&family=Press+Start+2P&display=swap');

        :root {
            --bg-color: #1a1a1a;
            --text-color: #00ff41;
            --border-color: #00ff41;
            --accent-color: #f7b731;
            --error-color: #ff4136;
            --player-color: #7fdbff;
            --font-main: 'VT323', monospace;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: var(--font-main);
            font-size: 20px;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .game-container {
            width: 100%;
            max-width: 900px;
            border: 2px solid var(--border-color);
            background-color: #000;
            padding: 20px;
            display: grid;
            grid-template-columns: 2fr 1fr;
            grid-template-rows: auto 1fr auto;
            grid-template-areas:
                "title title"
                "log sidebar"
                "input input";
            gap: 20px;
            box-shadow: 0 0 20px var(--border-color);
        }

        h1 {
            grid-area: title;
            text-align: center;
            color: var(--accent-color);
            font-family: 'Press Start 2P', cursive;
            font-size: 24px;
            margin: 0 0 10px 0;
            text-shadow: 0 0 5px var(--accent-color);
        }

        .game-log-wrapper {
            grid-area: log;
            border: 1px solid var(--border-color);
            padding: 10px;
            height: 400px;
            overflow-y: scroll;
            background-color: #111;
        }

        #game-log p {
            margin: 0 0 8px 0;
            white-space: pre-wrap;
            word-break: break-word;
        }
        
        #game-log .system { color: var(--accent-color); }
        #game-log .player { color: var(--player-color); }
        #game-log .combat { color: #e0e0e0; }
        #game-log .error { color: var(--error-color); }
        #game-log .reward { color: #2ecc40; }


        .sidebar {
            grid-area: sidebar;
            border: 1px solid var(--border-color);
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .sidebar-section h2 {
            margin: 0 0 10px 0;
            font-size: 22px;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 5px;
        }

        #inventory-list, #status-list {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }

        #inventory-list li, #status-list li {
            margin-bottom: 5px;
        }

        .input-area {
            grid-area: input;
            display: flex;
            gap: 10px;
        }

        #user-input {
            flex-grow: 1;
            background-color: #222;
            border: 1px solid var(--border-color);
            color: var(--text-color);
            padding: 10px;
            font-family: var(--font-main);
            font-size: 18px;
        }

        #user-input:focus {
            outline: none;
            box-shadow: 0 0 10px var(--border-color);
        }

        button {
            background-color: transparent;
            border: 1px solid var(--border-color);
            color: var(--border-color);
            padding: 10px 20px;
            font-family: var(--font-main);
            font-size: 18px;
            cursor: pointer;
            transition: all 0.2s;
        }

        button:hover {
            background-color: var(--border-color);
            color: #000;
        }
        
        /* Media query para pantallas pequeñas */
        @media (max-width: 768px) {
            body { padding: 10px; }
            .game-container {
                grid-template-columns: 1fr;
                grid-template-areas:
                    "title"
                    "sidebar"
                    "log"
                    "input";
            }
            .game-log-wrapper { height: 300px; }
        }
    </style>
</head>
<body>

    <div class="game-container">
        <h1>El Caldero del Azar</h1>

        <div class="game-log-wrapper">
            <div id="game-log"></div>
        </div>

        <div class="sidebar">
            <div class="sidebar-section">
                <h2>Estado</h2>
                <ul id="status-list">
                    <li id="status-level"></li>
                    <li id="status-hp"></li>
                    <li id="status-xp"></li>
                    <li id="status-chest"></li>
                </ul>
            </div>
            <div class="sidebar-section">
                <h2>Inventario</h2>
                <ul id="inventory-list"></ul>
            </div>
        </div>

        <div class="input-area">
            <input type="text" id="user-input" placeholder="Escribe tu comando aquí...">
            <button id="submit-btn">Enviar</button>
        </div>
    </div>

    <script>
    // --- JavaScript (Lógica del Juego) ---

    // 1. REFERENCIAS A ELEMENTOS DEL DOM
    const gameLog = document.getElementById('game-log');
    const userInput = document.getElementById('user-input');
    const submitBtn = document.getElementById('submit-btn');
    const statusLevel = document.getElementById('status-level');
    const statusHp = document.getElementById('status-hp');
    const statusXp = document.getElementById('status-xp');
    const statusChest = document.getElementById('status-chest');
    const inventoryList = document.getElementById('inventory-list');

    // 2. DATOS DEL JUEGO (Pociones, Cofres, NPCs)
    const POTIONS = {
        comun: [
            { name: 'Poción de Curación Menor', effect: (p, e) => { const h = 25; p.hp = Math.min(p.maxHp, p.hp + h); return `Restauras ${h} HP.`; }},
            { name: 'Frasco de Fuego Débil', effect: (p, e) => { const d = rand(15, 25); e.hp -= d; return `Infliges ${d} de daño de fuego.`; }},
            { name: 'Vial de Ácido Básico', effect: (p, e) => { e.defenseDebuff = 1; return `Infliges 20 de daño y reduces la defensa del enemigo.`; }, baseDamage: 20 },
            { name: 'Bomba de Humo', effect: (p, e) => { if(e.isBoss) return '¡No puedes huir de un jefe!'; gameState.flee = true; return 'Lanzas una bomba de humo para escapar.'; }}
        ],
        raro: [
            { name: 'Poción de Piel de Piedra', effect: (p, e) => { p.shield = 40; return `Ganas un escudo de 40 HP.`; }},
            { name: 'Rayo Embotellado', effect: (p, e) => { const d = rand(40, 60); e.hp -= d; return `Lanzas un rayo que inflige ${d} de daño eléctrico.`; }},
            { name: 'Vial de Veneno Persistente', effect: (p, e) => { e.poison = 3; return `El enemigo es envenenado.`; }},
            { name: 'Poción de Reflejos', effect: (p, e) => { p.dodge = true; return `Tus reflejos se agudizan. Esquivarás el próximo ataque.`; }}
        ],
        epico: [
            { name: 'Elixir de Furia de Gigante', effect: (p, e) => { p.fury = 2; return `¡Tu daño se duplica por 2 turnos!`; }},
            { name: 'Bomba Congelante', effect: (p, e) => { e.frozen = 1; return `Infliges 50 de daño y congelas al enemigo.`; }, baseDamage: 50 },
            { name: 'Poción de Regeneración Mayor', effect: (p, e) => { p.regen = 4; return `Comienzas a regenerar 20 HP por turno.`; }},
            { name: 'Esencia de Espejismo', effect: (p, e) => { gameState.cloneHp = 50; return `Creas un clon con 50 HP.`; }}
        ],
        legendario: [
            { name: 'Lágrima del Fénix', effect: (p, e) => { p.phoenixDown = true; return `Una energía cálida te rodea. Resucitarás si caes.`; }},
            { name: 'Brecha Temporal', effect: (p, e) => { gameState.extraTurn = true; return `¡Doblas el tiempo y ganas un turno extra!`; }},
            { name: 'Caldero Inestable', effect: (p, e) => { /* handled in combat */ return `Lanzas 3 pociones aleatorias al enemigo.`; }},
            { name: 'Sol Embotellado', effect: (p, e) => { e.hp -= 150; return `Desatas el poder del sol, infligiendo 150 de daño sagrado.`; }}
        ]
    };

    const CHESTS = {
        'Madera': { potions: 1, loot: { comun: 1.0 } },
        'Hierro': { potions: 2, loot: { comun: 0.8, raro: 0.2 } },
        'Oro': { potions: 3, loot: { comun: 0.6, raro: 0.3, epico: 0.1 } },
        'Cristal': { potions: 3, loot: { raro: 0.4, epico: 0.45, legendario: 0.15 } }
    };
    
    const NPCS = {
        'slime': { name: "Slime de Práctica", level: 1, hp: 50, maxHp: 50, damage: 10, xp: 50, chest: 'Madera' },
        'goblin': { name: "Goblin Ladrón", level: 2, hp: 80, maxHp: 80, damage: 20, xp: 100, chest: 'Hierro' },
        'orco': { name: "Orco Gladiador", level: 3, hp: 150, maxHp: 150, damage: 35, xp: 200, chest: 'Hierro', ability: (e) => { if(Math.random() < 0.25) { e.nextAttackBonus = 10; addLog('El orco ruge, ¡su próximo ataque será más fuerte!', 'combat'); }}},
        'mago': { name: "Mago Corrupto", level: 4, hp: 120, maxHp: 120, damage: 25, xp: 300, chest: 'Oro', ability: (e) => { if(!e.shielded && e.hp < 60) { e.shield = 50; e.shielded = true; addLog('El mago invoca un escudo mágico de 50 HP.', 'combat');}}},
        'golem': { name: "Golem de Ébano", level: 5, hp: 300, maxHp: 300, damage: 50, xp: 600, chest: 'Cristal', isBoss: true, immune: true }
    };
    
    const LEVEL_XP = [100, 250, 500, 1000, 9999];

    // 3. ESTADO DEL JUEGO
    let player;
    let gameState;
    
    function resetGame() {
        player = {
            level: 1,
            hp: 100,
            maxHp: 100,
            xp: 0,
            inventory: [],
            chest: 'Madera',
            // --- Buffs/Debuffs de combate ---
            shield: 0,
            fury: 0,
            dodge: false,
            regen: 0,
            phoenixDown: false
        };
        
        gameState = {
            inCombat: false,
            currentEnemy: null,
            flee: false,
            extraTurn: false,
            cloneHp: 0
        };
        
        gameLog.innerHTML = '';
        addLog("¡Bienvenido, joven alquimista, al desafío de 'El Caldero del Azar'!", 'system');
        addLog("Se te ha concedido un Cofre de Madera.", 'system');
        addLog("Escribe 'ayuda' para ver la lista de comandos.", 'system');
        updateUI();
    }


    // 4. FUNCIONES DEL JUEGO
    function addLog(message, type = 'combat') {
        const p = document.createElement('p');
        p.textContent = message;
        p.className = type;
        gameLog.appendChild(p);
        gameLog.scrollTop = gameLog.scrollHeight; // Auto-scroll
    }

    function updateUI() {
        statusLevel.textContent = `Nivel: ${player.level}`;
        statusHp.textContent = `HP: ${player.hp} / ${player.maxHp}`;
        statusXp.textContent = `XP: ${player.xp} / ${LEVEL_XP[player.level - 1]}`;
        statusChest.textContent = `Cofre: ${player.chest || 'Ninguno'}`;
        
        inventoryList.innerHTML = '';
        const potionCounts = player.inventory.reduce((acc, potion) => {
            acc[potion.name] = (acc[potion.name] || 0) + 1;
            return acc;
        }, {});

        if (Object.keys(potionCounts).length === 0) {
            inventoryList.innerHTML = '<li>Vacío</li>';
        } else {
            for (const name in potionCounts) {
                const li = document.createElement('li');
                li.textContent = `${name} (x${potionCounts[name]})`;
                inventoryList.appendChild(li);
            }
        }
    }
    
    function rand(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function handleCommand(command) {
        command = command.toLowerCase().trim();
        addLog(`> ${command}`, 'player');

        if (gameState.inCombat) {
            handleCombatCommand(command);
            return;
        }

        const parts = command.split(' ');
        const action = parts[0];
        const target = parts.slice(1).join(' ');

        switch (action) {
            case 'abrir':
                if (target === 'cofre') openChest();
                else addLog("¿Qué quieres abrir? Prueba 'abrir cofre'.", 'error');
                break;
            case 'inventario':
            case 'inv':
                showInventory();
                break;
            case 'estado':
                showStatus();
                break;
            case 'luchar':
                showEnemies();
                break;
            case 'ayuda':
                showHelp();
                break;
            case 'empezar':
                 if(NPCS[target]) startCombat(target);
                 else addLog(`No se encontró al enemigo '${target}'. Escribe 'luchar' para ver la lista.`, 'error');
                 break;
            default:
                addLog("Comando no reconocido. Escribe 'ayuda' para ver la lista de comandos.", 'error');
        }
        updateUI();
    }
    
    // --- Lógica de Comandos ---
    function showHelp() {
        addLog("--- Comandos Disponibles ---", 'system');
        addLog("abrir cofre - Abre el cofre que tengas.", 'system');
        addLog("inventario - Muestra tus pociones.", 'system');
        addLog("estado - Muestra tu nivel, HP y XP.", 'system');
        addLog("luchar - Muestra los enemigos disponibles.", 'system');
        addLog("empezar [nombre] - Inicia un combate (ej: 'empezar slime').", "system");
        addLog("usar [pocion] - (En combate) Usa una poción de tu inventario.", "system");
        addLog("reiniciar - Empieza una nueva partida.", "system");
    }

    function openChest() {
        if (!player.chest) {
            addLog("No tienes ningún cofre para abrir.", 'error');
            return;
        }
        
        const chestType = player.chest;
        const chestData = CHESTS[chestType];
        addLog(`Abres un Cofre de ${chestType}...`, 'reward');
        
        for (let i = 0; i < chestData.potions; i++) {
            const rand = Math.random();
            let cumulative = 0;
            for (const rarity in chestData.loot) {
                cumulative += chestData.loot[rarity];
                if (rand < cumulative) {
                    const potionPool = POTIONS[rarity];
                    const newPotion = potionPool[Math.floor(Math.random() * potionPool.length)];
                    player.inventory.push(newPotion);
                    addLog(`¡Has conseguido: ${newPotion.name}!`, 'reward');
                    break;
                }
            }
        }
        player.chest = null;
    }
    
    function showInventory() {
        const potionCounts = player.inventory.reduce((acc, potion) => {
            acc[potion.name] = (acc[potion.name] || 0) + 1;
            return acc;
        }, {});

        if (Object.keys(potionCounts).length === 0) {
            addLog('Tu inventario está vacío.', 'system');
        } else {
            addLog('--- Tu Inventario ---', 'system');
             for (const name in potionCounts) {
                addLog(`${name} (x${potionCounts[name]})`, 'system');
            }
        }
    }
    
    function showStatus() {
        addLog('--- Tu Estado ---', 'system');
        addLog(`Nivel: ${player.level}`, 'system');
        addLog(`HP: ${player.hp} / ${player.maxHp}`, 'system');
        addLog(`XP: ${player.xp} / ${LEVEL_XP[player.level - 1]}`, 'system');
        addLog(`Cofre: ${player.chest || 'Ninguno'}`, 'system');
    }

    function showEnemies() {
        addLog('--- Oponentes Disponibles ---', 'system');
        for(const key in NPCS) {
            const npc = NPCS[key];
            addLog(`- ${npc.name} (Nivel ${npc.level}) [Comando: empezar ${key}]`, 'system');
        }
    }

    // --- Lógica de Combate ---
    function startCombat(npcKey) {
        if (player.inventory.length === 0) {
            addLog('No puedes luchar sin pociones. ¡Abre un cofre primero!', 'error');
            return;
        }
        
        const npcData = JSON.parse(JSON.stringify(NPCS[npcKey])); // Deep copy
        gameState.inCombat = true;
        gameState.currentEnemy = npcData;
        
        addLog(`¡Un ${npcData.name} aparece!`, 'combat');
        addLog(`--- COMIENZA EL COMBATE ---`, 'combat');
        promptPlayerTurn();
    }
    
    function promptPlayerTurn() {
        updateUI();
        addLog(`Es tu turno. HP: ${player.hp}/${player.maxHp}. Enemigo HP: ${gameState.currentEnemy.hp}/${gameState.currentEnemy.maxHp}.`, 'system');
        addLog("Escribe 'usar [nombre de pocion]' para atacar.", 'system');
    }

    function handleCombatCommand(command) {
        const parts = command.split(' ');
        if (parts[0] !== 'usar') {
            addLog("En combate, solo puedes 'usar [nombre de pocion]'.", 'error');
            return;
        }

        const potionName = parts.slice(1).join(' ');
        const potionIndex = player.inventory.findIndex(p => p.name.toLowerCase() === potionName);

        if (potionIndex === -1) {
            addLog(`No tienes la poción '${potionName}'. Revisa tu inventario.`, 'error');
            return;
        }

        const potion = player.inventory[potionIndex];
        player.inventory.splice(potionIndex, 1);
        addLog(`Usas ${potion.name}.`, 'player');

        // --- Turno del Jugador ---
        let turnResult = '';
        let damageDealt = 0;
        
        if (potion.name === 'Caldero Inestable') {
            addLog('El caldero burbujea y lanza 3 efectos...', 'combat');
            for (let i = 0; i < 3; i++) {
                const randomRarity = Math.random() < 0.7 ? 'comun' : 'raro';
                const randomPool = POTIONS[randomRarity];
                const randomPotion = randomPool[Math.floor(Math.random() * randomPool.length)];
                addLog(`Efecto de ${randomPotion.name}:`, 'combat');
                const result = randomPotion.effect(player, gameState.currentEnemy);
                if (randomPotion.baseDamage) gameState.currentEnemy.hp -= randomPotion.baseDamage;
                addLog(`> ${result}`, 'combat');
            }
        } else {
             // Daño base (si lo tiene)
            if (potion.baseDamage) {
                damageDealt += potion.baseDamage;
            }
            // Ejecutar efecto principal
            turnResult = potion.effect(player, gameState.currentEnemy);
             // Aplicar daño de efecto (si lo tiene, como fuego débil)
            if(turnResult.includes('Infliges')){
                damageDealt += parseInt(turnResult.match(/\d+/)[0]);
            }
        }

        // Aplicar daño de furia
        if (player.fury > 0 && damageDealt > 0) {
            gameState.currentEnemy.hp -= damageDealt; // Daño extra
            addLog(`¡Furia de Gigante duplica tu daño!`, 'player');
        }

        if (turnResult) addLog(turnResult, 'combat');
        
        // --- Comprobación post-turno del jugador ---
        if (gameState.currentEnemy.hp <= 0) {
            winCombat();
            return;
        }
        
        if (gameState.flee) {
            endCombat();
            addLog('¡Has escapado con éxito!', 'system');
            return;
        }

        if (gameState.extraTurn) {
            gameState.extraTurn = false;
            addLog("Gracias a la Brecha Temporal, actúas de nuevo.", "system");
            promptPlayerTurn();
        } else {
            setTimeout(enemyTurn, 1000); // Dar un respiro antes del turno enemigo
        }
    }

    function enemyTurn() {
        addLog(`--- Turno de ${gameState.currentEnemy.name} ---`, 'combat');
        const enemy = gameState.currentEnemy;
        
        // --- Efectos de estado del enemigo (antes de actuar) ---
        if (enemy.frozen > 0) {
            enemy.frozen--;
            addLog(`${enemy.name} está congelado y no puede actuar.`, 'combat');
            endTurn();
            return;
        }
        if(enemy.poison > 0) {
            const poisonDmg = 10;
            enemy.hp -= poisonDmg;
            enemy.poison--;
            addLog(`${enemy.name} sufre ${poisonDmg} de daño por veneno. Le quedan ${enemy.poison} turnos.`, 'combat');
            if (enemy.hp <= 0) {
                winCombat();
                return;
            }
        }

        // --- Ataque del enemigo ---
        // Atacar al clon primero si existe
        if (gameState.cloneHp > 0) {
            addLog(`El enemigo ataca a tu Espejismo.`, 'combat');
            gameState.cloneHp -= enemy.damage;
            if(gameState.cloneHp <= 0) {
                addLog('¡Tu Espejismo ha sido destruido!', 'combat');
                gameState.cloneHp = 0;
            } else {
                addLog(`Al Espejismo le quedan ${gameState.cloneHp} HP.`, 'combat');
            }
        } else {
            // Habilidad especial del enemigo
            if(enemy.ability) enemy.ability(enemy);

            // Calcular daño
            let damage = enemy.damage + (enemy.nextAttackBonus || 0);
            enemy.nextAttackBonus = 0; // Reset bonus
            
            // Reducción de defensa del enemigo (aumenta daño recibido por el jugador)
            if(enemy.defenseDebuff > 0) {
                damage += 5;
                enemy.defenseDebuff--;
            }

            // Aplicar daño al jugador
            if (player.dodge) {
                player.dodge = false;
                addLog('¡Esquivas el ataque del enemigo!', 'player');
            } else {
                 let damageTaken = damage;
                // Absorber con escudo primero
                if (player.shield > 0) {
                    const absorbed = Math.min(player.shield, damageTaken);
                    player.shield -= absorbed;
                    damageTaken -= absorbed;
                    addLog(`Tu escudo absorbe ${absorbed} de daño. Escudo restante: ${player.shield}`, 'player');
                }
                
                if (damageTaken > 0) {
                    player.hp -= damageTaken;
                    addLog(`${enemy.name} te ataca y te inflige ${damageTaken} de daño.`, 'combat');
                }
            }
        }

        // --- Comprobación post-turno del enemigo ---
        if (player.hp <= 0) {
            if (player.phoenixDown) {
                player.hp = Math.floor(player.maxHp * 0.5);
                player.phoenixDown = false;
                addLog('¡Caes, pero la Lágrima del Fénix te devuelve a la vida!', 'reward');
                endTurn();
            } else {
                loseCombat();
            }
        } else {
            endTurn();
        }
    }
    
    function endTurn() {
        // --- Mantenimiento de buffs/debuffs del jugador ---
        if (player.fury > 0) {
            player.fury--;
            if (player.fury === 0) addLog('La Furia de Gigante se desvanece.', 'player');
        }
        if (player.regen > 0) {
            const regenHp = 20;
            player.hp = Math.min(player.maxHp, player.hp + regenHp);
            player.regen--;
            addLog(`Regeneras ${regenHp} HP. Te quedan ${player.regen} turnos de regeneración.`, 'player');
        }
        
        promptPlayerTurn();
    }

    function endCombat() {
        gameState.inCombat = false;
        gameState.currentEnemy = null;
        gameState.flee = false;
        gameState.extraTurn = false;
        gameState.cloneHp = 0;
        // Resetear buffs de combate
        player.shield = 0;
        player.fury = 0;
        player.dodge = false;
        player.regen = 0;
    }

    function winCombat() {
        const enemy = gameState.currentEnemy;
        addLog(`¡Has derrotado a ${enemy.name}!`, 'reward');
        
        // Ganar XP
        player.xp += enemy.xp;
        addLog(`Ganas ${enemy.xp} XP.`, 'reward');
        
        // Subir de nivel
        if (player.xp >= LEVEL_XP[player.level - 1]) {
            player.level++;
            player.maxHp += 15;
            player.hp = player.maxHp; // Cura completa al subir de nivel
            addLog(`¡SUBES DE NIVEL! Ahora eres Nivel ${player.level}. Tu HP máximo aumenta a ${player.maxHp}.`, 'reward');
        } else {
            player.hp = player.maxHp; // Cura completa al ganar
        }

        // Recibir cofre
        player.chest = enemy.chest;
        addLog(`Has conseguido un Cofre de ${enemy.chest}.`, 'reward');
        
        endCombat();
        updateUI();
    }
    
    function loseCombat() {
        addLog('Has sido derrotado...', 'error');
        addLog('--- FIN DEL JUEGO ---', 'error');
        addLog("Escribe 'reiniciar' para volver a empezar.", 'system');
        gameState.inCombat = false; // Permite el comando reiniciar
    }


    // 5. INICIALIZACIÓN Y EVENT LISTENERS
    userInput.addEventListener('keydown', (e) => {
        if (e.key === 'Enter') {
            const command = userInput.value;
            if (command.toLowerCase().trim() === 'reiniciar') {
                resetGame();
            } else if (command.trim()) {
                handleCommand(command);
            }
            userInput.value = '';
        }
    });

    submitBtn.addEventListener('click', () => {
        const command = userInput.value;
        if (command.toLowerCase().trim() === 'reiniciar') {
            resetGame();
        } else if (command.trim()) {
            handleCommand(command);
        }
        userInput.value = '';
        userInput.focus();
    });

    // Iniciar el juego por primera vez
    resetGame();
    </script>
</body>
</html>
