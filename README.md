<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tebak Unsur - Quiz Kimia Interaktif</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .game-container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            padding: 30px;
            max-width: 600px;
            width: 100%;
            text-align: center;
            color: white;
        }

        .title {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #FFD700, #FFA500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 30px;
            opacity: 0.8;
        }

        .stats {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 15px;
        }

        .timer-container {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }

        .timer-circle {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: conic-gradient(#FFD700 0deg, #FFD700 0deg, rgba(255, 255, 255, 0.2) 0deg);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px;
            position: relative;
            transition: background 0.1s ease;
        }

        .timer-text {
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }

        .timer-label {
            font-size: 1rem;
            color: rgba(255, 255, 255, 0.8);
        }

        .timer-warning {
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .timer-expired {
            background: conic-gradient(#ff4444 360deg, #ff4444 360deg) !important;
        }

        .stat-item {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #FFD700;
        }

        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }

        .question-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .question-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #FFD700;
        }

        .hints-container {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: left;
        }

        .hint-item {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
            padding: 8px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 8px;
            opacity: 0;
            animation: fadeIn 0.5s ease-in-out forwards;
        }

        @keyframes fadeIn {
            to { opacity: 1; }
        }

        .hint-icon {
            width: 20px;
            height: 20px;
            margin-right: 10px;
            color: #FFD700;
        }

        .input-container {
            margin-bottom: 20px;
        }

        .answer-input {
            width: 100%;
            padding: 15px;
            font-size: 1.1rem;
            border: none;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            text-align: center;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .answer-input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .answer-input:focus {
            outline: none;
            border-color: #FFD700;
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
        }

        .btn {
            padding: 12px 25px;
            font-size: 1rem;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            margin: 5px;
        }

        .btn-primary {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(45deg, #FFD700, #FFA500);
            color: #333;
        }

        .btn-danger {
            background: linear-gradient(45deg, #f44336, #da190b);
            color: white;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .result-card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .result-correct {
            border-left: 5px solid #4CAF50;
            background: rgba(76, 175, 80, 0.1);
        }

        .result-incorrect {
            border-left: 5px solid #f44336;
            background: rgba(244, 67, 54, 0.1);
        }

        .result-icon {
            font-size: 3rem;
            margin-bottom: 10px;
        }

        .element-info {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            padding: 15px;
            margin-top: 15px;
            text-align: left;
        }

        .element-info h4 {
            color: #FFD700;
            margin-bottom: 10px;
        }

        .element-property {
            margin-bottom: 5px;
            display: flex;
            justify-content: space-between;
        }

        .hidden {
            display: none;
        }

        .start-screen {
            text-align: center;
        }

        .start-screen .game-icon {
            font-size: 6rem;
            margin-bottom: 20px;
        }

        .instructions {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            text-align: left;
        }

        .instructions h3 {
            color: #FFD700;
            margin-bottom: 15px;
            text-align: center;
        }

        .instructions ul {
            list-style: none;
            padding: 0;
        }

        .instructions li {
            margin-bottom: 8px;
            padding-left: 20px;
            position: relative;
        }

        .instructions li::before {
            content: "⚛️";
            position: absolute;
            left: 0;
        }

        @media (max-width: 600px) {
            .game-container {
                padding: 20px;
                margin: 10px;
            }

            .title {
                font-size: 2rem;
            }

            .stats {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <!-- Start Screen -->
        <div id="startScreen" class="start-screen">
            <div class="game-icon">⚛️</div>
            <h1 class="title">Tebak Unsur</h1>
            <p class="subtitle">Quiz Interaktif Kimia</p>
            
            <div class="instructions">
                <h3>💡 Tips Bermain:</h3>
                <ul>
                    <li>Setiap pertanyaan diberi waktu 60 detik</li>
                    <li>Baca petunjuk pertama dengan cermat sebelum menebak</li>
                    <li>Tebak nama unsur dalam bahasa Indonesia</li>
                    <li>Gunakan tombol hint untuk petunjuk tambahan</li>
                    <li>Kumpulkan skor setinggi-tingginya!</li>
                </ul>
            </div>

            <div class="instructions">
                <h3>📝 Cara Menjawab:</h3>
                <ul>
                    <li>Ketik nama unsur dalam Bahasa Indonesia (contoh: "Emas" bukan "Gold")
                    <li>Huruf besar/kecil tidak berpengaruh
                    <li>Tekan Enter atau klik tombol "Jawab"
                    <li>Jawaban harus tepat dan lengkap
                </ul>
            </div>

            <div class="instructions">
                <h3>🎮 Fitur Game:</h3>
                <ul>
                    <li><strong>Petunjuk Bertahap:</strong> 4 petunjuk per unsur</li>
                    <li><strong>10 Unsur Kimia:</strong> Berbagai tingkat kesulitan</li>
                    <li><strong>Sistem Skor:</strong> Melacak performa Anda</li>
                    <li><strong>Hint System:</strong> Bantuan tambahan tersedia</li>
                    <li><strong>Reset Game:</strong> Mulai ulang dari awal</li>
                    <li><strong>Pertanyaan Selanjutnya:</strong> Lanjut ke soal baru</li>
                </ul>
            </div>

            <button class="btn btn-primary" onclick="startGame()">🚀 Mulai Quiz</button>
        </div>

        <!-- Game Screen -->
        <div id="gameScreen" class="hidden">
            <h1 class="title">⚛️ Tebak Unsur!</h1>
            
            <div class="stats">
                <div class="stat-item">
                    <div class="stat-number" id="score">0</div>
                    <div class="stat-label">Skor</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="totalQuestions">0</div>
                    <div class="stat-label">Pertanyaan</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="accuracy">0%</div>
                    <div class="stat-label">Akurasi</div>
                </div>
            </div>

            <!-- Timer Section -->
            <div class="timer-container">
                <div class="timer-circle" id="timerCircle">
                    <div class="timer-text" id="timerText">60</div>
                </div>
                <div class="timer-label">Detik Tersisa</div>
            </div>

            <div class="question-card">
                <h2 class="question-title">Unsur Apakah Ini?</h2>
                
                <div class="hints-container" id="hintsContainer">
                    <!-- Hints will be populated here -->
                </div>

                <button class="btn btn-secondary" id="hintBtn" onclick="showNextHint()">
                    💡 Tampilkan Hint Lainnya
                </button>
            </div>

            <!-- Answer Input -->
            <div id="answerSection">
                <div class="input-container">
                    <input type="text" class="answer-input" id="answerInput" 
                           placeholder="Masukkan nama unsur..." 
                           onkeypress="handleKeyPress(event)">
                </div>
                <button class="btn btn-primary" onclick="checkAnswer()">✓ Jawab</button>
            </div>

            <!-- Result Section -->
            <div id="resultSection" class="hidden">
                <div class="result-card" id="resultCard">
                    <div class="result-icon" id="resultIcon"></div>
                    <h3 id="resultText"></h3>
                    <div class="element-info" id="elementInfo">
                        <!-- Element information will be populated here -->
                    </div>
                </div>
                <button class="btn btn-primary" onclick="nextQuestion()">➡️ Pertanyaan Selanjutnya</button>
            </div>

            <div style="margin-top: 20px;">
                <button class="btn btn-danger" onclick="resetGame()">🔄 Reset Game</button>
            </div>
        </div>
    </div>

    <script>
        // Game data
        const elements = [
            {
                name: "Hidrogen",
                symbol: "H",
                atomicNumber: 1,
                group: "Golongan 1 (Alkali)",
                hints: [
                    "🌟 Unsur paling ringan di alam semesta",
                    "🔤 Simbol: H",
                    "🔢 Nomor atom: 1",
                    "⚗️ Golongan 1, berbentuk gas"
                ]
            },
            {
                name: "Helium",
                symbol: "He",
                atomicNumber: 2,
                group: "Golongan 18 (Gas Mulia)",
                hints: [
                    "🎈 Gas mulia yang membuat balon terbang",
                    "🔤 Simbol: He",
                    "🔢 Nomor atom: 2",
                    "⚗️ Gas mulia yang tidak reaktif"
                ]
            },
            {
                name: "Karbon",
                symbol: "C",
                atomicNumber: 6,
                group: "Golongan 14",
                hints: [
                    "💎 Dasar kehidupan organik, membentuk berlian",
                    "🔤 Simbol: C",
                    "🔢 Nomor atom: 6",
                    "⚗️ Golongan 14, bisa jadi berlian atau grafit"
                ]
            },
            {
                name: "Oksigen",
                symbol: "O",
                atomicNumber: 8,
                group: "Golongan 16",
                hints: [
                    "🫁 Gas yang kita hirup untuk bernapas",
                    "🔤 Simbol: O",
                    "🔢 Nomor atom: 8",
                    "💧 Membentuk air bersama hidrogen (H₂O)"
                ]
            },
            {
                name: "Sodium",
                symbol: "Na",
                atomicNumber: 11,
                group: "Golongan 1 (Alkali)",
                hints: [
                    "🧂 Logam alkali, komponen utama garam dapur",
                    "🔤 Simbol: Na",
                    "🔢 Nomor atom: 11",
                    "⚗️ Logam yang sangat reaktif dengan air"
                ]
            },
            {
                name: "Klorin",
                symbol: "Cl",
                atomicNumber: 17,
                group: "Golongan 17 (Halogen)",
                hints: [
                    "🏊 Gas hijau, digunakan untuk disinfektan kolam",
                    "🔤 Simbol: Cl",
                    "🔢 Nomor atom: 17",
                    "⚗️ Halogen yang sangat reaktif dan berbahaya"
                ]
            },
            {
                name: "Besi",
                symbol: "Fe",
                atomicNumber: 26,
                group: "Golongan 8 (Logam Transisi)",
                hints: [
                    "🔨 Logam yang mudah berkarat, bahan baja",
                    "🔤 Simbol: Fe",
                    "🔢 Nomor atom: 26",
                    "⚗️ Logam transisi, komponen utama baja"
                ]
            },
            {
                name: "Emas",
                symbol: "Au",
                atomicNumber: 79,
                group: "Golongan 11 (Logam Transisi)",
                hints: [
                    "💰 Logam mulia berwarna kuning, untuk perhiasan",
                    "🔤 Simbol: Au",
                    "🔢 Nomor atom: 79",
                    "⚗️ Logam mulia yang tidak mudah berkarat"
                ]
            },
            {
                name: "Perak",
                symbol: "Ag",
                atomicNumber: 47,
                group: "Golongan 11 (Logam Transisi)",
                hints: [
                    "🥈 Logam mengkilap putih, konduktor terbaik",
                    "🔤 Simbol: Ag",
                    "🔢 Nomor atom: 47",
                    "⚗️ Konduktor listrik dan panas terbaik"
                ]
            },
            {
                name: "Kalsium",
                symbol: "Ca",
                atomicNumber: 20,
                group: "Golongan 2 (Alkali Tanah)",
                hints: [
                    "🦴 Mineral penting untuk tulang dan gigi",
                    "🔤 Simbol: Ca",
                    "🔢 Nomor atom: 20",
                    "🥛 Banyak ditemukan dalam susu dan produk susu"
                ]
            }
        ];

        // Game state
        let currentElement = null;
        let score = 0;
        let totalQuestions = 0;
        let currentHintIndex = 0;
        let gameStarted = false;
        let timeLeft = 60;
        let timerInterval = null;

        // DOM elements
        const startScreen = document.getElementById('startScreen');
        const gameScreen = document.getElementById('gameScreen');
        const hintsContainer = document.getElementById('hintsContainer');
        const hintBtn = document.getElementById('hintBtn');
        const answerInput = document.getElementById('answerInput');
        const answerSection = document.getElementById('answerSection');
        const resultSection = document.getElementById('resultSection');
        const resultCard = document.getElementById('resultCard');
        const resultIcon = document.getElementById('resultIcon');
        const resultText = document.getElementById('resultText');
        const elementInfo = document.getElementById('elementInfo');
        const timerCircle = document.getElementById('timerCircle');
        const timerText = document.getElementById('timerText');

        function startGame() {
            startScreen.classList.add('hidden');
            gameScreen.classList.remove('hidden');
            gameStarted = true;
            generateNewQuestion();
        }

        function generateNewQuestion() {
            // Reset UI
            answerSection.classList.remove('hidden');
            resultSection.classList.add('hidden');
            answerInput.value = '';
            answerInput.focus();
            
            // Reset timer
            timeLeft = 60;
            updateTimerDisplay();
            startTimer();
            
            // Select random element
            currentElement = elements[Math.floor(Math.random() * elements.length)];
            currentHintIndex = 0;
            
            // Show first hint
            showHints();
            updateHintButton();
        }

        function startTimer() {
            clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 10) {
                    timerCircle.classList.add('timer-warning');
                } else {
                    timerCircle.classList.remove('timer-warning');
                }
                
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    timeExpired();
                }
            }, 1000);
        }

        function stopTimer() {
            clearInterval(timerInterval);
            timerCircle.classList.remove('timer-warning');
        }

        function updateTimerDisplay() {
            timerText.textContent = timeLeft;
            const percentage = (timeLeft / 60) * 100;
            const degrees = (percentage / 100) * 360;
            
            if (timeLeft <= 0) {
                timerCircle.classList.add('timer-expired');
                timerCircle.style.background = 'conic-gradient(#ff4444 360deg, #ff4444 360deg)';
            } else {
                timerCircle.classList.remove('timer-expired');
                timerCircle.style.background = `conic-gradient(#FFD700 ${degrees}deg, rgba(255, 255, 255, 0.2) ${degrees}deg)`;
            }
        }

        function timeExpired() {
            totalQuestions++;
            updateStats();
            showResult(false, true); // false = incorrect, true = time expired
        }

        function showHints() {
            hintsContainer.innerHTML = '';
            for (let i = 0; i <= currentHintIndex; i++) {
                const hintDiv = document.createElement('div');
                hintDiv.className = 'hint-item';
                hintDiv.innerHTML = `
                    <span class="hint-icon">💡</span>
                    <span>${currentElement.hints[i]}</span>
                `;
                hintsContainer.appendChild(hintDiv);
            }
        }

        function showNextHint() {
            if (currentHintIndex < currentElement.hints.length - 1) {
                currentHintIndex++;
                showHints();
                updateHintButton();
            }
        }

        function updateHintButton() {
            const remainingHints = currentElement.hints.length - currentHintIndex - 1;
            if (remainingHints > 0) {
                hintBtn.innerHTML = `💡 Tampilkan Hint Lainnya (${remainingHints} tersisa)`;
                hintBtn.disabled = false;
            } else {
                hintBtn.innerHTML = `💡 Semua Hint Ditampilkan`;
                hintBtn.disabled = true;
            }
        }

        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                checkAnswer();
            }
        }

        function checkAnswer() {
            const userAnswer = answerInput.value.trim();
            if (!userAnswer) return;

            const isCorrect = userAnswer.toLowerCase() === currentElement.name.toLowerCase();
            
            // Update stats
            totalQuestions++;
            if (isCorrect) score++;
            
            updateStats();
            showResult(isCorrect);
        }

        function showResult(isCorrect) {
            answerSection.classList.add('hidden');
            resultSection.classList.remove('hidden');
            
            if (isCorrect) {
                resultCard.className = 'result-card result-correct';
                resultIcon.textContent = '✅';
                resultText.textContent = 'Benar! Hebat!';
            } else {
                resultCard.className = 'result-card result-incorrect';
                resultIcon.textContent = '❌';
                resultText.textContent = 'Salah! Coba lagi next time!';
            }

            // Show element information
            elementInfo.innerHTML = `
                <h4>📋 Informasi Unsur:</h4>
                <div class="element-property">
                    <span><strong>Nama:</strong></span>
                    <span>${currentElement.name}</span>
                </div>
                <div class="element-property">
                    <span><strong>Simbol:</strong></span>
                    <span>${currentElement.symbol}</span>
                </div>
                <div class="element-property">
                    <span><strong>Nomor Atom:</strong></span>
                    <span>${currentElement.atomicNumber}</span>
                </div>
                <div class="element-property">
                    <span><strong>Golongan:</strong></span>
                    <span>${currentElement.group}</span>
                </div>
            `;
        }

        function nextQuestion() {
            generateNewQuestion();
        }

        function updateStats() {
            document.getElementById('score').textContent = score;
            document.getElementById('totalQuestions').textContent = totalQuestions;
            const accuracy = totalQuestions > 0 ? Math.round((score / totalQuestions) * 100) : 0;
            document.getElementById('accuracy').textContent = accuracy + '%';
        }

        function resetGame() {
            score = 0;
            totalQuestions = 0;
            currentHintIndex = 0;
            stopTimer();
            updateStats();
            startScreen.classList.remove('hidden');
            gameScreen.classList.add('hidden');
            gameStarted = false;
        }

        // Initial3ize the game
        updateStats();
    </script>
</body>
</html>
