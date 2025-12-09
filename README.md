<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VibeShop - одежда и кроссовки</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 15px;
            color: #333;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            margin-bottom: 20px;
        }
        
        .header h1 {
            margin: 0;
            font-size: 24px;
        }
        
        .nav {
            display: flex;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .nav-btn {
            flex: 1;
            padding: 12px;
            border: none;
            background: none;
            cursor: pointer;
            font-size: 14px;
        }
        
        .nav-btn.active {
            background-color: #3498db;
            color: white;
        }
        
        .section {
            display: none;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .section.active {
            display: block;
        }
        
        .product-card {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }
        
        .product-card h3 {
            margin: 0 0 10px 0;
            color: #2c3e50;
        }
        
        .price {
            color: #e74c3c;
            font-weight: bold;
            font-size: 18px;
            margin: 10px 0;
        }
        
        .btn {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-size: 14px;
            margin-top: 10px;
        }
        
        .btn:hover {
            background-color: #2980b9;
        }
        
        .cart-item {
            background: #ecf0f1;
            padding: 10px;
            border-radius: 5px;
            margin: 8px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>VibeShop</h1>
        <p>Качественные вещи по нормальным ценам</p>
    </div>
    
    <div class="nav">
        <button class="nav-btn active" onclick="showSection('home')">Главная</button>
        <button class="nav-btn" onclick="showSection('catalog')">Каталог</button>
        <button class="nav-btn" onclick="showSection('cart')">Корзина</button>
    </div>
    
    <div id="home" class="section active">
        <h2>Добро пожаловать в VibeShop!</h2>
        <p>Мы предлагаем качественную одежду и кроссовки по доступным ценам.</p>
        
        <div style="background: #e8f4fc; padding: 15px; border-radius: 8px; margin: 15px 0;">
            <h3>🚚 Быстрая доставка</h3>
            <p>По всей России за 3-7 дней</p>
        </div>
        
        <div style="background: #e8f4fc; padding: 15px; border-radius: 8px; margin: 15px 0;">
            <h3>✅ Гарантия качества</h3>
            <p>Возврат в течение 14 дней</p>
        </div>
    </div>
    
    <div id="catalog" class="section">
        <h2>Каталог товаров</h2>
        
        <div class="product-card">
            <h3>Кроссовки Model X</h3>
            <div class="price">5 500 ₽</div>
            <button class="btn" onclick="addToCart('Кроссовки Model X', 5500)">В корзину</button>
        </div>
        
        <div class="product-card">
            <h3>Худи Oversized</h3>
            <div class="price">3 200 ₽</div>
            <button class="btn" onclick="addToCart('Худи Oversized', 3200)">В корзину</button>
        </div>
        
        <div class="product-card">
            <h3>Футболка Basic</h3>
            <div class="price">1 500 ₽</div>
            <button class="btn" onclick="addToCart('Футболка Basic', 1500)">В корзину</button>
        </div>
    </div>
    
    <div id="cart" class="section">
        <h2>Ваша корзина</h2>
        <div id="cart-items">
            <!-- Товары будут здесь -->
        </div>
        
        <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-top: 15px; text-align: center;">
            <strong style="font-size: 18px;">Итого: <span id="total-price">0</span> ₽</strong>
        </div>
        
        <button class="btn" onclick="checkout()" style="background-color: #27ae60; margin-top: 15px;">Оформить заказ</button>
    </div>
    
    <script>
        let cart = [];
        let total = 0;
        
        function showSection(sectionName) {
            // Скрываем все секции
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Показываем нужную секцию
            document.getElementById(sectionName).classList.add('active');
            
            // Обновляем активные кнопки навигации
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Если открыли корзину - обновляем ее
            if (sectionName === 'cart') {
                updateCart();
            }
        }
        
        function addToCart(name, price) {
            cart.push({ name: name, price: price });
            total += price;
            
            // Показываем уведомление
            alert('Товар "' + name + '" добавлен в корзину!');
            
            // Обновляем корзину
            updateCart();
        }
        
        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            const totalPrice = document.getElementById('total-price');
            
            // Очищаем корзину
            cartItems.innerHTML = '';
            
            // Добавляем товары
            cart.forEach((item, index) => {
                const itemElement = document.createElement('div');
                itemElement.className = 'cart-item';
                itemElement.innerHTML = `
                    <span>${item.name} - ${item.price} ₽</span>
                    <button onclick="removeFromCart(${index})" style="background: #e74c3c; color: white; border: none; padding: 5px 10px; border-radius: 3px; cursor: pointer;">Удалить</button>
                `;
                cartItems.appendChild(itemElement);
            });
            
            // Обновляем общую сумму
            totalPrice.textContent = total;
        }
        
        function removeFromCart(index) {
            total -= cart[index].price;
            cart.splice(index, 1);
            updateCart();
        }
        
        function checkout() {
            if (cart.length === 0) {
                alert('Добавьте товары в корзину!');
                return;
            }
            
            // Формируем сообщение о заказе
            let orderDetails = 'ВАШ ЗАКАЗ:\n\n';
            cart.forEach(item => {
                orderDetails += `${item.name} - ${item.price} ₽\n`;
            });
            orderDetails += `\nИТОГО: ${total} ₽`;
            
            if (confirm('Подтвердить заказ?\n\n' + orderDetails)) {
                alert('✅ Заказ оформлен!\n\nС вами свяжется менеджер для подтверждения заказа и оплаты.');
                
                // Очищаем корзину
                cart = [];
                total = 0;
                updateCart();
                
                // Возвращаем на главную
                showSection('home');
            }
        }
        
        // При загрузке страницы показываем главную
        document.addEventListener('DOMContentLoaded', function() {
            showSection('home');
        });
    </script>
</body>
</html>
