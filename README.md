<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Історія України: Minecraft Edition</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

        :root {
            --mc-dirt: #5d4037; /* Brown */
            --mc-grass: #4caf50; /* Green */
            --mc-stone: #757575; /* Grey */
            --mc-text: #ffffff;
            --mc-btn-bg: #bdbdbd;
            --mc-btn-shadow: #565656;
            --mc-btn-border: #000;
            --heart: #f44336;
        }

        body {
            font-family: 'VT323', monospace;
            background-color: #1a1a1a;
            background-image: repeating-linear-gradient(45deg, #222 25%, transparent 25%, transparent 75%, #222 75%, #222), repeating-linear-gradient(45deg, #222 25%, #1a1a1a 25%, #1a1a1a 75%, #222 75%, #222);
            background-position: 0 0, 10px 10px;
            background-size: 20px 20px;
            color: var(--mc-text);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            text-align: center;
            user-select: none;
        }

        .game-container {
            width: 90%;
            max-width: 600px;
            background-color: rgba(0, 0, 0, 0.7);
            border: 4px solid #fff;
            padding: 20px;
            box-shadow: 0 0 20px rgba(0,0,0,0.8);
            position: relative;
        }

        h1 {
            font-size: 3rem;
            color: #ffeb3b;
            text-shadow: 4px 4px 0 #3e2723;
            margin-bottom: 10px;
            line-height: 1;
        }

        .subtitle {
            color: #aaa;
            margin-bottom: 30px;
            font-size: 1.5rem;
        }

        /* Stats Bar */
        .stats-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0,0,0,0.5);
            padding: 10px;
            border: 2px solid #555;
            margin-bottom: 20px;
            font-size: 1.5rem;
        }

        .hearts {
            color: var(--heart);
            text-shadow: 2px 2px 0 #000;
            letter-spacing: 5px;
        }

        .xp-bar-container {
            flex-grow: 1;
            height: 20px;
            background: #333;
            border: 2px solid #fff;
            margin: 0 15px;
            position: relative;
        }

        .xp-bar-fill {
            height: 100%;
            background: linear-gradient(to right, #4caf50, #81c784);
            width: 0%;
            transition: width 0.3s;
        }

        .xp-text {
            position: absolute;
            width: 100%;
            text-align: center;
            top: -2px;
            font-size: 1rem;
            text-shadow: 1px 1px 0 #000;
        }

        /* Question Area */
        .question-box {
            background-color: rgba(60, 60, 60, 0.9);
            border: 4px solid var(--mc-stone);
            padding: 20px;
            margin-bottom: 20px;
            font-size: 1.8rem;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }

        .period-label {
            font-size: 1.2rem;
            color: #4fc3f7;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        /* Buttons */
        .options-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .mc-btn {
            background-color: #7f8c8d;
            border: 4px solid;
            border-color: #bdc3c7 #2c3e50 #2c3e50 #bdc3c7;
            color: #fff;
            padding: 15px;
            font-family: 'VT323', monospace;
            font-size: 1.8rem;
            cursor: pointer;
            text-shadow: 2px 2px 0 #000;
            transition: transform 0.1s;
            position: relative;
        }

        .mc-btn:active {
            transform: scale(0.98);
            border-color: #2c3e50 #bdc3c7 #bdc3c7 #2c3e50;
        }

        .mc-btn:hover {
            background-color: #95a5a6;
        }

        .mc-btn.correct {
            background-color: #4caf50;
            border-color: #81c784 #1b5e20 #1b5e20 #81c784;
        }

        .mc-btn.wrong {
            background-color: #f44336;
            border-color: #e57373 #b71c1c #b71c1c #e57373;
            animation: shake 0.5s;
        }

        /* Start & End Screens */
        .screen {
            display: none;
        }
        
        .screen.active {
            display: block;
        }

        .start-btn {
            width: 100%;
            margin-top: 20px;
            background-color: #4caf50;
            border-color: #81c784 #1b5e20 #1b5e20 #81c784;
        }

        .item-icon {
            width: 64px;
            height: 64px;
            image-rendering: pixelated;
            margin: 10px auto;
            display: block;
        }

        /* Animations */
        @keyframes shake {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(3px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(3px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(1px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
        }

        .notification {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            background: #fff;
            color: #000;
            padding: 5px 10px;
            border: 2px solid #000;
            font-size: 1.2rem;
            display: none;
            z-index: 10;
        }

        @media (max-width: 500px) {
            .options-grid {
                grid-template-columns: 1fr;
            }
            h1 {
                font-size: 2rem;
            }
            .game-container {
                width: 95%;
                padding: 10px;
            }
        }
    </style>
</head>
<body>

    <div class="game-container">
        <!-- Start Screen -->
        <div id="start-screen" class="screen active">
            <h1>ІСТОРІЯ КРАФТ</h1>
            <p class="subtitle">Квест-вікторина для 7 класу</p>
            
            <div style="background: rgba(0,0,0,0.3); padding: 15px; margin-bottom: 20px; text-align: left; font-size: 1.2rem;">
                <p>⛏️ <b>Місія:</b> Побудувати хронологію України.</p>
                <p>❤️ <b>Життя:</b> У тебе є 3 серця.</p>
                <p>🧟 <b>Обережно:</b> Помилка розбудить Кріпера!</p>
            </div>

            <button class="mc-btn start-btn" onclick="startGame()">ПОЧАТИ ГРУ</button>
        </div>

        <!-- Game Screen -->
        <div id="game-screen" class="screen">
            <div class="notification" id="notification">Скрафчено!</div>
            
            <div class="stats-bar">
                <div class="hearts" id="hearts-display">❤️❤️❤️</div>
                <div class="xp-bar-container">
                    <div class="xp-bar-fill" id="xp-fill"></div>
                    <div class="xp-text" id="level-display">Рівень 1</div>
                </div>
            </div>

            <div class="question-box">
                <div class="period-label" id="period-label">Раннє Середньовіччя</div>
                <div id="question-text">Питання з'явиться тут...</div>
            </div>

            <div class="options-grid" id="options-container">
                <!-- Buttons generated by JS -->
            </div>
        </div>

        <!-- End Screen -->
        <div id="end-screen" class="screen">
            <h1 id="end-title">ГРУ ЗАВЕРШЕНО!</h1>
            <div id="end-message" style="font-size: 1.5rem; margin: 20px 0;"></div>
            <div style="font-size: 4rem; margin: 20px 0;" id="end-icon">🏆</div>
            <p>Твій рахунок: <span id="final-score" style="color: #4caf50;">0</span> XP</p>
            <button class="mc-btn start-btn" onclick="location.reload()">ГРАТИ ЗНОВУ</button>
        </div>
    </div>

    <script>
        // Data from the textbook provided
        const questions = [
            {
                period: "Становлення Русі",
                question: "Князь Олег захопив Київ і об'єднав північні та південні землі. Початок династії Рюриковичів.",
                correct: "882 р.",
                options: ["860 р.", "882 р.", "907 р.", "988 р."]
            },
            {
                period: "Правління Ольги",
                question: "Повстання деревлян та трагічна загибель князя Ігоря під час полюддя.",
                correct: "945 р.",
                options: ["911 р.", "941 р.", "945 р.", "957 р."]
            },
            {
                period: "Правління Ольги",
                question: "Дипломатичний візит княгині Ольги до Константинополя.",
                correct: "957 р.",
                options: ["946 р.", "957 р.", "964 р.", "972 р."]
            },
            {
                period: "Доба Святослава",
                question: "Розгром Святославом Хозарського каганату та взяття Білої Вежі.",
                correct: "965 р.",
                options: ["965 р.", "968 р.", "972 р.", "980 р."]
            },
            {
                period: "Розквіт Русі",
                question: "Хрещення Русі-України Володимиром Великим. Християнство стає державною релігією.",
                correct: "988 р.",
                options: ["957 р.", "988 р.", "1019 р.", "1054 р."]
            },
            {
                period: "Розквіт Русі",
                question: "Остаточний розгром печенігів під Києвом військами Ярослава Мудрого.",
                correct: "1036 р.",
                options: ["1015 р.", "1036 р.", "1037 р.", "1054 р."]
            },
            {
                period: "Розквіт Русі",
                question: "Завершення будівництва Софійського собору в Києві.",
                correct: "1037 р.",
                options: ["1036 р.", "1037 р.", "1051 р.", "1113 р."]
            },
            {
                period: "Період роздробленості",
                question: "Любецький з’їзд князів. Принцип «Кожен хай держить отчину свою».",
                correct: "1097 р.",
                options: ["1068 р.", "1072 р.", "1097 р.", "1113 р."]
            },
            {
                period: "Період роздробленості",
                question: "Перша літописна згадка назви «Україна».",
                correct: "1187 р.",
                options: ["1169 р.", "1185 р.", "1187 р.", "1199 р."]
            },
            {
                period: "Галицько-Волинська держава",
                question: "Роман Мстиславич об'єднав Галичину і Волинь. Утворення Галицько-Волинської держави.",
                correct: "1199 р.",
                options: ["1187 р.", "1199 р.", "1205 р.", "1223 р."]
            },
            {
                period: "Монгольська навала",
                question: "Битва на річці Калка. Перша поразка від монголів.",
                correct: "1223 р.",
                options: ["1199 р.", "1223 р.", "1240 р.", "1253 р."]
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;
        let lives = 3;
        let isAnswering = false;

        // Sound effects (Simulated with visual cues since simple HTML shouldn't rely on external MP3s)
        function playSound(type) {
            // Placeholder for sound logic if needed later
        }

        function startGame() {
            score = 0;
            lives = 3;
            currentQuestionIndex = 0;
            document.getElementById('start-screen').classList.remove('active');
            document.getElementById('end-screen').classList.remove('active');
            document.getElementById('game-screen').classList.add('active');
            
            // Shuffle questions slightly for replayability
            questions.sort(() => Math.random() - 0.5);
            
            updateStats();
            loadQuestion();
        }

        function updateStats() {
            // Hearts
            let heartsStr = "";
            for(let i=0; i<lives; i++) heartsStr += "❤️";
            document.getElementById('hearts-display').innerText = heartsStr;

            // XP Bar
            let progress = (currentQuestionIndex / questions.length) * 100;
            document.getElementById('xp-fill').style.width = `${progress}%`;
            document.getElementById('level-display').innerText = `Питання ${currentQuestionIndex + 1}/${questions.length}`;
        }

        function loadQuestion() {
            isAnswering = false;
            const q = questions[currentQuestionIndex];
            
            document.getElementById('period-label').innerText = q.period;
            document.getElementById('question-text').innerText = q.question;
            
            const optionsContainer = document.getElementById('options-container');
            optionsContainer.innerHTML = '';

            // Randomize options specifically for display, keep logic intact
            let displayOptions = [...q.options];
            displayOptions.sort(() => Math.random() - 0.5);

            displayOptions.forEach(opt => {
                const btn = document.createElement('button');
                btn.className = 'mc-btn';
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(btn, opt, q.correct);
                optionsContainer.appendChild(btn);
            });
            
            updateStats();
        }

        function checkAnswer(btn, selected, correct) {
            if (isAnswering) return;
            isAnswering = true;

            if (selected === correct) {
                btn.classList.add('correct');
                score += 100;
                showNotification("БЛОК ЗДОБУТО! +100 XP");
                setTimeout(nextQuestion, 1000);
            } else {
                btn.classList.add('wrong');
                lives--;
                showNotification("ОЙ! КРІПЕР ВИБУХНУВ!");
                updateStats();
                
                // Highlight correct one
                const buttons = document.querySelectorAll('.options-grid .mc-btn');
                buttons.forEach(b => {
                    if (b.innerText === correct) b.classList.add('correct');
                });

                if (lives <= 0) {
                    setTimeout(gameOver, 1500);
                } else {
                    setTimeout(nextQuestion, 1500);
                }
            }
        }

        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                loadQuestion();
            } else {
                winGame();
            }
        }

        function showNotification(text) {
            const notif = document.getElementById('notification');
            notif.innerText = text;
            notif.style.display = 'block';
            setTimeout(() => {
                notif.style.display = 'none';
            }, 1000);
        }

        function gameOver() {
            document.getElementById('game-screen').classList.remove('active');
            document.getElementById('end-screen').classList.add('active');
            document.getElementById('end-title').innerText = "GAME OVER";
            document.getElementById('end-title').style.color = "#f44336";
            document.getElementById('end-message').innerText = "Ти витратив усі життя. Історія змінилася...";
            document.getElementById('end-icon').innerText = "☠️";
            document.getElementById('final-score').innerText = score;
        }

        function winGame() {
            document.getElementById('game-screen').classList.remove('active');
            document.getElementById('end-screen').classList.add('active');
            document.getElementById('end-title').innerText = "ПЕРЕМОГА!";
            document.getElementById('end-title').style.color = "#4caf50";
            document.getElementById('end-message').innerText = "Ти успішно побудував стрічку часу Русі-України!";
            document.getElementById('end-icon').innerText = "💎";
            document.getElementById('final-score').innerText = score;
        }

    </script>
</body>
</html># scaling-adventure
