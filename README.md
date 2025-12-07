<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сердечко любви</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Georgia', serif;
        }
        
        body {
            background: linear-gradient(135deg, #fff0f5, #ffe6ee);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            color: #5a003a;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            text-align: center;
            padding: 20px;
        }
        
        h1 {
            text-align: center;
            color: #cc0066;
            margin: 30px 0;
            font-size: 2.8rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            padding-bottom: 15px;
            border-bottom: 3px solid #ff99cc;
            font-family: 'Brush Script MT', cursive;
        }
        
        .main-thought {
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 25px;
            margin: 30px auto;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
            max-width: 700px;
            border-left: 6px solid #ff66b2;
            font-size: 1.2rem;
            line-height: 1.6;
            color: #660033;
        }
        
        .main-thought p {
            margin-bottom: 15px;
        }
        
        .quote {
            font-style: italic;
            color: #cc0066;
            font-weight: bold;
            margin-top: 10px;
            font-size: 1.1rem;
        }
        
        .button-container {
            margin: 40px 0;
        }
        
        .heart-button {
            background: linear-gradient(to right, #ff3385, #cc0066);
            color: white;
            border: none;
            padding: 18px 35px;
            font-size: 1.3rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(255, 102, 178, 0.4);
            font-weight: bold;
            letter-spacing: 1px;
        }
        
        .heart-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(255, 102, 178, 0.6);
            background: linear-gradient(to right, #ff0066, #990033);
        }
        
        .heart-button:active {
            transform: translateY(0);
        }
        
        .heart-modal, .note-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.85);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .heart-modal-content {
            background-color: white;
            border-radius: 20px;
            padding: 25px;
            width: 90%;
            max-width: 550px; /* Уменьшено с 700px */
            text-align: center;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            animation: modalAppear 0.5s ease-out;
            max-height: 85vh;
            overflow-y: auto;
        }
        
        .note-modal-content {
            background-color: white;
            border-radius: 20px;
            padding: 25px;
            width: 90%;
            max-width: 550px; /* Уменьшено с 700px */
            text-align: center;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            animation: modalAppear 0.5s ease-out;
            max-height: 85vh;
            overflow-y: auto;
        }
        
        @keyframes modalAppear {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            border-bottom: 2px solid #ff99cc;
            padding-bottom: 10px;
        }
        
        .modal-header h2 {
            color: #cc0066;
            font-size: 1.6rem; /* Уменьшено */
            font-family: 'Brush Script MT', cursive;
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.8rem; /* Уменьшено */
            color: #cc0066;
            cursor: pointer;
            line-height: 1;
        }
        
        .love-message {
            margin: 15px 0; /* Уменьшено */
            padding: 15px; /* Уменьшено */
            background-color: #fff5f9;
            border-radius: 12px;
            border-left: 4px solid #ff66b2;
            font-size: 1.1rem; /* Уменьшено */
            line-height: 1.5;
            color: #660033;
            min-height: 80px; /* Уменьшено */
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.5s ease;
            box-shadow: 0 4px 10px rgba(255, 102, 178, 0.1);
        }
        
        .love-message.highlight {
            background-color: #ffebf3;
            border-left: 4px solid #ff3385;
            transform: scale(1.02);
        }
        
        .canvas-container {
            background-color: #fff9fc;
            border-radius: 10px;
            padding: 12px; /* Уменьшено */
            margin: 15px 0; /* Уменьшено */
            border: 2px solid #ffccdd;
            position: relative;
            height: 280px; /* Уменьшено */
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        #heartCanvas {
            background-color: white;
            border-radius: 8px;
            width: 450px; /* Уменьшено */
            height: 250px; /* Уменьшено */
        }
        
        .step-indicator {
            margin: 10px 0; /* Уменьшено */
            color: #990033;
            font-weight: bold;
            font-size: 1rem; /* Уменьшено */
        }
        
        .next-button-container {
            margin: 15px 0; /* Уменьшено */
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px; /* Уменьшено */
        }
        
        .next-button {
            background: linear-gradient(to right, #ff66b2, #ff3385);
            color: white;
            border: none;
            padding: 12px 30px; /* Уменьшено */
            font-size: 1.1rem; /* Уменьшено */
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(255, 102, 178, 0.4);
            font-weight: bold;
            letter-spacing: 1px;
        }
        
        .next-button:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 8px 18px rgba(255, 102, 178, 0.6);
            background: linear-gradient(to right, #ff3385, #ff0066);
        }
        
        .next-button:disabled {
            background: #cccccc;
            cursor: not-allowed;
            box-shadow: none;
        }
        
        .note-button {
            background: linear-gradient(to right, #66cc66, #33aa33);
            color: white;
            border: none;
            padding: 12px 30px; /* Уменьшено */
            font-size: 1.1rem; /* Уменьшено */
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(102, 204, 102, 0.4);
            font-weight: bold;
            letter-spacing: 1px;
            display: none;
        }
        
        .note-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 18px rgba(102, 204, 102, 0.6);
            background: linear-gradient(to right, #55bb55, #229922);
        }
        
        .heart-progress {
            display: flex;
            justify-content: center;
            margin: 15px 0; /* Уменьшено */
        }
        
        .heart-dot {
            width: 14px; /* Уменьшено */
            height: 14px; /* Уменьшено */
            border-radius: 50%;
            background-color: #ffcccc;
            margin: 0 8px; /* Уменьшено */
            transition: all 0.3s ease;
        }
        
        .heart-dot.active {
            background-color: #ff3385;
            transform: scale(1.2);
        }
        
        .heart-dot.completed {
            background-color: #ff0066;
        }
        
        /* Стили для записки */
        .note-content {
            text-align: left;
            padding: 15px; /* Уменьшено */
            background-color: #fff9fc;
            border-radius: 10px;
            margin: 15px 0; /* Уменьшено */
            border: 2px solid #ffccdd;
            max-height: 350px; /* Уменьшено */
            overflow-y: auto;
            line-height: 1.7;
            font-size: 0.95rem; /* Уменьшено */
        }
        
        .note-content h3 {
            color: #cc0066;
            text-align: center;
            margin-bottom: 15px; /* Уменьшено */
            font-family: 'Brush Script MT', cursive;
            font-size: 1.8rem; /* Уменьшено */
        }
        
        .note-content p {
            margin-bottom: 12px; /* Уменьшено */
            text-indent: 15px; /* Уменьшено */
        }
        
        .signature {
            text-align: right;
            font-style: italic;
            margin-top: 20px; /* Уменьшено */
            color: #990033;
            font-weight: bold;
            font-size: 1.1rem; /* Уменьшено */
        }
        
        footer {
            margin-top: 40px;
            color: #993366;
            font-size: 0.9rem;
            text-align: center;
            padding: 20px;
            border-top: 1px solid #ffccdd;
            width: 100%;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .main-thought {
                padding: 20px;
                font-size: 1.1rem;
            }
            
            .heart-button {
                padding: 15px 30px;
                font-size: 1.2rem;
            }
            
            .heart-modal-content, .note-modal-content {
                padding: 18px;
                width: 95%;
                max-width: 500px;
            }
            
            .love-message {
                font-size: 1rem;
                padding: 12px;
                min-height: 70px;
            }
            
            .canvas-container {
                height: 240px;
                padding: 10px;
            }
            
            #heartCanvas {
                width: 380px;
                height: 210px;
            }
            
            .next-button-container {
                flex-direction: column;
                align-items: center;
            }
            
            .next-button, .note-button {
                width: 100%;
                max-width: 280px;
                padding: 10px 25px;
                font-size: 1rem;
            }
            
            .modal-header h2 {
                font-size: 1.4rem;
            }
            
            .note-content {
                max-height: 300px;
                font-size: 0.9rem;
            }
            
            .note-content h3 {
                font-size: 1.6rem;
            }
        }
        
        @media (max-width: 480px) {
            h1 {
                font-size: 1.8rem;
            }
            
            .main-thought {
                padding: 15px;
                font-size: 1rem;
            }
            
            .heart-button {
                padding: 12px 25px;
                font-size: 1.1rem;
            }
            
            .heart-modal-content, .note-modal-content {
                padding: 15px;
                max-width: 450px;
            }
            
            .love-message {
                font-size: 0.95rem;
                min-height: 60px;
            }
            
            .canvas-container {
                height: 200px;
            }
            
            #heartCanvas {
                width: 320px;
                height: 180px;
            }
            
            .next-button, .note-button {
                padding: 8px 20px;
                font-size: 0.95rem;
                max-width: 250px;
            }
            
            .modal-header h2 {
                font-size: 1.3rem;
            }
            
            .close-modal {
                font-size: 1.6rem;
            }
            
            .note-content {
                font-size: 0.85rem;
                max-height: 250px;
            }
            
            .note-content h3 {
                font-size: 1.4rem;
            }
        }
        
        .completion-message {
            font-size: 1.3rem; /* Уменьшено */
            color: #cc0066;
            font-weight: bold;
            margin: 15px 0; /* Уменьшено */
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Сегодня мы уже целых полгода вместе и в честь этого, я подготовил тебе небольшой подарок</h1>
        
        <div class="main-thought">
            <p>Любовь - это не просто чувство, это путь, который мы проходим вместе. Каждый шаг этого пути наполнен смыслом и эмоциями.</p>
            <p>Нажми на кнопку ниже, чтобы пройти по пяти этапам создания моего сердечка, наполненного любовью.</p>
            <p class="quote">Моя любовь к тебе навечно!</p>
        </div>
        
        <div class="button-container">
            <button class="heart-button" id="openHeartModal">Начать путь любви</button>
        </div>
    </div>
    
    <!-- Модальное окно для поэтапного рисования сердечка -->
    <div class="heart-modal" id="heartModal">
        <div class="heart-modal-content">
            <div class="modal-header">
                <h2>Создание сердечка любви</h2>
                <button class="close-modal" id="closeHeartModal">&times;</button>
            </div>
            
            <div class="step-indicator" id="stepIndicator">Этап 1 из 5</div>
            
            <div class="love-message" id="loveMessage">
                Это моя любовь к тебе - начало сердца
            </div>
            
            <div class="heart-progress">
                <div class="heart-dot active" id="dot1"></div>
                <div class="heart-dot" id="dot2"></div>
                <div class="heart-dot" id="dot3"></div>
                <div class="heart-dot" id="dot4"></div>
                <div class="heart-dot" id="dot5"></div>
            </div>
            
            <div class="canvas-container">
                <canvas id="heartCanvas" width="450" height="250"></canvas>
            </div>
            
            <div class="next-button-container">
                <button class="next-button" id="nextButton">Продолжить создание сердца</button>
                <button class="note-button" id="noteButton">📜 Посмотреть записку</button>
            </div>
            
            <div class="completion-message" id="completionMessage" style="display: none;">
                Сердечко любви завершено! ❤️
            </div>
        </div>
    </div>
    
    <!-- Модальное окно с запиской -->
    <div class="note-modal" id="noteModal">
        <div class="note-modal-content">
            <div class="modal-header">
                <h2>Моё признание</h2>
                <button class="close-modal" id="closeNoteModal">&times;</button>
            </div>
            
            <div class="note-content">
                <h3>Моё дорогое сокровище...</h3>
                
                <p>С каждым днём я понимаю всё больше, насколько ты важна для меня. Когда ты рядом, мир становится ярче, проблемы кажутся мелочами, а обычные дни превращаются в праздники. Твоя улыбка способна растопить лёд даже в самый холодный день, а твой смех звучит для меня самой прекрасной музыкой.</p>
                
                <p>Я помню каждый наш момент вместе: от первой встречи, когда я понял, что встретил кого-то особенного, до сегодняшнего дня, когда я с уверенностью могу сказать, что ты - моя судьба. Ты вошла в мою жизнь так незаметно и в то же время так ярко, что теперь я не представляю своего будущего без тебя.</p>
                
                <p>Ты научила меня видеть красоту в простых вещах, ценить каждый миг и верить в лучшее даже тогда, когда кажется, что всё против нас. Твоя поддержка даёт мне силы двигаться вперёд, твоя вера в меня вдохновляет на свершения, а твоя любовь делает меня лучше с каждым днём.</p>
                
                <p>Я благодарен судьбе за то, что она подарила мне тебя. За то, что я могу просыпаться с мыслью о тебе, засыпать с твоим образом в сердце и мечтать о нашем общем будущем. Ты - моя тихая гавань в бурном море жизни, моё утешение в трудные минуты и моя самая большая радость в моменты счастья.</p>
                
                <p>Я люблю тебя не за что-то конкретное, а просто за то, что ты есть. За твою душу, которая так созвучна моей. За твоё сердце, которое бьётся в унисон с моим. За твой характер, который идеально дополняет мой. Ты - мой самый лучший подарок судьбы, моё самое ценное сокровище.</p>
                
                <p>И сегодня, глядя на это сердечко, которое мы создали вместе, я хочу сказать тебе: я люблю тебя. Люблю сильнее с каждым днём, с каждым часом, с каждым мгновением. Моя любовь к тебе будет расти и крепнуть, как это сердечко, которое мы по крупицам создавали вместе.</p>
                
                <p>Спасибо тебе за всё. За твоё терпение, за твою мудрость, за твою нежность. Я обещаю беречь нашу любовь, как самое драгоценное, что есть у меня в жизни. Обещаю быть рядом в радости и в горе, в здравии и в болезни, в богатстве и в бедности. Обещаю делать всё, чтобы ты была счастлива.</p>
                
                <p>Ты - моя любовь, моя муза, моё вдохновение. Ты - мой дом, куда я всегда хочу возвращаться. Ты - моя судьба, которую я благодарю каждый день.</p>
                
                <div class="signature">
                    С любовью до конца жизни,<br>
                    Твой навсегда.
                </div>
            </div>
            
            <button class="next-button" onclick="closeNoteModal()" style="margin-top: 15px;">Закрыть записку</button>
        </div>
    </div>
    
    <footer>
        <p>Создано с любовью | Пусть твое сердце всегда будет наполнено теплом и заботой</p>
    </footer>

    <script>
        // Элементы DOM
        const openHeartModalBtn = document.getElementById('openHeartModal');
        const heartModal = document.getElementById('heartModal');
        const closeHeartModalBtn = document.getElementById('closeHeartModal');
        const noteModal = document.getElementById('noteModal');
        const closeNoteModalBtn = document.getElementById('closeNoteModal');
        const heartCanvas = document.getElementById('heartCanvas');
        const nextButton = document.getElementById('nextButton');
        const noteButton = document.getElementById('noteButton');
        const loveMessage = document.getElementById('loveMessage');
        const stepIndicator = document.getElementById('stepIndicator');
        const completionMessage = document.getElementById('completionMessage');
        
        // Точки прогресса
        const dot1 = document.getElementById('dot1');
        const dot2 = document.getElementById('dot2');
        const dot3 = document.getElementById('dot3');
        const dot4 = document.getElementById('dot4');
        const dot5 = document.getElementById('dot5');
        
        // Контекст холста
        const ctx = heartCanvas.getContext('2d');
        
        // Переменные для поэтапного рисования
        let currentStep = 0;
        const totalSteps = 5;
        let heartPoints = [];
        
        // Сообщения для каждого этапа
        const messages = [
            "Это маленькая часть всей моей любви к тебе!",
            "Когда пишешь)",
            "Каждый момент с тобой, новая сила любви!)",
            "Моя верность и преданность тебе до конца!",
            "Это когда ты меня обнимаешь, целуешь или просто находишься рядом!"
        ];
        
        // Цвета для каждого этапа
        const stepColors = [
            '#ffcccc', // Светло-красный
            '#ff9999', // Красный
            '#ff6666', // Ярко-красный
            '#ff3385', // Розово-красный
            '#cc0066'  // Темно-розовый
        ];
        
        // Функция для генерации точек сердечка
        function generateHeartPoints() {
            const points = [];
            const centerX = heartCanvas.width / 2;
            const centerY = heartCanvas.height / 2;
            const size = 70; // Уменьшено для меньшего холста
            
            // Генерируем точки сердечка с использованием параметрического уравнения
            for (let i = 0; i <= 100; i++) {
                const t = i / 100 * 2 * Math.PI;
                
                // Уравнение сердечка
                const x = 16 * Math.pow(Math.sin(t), 3);
                const y = 13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t);
                
                // Масштабируем и позиционируем
                const scaledX = centerX - x * size/16;
                const scaledY = centerY - y * size/16;
                
                points.push({x: scaledX, y: scaledY});
            }
            
            return points;
        }
        
        // Инициализация холста
        function initCanvas() {
            // Очищаем холст
            ctx.clearRect(0, 0, heartCanvas.width, heartCanvas.height);
            
            // Устанавливаем белый фон
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, heartCanvas.width, heartCanvas.height);
            
            // Генерируем точки сердечка
            heartPoints = generateHeartPoints();
            
            // Сбрасываем состояние
            currentStep = 0;
            
            // Скрываем кнопку записки
            noteButton.style.display = 'none';
            completionMessage.style.display = 'none';
            
            // Рисуем первый этап
            drawHeartStep();
            
            // Обновляем UI
            updateUI();
        }
        
        // Функция для рисования сердечка на текущем этапе
        function drawHeartStep() {
            // Очищаем холст
            ctx.clearRect(0, 0, heartCanvas.width, heartCanvas.height);
            
            // Рисуем белый фон
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, heartCanvas.width, heartCanvas.height);
            
            // Определяем, сколько точек рисовать на текущем этапе
            const pointsPerStep = Math.floor(heartPoints.length / totalSteps);
            const pointsToDraw = (currentStep + 1) * pointsPerStep;
            
            // Начинаем путь для сердечка
            ctx.beginPath();
            
            // Перемещаемся к первой точке
            ctx.moveTo(heartPoints[0].x, heartPoints[0].y);
            
            // Рисуем линии до текущего количества точек
            for (let i = 1; i < pointsToDraw && i < heartPoints.length; i++) {
                ctx.lineTo(heartPoints[i].x, heartPoints[i].y);
            }
            
            // Настраиваем стиль линии
            ctx.strokeStyle = stepColors[currentStep];
            ctx.lineWidth = 4;
            ctx.lineJoin = 'round';
            ctx.lineCap = 'round';
            
            // Рисуем контур
            ctx.stroke();
            
            // Если это последний этап, закрашиваем сердечко
            if (currentStep === totalSteps - 1) {
                ctx.closePath();
                
                // Закрашиваем сердечко
                ctx.fillStyle = 'rgba(255, 102, 178, 0.2)';
                ctx.fill();
                
                // Рисуем контур еще раз для четкости
                ctx.stroke();
                
                // Показываем сообщение о завершении
                completionMessage.style.display = 'block';
                nextButton.disabled = true;
                nextButton.textContent = "Сердечко завершено";
                
                // Показываем кнопку записки
                noteButton.style.display = 'block';
            }
        }
        
        // Функция для обновления UI
        function updateUI() {
            // Обновляем сообщение
            loveMessage.textContent = messages[currentStep];
            
            // Добавляем подсветку к сообщению
            loveMessage.classList.remove('highlight');
            void loveMessage.offsetWidth; // Триггер перерисовки для анимации
            loveMessage.classList.add('highlight');
            
            // Обновляем индикатор этапа
            stepIndicator.textContent = `Этап ${currentStep + 1} из ${totalSteps}`;
            
            // Обновляем точки прогресса
            updateProgressDots();
            
            // Обновляем текст кнопки
            if (currentStep < totalSteps - 1) {
                nextButton.textContent = "Продолжить создание сердца";
                nextButton.disabled = false;
            }
        }
        
        // Функция для обновления точек прогресса
        function updateProgressDots() {
            // Сбрасываем все точки
            dot1.classList.remove('active', 'completed');
            dot2.classList.remove('active', 'completed');
            dot3.classList.remove('active', 'completed');
            dot4.classList.remove('active', 'completed');
            dot5.classList.remove('active', 'completed');
            
            // Устанавливаем активную точку
            if (currentStep === 0) {
                dot1.classList.add('active');
            } else if (currentStep === 1) {
                dot1.classList.add('completed');
                dot2.classList.add('active');
            } else if (currentStep === 2) {
                dot1.classList.add('completed');
                dot2.classList.add('completed');
                dot3.classList.add('active');
            } else if (currentStep === 3) {
                dot1.classList.add('completed');
                dot2.classList.add('completed');
                dot3.classList.add('completed');
                dot4.classList.add('active');
            } else if (currentStep === 4) {
                dot1.classList.add('completed');
                dot2.classList.add('completed');
                dot3.classList.add('completed');
                dot4.classList.add('completed');
                dot5.classList.add('active', 'completed');
            }
        }
        
        // Функция для перехода к следующему этапу
        function nextStep() {
            if (currentStep < totalSteps - 1) {
                currentStep++;
                drawHeartStep();
                updateUI();
            }
        }
        
        // Функция для открытия записки
        function openNoteModal() {
            noteModal.style.display = 'flex';
        }
        
        // Функция для закрытия записки
        function closeNoteModal() {
            noteModal.style.display = 'none';
        }
        
        // Открытие модального окна с сердечком
        openHeartModalBtn.addEventListener('click', () => {
            heartModal.style.display = 'flex';
            initCanvas();
        });
        
        // Закрытие модального окна с сердечком
        closeHeartModalBtn.addEventListener('click', () => {
            heartModal.style.display = 'none';
        });
        
        // Закрытие модального окна с запиской
        closeNoteModalBtn.addEventListener('click', closeNoteModal);
        
        // Закрытие модального окна с сердечком при клике вне его
        heartModal.addEventListener('click', (e) => {
            if (e.target === heartModal) {
                heartModal.style.display = 'none';
            }
        });
        
        // Закрытие модального окна с запиской при клике вне его
        noteModal.addEventListener('click', (e) => {
            if (e.target === noteModal) {
                closeNoteModal();
            }
        });
        
        // Обработчик кнопки "Продолжить"
        nextButton.addEventListener('click', nextStep);
        
        // Обработчик кнопки "Посмотреть записку"
        noteButton.addEventListener('click', openNoteModal);
        
        // Инициализация при загрузке страницы
        window.addEventListener('load', () => {
            // Модальные окна изначально скрыты
            heartModal.style.display = 'none';
            noteModal.style.display = 'none';
        });
        
        // Обработка изменения размера окна
        window.addEventListener('resize', () => {
            if (heartModal.style.display === 'flex') {
                // Перерисовываем сердечко при изменении размера окна
                heartPoints = generateHeartPoints();
                drawHeartStep();
            }
        });
    </script>
</body>
</html>
