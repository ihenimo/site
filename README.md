<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ангелина - директор зоомагазина</title>
    <!-- Подключаем jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        /* Общие стили для навигации */
        body {
            font-family: 'Inter', system-ui, sans-serif;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            position: relative;
            overflow-x: hidden;
        }
        
        /* Навигационное меню */
        nav {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 15px 20px;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .nav-container {
            max-width: 1100px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: #FFD700;
            text-decoration: none;
        }
        
        .nav-menu {
            display: flex;
            list-style: none;
            margin: 0;
            padding: 0;
            gap: 30px;
        }
        
        .nav-item {
            position: relative;
        }
        
        .nav-link {
            color: white;
            text-decoration: none;
            font-weight: 500;
            padding: 8px 0;
            transition: color 0.3s;
            position: relative;
        }
        
        .nav-link:hover {
            color: #FFD700;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: #FFD700;
            transition: width 0.3s;
        }
        
        .nav-link:hover::after {
            width: 100%;
        }
        
        /* Бургер-меню */
        .burger-menu {
            display: none;
            flex-direction: column;
            cursor: pointer;
            gap: 4px;
            padding: 5px;
        }
        
        .burger-line {
            width: 25px;
            height: 3px;
            background: white;
            border-radius: 2px;
            transition: 0.3s;
        }
        
        .burger-menu.active .burger-line:nth-child(1) {
            transform: rotate(45deg) translate(6px, 6px);
        }
        
        .burger-menu.active .burger-line:nth-child(2) {
            opacity: 0;
        }
        
        .burger-menu.active .burger-line:nth-child(3) {
            transform: rotate(-45deg) translate(6px, -6px);
        }
        
        /* Стили для мобильного меню */
        @media (max-width: 768px) {
            .burger-menu {
                display: flex;
            }
            
            .nav-menu {
                position: fixed;
                top: 70px;
                left: 0;
                right: 0;
                background: rgba(255, 255, 255, 0.95);
                backdrop-filter: blur(10px);
                flex-direction: column;
                padding: 20px;
                gap: 15px;
                transform: translateY(-100%);
                opacity: 0;
                visibility: hidden;
                transition: 0.3s;
                box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
                border-radius: 0 0 15px 15px;
            }
            
            .nav-menu.active {
                transform: translateY(0);
                opacity: 1;
                visibility: visible;
            }
            
            .nav-link {
                color: #333;
                display: block;
                padding: 10px;
                border-radius: 8px;
                transition: background 0.3s;
            }
            
            .nav-link:hover {
                background: rgba(255, 215, 0, 0.1);
                color: #333;
            }
        }
        
        /* Отступ для фиксированной навигации */
        .hero-section {
            margin-top: 80px;
        }
        
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }
        
        .star {
            position: absolute;
            background: #ffffff;
            border-radius: 50%;
            animation: twinkle 3s infinite;
        }
        
        @keyframes twinkle {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 1; }
        }
        
        .hero-section {
            display: flex;
            align-items: center;
            max-width: 1100px;
            margin: 0 auto;
            padding: 40px 20px 0px 20px;
            min-height: 100vh;
            gap: 60px;
            position: relative;
            z-index: 1;
        }
        
        .hero-content {
            flex: 1;
            margin-top: -60px;
        }
        
        .hero-content h1 {
            font-size: 3rem;
            margin-bottom: 15px;
            font-weight: 700;
        }
        
        .hero-content h1 span {
            color: #FFD700;
        }
        
        .hero-content h2 {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: #ffffffe6;
            font-weight: 400;
            position: relative;
            padding-left: 20px;
        }
        
        .hero-content h2::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 4px;
            background: #FFD700;
            border-radius: 2px;
        }
        
        .hero-description {
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: #ffffffcc;
            line-height: 1.7;
            background: #ffffff1a;
            padding: 15px;
            border-radius: 12px;
            border-left: 4px solid #ef7e0d;
        }
        
        /* Стили для кнопок с подсветкой вместо прыгания */
        .cta-button {
            display: inline-block;
            padding: 12px 25px;
            background: #ef7e0d;
            color: #ffffff;
            text-decoration: none;
            border-radius: 25px;
            font-weight: 600;
            box-shadow: 0 4px 15px #ef7e0d4d;
            transition: all 0.3s ease;
            margin-bottom: 0;
            cursor: pointer;
            border: none;
            font-size: 16px;
        }
        
        .cta-button:hover {
            background: #ff9500;
            box-shadow: 0 6px 20px #ef7e0d99;
        }
        
        .hero-image {
            flex: 1;
            text-align: center;
            position: relative;
        }
        
        .hero-image img {
            width: 400px;
            height: 400px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid #ffffff4d;
        }
        
        .small-circle {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 150px;
            height: 150px;
            border-radius: 50%;
            border: 3px solid #FFD700;
            overflow: hidden;
            background: white;
        }
        
        .small-circle img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border: none;
        }

        /* ОБЩИЙ КОНТЕЙНЕР ДЛЯ ВСЕХ СЕКЦИЙ */
        .sections-container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Стили для секции достижений */
        .achievements-section {
            padding: 60px 0;
            position: relative;
            z-index: 1;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin: 0 0 40px 0;
            color: #FFD700;
            font-weight: 700;
            position: relative;
            display: inline-block;
            left: 50%;
            transform: translateX(-50%);
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 25%;
            width: 50%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #FFD700, transparent);
            border-radius: 2px;
        }

        /* НОВЫЙ ГРИД ДЛЯ ДОСТИЖЕНИЙ */
        .achievements-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .achievement-card {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 15px;
            padding: 25px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            transition: all 0.3s ease;
            min-height: 250px;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        .achievement-card:hover {
            background: rgba(255, 255, 255, 0.12);
            border-color: rgba(255, 215, 0, 0.4);
        }

        .achievement-icon {
            width: 70px;
            height: 70px;
            margin: 0 auto 20px;
            background: rgba(255, 215, 0, 0.15);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: #FFD700;
        }

        .achievement-title {
            font-size: 1.3rem;
            font-weight: 600;
            margin: 0 0 12px 0;
            color: #ffffff;
            line-height: 1.3;
        }

        .achievement-description {
            color: rgba(255, 255, 255, 0.85);
            line-height: 1.6;
            font-size: 1rem;
            margin: 0;
        }

        /* Стили для секции товаров и услуг */
        .products-section {
            padding: 60px 0;
            position: relative;
            z-index: 1;
        }

        /* НОВЫЙ ГРИД ДЛЯ ТОВАРОВ И УСЛУГ */
        .products-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .product-card {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 25px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            min-height: 380px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            cursor: pointer;
        }

        .product-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #ef7e0d, #FFD700, #56CCF2);
            border-radius: 20px 20px 0 0;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .product-card:hover {
            background: rgba(255, 255, 255, 0.12);
            border-color: rgba(255, 215, 0, 0.4);
        }

        .product-card:hover::before {
            opacity: 1;
        }

        .product-header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        .product-icon {
            width: 80px;
            height: 80px;
            background: linear-gradient(135deg, rgba(239, 126, 13, 0.15), rgba(255, 215, 0, 0.1));
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: #FFD700;
            border: 2px solid rgba(255, 215, 0, 0.2);
            flex-shrink: 0;
            transition: all 0.3s ease;
        }

        .product-card:hover .product-icon {
            background: linear-gradient(135deg, rgba(239, 126, 13, 0.25), rgba(255, 215, 0, 0.2));
            border-color: rgba(255, 215, 0, 0.4);
            transform: rotate(15deg);
        }

        .product-title-wrapper {
            flex: 1;
        }

        .product-title {
            font-size: 1.4rem;
            font-weight: 600;
            margin: 0 0 5px 0;
            color: #ffffff;
            line-height: 1.3;
        }

        .product-category {
            font-size: 0.85rem;
            color: rgba(255, 255, 255, 0.7);
            text-transform: uppercase;
            letter-spacing: 1px;
            display: inline-block;
            padding: 3px 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
        }

        .product-description {
            color: rgba(255, 255, 255, 0.85);
            line-height: 1.6;
            font-size: 1rem;
            margin: 0 0 25px 0;
            flex-grow: 1;
        }

        .product-features {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 25px;
        }

        .product-feature {
            background: rgba(239, 126, 13, 0.15);
            color: #ffffff;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 500;
            border: 1px solid rgba(239, 126, 13, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .product-feature:hover {
            background: rgba(239, 126, 13, 0.25);
        }

        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* ИЗМЕНЁННЫЙ СТИЛЬ ДЛЯ ЦЕНЫ - "от 10 BYN" */
        .product-price {
            font-size: 1.3rem;
            font-weight: 700;
            color: #FFD700;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        /* Убираем старый псевдоэлемент ::before и добавляем ::after */
        .product-price::after {
            content: ' BYN';
            font-size: 0.9rem;
            opacity: 0.8;
        }

        .product-price.free {
            color: #4CAF50;
        }

        /* Для бесплатных услуг скрываем "BYN" */
        .product-price.free::after {
            content: '';
        }

        .product-action {
            background: linear-gradient(135deg, #ef7e0d, #ff9500);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            font-size: 0.9rem;
            box-shadow: 0 4px 15px rgba(239, 126, 13, 0.3);
        }

        .product-action:hover {
            background: linear-gradient(135deg, #ff9500, #ffaa33);
            box-shadow: 0 6px 20px rgba(239, 126, 13, 0.4);
        }

        /* Стили для разделения товаров и услуг */
        .product-type-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            z-index: 2;
        }

        .type-product {
            background: rgba(86, 204, 242, 0.2);
            color: #56CCF2;
            border: 1px solid rgba(86, 204, 242, 0.4);
        }

        .type-service {
            background: rgba(156, 39, 176, 0.2);
            color: #9C27B0;
            border: 1px solid rgba(156, 39, 176, 0.4);
        }

        /* Секция контактов с формой Getform.io */
        .contact-section {
            padding: 60px 0;
            position: relative;
            z-index: 1;
        }

        .contact-form {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 40px;
            border: 1px solid rgba(255, 255, 255, 0.15);
            max-width: 1100px;
            margin: 0 auto;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #FFD700;
            font-weight: 500;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 14px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.05);
            color: white;
            font-size: 16px;
            transition: all 0.3s ease;
            font-family: 'Inter', system-ui, sans-serif;
            box-sizing: border-box;
        }

        .form-group select {
            appearance: none;
            -webkit-appearance: none;
            -moz-appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23FFD700' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 15px center;
            background-size: 20px;
            padding-right: 45px;
        }

        .form-group select option {
            background: #667eea;
            color: white;
            padding: 10px;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: #FFD700;
            background: rgba(255, 255, 255, 0.1);
            box-shadow: 0 0 0 3px rgba(255, 215, 0, 0.1);
        }

        .form-group input::placeholder,
        .form-group textarea::placeholder {
            color: rgba(255, 255, 255, 0.5);
        }

        .form-group textarea {
            min-height: 150px;
            resize: vertical;
        }

        /* Стили для чекбокса на одном уровне с текстом */
        .checkbox-container {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            font-weight: normal;
            color: rgba(255, 255, 255, 0.85);
            margin: 0;
            padding: 5px 0;
        }

        .checkbox-container input[type="checkbox"] {
            margin: 0;
            width: 18px;
            height: 18px;
            cursor: pointer;
            flex-shrink: 0;
        }

        .checkbox-text {
            line-height: 1.4;
        }

        /* Сообщения об успехе/ошибке */
        .form-message {
            padding: 12px 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
            font-weight: 500;
            display: none;
        }

        .form-message.success {
            background: rgba(76, 175, 80, 0.2);
            border: 1px solid rgba(76, 175, 80, 0.4);
            color: #a5d6a7;
            display: block;
        }

        .form-message.error {
            background: rgba(244, 67, 54, 0.2);
            border: 1px solid rgba(244, 67, 54, 0.4);
            color: #ef9a9a;
            display: block;
        }

        /* Индикатор загрузки */
        .form-loading {
            display: none;
            text-align: center;
            margin: 15px 0;
        }

        .form-loading.active {
            display: block;
        }

        .spinner {
            display: inline-block;
            width: 30px;
            height: 30px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: #FFD700;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .page-bottom-spacing {
            height: 50px;
            width: 100%;
            clear: both;
        }

        /* jQuery-анимации */
        .nav-link.active {
            color: #FFD700 !important;
            font-weight: 700;
        }
        
        .nav-link.active::after {
            width: 100% !important;
        }
        
        .product-card.selected {
            border: 2px solid #FFD700 !important;
            background: rgba(255, 215, 0, 0.05) !important;
            transform: scale(1.02);
        }
        
        @keyframes logoPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .footer-text {
            text-align: center;
            padding: 20px;
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9rem;
            margin-top: 30px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* Медиа-запросы для адаптивности */
        @media (max-width: 768px) {
            .hero-section {
                flex-direction: column;
                text-align: center;
                gap: 30px;
                padding: 30px 20px 0px 20px;
            }

            .hero-content h1 {
                font-size: 2.2rem;
                margin-bottom: 12px;
            }

            .hero-content h2 {
                font-size: 1.2rem;
                padding-left: 0;
                margin-bottom: 12px;
            }

            .hero-content h2::before {
                display: none;
            }

            .hero-image img {
                width: 300px;
                height: 300px;
            }

            .small-circle {
                width: 120px;
                height: 120px;
                top: 10px;
                right: 10px;
            }

            .section-title {
                font-size: 2rem;
                margin-bottom: 30px;
            }

            .achievements-container,
            .products-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .product-card {
                padding: 25px;
                min-height: auto;
            }
            
            .product-header {
                gap: 15px;
            }
            
            .product-icon {
                width: 70px;
                height: 70px;
                font-size: 1.8rem;
            }
            
            .product-title {
                font-size: 1.3rem;
            }
            
            .contact-form {
                padding: 30px;
            }

            .checkbox-container {
                gap: 8px;
            }
            
            .checkbox-container input[type="checkbox"] {
                width: 16px;
                height: 16px;
            }

            .form-group select {
                padding-right: 40px;
                background-position: right 12px center;
                background-size: 18px;
            }

            .page-bottom-spacing {
                height: 40px;
            }
        }

        @media (max-width: 480px) {
            .hero-content h1 {
                font-size: 1.8rem;
                margin-bottom: 10px;
            }

            .hero-image img {
                width: 250px;
                height: 250px;
            }

            .small-circle {
                width: 100px;
                height: 100px;
            }

            .section-title {
                font-size: 1.6rem;
                margin-bottom: 25px;
            }

            .achievement-card,
            .product-card {
                padding: 20px;
            }
            
            .product-header {
                flex-direction: column;
                text-align: center;
                gap: 15px;
            }
            
            .product-title-wrapper {
                width: 100%;
            }
            
            .product-footer {
                flex-direction: column;
                gap: 15px;
                align-items: stretch;
            }
            
            .product-action {
                text-align: center;
            }
            
            .product-features {
                justify-content: center;
            }

            .contact-form {
                padding: 25px;
            }

            .checkbox-container {
                gap: 6px;
                font-size: 0.9rem;
            }
            
            .checkbox-container input[type="checkbox"] {
                width: 14px;
                height: 14px;
            }

            .form-group select {
                padding-right: 35px;
                background-position: right 10px center;
                background-size: 16px;
            }

            .page-bottom-spacing {
                height: 30px;
            }
        }
    </style>
</head>
<body>
    <!-- Навигационное меню -->
    <nav>
        <div class="nav-container">
            <a href="#home" class="logo">ЗооМир</a>
            
            <div class="burger-menu" id="burgerMenu">
                <div class="burger-line"></div>
                <div class="burger-line"></div>
                <div class="burger-line"></div>
            </div>
            
            <ul class="nav-menu" id="navMenu">
                <li class="nav-item"><a href="#home" class="nav-link">Главная</a></li>
                <li class="nav-item"><a href="#achievements" class="nav-link">Достижения</a></li>
                <li class="nav-item"><a href="#products" class="nav-link">Товары и услуги</a></li>
                <li class="nav-item"><a href="#contact" class="nav-link">Обратная связь</a></li>
            </ul>
        </div>
    </nav>

    <div class="stars" id="stars"></div>
    
    <section class="hero-section" id="home">
        <div class="hero-content">
            <h1>Эксперт в заботе о ваших <span>питомцах!</span></h1>
            <h2>Мы помогаем создать дом, полный любви и заботы для вашего пушистого друга. От первого поводка до любимой игрушки — мы рядом на каждом этапе жизни вашего питомца.</h2>
            <p class="hero-description">Ленивец - тотем нашего директора.</p>
            <button class="cta-button" id="contactBtn">Связаться со мной</button>
        </div>
        <div class="hero-image">
            <img src="я.jpg" alt="Ангелина - директор зоомагазина">
            <div class="small-circle">
                <img src="ленивец.jpg" alt="Ленивец">
            </div>
        </div>
    </section>

    <!-- ОБЩИЙ КОНТЕЙНЕР ДЛЯ ВСЕХ СЕКЦИЙ -->
    <div class="sections-container">
        <!-- Секция достижений -->
        <section class="achievements-section" id="achievements">
            <h2 class="section-title">Наши Достижения</h2>
            <div class="achievements-container">
                <div class="achievement-card">
                    <div class="achievement-icon">🎯</div>
                    <h3 class="achievement-title">Более 10 000 довольных хвостатых клиентов</h3>
                    <p class="achievement-description">С 2018 года мы помогли обустроить комфортную жизнь для 10 000+ питомцев. Каждая вторая покупка — по рекомендации довольных клиентов!</p>
                </div>

                <div class="achievement-card">
                    <div class="achievement-icon">👨‍⚕️</div>
                    <h3 class="achievement-title">Эксперты с ветеринарным образованием</h3>
                    <p class="achievement-description">Наши консультанты — специалисты с ветеринарным образованием. Бесплатно помогаем подобрать оптимальный рацион и уход именно для вашего питомца.</p>
                </div>

                <div class="achievement-card">
                    <div class="achievement-icon">⭐</div>
                    <h3 class="achievement-title">95% товаров — премиум-качество</h3>
                    <p class="achievement-description">Мы тщательно тестируем ассортимент: 95% товаров в нашем магазине имеют сертификаты качества и одобрены ветеринарами.</p>
                </div>

                <div class="achievement-card">
                    <div class="achievement-icon">🤝</div>
                    <h3 class="achievement-title">Партнерство с приютами для животных</h3>
                    <p class="achievement-description">Ежемесячно помогаем местным приютам: передаем корм, лекарства и аксессуары. Уже подарили вторую жизнь 500+ бездомным животным.</p>
                </div>

                <div class="achievement-card">
                    <div class="achievement-icon">👑</div>
                    <h3 class="achievement-title">Собственная линия гипоаллергенных кормов</h3>
                    <p class="achievement-description">Разработали эксклюзивную линейку кормов для питомцев с особенностями здоровья. У 98% животных отметили улучшение состояния.</p>
                </div>

                <div class="achievement-card">
                    <div class="achievement-icon">🏅</div>
                    <h3 class="achievement-title">Лучший зоомагазин города 2023-2024</h3>
                    <p class="achievement-description">По оценкам покупателей стали лучшим зоомагазином города два года подряд. Ваша любовь — наша главная награда!</p>
                </div>
            </div>
        </section>

        <!-- Секция товаров и услуг -->
        <section class="products-section" id="products">
            <h2 class="section-title">Наши товары и услуги</h2>
            <div class="products-container">
                <!-- Товар 1: Корма -->
                <div class="product-card">
                    <span class="product-type-badge type-product">Товар</span>
                    <div class="product-header">
                        <div class="product-icon">🍖</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Качественные корма</h3>
                            <span class="product-category">Питание</span>
                        </div>
                    </div>
                    <p class="product-description">Широкий ассортимент кормов премиум-класса для собак, кошек, грызунов, птиц и экзотических животных от ведущих мировых производителей.</p>
                    <div class="product-features">
                        <span class="product-feature">Сухие корма</span>
                        <span class="product-feature">Влажные корма</span>
                        <span class="product-feature">Лечебные диеты</span>
                        <span class="product-feature">Натуральные лакомства</span>
                    </div>
                    <div class="product-footer">
                        <!-- ИЗМЕНЁННАЯ СТРУКТУРА ЦЕНЫ - теперь "от 15" -->
                        <div class="product-price">от 15</div>
                        <a href="#contact" class="product-action">Заказать</a>
                    </div>
                </div>

                <!-- Товар 2: Аксессуары -->
                <div class="product-card">
                    <span class="product-type-badge type-product">Товар</span>
                    <div class="product-header">
                        <div class="product-icon">🐕</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Аксессуары и игрушки</h3>
                            <span class="product-category">Аксессуары</span>
                        </div>
                    </div>
                    <p class="product-description">Все необходимое для комфорта вашего питомца: ошейники, поводки, миски, лежанки, переноски и развивающие игрушки.</p>
                    <div class="product-features">
                        <span class="product-feature">Ошейники</span>
                        <span class="product-feature">Миски и поилки</span>
                        <span class="product-feature">Лежанки</span>
                        <span class="product-feature">Интерактивные игрушки</span>
                    </div>
                    <div class="product-footer">
                        <!-- ИЗМЕНЁННАЯ СТРУКТУРА ЦЕНЫ - теперь "от 10" -->
                        <div class="product-price">от 10</div>
                        <a href="#contact" class="product-action">Заказать</a>
                    </div>
                </div>

                <!-- Товар 3: Средства ухода -->
                <div class="product-card">
                    <span class="product-type-badge type-product">Товар</span>
                    <div class="product-header">
                        <div class="product-icon">✨</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Средства по уходу</h3>
                            <span class="product-category">Гигиена</span>
                        </div>
                    </div>
                    <p class="product-description">Профессиональная косметика и средства гигиены для поддержания здоровья и красоты вашего питомца.</p>
                    <div class="product-features">
                        <span class="product-feature">Шампуни</span>
                        <span class="product-feature">Расчески</span>
                        <span class="product-feature">Средства от паразитов</span>
                        <span class="product-feature">Гигиеническая косметика</span>
                    </div>
                    <div class="product-footer">
                        <!-- ИЗМЕНЁННАЯ СТРУКТУРА ЦЕНЫ - теперь "от 10" -->
                        <div class="product-price">от 10</div>
                        <a href="#contact" class="product-action">Заказать</a>
                    </div>
                </div>

                <!-- Услуга 1: Консультации -->
                <div class="product-card">
                    <span class="product-type-badge type-service">Услуга</span>
                    <div class="product-header">
                        <div class="product-icon">👨‍⚕️</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Ветеринарные консультации</h3>
                            <span class="product-category">Консультация</span>
                        </div>
                    </div>
                    <p class="product-description">Бесплатные консультации от наших специалистов с ветеринарным образованием по подбору корма и уходу за питомцем.</p>
                    <div class="product-features">
                        <span class="product-feature">Подбор рациона</span>
                        <span class="product-feature">Рекомендации по уходу</span>
                        <span class="product-feature">Первая помощь</span>
                        <span class="product-feature">Профилактика заболеваний</span>
                    </div>
                    <div class="product-footer">
                        <!-- Для бесплатных услуг используем класс free -->
                        <div class="product-price free">Бесплатно</div>
                        <a href="#contact" class="product-action">Записаться</a>
                    </div>
                </div>

                <!-- Услуга 2: Груминг -->
                <div class="product-card">
                    <span class="product-type-badge type-service">Услуга</span>
                    <div class="product-header">
                        <div class="product-icon">✂️</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Услуги груминга</h3>
                            <span class="product-category">Уход</span>
                        </div>
                    </div>
                    <p class="product-description">Профессиональный уход за шерстью, стрижка, мытье и другие процедуры для поддержания опрятного вида вашего питомца.</p>
                    <div class="product-features">
                        <span class="product-feature">Стрижка</span>
                        <span class="product-feature">Мытье и сушка</span>
                        <span class="product-feature">Чистка ушей</span>
                        <span class="product-feature">Стрижка когтей</span>
                    </div>
                    <div class="product-footer">
                        <!-- ИЗМЕНЁННАЯ СТРУКТУРА ЦЕНЫ - теперь "от 30" -->
                        <div class="product-price">от 30</div>
                        <a href="#contact" class="product-action">Записаться</a>
                    </div>
                </div>

                <!-- Услуга 3: Дрессировка -->
                <div class="product-card">
                    <span class="product-type-badge type-service">Услуга</span>
                    <div class="product-header">
                        <div class="product-icon">🎓</div>
                        <div class="product-title-wrapper">
                            <h3 class="product-title">Курсы дрессировки</h3>
                            <span class="product-category">Обучение</span>
                        </div>
                    </div>
                    <p class="product-description">Обучение собак основным командам, коррекция поведения и социализация под руководством опытных кинологов.</p>
                    <div class="product-features">
                        <span class="product-feature">Базовые команды</span>
                        <span class="product-feature">Коррекция поведения</span>
                        <span class="product-feature">Социализация</span>
                        <span class="product-feature">Специальные курсы</span>
                    </div>
                    <div class="product-footer">
                        <!-- ИЗМЕНЁННАЯ СТРУКТУРА ЦЕНЫ - теперь "от 55" -->
                        <div class="product-price">от 55</div>
                        <a href="#contact" class="product-action">Записаться</a>
                    </div>
                </div>
            </div>
        </section>

        <!-- Секция обратной связи с Getform.io -->
        <section class="contact-section" id="contact">
            <h2 class="section-title">Обратная связь</h2>
            
            <div class="contact-form">
                <!-- Сообщения об успехе/ошибке -->
                <div id="formMessage" class="form-message"></div>
                
                <!-- Индикатор загрузки -->
                <div id="formLoading" class="form-loading">
                    <div class="spinner"></div>
                    <p>Отправка формы...</p>
                </div>
                
                <!-- Форма Getform.io -->
                <!-- ВАЖНО: Замените YOUR_FORM_ID на ваш реальный ID из Getform.io -->
                <form id="feedbackForm" action="https://getform.io/f/bejvrvla" method="POST">
                    <!-- Скрытое поле для указания формы -->
                    <input type="hidden" name="form_name" value="Форма обратной связи с сайта ЗооМир">
                    
                    <div class="form-group">
                        <label for="name">Ваше имя *</label>
                        <input type="text" id="name" name="name" placeholder="Введите ваше имя" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="email">Ваш email *</label>
                        <input type="email" id="email" name="email" placeholder="Введите ваш email" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="phone">Ваш телефон</label>
                        <input type="tel" id="phone" name="phone" placeholder="+375 (XX) XXX-XX-XX">
                    </div>
                    
                    <div class="form-group">
                        <label for="interest">Меня интересует:</label>
                        <select id="interest" name="interest">
                            <option value="">Выберите вариант</option>
                            <option value="product">Покупка товаров</option>
                            <option value="service">Заказ услуг</option>
                            <option value="consultation">Консультация специалиста</option>
                            <option value="partnership">Сотрудничество</option>
                            <option value="other">Другое</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="budget">Бюджет (BYN):</label>
                        <select id="budget" name="budget">
                            <option value="">Не указано</option>
                            <option value="0-50">до 50 BYN</option>
                            <option value="50-100">50-100 BYN</option>
                            <option value="100-200">100-200 BYN</option>
                            <option value="200-500">200-500 BYN</option>
                            <option value="500+">более 500 BYN</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="message">Ваше сообщение *</label>
                        <textarea id="message" name="message" placeholder="Опишите ваш вопрос или пожелание..." required></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label class="checkbox-container">
                            <input type="checkbox" name="newsletter" checked>
                            <span class="checkbox-text">Я согласен получать новости и специальные предложения</span>
                        </label>
                    </div>
                    
                    <button type="submit" class="cta-button" id="submitBtn">Отправить сообщение</button>
                </form>
            </div>
        </section>
    </div>

    <!-- Футер -->
    <div class="footer-text" id="footerText"></div>

    <!-- Отступ в самом низу страницы -->
    <div class="page-bottom-spacing"></div>

    <script>
        $(document).ready(function() {
            // ==================== ОСНОВНОЙ JAVASCRIPT ====================
            
            // Создание звездочек
            const starsContainer = document.getElementById('stars');
            const starsCount = 100;
            
            for (let i = 0; i < starsCount; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                
                const size = Math.random() * 3 + 1;
                const left = Math.random() * 100;
                const top = Math.random() * 100;
                const delay = Math.random() * 3;
                
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                star.style.left = `${left}%`;
                star.style.top = `${top}%`;
                star.style.animationDelay = `${delay}s`;
                
                starsContainer.appendChild(star);
            }
            
            // Обработчики для навигации
            const burgerMenu = document.getElementById('burgerMenu');
            const navMenu = document.getElementById('navMenu');
            const navLinks = document.querySelectorAll('.nav-link');
            const contactBtn = document.getElementById('contactBtn');
            const feedbackForm = document.getElementById('feedbackForm');
            const formMessage = document.getElementById('formMessage');
            const formLoading = document.getElementById('formLoading');
            const productActions = document.querySelectorAll('.product-action');
            
            // Переключение бургер-меню
            burgerMenu.addEventListener('click', function() {
                burgerMenu.classList.toggle('active');
                navMenu.classList.toggle('active');
            });
            
            // Закрытие меню при клике на ссылку (для мобильной версии)
            navLinks.forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href');
                    const targetSection = document.querySelector(targetId);
                    
                    // Закрываем меню на мобильных устройствах
                    if (window.innerWidth <= 768) {
                        burgerMenu.classList.remove('active');
                        navMenu.classList.remove('active');
                    }
                    
                    // Плавная прокрутка
                    window.scrollTo({
                        top: targetSection.offsetTop - 80,
                        behavior: 'smooth'
                    });
                });
            });
            
            // Обработчик для кнопки "Связаться со мной"
            contactBtn.addEventListener('click', function() {
                const contactSection = document.getElementById('contact');
                window.scrollTo({
                    top: contactSection.offsetTop - 80,
                    behavior: 'smooth'
                });
            });
            
            // Обработчик для кнопок в карточках товаров и услуг
            productActions.forEach(button => {
                button.addEventListener('click', function(e) {
                    e.preventDefault();
                    const contactSection = document.getElementById('contact');
                    window.scrollTo({
                        top: contactSection.offsetTop - 80,
                        behavior: 'smooth'
                    });
                });
            });
            
            // Обработчик для формы обратной связи (Getform.io)
            feedbackForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                // Показать индикатор загрузки
                formLoading.classList.add('active');
                formMessage.style.display = 'none';
                
                // Собираем данные формы
                const formData = new FormData(this);
                
                // Отправляем данные на Getform.io
                fetch(this.action, {
                    method: 'POST',
                    body: formData,
                    headers: {
                        'Accept': 'application/json'
                    }
                })
                .then(response => {
                    if (response.ok) {
                        // Успешная отправка
                        formMessage.textContent = 'Спасибо! Ваше сообщение отправлено. Мы свяжемся с вами в ближайшее время.';
                        formMessage.className = 'form-message success';
                        formMessage.style.display = 'block';
                        
                        // Очистка формы
                        feedbackForm.reset();
                        
                        // Прокрутка к сообщению об успехе
                        formMessage.scrollIntoView({ behavior: 'smooth', block: 'center' });
                    } else {
                        // Ошибка сервера
                        throw new Error('Ошибка сервера');
                    }
                })
                .catch(error => {
                    // Ошибка сети или сервера
                    formMessage.textContent = 'Произошла ошибка при отправке формы. Пожалуйста, попробуйте еще раз или свяжитесь с нами другим способом.';
                    formMessage.className = 'form-message error';
                    formMessage.style.display = 'block';
                    
                    // Прокрутка к сообщению об ошибке
                    formMessage.scrollIntoView({ behavior: 'smooth', block: 'center' });
                })
                .finally(() => {
                    // Скрыть индикатор загрузки
                    formLoading.classList.remove('active');
                });
            });
            
            // Маска для телефона
            const phoneInput = document.getElementById('phone');
            if (phoneInput) {
                phoneInput.addEventListener('input', function(e) {
                    let value = this.value.replace(/\D/g, '');
                    let formattedValue = '';
                    
                    if (value.length > 0) {
                        formattedValue = '+375 (';
                        if (value.length > 3) {
                            formattedValue += value.substring(3, 5);
                            if (value.length > 5) {
                                formattedValue += ') ' + value.substring(5, 8);
                                if (value.length > 8) {
                                    formattedValue += '-' + value.substring(8, 10);
                                    if (value.length > 10) {
                                        formattedValue += '-' + value.substring(10, 12);
                                    }
                                }
                            }
                        } else {
                            formattedValue += value.substring(3);
                        }
                    }
                    
                    this.value = formattedValue;
                });
            }
            
            // Закрытие меню при клике вне его области (для мобильной версии)
            document.addEventListener('click', function(e) {
                if (window.innerWidth <= 768) {
                    const isClickInsideMenu = navMenu.contains(e.target) || burgerMenu.contains(e.target);
                    
                    if (!isClickInsideMenu && navMenu.classList.contains('active')) {
                        burgerMenu.classList.remove('active');
                        navMenu.classList.remove('active');
                    }
                }
            });
            
            // Закрытие меню при изменении размера окна
            window.addEventListener('resize', function() {
                if (window.innerWidth > 768) {
                    burgerMenu.classList.remove('active');
                    navMenu.classList.remove('active');
                }
            });
            
            // ==================== JQUERY АНИМАЦИИ ====================
            
            // 1. Плавная прокрутка к разделам с jQuery
            $('a[href^="#"]').on('click', function(e) {
                e.preventDefault();
                const target = $(this.hash);
                if (target.length) {
                    $('html, body').animate({
                        scrollTop: target.offset().top - 80
                    }, 800);
                    
                    // Закрытие мобильного меню
                    if ($(window).width() <= 768) {
                        $('#burgerMenu').removeClass('active');
                        $('#navMenu').removeClass('active');
                    }
                }
            });
            
            // 2. Анимация появления элементов при прокрутке
            function animateOnScroll() {
                $('.achievement-card, .product-card').each(function() {
                    const elementTop = $(this).offset().top;
                    const windowBottom = $(window).scrollTop() + $(window).height();
                    
                    if (elementTop < windowBottom - 100) {
                        $(this).css({
                            'opacity': '1',
                            'transform': 'translateY(0)'
                        });
                    }
                });
            }
            
            // Устанавливаем начальные стили для анимации
            $('.achievement-card, .product-card').css({
                'opacity': '0',
                'transform': 'translateY(30px)',
                'transition': 'all 0.6s ease'
            });
            
            // Запускаем анимацию при загрузке и прокрутке
            animateOnScroll();
            $(window).on('scroll', animateOnScroll);
            
            // 3. Динамическое изменение активного пункта меню
            $(window).on('scroll', function() {
                const scrollPos = $(document).scrollTop() + 100;
                
                $('.nav-link').each(function() {
                    const currLink = $(this);
                    const refElement = $(currLink.attr('href'));
                    
                    if (refElement.length && refElement.position().top <= scrollPos && 
                        refElement.position().top + refElement.height() > scrollPos) {
                        $('.nav-link').removeClass('active');
                        currLink.addClass('active');
                    }
                });
            });
            
            // 4. Всплывающая подсказка для кнопок
            $('.cta-button, .product-action').hover(
                function() {
                    $(this).css('transform', 'scale(1.05)');
                },
                function() {
                    $(this).css('transform', 'scale(1)');
                }
            );
            
            // 5. Плавное скрытие/показа секций по клику на заголовки
            $('.section-title').on('click', function() {
                const section = $(this).closest('section').find('.achievements-container, .products-container');
                if (section.is(':visible')) {
                    section.slideUp(400);
                    $(this).css('color', '#ffffff');
                } else {
                    section.slideDown(600);
                    $(this).css('color', '#FFD700');
                }
            });
            
            // 6. Интерактивный счетчик для достижений
            function animateCounter() {
                const achievementCards = $('.achievement-card');
                achievementCards.each(function(index) {
                    const card = $(this);
                    
                    // Добавляем небольшую задержку для каждого элемента
                    setTimeout(function() {
                        card.css({
                            'box-shadow': '0 10px 25px rgba(0,0,0,0.2)',
                            'transform': 'translateY(-5px)'
                        });
                        
                        // Возвращаем к исходному состоянию через 1 секунду
                        setTimeout(function() {
                            card.css({
                                'box-shadow': '',
                                'transform': ''
                            });
                        }, 1000);
                    }, index * 200);
                });
            }
            
            // Активируем анимацию счетчика при клике на заголовок секции достижений
            $('#achievements .section-title').on('click', function() {
                animateCounter();
            });
            
            // 7. Анимация для формы обратной связи
            $('#feedbackForm input, #feedbackForm textarea, #feedbackForm select').focus(function() {
                $(this).parent().css('transform', 'scale(1.02)');
            }).blur(function() {
                $(this).parent().css('transform', 'scale(1)');
            });
            
            // 8. Подсветка выбранного товара/услуги при клике
            $('.product-card').on('click', function() {
                $('.product-card').removeClass('selected');
                $(this).addClass('selected');
                
                // Анимация выбора
                $(this).animate({
                    'box-shadow': '0 15px 35px rgba(255, 215, 0, 0.3)'
                }, 300);
                
                // Скролл к форме заказа
                setTimeout(function() {
                    $('html, body').animate({
                        scrollTop: $('#contact').offset().top - 100
                    }, 800);
                }, 500);
            });
            
            // 9. Анимация логотипа при загрузке
            $('.logo').hide().fadeIn(1500).css({
                'animation': 'logoPulse 2s infinite'
            });
            
            // 10. Динамическое обновление года в футере
            const currentYear = new Date().getFullYear();
            $('#footerText').html(`&copy; ${currentYear} ЗооМир. Все права защищены.`);
        });
    </script>
</body>
</html>
