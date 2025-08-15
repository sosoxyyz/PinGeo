<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo de Geografia Mundial</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ffc0cb, #e6f3ff);
            min-height: 100vh;
            color: #2c3e50;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .title {
            font-size: 2.5em;
            color: #ff69b4;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 10px;
            font-weight: 700;
        }

        .subtitle {
            font-size: 1.2em;
            color: #4169e1;
            margin-bottom: 20px;
            font-weight: 400;
        }

        .game-info {
            display: flex;
            justify-content: space-around;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .info-box {
            background: linear-gradient(45deg, #ff69b4, #87ceeb);
            color: white;
            padding: 15px 25px;
            border-radius: 15px;
            margin: 5px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            font-weight: 600;
            text-align: center;
            min-width: 120px;
        }

        .question-section {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .question {
            font-size: 1.8em;
            color: #ff1493;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .current-location {
            font-size: 2.2em;
            color: #4169e1;
            background: linear-gradient(45deg, #ffc0cb, #e6f3ff);
            padding: 15px 30px;
            border-radius: 15px;
            display: inline-block;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            font-weight: 700;
        }

        .map-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            text-align: center;
            margin-bottom: 20px;
        }

        .world-map {
            width: 100%;
            max-width: 900px;
            height: auto;
            border-radius: 15px;
            cursor: crosshair;
            border: 3px solid #ff69b4;
            transition: transform 0.3s ease;
        }

        .world-map:hover {
            transform: scale(1.02);
        }

        .controls {
            text-align: center;
            margin-bottom: 20px;
        }

        .btn {
            background: linear-gradient(45deg, #ff69b4, #87ceeb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            margin: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
            font-weight: 600;
            font-family: 'Poppins', sans-serif;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }

        .btn:active {
            transform: translateY(0);
        }

        .feedback {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            text-align: center;
            font-size: 1.2em;
            font-weight: 600;
        }

        .feedback.correct {
            color: #28a745;
            background: linear-gradient(45deg, #d4edda, #c3e6cb);
        }

        .feedback.incorrect {
            color: #dc3545;
            background: linear-gradient(45deg, #f8d7da, #f5c6cb);
        }

        .difficulty-selector {
            margin-bottom: 20px;
            text-align: center;
        }

        .difficulty-btn {
            background: linear-gradient(45deg, #87ceeb, #ffc0cb);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            margin: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            font-family: 'Poppins', sans-serif;
        }

        .difficulty-btn.active {
            background: linear-gradient(45deg, #ff69b4, #4169e1);
            transform: scale(1.1);
        }

        .click-indicator {
            position: absolute;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle, #ff69b4, #ff1493);
            border-radius: 50%;
            pointer-events: none;
            transform: translate(-50%, -50%);
            animation: clickPulse 0.6s ease-out;
            border: 3px solid white;
            box-shadow: 0 0 15px rgba(255, 105, 180, 0.8);
        }

        @keyframes clickPulse {
            0% {
                transform: translate(-50%, -50%) scale(0);
                opacity: 1;
            }
            100% {
                transform: translate(-50%, -50%) scale(2);
                opacity: 0;
            }
        }

        .credits {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            color: #ff69b4;
            font-weight: 600;
            margin-top: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .progress-bar {
            background: rgba(255, 255, 255, 0.3);
            height: 10px;
            border-radius: 5px;
            margin: 10px 0;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(45deg, #ff69b4, #87ceeb);
            height: 100%;
            transition: width 0.3s ease;
            border-radius: 5px;
        }

        @media (max-width: 768px) {
            .title {
                font-size: 2em;
            }
            
            .question {
                font-size: 1.4em;
            }
            
            .current-location {
                font-size: 1.6em;
                padding: 10px 20px;
            }
            
            .game-info {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1 class="title">🌍 Jogo de Geografia Mundial 🌍</h1>
            <p class="subtitle">Encontre a localização correta no mapa!</p>
            
            <div class="difficulty-selector">
                <button class="difficulty-btn active" onclick="setDifficulty('paises')">Países</button>
                <button class="difficulty-btn" onclick="setDifficulty('capitais')">Capitais</button>
                <button class="difficulty-btn" onclick="setDifficulty('cidades')">Cidades Famosas</button>
            </div>
        </div>

        <div class="game-info">
            <div class="info-box">
                <div>Pontuação: <span id="score">0</span></div>
            </div>
            <div class="info-box">
                <div>Pergunta: <span id="questionNumber">1</span>/10</div>
            </div>
            <div class="info-box">
                <div>Acertos: <span id="correct">0</span></div>
            </div>
            <div class="info-box">
                <div>Erros: <span id="incorrect">0</span></div>
            </div>
        </div>

        <div class="progress-bar">
            <div class="progress-fill" id="progressFill" style="width: 10%"></div>
        </div>

        <div class="question-section">
            <div class="question">Onde fica:</div>
            <div class="current-location" id="currentLocation">Brasil</div>
        </div>

        <div class="map-container">
            <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/bcc53c8f-5017-4dbf-b979-ae05362e140f.png" 
                 alt="Detailed world map showing all continents, countries, and major geographical features with clear country borders and labels for an interactive geography game" 
                 class="world-map" 
                 id="worldMap"
                 onclick="handleMapClick(event)">
        </div>

        <div class="controls">
            <button class="btn" onclick="nextQuestion()">Próxima Pergunta</button>
            <button class="btn" onclick="resetGame()">Reiniciar Jogo</button>
            <button class="btn" onclick="showHint()">Dica</button>
        </div>

        <div class="feedback" id="feedback" style="display: none;">
            Clique no mapa para começar!
        </div>

        <div class="credits">
            Desenvolvido por Alice Ribeiro e Sofia Aguiar
        </div>
    </div>

    <script>
        class GeographyGame {
            constructor() {
                this.score = 0;
                this.currentQuestion = 1;
                this.totalQuestions = 10;
                this.correctAnswers = 0;
                this.incorrectAnswers = 0;
                this.currentDifficulty = 'paises';
                this.currentLocationData = null;
                this.gameLocations = {
                    paises: [
                        { name: 'Brasil', region: 'América do Sul', hint: 'Maior país da América do Sul' },
                        { name: 'França', region: 'Europa', hint: 'País da Torre Eiffel' },
                        { name: 'Japão', region: 'Ásia', hint: 'Terra do Sol Nascente' },
                        { name: 'Austrália', region: 'Oceania', hint: 'Continente-país' },
                        { name: 'Egito', region: 'África', hint: 'Terra das pirâmides' },
                        { name: 'Canadá', region: 'América do Norte', hint: 'Segundo maior país do mundo' },
                        { name: 'Índia', region: 'Ásia', hint: 'Segundo país mais populoso' },
                        { name: 'Argentina', region: 'América do Sul', hint: 'Terra do tango' },
                        { name: 'Rússia', region: 'Europa/Ásia', hint: 'Maior país do mundo' },
                        { name: 'Reino Unido', region: 'Europa', hint: 'Inglaterra, Escócia, País de Gales' },
                        { name: 'China', region: 'Ásia', hint: 'País mais populoso do mundo' },
                        { name: 'Estados Unidos', region: 'América do Norte', hint: 'Terra da liberdade' },
                        { name: 'Alemanha', region: 'Europa', hint: 'Coração da Europa' },
                        { name: 'Itália', region: 'Europa', hint: 'País em forma de bota' },
                        { name: 'México', region: 'América do Norte', hint: 'Terra dos astecas' }
                    ],
                    capitais: [
                        { name: 'Brasília', region: 'Brasil', hint: 'Capital planejada do Brasil' },
                        { name: 'Paris', region: 'França', hint: 'Cidade Luz' },
                        { name: 'Tóquio', region: 'Japão', hint: 'Maior metrópole do mundo' },
                        { name: 'Canberra', region: 'Austrália', hint: 'Capital da Austrália' },
                        { name: 'Cairo', region: 'Egito', hint: 'Próxima às pirâmides' },
                        { name: 'Ottawa', region: 'Canadá', hint: 'Capital do Canadá' },
                        { name: 'Nova Delhi', region: 'Índia', hint: 'Capital da Índia' },
                        { name: 'Buenos Aires', region: 'Argentina', hint: 'Capital do tango' },
                        { name: 'Moscou', region: 'Rússia', hint: 'Praça Vermelha' },
                        { name: 'Londres', region: 'Reino Unido', hint: 'Big Ben' },
                        { name: 'Pequim', region: 'China', hint: 'Cidade Proibida' },
                        { name: 'Washington D.C.', region: 'Estados Unidos', hint: 'Casa Branca' },
                        { name: 'Berlim', region: 'Alemanha', hint: 'Queda do muro' },
                        { name: 'Roma', region: 'Itália', hint: 'Cidade Eterna' },
                        { name: 'Cidade do México', region: 'México', hint: 'Maior cidade do México' }
                    ],
                    cidades: [
                        { name: 'Rio de Janeiro', region: 'Brasil', hint: 'Cristo Redentor' },
                        { name: 'Nova York', region: 'Estados Unidos', hint: 'Big Apple' },
                        { name: 'Barcelona', region: 'Espanha', hint: 'Sagrada Família' },
                        { name: 'Sydney', region: 'Austrália', hint: 'Opera House' },
                        { name: 'Mumbai', region: 'Índia', hint: 'Bollywood' },
                        { name: 'Dubai', region: 'Emirados Árabes', hint: 'Burj Khalifa' },
                        { name: 'Istambul', region: 'Turquia', hint: 'Entre Europa e Ásia' },
                        { name: 'São Francisco', region: 'Estados Unidos', hint: 'Golden Gate' },
                        { name: 'Veneza', region: 'Itália', hint: 'Cidade dos canais' },
                        { name: 'Amsterdã', region: 'Holanda', hint: 'Cidade das bicicletas' },
                        { name: 'Singapura', region: 'Singapura', hint: 'Cidade-estado asiática' },
                        { name: 'Cape Town', region: 'África do Sul', hint: 'Montanha da Mesa' },
                        { name: 'Machu Picchu', region: 'Peru', hint: 'Cidade perdida dos Incas' },
                        { name: 'Petra', region: 'Jordânia', hint: 'Cidade rosa no deserto' },
                        { name: 'Santorini', region: 'Grécia', hint: 'Ilha com casas brancas' }
                    ]
                };
                this.usedLocations = [];
                this.init();
            }

            init() {
                this.updateDisplay();
                this.loadNewLocation();
                this.showFeedback('Clique no mapa para indicar a localização!', '');
            }

            setDifficulty(difficulty) {
                this.currentDifficulty = difficulty;
                this.resetGame();
                
                // Update active button
                document.querySelectorAll('.difficulty-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                event.target.classList.add('active');
            }

            loadNewLocation() {
                const locations = this.gameLocations[this.currentDifficulty];
                const availableLocations = locations.filter(loc => !this.usedLocations.includes(loc.name));
                
                if (availableLocations.length === 0) {
                    this.usedLocations = [];
                }
                
                const randomIndex = Math.floor(Math.random() * availableLocations.length);
                this.currentLocationData = availableLocations[randomIndex];
                this.usedLocations.push(this.currentLocationData.name);
                
                document.getElementById('currentLocation').textContent = this.currentLocationData.name;
            }

            handleMapClick(event) {
                const map = event.target;
                const rect = map.getBoundingClientRect();
                const x = event.clientX - rect.left;
                const y = event.clientY - rect.top;
                
                // Create click indicator
                this.createClickIndicator(event.clientX, event.clientY);
                
                // Simple scoring based on map regions (this is a simplified version)
                const isCorrect = this.checkAnswer(x, y, map.offsetWidth, map.offsetHeight);
                
                if (isCorrect) {
                    this.score += 10;
                    this.correctAnswers++;
                    this.showFeedback(`Parabéns! Você acertou!`, 'correct');
                    
                    // Confetti effect
                    this.createConfetti();
                } else {
                    this.incorrectAnswers++;
                    this.showFeedback(`Ops! A resposta correta seria na região: ${this.currentLocationData.region}`, 'incorrect');
                }
                
                this.updateDisplay();
                
                setTimeout(() => {
                    if (this.currentQuestion < this.totalQuestions) {
                        this.nextQuestion();
                    } else {
                        this.endGame();
                    }
                }, 2000);
            }

            checkAnswer(clickX, clickY, mapWidth, mapHeight) {
                // Simplified region detection based on map coordinates
                const regionMap = {
                    'América do Norte': { x: [0, 0.35], y: [0, 0.45] },
                    'América do Sul': { x: [0.2, 0.45], y: [0.45, 1] },
                    'Europa': { x: [0.45, 0.65], y: [0, 0.45] },
                    'África': { x: [0.45, 0.7], y: [0.3, 0.9] },
                    'Ásia': { x: [0.65, 1], y: [0, 0.7] },
                    'Oceania': { x: [0.75, 1], y: [0.7, 1] },
                    'Brasil': { x: [0.25, 0.4], y: [0.5, 0.8] },
                    'França': { x: [0.48, 0.52], y: [0.25, 0.35] },
                    'Japão': { x: [0.85, 0.9], y: [0.25, 0.4] },
                    'Austrália': { x: [0.8, 0.95], y: [0.75, 0.95] }
                };

                const clickXPercent = clickX / mapWidth;
                const clickYPercent = clickY / mapHeight;
                
                const targetRegion = regionMap[this.currentLocationData.region] || regionMap[this.currentLocationData.name];
                
                if (targetRegion) {
                    const withinX = clickXPercent >= targetRegion.x[0] && clickXPercent <= targetRegion.x[1];
                    const withinY = clickYPercent >= targetRegion.y[0] && clickYPercent <= targetRegion.y[1];
                    return withinX && withinY;
                }
                
                // Fallback: random chance for unknown regions
                return Math.random() > 0.7;
            }

            createClickIndicator(x, y) {
                const indicator = document.createElement('div');
                indicator.className = 'click-indicator';
                indicator.style.left = x + 'px';
                indicator.style.top = y + 'px';
                document.body.appendChild(indicator);
                
                setTimeout(() => {
                    document.body.removeChild(indicator);
                }, 600);
            }

            createConfetti() {
                for (let i = 0; i < 20; i++) {
                    setTimeout(() => {
                        const confetti = document.createElement('div');
                        confetti.style.position = 'fixed';
                        confetti.style.left = Math.random() * window.innerWidth + 'px';
                        confetti.style.top = '-10px';
                        confetti.style.width = '10px';
                        confetti.style.height = '10px';
                        confetti.style.background = Math.random() > 0.5 ? '#ff69b4' : '#87ceeb';
                        confetti.style.pointerEvents = 'none';
                        confetti.style.borderRadius = '50%';
                        confetti.style.animation = 'fall 2s linear forwards';
                        
                        document.body.appendChild(confetti);
                        
                        setTimeout(() => {
                            if (document.body.contains(confetti)) {
                                document.body.removeChild(confetti);
                            }
                        }, 2000);
                    }, i * 100);
                }
            }

            showFeedback(message, type) {
                const feedback = document.getElementById('feedback');
                feedback.textContent = message;
                feedback.className = `feedback ${type}`;
                feedback.style.display = 'block';
            }

            showHint() {
                if (this.currentLocationData) {
                    this.showFeedback(`Dica: ${this.currentLocationData.hint}`, '');
                }
            }

            nextQuestion() {
                if (this.currentQuestion < this.totalQuestions) {
                    this.currentQuestion++;
                    this.loadNewLocation();
                    this.updateDisplay();
                    this.showFeedback('Clique no mapa para indicar a localização!', '');
                }
            }

            updateDisplay() {
                document.getElementById('score').textContent = this.score;
                document.getElementById('questionNumber').textContent = this.currentQuestion;
                document.getElementById('correct').textContent = this.correctAnswers;
                document.getElementById('incorrect').textContent = this.incorrectAnswers;
                
                const progress = (this.currentQuestion / this.totalQuestions) * 100;
                document.getElementById('progressFill').style.width = progress + '%';
            }

            endGame() {
                const percentage = Math.round((this.correctAnswers / this.totalQuestions) * 100);
                let message = `Jogo finalizado!\n\n`;
                message += `Pontuação final: ${this.score}\n`;
                message += `Acertos: ${this.correctAnswers}/${this.totalQuestions} (${percentage}%)\n\n`;
                
                if (percentage >= 80) {
                    message += `Excelente! Você é um expert em geografia!`;
                } else if (percentage >= 60) {
                    message += `Muito bem! Você tem um bom conhecimento geográfico!`;
                } else if (percentage >= 40) {
                    message += `Não foi mal! Continue praticando!`;
                } else {
                    message += `Precisa estudar mais geografia! Não desista!`;
                }
                
                this.showFeedback(message, percentage >= 60 ? 'correct' : 'incorrect');
                
                setTimeout(() => {
                    if (confirm('Deseja jogar novamente?')) {
                        this.resetGame();
                    }
                }, 3000);
            }

            resetGame() {
                this.score = 0;
                this.currentQuestion = 1;
                this.correctAnswers = 0;
                this.incorrectAnswers = 0;
                this.usedLocations = [];
                this.loadNewLocation();
                this.updateDisplay();
                this.showFeedback('Novo jogo iniciado! Boa sorte!', '');
            }
        }

        // CSS for falling animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fall {
                0% { transform: translateY(-10px) rotate(0deg); opacity: 1; }
                100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
            }
        `;
        document.head.appendChild(style);

        // Initialize game
        let game;
        
        window.onload = function() {
            game = new GeographyGame();
        };

        // Global functions for HTML onclick events
        function handleMapClick(event) {
            game.handleMapClick(event);
        }

        function nextQuestion() {
            game.nextQuestion();
        }

        function resetGame() {
            game.resetGame();
        }

        function showHint() {
            game.showHint();
        }

        function setDifficulty(difficulty) {
            game.setDifficulty(difficulty);
        }
    </script>
</body>
</html>


