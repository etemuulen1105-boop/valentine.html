<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Valentine?</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #ffe6f0 0%, #ffd6e7 100%);
            padding: 20px;
            overflow-x: hidden;
        }
        
        .container {
            width: 100%;
            max-width: 900px;
            background: white;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(255, 105, 180, 0.25);
            padding: 50px 40px;
            text-align: center;
            position: relative;
            border: 4px solid #ffebf3;
        }
        
        .question {
            color: #ff69b4;
            font-size: 4rem;
            margin-bottom: 60px;
            font-weight: bold;
            text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.1);
            padding: 25px;
            letter-spacing: 1px;
        }
        
        .buttons-container {
            position: relative;
            min-height: 350px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 60px;
            margin: 50px 0;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 35px 70px;
            font-size: 2.8rem;
            font-weight: bold;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.25);
            min-width: 250px;
            height: 150px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        
        .btn:active {
            transform: translateY(6px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
        }
        
        #yes-btn {
            background-color: #4CAF50;
            color: white;
            border: 10px solid #3d8b40;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        
        #yes-btn:hover {
            background-color: #45a049;
        }
        
        #no-btn {
            background-color: #ff4444;
            color: white;
            border: 10px solid #cc0000;
            position: relative;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        
        #no-btn:hover {
            background-color: #ff3333;
        }
        
        .message-container {
            margin: 50px 0;
            padding: 40px;
            background-color: #fff5fa;
            border-radius: 25px;
            border: 5px solid #ffb6c1;
            display: none;
            animation: fadeIn 1s ease;
        }
        
        .message {
            font-size: 2.5rem;
            color: #ff69b4;
            font-weight: bold;
            line-height: 1.6;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
        }
        
        .think-again {
            margin-top: 40px;
            padding: 25px;
            background-color: #f8f9fa;
            border-radius: 20px;
            border-left: 8px solid #ff69b4;
            font-size: 2rem;
            color: #555;
            font-style: italic;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        
        .counter {
            margin: 30px 0;
            color: #ff4444;
            font-size: 1.8rem;
            font-weight: bold;
            background-color: #fff0f0;
            padding: 15px 25px;
            border-radius: 15px;
            display: inline-block;
        }
        
        .effects-container {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: 10;
        }
        
        .clap {
            position: absolute;
            font-size: 50px;
            animation: clapAnimation 1.2s ease-out forwards;
            z-index: 100;
        }
        
        .flower {
            position: absolute;
            font-size: 45px;
            animation: flowerFloat 4s ease-out forwards;
            z-index: 50;
        }
        
        @keyframes fadeIn {
            from { 
                opacity: 0; 
                transform: translateY(40px) scale(0.9); 
            }
            to { 
                opacity: 1; 
                transform: translateY(0) scale(1); 
            }
        }
        
        @keyframes clapAnimation {
            0% {
                transform: scale(0) rotate(-30deg);
                opacity: 0;
            }
            50% {
                transform: scale(1.3) rotate(15deg);
                opacity: 1;
            }
            100% {
                transform: scale(1) rotate(0deg);
                opacity: 0;
            }
        }
        
        @keyframes flowerFloat {
            0% {
                transform: translateY(150px) rotate(0deg) scale(0.6);
                opacity: 0;
            }
            20% {
                opacity: 1;
                transform: translateY(50px) rotate(0deg) scale(1.1);
            }
            60% {
                opacity: 1;
                transform: translateY(-50px) rotate(180deg) scale(1);
            }
            100% {
                transform: translateY(-200px) rotate(360deg) scale(0.7);
                opacity: 0;
            }
        }
        
        @keyframes growButton {
            0% { 
                transform: scale(1); 
                border-width: 10px;
            }
            100% { 
                transform: scale(1.25); 
                border-width: 15px;
            }
        }
        
        @keyframes shrinkButton {
            0% { 
                transform: scale(1); 
                border-width: 10px;
            }
            100% { 
                transform: scale(0.7); 
                border-width: 7px;
            }
        }
        
        @keyframes disappearButton {
            0% { 
                opacity: 1; 
                transform: scale(0.7); 
            }
            100% { 
                opacity: 0; 
                transform: scale(0); 
                display: none;
            }
        }
        
        @keyframes moveButton {
            0% { transform: translate(0, 0); }
            100% { transform: translate(var(--move-x), var(--move-y)); }
        }
        
        /* Адаптив дизайн */
        @media (max-width: 768px) {
            .question {
                font-size: 3rem;
            }
            
            .btn {
                font-size: 2.2rem;
                min-width: 200px;
                height: 120px;
                padding: 30px 50px;
                border-width: 8px;
            }
            
            .buttons-container {
                gap: 40px;
                min-height: 300px;
            }
            
            .message {
                font-size: 2rem;
            }
            
            .think-again {
                font-size: 1.6rem;
            }
        }
        
        @media (max-width: 480px) {
            .question {
                font-size: 2.4rem;
            }
            
            .btn {
                font-size: 1.8rem;
                min-width: 160px;
                height: 100px;
                padding: 25px 40px;
                border-width: 6px;
            }
            
            .buttons-container {
                flex-direction: column;
                gap: 35px;
                min-height: 400px;
            }
            
            .message {
                font-size: 1.6rem;
            }
            
            .think-again {
                font-size: 1.4rem;
            }
            
            .counter {
                font-size: 1.4rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="question">Will you be my valentine?</h1>
        
        <div class="buttons-container" id="buttons-container">
            <button class="btn" id="yes-btn">YES</button>
            <button class="btn" id="no-btn">NO</button>
        </div>
        
        <div class="think-again" id="think-again">Дахиад бодоод үзээрэй</div>
        
        <div class="counter" id="counter">NO дарагдсан: 0 удаа</div>
        
        <div class="message-container" id="message-container">
            <div class="message" id="message">
                Тэмүүлэн чам дээр очиж ямар нэг юм өгөх болно 10:55д ангийхаа гадаа хүлээж байгаарай
            </div>
        </div>
        
        <div class="effects-container" id="effects-container"></div>
    </div>

    <script>
        // Элементүүдийг авах
        const yesBtn = document.getElementById('yes-btn');
        const noBtn = document.getElementById('no-btn');
        const messageContainer = document.getElementById('message-container');
        const message = document.getElementById('message');
        const buttonsContainer = document.getElementById('buttons-container');
        const effectsContainer = document.getElementById('effects-container');
        const counter = document.getElementById('counter');
        const thinkAgain = document.getElementById('think-again');
        
        // Хувьсагчдыг тохируулах
        let noClickCount = 0;
        const maxNoClicks = 10;
        const originalYesFontSize = window.getComputedStyle(yesBtn).fontSize;
        const originalYesBorderWidth = "10px";
        const originalNoBorderWidth = "10px";
        
        // Алга ташилт үүсгэх функц
        function createClaps(count) {
            for (let i = 0; i < count; i++) {
                const clap = document.createElement('div');
                clap.classList.add('clap');
                clap.innerHTML = '👏';
                
                // Санамсаргүй байрлал
                const xPos = Math.random() * 80 + 10;
                const yPos = Math.random() * 80 + 10;
                clap.style.left = xPos + '%';
                clap.style.top = yPos + '%';
                
                // Санамсаргүй хэмжээ, хурд
                clap.style.animationDelay = (Math.random() * 0.8) + 's';
                clap.style.fontSize = (Math.random() * 30 + 40) + 'px';
                
                effectsContainer.appendChild(clap);
                
                // Анимацийн дараа устгах
                setTimeout(() => {
                    if (clap.parentNode) {
                        clap.parentNode.removeChild(clap);
                    }
                }, 1200);
            }
        }
        
        // Цэцэг үүсгэх функц
        function createFlowers(count) {
            const flowers = ['🌹', '🌷', '🌸', '💐', '🌺', '🌻', '🌼'];
            for (let i = 0; i < count; i++) {
                const flower = document.createElement('div');
                flower.classList.add('flower');
                flower.innerHTML = flowers[Math.floor(Math.random() * flowers.length)];
                
                // Санамсаргүй байрлал
                const xPos = Math.random() * 100;
                flower.style.left = xPos + '%';
                
                // Санамсаргүй хэмжээ, хурд
                const delay = Math.random() * 2;
                flower.style.animationDelay = delay + 's';
                flower.style.fontSize = (Math.random() * 30 + 35) + 'px';
                
                effectsContainer.appendChild(flower);
                
                // Анимацийн дараа устгах
                setTimeout(() => {
                    if (flower.parentNode) {
                        flower.parentNode.removeChild(flower);
                    }
                }, 4000);
            }
        }
        
        // NO товч хөдөлгөх функц
        function moveNoButton() {
            noClickCount++;
            counter.textContent = `NO дарагдсан: ${noClickCount} удаа`;
            
            // YES товчийг томруулах (ногоон хүрээтэй нь)
            const currentYesSize = parseFloat(window.getComputedStyle(yesBtn).fontSize);
            const newYesSize = currentYesSize * 1.25;
            
            yesBtn.style.fontSize = newYesSize + 'px';
            yesBtn.style.borderWidth = '15px'; // Хүрээ томорно
            
            // Өсөх анимаци
            yesBtn.style.animation = 'growButton 0.4s ease forwards';
            
            // NO товчийг жижигрүүлэх (улаан хүрээтэй нь)
            const currentNoSize = parseFloat(window.getComputedStyle(noBtn).fontSize);
            const newNoSize = currentNoSize * 0.7;
            
            noBtn.style.fontSize = newNoSize + 'px';
            noBtn.style.borderWidth = '7px'; // Хүрээ жижигрэх
            
            // Жижигрэх анимаци
            noBtn.style.animation = 'shrinkButton 0.4s ease forwards';
            
            // Анимацийг дууссаны дараа хэвээр үлдээх
            setTimeout(() => {
                yesBtn.style.animation = '';
                noBtn.style.animation = '';
            }, 400);
            
            // NO товчийг санамсаргүй байрлалд хөдөлгөх
            const containerRect = buttonsContainer.getBoundingClientRect();
            const buttonRect = noBtn.getBoundingClientRect();
            
            const maxX = containerRect.width - buttonRect.width;
            const maxY = containerRect.height - buttonRect.height;
            
            // Санамсаргүй байрлал
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            // Хөдөлгөөний анимаци
            noBtn.style.setProperty('--move-x', (randomX - parseFloat(noBtn.style.left || 0)) + 'px');
            noBtn.style.setProperty('--move-y', (randomY - parseFloat(noBtn.style.top || 0)) + 'px');
            
            noBtn.style.position = 'absolute';
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
            
            // 10 удаа дарахад алга болгох
            if (noClickCount >= maxNoClicks) {
                setTimeout(() => {
                    noBtn.style.animation = 'disappearButton 1s ease forwards';
                    setTimeout(() => {
                        noBtn.style.display = 'none';
                        counter.textContent = `NO алга боллоо! Одоо YES товчийг дарна уу!`;
                    }, 1000);
                }, 400);
            }
        }
        
        // YES товч дарсан үед
        function handleYesClick() {
            // Мессеж харуулах
            messageContainer.style.display = 'block';
            
            // "Дахиад бодоод үзээрэй" текстийг нуух
            thinkAgain.style.display = 'none';
            
            // YES товчийн хэмжээг эхний хэмжээнд нь буцаах
            yesBtn.style.fontSize = originalYesFontSize;
            yesBtn.style.borderWidth = originalYesBorderWidth;
            
            // Анимацийг зогсоох
            yesBtn.style.animation = '';
            
            // Тэмдэглэл үйлдэл
            createClaps(20);
            createFlowers(25);
            
            // Товчнуудын текстийг өөрчлөх
            yesBtn.textContent = "ТИЙМ! 💖";
            yesBtn.disabled = true;
            yesBtn.style.cursor = "default";
            
            if (noBtn.style.display !== 'none') {
                noBtn.textContent = "ХЭЗҮЭ!";
                noBtn.disabled = true;
                noBtn.style.cursor = "default";
                noBtn.style.borderWidth = originalNoBorderWidth;
            }
            
            // NO алга болсон бол YES товчийг төвд байрлуулах
            if (noBtn.style.display === 'none') {
                buttonsContainer.style.justifyContent = "center";
            }
            
            // Нэмэлт анимаци үргэлжлүүлэх
            const effectInterval = setInterval(() => {
                if (Math.random() > 0.4) createClaps(2);
                if (Math.random() > 0.3) createFlowers(3);
            }, 2000);
            
            // 10 секундын дараа анимаци зогсоох
            setTimeout(() => {
                clearInterval(effectInterval);
            }, 10000);
        }
        
        // Үйл явдлын сонсогч нэмэх
        noBtn.addEventListener('click', moveNoButton);
        yesBtn.addEventListener('click', handleYesClick);
        
        // NO товч дээр хулганаар чирхэд бас хөдлөх (эхний 5 удаа)
        noBtn.addEventListener('mouseover', function() {
            if (noClickCount < 5 && noClickCount < maxNoClicks) {
                moveNoButton();
            }
        });
        
        // Вэбсайт ачааллагдсан үед анхны байрлалыг тогтоох
        window.addEventListener('load', function() {
            // NO товчийн анхны байрлалыг тогтоох
            noBtn.style.position = 'relative';
            noBtn.style.left = '0';
            noBtn.style.top = '0';
        });
    </script>
</body>
</html>
