<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StreamWave - Яркий стриминговый портал</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff4d7d;
            --secondary: #6e45e2;
            --accent: #88d3ce;
            --dark: #1a1a2e;
            --light: #f8f9fa;
            --gradient: linear-gradient(135deg, var(--primary), var(--secondary));
            --error: #ff4757;
            --success: #2ed573;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            scroll-behavior: smooth;
        }
        
        body {
            font-family: 'Montserrat', sans-serif;
            background: var(--dark);
            color: var(--light);
            overflow-x: hidden;
        }
        
        /* Шапка */
        header {
            background: rgba(26, 26, 46, 0.9);
            backdrop-filter: blur(10px);
            padding: 1rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: fixed;
            width: 100%;
            z-index: 1000;
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: 800;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .auth-btn {
            background: var(--gradient);
            color: white;
            border: none;
            padding: 0.6rem 1.5rem;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .auth-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 77, 125, 0.3);
        }
        
        /* Основной контент */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            padding: 0 10%;
            background: linear-gradient(to right, rgba(26, 26, 46, 0.9), rgba(26, 26, 46, 0.7)), 
                        url('https://images.unsplash.com/photo-1558008258-3256797b43f3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2000&q=80') no-repeat center/cover;
        }
        
        .hero-content {
            max-width: 600px;
            animation: fadeInUp 1s ease-out;
        }
        
        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 1rem;
            background: linear-gradient(to right, var(--primary), var(--accent));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            line-height: 1.6;
        }
        
        .stream-container {
            padding: 5rem 10%;
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 2rem;
        }
        
        .video-container {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 */
            height: 0;
            overflow: hidden;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }
        
        /* Чат */
        .chat-container {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 1.5rem;
            backdrop-filter: blur(10px);
            height: 600px;
            display: flex;
            flex-direction: column;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .chat-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .chat-header h3 {
            font-size: 1.3rem;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .chat-messages {
            flex-grow: 1;
            overflow-y: auto;
            margin-bottom: 1rem;
            scrollbar-width: thin;
            scrollbar-color: var(--primary) transparent;
        }
        
        .chat-messages::-webkit-scrollbar {
            width: 6px;
        }
        
        .chat-messages::-webkit-scrollbar-thumb {
            background-color: var(--primary);
            border-radius: 3px;
        }
        
        .message {
            background: rgba(255, 255, 255, 0.1);
            padding: 0.8rem;
            border-radius: 10px;
            margin-bottom: 0.8rem;
            animation: fadeIn 0.3s ease-out;
        }
        
        .message-user {
            font-weight: 600;
            color: var(--accent);
            margin-bottom: 0.3rem;
        }
        
        .message-text {
            line-height: 1.4;
        }
        
        .chat-input {
            display: flex;
            gap: 0.5rem;
        }
        
        .chat-input input {
            flex-grow: 1;
            background: rgba(255, 255, 255, 0.1);
            border: none;
            padding: 0.8rem 1rem;
            border-radius: 50px;
            color: white;
            font-family: inherit;
            outline: none;
            transition: background 0.3s;
        }
        
        .chat-input input:focus {
            background: rgba(255, 255, 255, 0.2);
        }
        
        .chat-input button {
            background: var(--gradient);
            color: white;
            border: none;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: transform 0.3s;
        }
        
        .chat-input button:hover {
            transform: scale(1.05);
        }
        
        /* Модальное окно авторизации */
        .auth-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(5px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease-out;
        }
        
        .auth-modal.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .auth-content {
            background: var(--dark);
            padding: 2.5rem;
            border-radius: 15px;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
            transform: translateY(20px);
            transition: transform 0.4s ease-out;
            position: relative;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .auth-modal.active .auth-content {
            transform: translateY(0);
        }
        
        .close-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: none;
            border: none;
            color: rgba(255, 255, 255, 0.5);
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-btn:hover {
            color: var(--primary);
        }
        
        .auth-tabs {
            display: flex;
            margin-bottom: 1.5rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .auth-tab {
            padding: 0.5rem 1rem;
            cursor: pointer;
            position: relative;
            color: rgba(255, 255, 255, 0.6);
            transition: color 0.3s;
        }
        
        .auth-tab.active {
            color: white;
        }
        
        .auth-tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 2px;
            background: var(--gradient);
        }
        
        .auth-form {
            display: none;
        }
        
        .auth-form.active {
            display: block;
        }
        
        .auth-content h2 {
            text-align: center;
            margin-bottom: 1.5rem;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .auth-form .form-group {
            margin-bottom: 1.2rem;
        }
        
        .auth-form label {
            display: block;
            margin-bottom: 0.5rem;
            color: rgba(255, 255, 255, 0.8);
        }
        
        .auth-form input {
            width: 100%;
            padding: 0.8rem 1rem;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: white;
            font-family: inherit;
            outline: none;
            transition: border-color 0.3s;
        }
        
        .auth-form input:focus {
            border-color: var(--primary);
        }
        
        .submit-btn {
            width: 100%;
            padding: 0.8rem;
            background: var(--gradient);
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 1rem;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 77, 125, 0.3);
        }
        
        .form-footer {
            text-align: center;
            margin-top: 1.5rem;
            color: rgba(255, 255, 255, 0.6);
        }
        
        .form-footer a {
            color: var(--accent);
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .form-footer a:hover {
            color: var(--primary);
        }
        
        .error-message {
            color: var(--error);
            font-size: 0.8rem;
            margin-top: 0.3rem;
            display: none;
        }
        
        .success-message {
            color: var(--success);
            text-align: center;
            margin-top: 1rem;
            display: none;
        }
        
        /* Анимации */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Адаптивность */
        @media (max-width: 992px) {
            .stream-container {
                grid-template-columns: 1fr;
                padding: 3rem 5%;
            }
            
            .hero {
                padding: 0 5%;
            }
            
            .hero h1 {
                font-size: 2.5rem;
            }
        }
        
        @media (max-width: 576px) {
            .hero h1 {
                font-size: 2rem;
            }
            
            .hero p {
                font-size: 1rem;
            }
            
            .auth-content {
                padding: 1.5rem;
                margin: 0 1rem;
            }
        }
    </style>
</head>
<body>
    <!-- Шапка -->
    <header>
        <div class="logo">StreamWave</div>
        <button class="auth-btn" id="openAuth">Войти</button>
    </header>
    
    <!-- Главный экран -->
    <section class="hero">
        <div class="hero-content">
            <h1>Погрузитесь в мир живых стримов</h1>
            <p>Присоединяйтесь к сообществу StreamWave и наслаждайтесь лучшими игровыми трансляциями в ярком и стильном оформлении.</p>
            <button class="auth-btn" id="heroAuthBtn">Начать просмотр</button>
        </div>
    </section>
    
    <!-- Стрим и чат -->
    <section class="stream-container">
        <div class="video-container">
            <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1&mute=1" allowfullscreen></iframe>
        </div>
        
        <div class="chat-container">
            <div class="chat-header">
                <h3>Чат стрима</h3>
                <span>🔴 2.5K зрителей</span>
            </div>
            
            <div class="chat-messages" id="chatMessages">
                <div class="message">
                    <div class="message-user">StreamerPro <span class="badge">стример</span></div>
                    <div class="message-text">Привет всем! Сегодня играем в новую игру, не пропустите!</div>
                </div>
                <div class="message">
                    <div class="message-user">GameFan123</div>
                    <div class="message-text">Ого, давно ждал этот стрим!</div>
                </div>
                <div class="message">
                    <div class="message-user">CoolViewer</div>
                    <div class="message-text">Какой крутой интерфейс у сайта, мне нравится!</div>
                </div>
            </div>
            
            <div class="chat-input">
                <input type="text" placeholder="Напишите сообщение..." id="messageInput">
                <button id="sendMessage"><i class="fas fa-paper-plane"></i></button>
            </div>
        </div>
    </section>
    
    <!-- Модальное окно авторизации -->
    <div class="auth-modal" id="authModal">
        <div class="auth-content">
            <button class="close-btn" id="closeAuth">&times;</button>
            <h2>Добро пожаловать в StreamWave</h2>
            
            <div class="auth-tabs">
                <div class="auth-tab active" data-tab="login">Вход</div>
                <div class="auth-tab" data-tab="register">Регистрация</div>
            </div>
            
            <!-- Форма входа -->
            <form class="auth-form active" id="loginForm">
                <div class="form-group">
                    <label for="loginUsername">Имя пользователя</label>
                    <input type="text" id="loginUsername" placeholder="Введите ваш никнейм" required>
                    <div class="error-message" id="loginUsernameError"></div>
                </div>
                
                <div class="form-group">
                    <label for="loginPassword">Пароль</label>
                    <input type="password" id="loginPassword" placeholder="Введите пароль" required>
                    <div class="error-message" id="loginPasswordError"></div>
                </div>
                
                <button type="submit" class="submit-btn">Войти</button>
                
                <div class="form-footer">
                    Нет аккаунта? <a href="#" id="switchToRegister">Зарегистрируйтесь</a>
                </div>
                
                <div class="success-message" id="loginSuccess"></div>
            </form>
            
            <!-- Форма регистрации -->
            <form class="auth-form" id="registerForm">
                <div class="form-group">
                    <label for="regUsername">Имя пользователя</label>
                    <input type="text" id="regUsername" placeholder="Придумайте никнейм" required>
                    <div class="error-message" id="regUsernameError"></div>
                </div>
                
                <div class="form-group">
                    <label for="regEmail">Email</label>
                    <input type="email" id="regEmail" placeholder="Введите ваш email" required>
                    <div class="error-message" id="regEmailError"></div>
                </div>
                
                <div class="form-group">
                    <label for="regPassword">Пароль</label>
                    <input type="password" id="regPassword" placeholder="Придумайте пароль" required>
                    <div class="error-message" id="regPasswordError"></div>
                </div>
                
                <div class="form-group">
                    <label for="regConfirmPassword">Подтвердите пароль</label>
                    <input type="password" id="regConfirmPassword" placeholder="Повторите пароль" required>
                    <div class="error-message" id="regConfirmPasswordError"></div>
                </div>
                
                <button type="submit" class="submit-btn">Зарегистрироваться</button>
                
                <div class="form-footer">
                    Уже есть аккаунт? <a href="#" id="switchToLogin">Войдите</a>
                </div>
                
                <div class="success-message" id="registerSuccess"></div>
            </form>
        </div>
    </div>
    
    <script>
        // Открытие/закрытие модального окна авторизации
        const authModal = document.getElementById('authModal');
        const openAuthBtn = document.getElementById('openAuth');
        const heroAuthBtn = document.getElementById('heroAuthBtn');
        const closeAuthBtn = document.getElementById('closeAuth');
        
        openAuthBtn.addEventListener('click', () => {
            authModal.classList.add('active');
        });
        
        heroAuthBtn.addEventListener('click', () => {
            authModal.classList.add('active');
        });
        
        closeAuthBtn.addEventListener('click', () => {
            authModal.classList.remove('active');
            resetForms();
        });
        
        // Закрытие по клику вне модального окна
        authModal.addEventListener('click', (e) => {
            if (e.target === authModal) {
                authModal.classList.remove('active');
                resetForms();
            }
        });
        
        // Переключение между вкладками входа и регистрации
        const tabs = document.querySelectorAll('.auth-tab');
        const loginForm = document.getElementById('loginForm');
        const registerForm = document.getElementById('registerForm');
        const switchToRegister = document.getElementById('switchToRegister');
        const switchToLogin = document.getElementById('switchToLogin');
        
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                tabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                
                if (tab.dataset.tab === 'login') {
                    loginForm.classList.add('active');
                    registerForm.classList.remove('active');
                } else {
                    loginForm.classList.remove('active');
                    registerForm.classList.add('active');
                }
            });
        });
        
        switchToRegister.addEventListener('click', (e) => {
            e.preventDefault();
            tabs[1].click();
        });
        
        switchToLogin.addEventListener('click', (e) => {
            e.preventDefault();
            tabs[0].click();
        });
        
        // Валидация форм
        function showError(element, message) {
            const errorElement = document.getElementById(`${element.id}Error`);
            errorElement.textContent = message;
            errorElement.style.display = 'block';
            element.style.borderColor = 'var(--error)';
        }
        
        function hideError(element) {
            const errorElement = document.getElementById(`${element.id}Error`);
            errorElement.style.display = 'none';
            element.style.borderColor = '';
        }
        
        function resetForms() {
            // Сброс ошибок
            document.querySelectorAll('.error-message').forEach(el => {
                el.style.display = 'none';
            });
            
            document.querySelectorAll('.success-message').forEach(el => {
                el.style.display = 'none';
            });
            
            // Сброс значений полей
            document.querySelectorAll('.auth-form input').forEach(input => {
                input.value = '';
                input.style.borderColor = '';
            });
            
            // Переключение на форму входа
            tabs[0].click();
        }
        
        // Обработка формы входа
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const username = document.getElementById('loginUsername');
            const password = document.getElementById('loginPassword');
            const loginSuccess = document.getElementById('loginSuccess');
            
            let isValid = true;
            
            // Валидация имени пользователя
            if (username.value.trim() === '') {
                showError(username, 'Введите имя пользователя');
                isValid = false;
            } else {
                hideError(username);
            }
            
            // Валидация пароля
            if (password.value.trim() === '') {
                showError(password, 'Введите пароль');
                isValid = false;
            } else if (password.value.length < 6) {
                showError(password, 'Пароль должен содержать минимум 6 символов');
                isValid = false;
            } else {
                hideError(password);
            }
            
            if (isValid) {
                // Имитация успешного входа
                loginSuccess.textContent = 'Вход выполнен успешно!';
                loginSuccess.style.display = 'block';
                
                setTimeout(() => {
                    authModal.classList.remove('active');
                    resetForms();
                    
                    // Обновляем кнопку в шапке
                    openAuthBtn.textContent = username.value;
                    openAuthBtn.style.background = 'var(--success)';
                    
                    // Разблокируем чат
                    document.getElementById('messageInput').placeholder = 'Напишите сообщение...';
                    document.getElementById('messageInput').disabled = false;
                }, 1500);
            }
        });
        
        // Обработка формы регистрации
        registerForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const username = document.getElementById('regUsername');
            const email = document.getElementById('regEmail');
            const password = document.getElementById('regPassword');
            const confirmPassword = document.getElementById('regConfirmPassword');
            const registerSuccess = document.getElementById('registerSuccess');
            
            let isValid = true;
            
            // Валидация имени пользователя
            if (username.value.trim() === '') {
                showError(username, 'Введите имя пользователя');
                isValid = false;
            } else if (username.value.length < 3) {
                showError(username, 'Имя пользователя должно содержать минимум 3 символа');
                isValid = false;
            } else {
                hideError(username);
            }
            
            // Валидация email
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (email.value.trim() === '') {
                showError(email, 'Введите email');
                isValid = false;
            } else if (!emailRegex.test(email.value)) {
                showError(email, 'Введите корректный email');
                isValid = false;
            } else {
                hideError(email);
            }
            
            // Валидация пароля
            if (password.value.trim() === '') {
                showError(password, 'Введите пароль');
                isValid = false;
            } else if (password.value.length < 6) {
                showError(password, 'Пароль должен содержать минимум 6 символов');
                isValid = false;
            } else {
                hideError(password);
            }
            
            // Подтверждение пароля
            if (confirmPassword.value.trim() === '') {
                showError(confirmPassword, 'Подтвердите пароль');
                isValid = false;
            } else if (confirmPassword.value !== password.value) {
                showError(confirmPassword, 'Пароли не совпадают');
                isValid = false;
            } else {
                hideError(confirmPassword);
            }
            
            if (isValid) {
                // Имитация успешной регистрации
                registerSuccess.textContent = 'Регистрация прошла успешно!';
                registerSuccess.style.display = 'block';
                
                setTimeout(() => {
                    // Переключаем на форму входа
                    tabs[0].click();
                    registerSuccess.style.display = 'none';
                    
                    // Заполняем поля входа
                    document.getElementById('loginUsername').value = username.value;
                    document.getElementById('loginPassword').value = password.value;
                }, 1500);
            }
        });
        
        // Чат
        const chatMessages = document.getElementById('chatMessages');
        const messageInput = document.getElementById('messageInput');
        const sendMessageBtn = document.getElementById('sendMessage');
        
        // Блокируем чат для неавторизованных пользователей
        messageInput.placeholder = 'Войдите, чтобы писать в чат';
        messageInput.disabled = true;
        
        function addMessage(user, text, isStreamer = false) {
            const message = document.createElement('div');
            message.className = 'message';
            
            const userEl = document.createElement('div');
            userEl.className = 'message-user';
            userEl.textContent = user;
            
            if (isStreamer) {
                const badge = document.createElement('span');
                badge.className = 'badge';
                badge.textContent = 'стример';
                userEl.appendChild(document.createTextNode(' '));
                userEl.appendChild(badge);
            }
            
            const textEl = document.createElement('div');
            textEl.className = 'message-text';
            textEl.textContent = text;
            
            message.appendChild(userEl);
            message.appendChild(textEl);
            
            chatMessages.appendChild(message);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }
        
        sendMessageBtn.addEventListener('click', () => {
            const message = messageInput.value.trim();
            if (message) {
                addMessage('Вы', message);
                messageInput.value = '';
                
                // Имитация ответа стримера
                if (Math.random() > 0.7) {
                    setTimeout(() => {
                        addMessage('StreamerPro', 'Спасибо за сообщение!', true);
                    }, 1000 + Math.random() * 2000);
                }
            }
        });
        
        messageInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendMessageBtn.click();
            }
        });
        
        // Плавное появление элементов при скролле
        const fadeElements = document.querySelectorAll('.hero-content, .stream-container');
        
        const fadeInOnScroll = () => {
            fadeElements.forEach(element => {
                const elementTop = element.getBoundingClientRect().top;
                const windowHeight = window.innerHeight;
                
                if (elementTop < windowHeight - 100) {
                    element.style.opacity = '1';
                    element.style.transform = 'translateY(0)';
                }
            });
        };
        
        // Инициализация
        window.addEventListener('load', () => {
            fadeElements.forEach(el => {
                el.style.opacity = '0';
                el.style.transform = 'translateY(20px)';
                el.style.transition = 'opacity 0.6s ease-out, transform 0.6s ease-out';
            });
            
            fadeInOnScroll();
        });
        
        window.addEventListener('scroll', fadeInOnScroll);
    </script>
</body>
</html>
