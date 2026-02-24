<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VibeShop - Админ панель</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }
        
        /* Шапка */
        .header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid #eee;
        }
        
        .header h1 {
            color: #2c3e50;
            font-size: 32px;
            margin-bottom: 10px;
        }
        
        .mode-switch {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }
        
        .mode-btn {
            padding: 12px 30px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }
        
        .mode-btn.active {
            background: #3498db;
            color: white;
        }
        
        .mode-btn:not(.active) {
            background: #f8f9fa;
            color: #666;
        }
        
        /* Админ панель */
        .admin-panel {
            display: none;
        }
        
        .admin-panel.active {
            display: block;
        }
        
        .shop-panel {
            display: none;
        }
        
        .shop-panel.active {
            display: block;
        }
        
        /* Форма добавления товара */
        .add-product-form {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
        }
        
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
        }
        
        .form-group label {
            margin-bottom: 8px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .form-group input,
        .form-group textarea {
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 14px;
            transition: border 0.3s;
        }
        
        .form-group input:focus,
        .form-group textarea:focus {
            border-color: #3498db;
            outline: none;
        }
        
        .form-actions {
            display: flex;
            gap: 15px;
            justify-content: flex-end;
        }
        
        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }
        
        .btn-primary {
            background: #3498db;
            color: white;
        }
        
        .btn-primary:hover {
            background: #2980b9;
        }
        
        .btn-danger {
            background: #e74c3c;
            color: white;
        }
        
        .btn-danger:hover {
            background: #c0392b;
        }
        
        .btn-success {
            background: #27ae60;
            color: white;
        }
        
        .btn-success:hover {
            background: #219653;
        }
        
        /* Список товаров (админ) */
        .products-list-admin {
            margin-top: 30px;
        }
        
        .product-item-admin {
            background: white;
            border: 2px solid #eee;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 15px;
            display: grid;
            grid-template-columns: 100px 1fr auto;
            gap: 20px;
            align-items: center;
            transition: transform 0.3s;
        }
        
        .product-item-admin:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .product-image {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 10px;
            background: #f8f9fa;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #999;
            font-size: 12px;
        }
        
        .product-info {
            flex: 1;
        }
        
        .product-info h3 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        .product-price {
            color: #e74c3c;
            font-weight: bold;
            font-size: 20px;
            margin: 10px 0;
        }
        
        .product-composition {
            color: #666;
            font-size: 14px;
            margin: 5px 0;
        }
        
        .product-actions {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        /* Магазин для покупателей */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }
        
        .product-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            transition: transform 0.3s;
        }
        
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }
        
        .product-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 10px;
            margin-bottom: 15px;
            background: #f8f9fa;
        }
        
        .product-card h3 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 18px;
        }
        
        .product-card .description {
            color: #666;
            font-size: 14px;
            margin-bottom: 10px;
            line-height: 1.5;
        }
        
        .product-card .composition {
            color: #888;
            font-size: 13px;
            margin-bottom: 15px;
            font-style: italic;
        }
        
        .cart-section {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 2px solid #eee;
        }
        
        /* Уведомления */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            border-radius: 10px;
            color: white;
            font-weight: bold;
            z-index: 1000;
            animation: slideIn 0.3s ease;
        }
        
        .notification.success {
            background: #27ae60;
        }
        
        .notification.error {
            background: #e74c3c;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        /* Адаптивность */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .product-item-admin {
                grid-template-columns: 1fr;
                text-align: center;
            }
            
            .products-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Шапка с переключателем режимов -->
        <div class="header">
            <h1>🛍️ VibeShop - Панель управления</h1>
            <p>Режим управления товарами и продаж</p>
            
            <div class="mode-switch">
                <button class="mode-btn active" onclick="switchMode('admin')">Админ панель</button>
                <button class="mode-btn" onclick="switchMode('shop')">Магазин (покупатель)</button>
            </div>
        </div>
        
        <!-- АДМИН ПАНЕЛЬ -->
        <div id="adminPanel" class="admin-panel active">
            <h2>📦 Управление товарами</h2>
            
            <!-- Форма добавления товара -->
            <div class="add-product-form">
                <h3>Добавить новый товар</h3>
                <div class="form-grid">
                    <div class="form-group">
                        <label for="productName">Название товара *</label>
                        <input type="text" id="productName" placeholder="Например: Кроссовки Nike Air">
                    </div>
                    
                    <div class="form-group">
                        <label for="productPrice">Цена (руб) *</label>
                        <input type="number" id="productPrice" placeholder="Например: 5500">
                    </div>
                    
                    <div class="form-group">
                        <label for="productImage">Ссылка на изображение</label>
                        <input type="text" id="productImage" placeholder="https://example.com/image.jpg">
                    </div>
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label for="productDescription">Описание товара</label>
                        <textarea id="productDescription" rows="3" placeholder="Подробное описание товара..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="productComposition">Состав / Материалы</label>
                        <textarea id="productComposition" rows="3" placeholder="Хлопок 100%, полиэстер..."></textarea>
                    </div>
                </div>
                
                <div class="form-actions">
                    <button class="btn btn-primary" onclick="addProduct()">Добавить товар</button>
                    <button class="btn" onclick="clearForm()" style="background: #95a5a6; color: white;">Очистить форму</button>
                </div>
            </div>
            
            <!-- Список товаров (админ) -->
            <div class="products-list-admin">
                <h3>Список товаров (всего: <span id="productsCount">0</span>)</h3>
                <div id="adminProductsList">
                    <!-- Товары будут добавляться сюда -->
                </div>
            </div>
        </div>
        
        <!-- МАГАЗИН ДЛЯ ПОКУПАТЕЛЕЙ -->
        <div id="shopPanel" class="shop-panel">
            <h2>🛒 Магазин VibeShop</h2>
            <p>Выберите товары и добавьте в корзину</p>
            
            <!-- Сетка товаров -->
            <div class="products-grid" id="shopProductsList">
                <!-- Товары будут добавляться сюда -->
            </div>
            
            <!-- Корзина -->
            <div class="cart-section">
                <h3>🛍️ Ваша корзина (<span id="cartCount">0</span> товаров)</h3>
                <div id="cartItems">
                    <!-- Товары в корзине -->
                </div>
                <div style="margin-top: 20px; text-align: right;">
                    <strong style="font-size: 24px;">Итого: <span id="totalPrice">0</span> руб</strong>
                    <button class="btn btn-success" onclick="checkout()" style="margin-top: 15px; width: 100%;">Оформить заказ</button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Уведомления -->
    <div id="notification" class="notification" style="display: none;"></div>
    
    <script>
        // ==================== ГЛОБАЛЬНЫЕ ПЕРЕМЕННЫЕ ====================
        let products = JSON.parse(localStorage.getItem('vibeshop_products')) || [];
        let cart = JSON.parse(localStorage.getItem('vibeshop_cart')) || [];
        
        // ==================== ФУНКЦИИ АДМИН-ПАНЕЛИ ====================
        
        // Переключение режимов
        function switchMode(mode) {
            // Обновляем активные кнопки
            document.querySelectorAll('.mode-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Показываем нужную панель
            document.getElementById('adminPanel').classList.remove('active');
            document.getElementById('shopPanel').classList.remove('active');
            
            if (mode === 'admin') {
                document.getElementById('adminPanel').classList.add('active');
                loadAdminProducts();
            } else {
                document.getElementById('shopPanel').classList.add('active');
                loadShopProducts();
                updateCart();
            }
        }
        
        // Добавление товара
        function addProduct() {
            const name = document.getElementById('productName').value.trim();
            const price = parseInt(document.getElementById('productPrice').value);
            const image = document.getElementById('productImage').value.trim();
            const description = document.getElementById('productDescription').value.trim();
            const composition = document.getElementById('productComposition').value.trim();
            
            if (!name || !price) {
                showNotification('Заполните название и цену!', 'error');
                return;
            }
            
            const newProduct = {
                id: Date.now(),
                name: name,
                price: price,
                image: image || 'https://via.placeholder.com/300x300/cccccc/ffffff?text=No+Image',
                description: description || 'Описание отсутствует',
                composition: composition || 'Состав не указан',
                createdAt: new Date().toLocaleString()
            };
            
            products.push(newProduct);
            saveProducts();
            loadAdminProducts();
            clearForm();
            
            showNotification(`Товар "${name}" добавлен!`, 'success');
        }
        
        // Удаление товара
        function deleteProduct(id) {
            if (confirm('Удалить этот товар?')) {
                products = products.filter(product => product.id !== id);
                saveProducts();
                loadAdminProducts();
                showNotification('Товар удален', 'success');
            }
        }
        
        // Редактирование товара
        function editProduct(id) {
            const product = products.find(p => p.id === id);
            if (!product) return;
            
            // Заполняем форму данными товара
            document.getElementById('productName').value = product.name;
            document.getElementById('productPrice').value = product.price;
            document.getElementById('productImage').value = product.image;
            document.getElementById('productDescription').value = product.description;
            document.getElementById('productComposition').value = product.composition;
            
            // Удаляем старый товар
            deleteProduct(id);
            
            showNotification('Редактируйте товар в форме выше', 'success');
        }
        
        // Загрузка товаров в админ-панель
        function loadAdminProducts() {
            const container = document.getElementById('adminProductsList');
            const countElement = document.getElementById('productsCount');
            
            if (products.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 40px; background: #f8f9fa; border-radius: 10px;">
                        <p style="color: #666; font-size: 18px;">Нет товаров</p>
                        <p>Добавьте первый товар через форму выше</p>
                    </div>
                `;
                countElement.textContent = '0';
                return;
            }
            
            let html = '';
            products.forEach(product => {
                html += `
                    <div class="product-item-admin">
                        <div class="product-image">
                            ${product.image ? `<img src="${product.image}" alt="${product.name}" style="width: 100px; height: 100px; object-fit: cover;">` : '📷 Нет фото'}
                        </div>
                        <div class="product-info">
                            <h3>${product.name}</h3>
                            <p class="product-description">${product.description}</p>
                            <p class="product-composition">Состав: ${product.composition}</p>
                            <div class="product-price">${product.price.toLocaleString()} руб</div>
                            <small style="color: #999;">Добавлен: ${product.createdAt}</small>
                        </div>
                        <div class="product-actions">
                            <button class="btn btn-primary" onclick="editProduct(${product.id})">✏️ Редактировать</button>
                            <button class="btn btn-danger" onclick="deleteProduct(${product.id})">🗑️ Удалить</button>
                        </div>
                    </div>
                `;
            });
            
            container.innerHTML = html;
            countElement.textContent = products.length.toString();
        }
        
        // Очистка формы
        function clearForm() {
            document.getElementById('productName').value = '';
            document.getElementById('productPrice').value = '';
            document.getElementById('productImage').value = '';
            document.getElementById('productDescription').value = '';
            document.getElementById('productComposition').value = '';
        }
        
        // ==================== ФУНКЦИИ МАГАЗИНА ====================
        
        // Загрузка товаров в магазин
        function loadShopProducts() {
            const container = document.getElementById('shopProductsList');
            
            if (products.length === 0) {
                container.innerHTML = `
                    <div style="grid-column: 1 / -1; text-align: center; padding: 50px;">
                        <h3 style="color: #666;">Магазин пуст</h3>
                        <p>Товары появятся скоро!</p>
                    </div>
                `;
                return;
            }
            
            let html = '';
            products.forEach(product => {
                html += `
                    <div class="product-card">
                        <img src="${product.image}" alt="${product.name}">
                        <h3>${product.name}</h3>
                        <p class="description">${product.description}</p>
                        <p class="composition">${product.composition}</p>
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-top: 15px;">
                            <div class="product-price">${product.price.toLocaleString()} руб</div>
                            <button class="btn btn-primary" onclick="addToCart(${product.id})">В корзину</button>
                        </div>
                    </div>
                `;
            });
            
            container.innerHTML = html;
        }
        
        // ==================== ФУНКЦИИ КОРЗИНЫ ====================
        
        // Добавление в корзину
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            // Проверяем, есть ли уже в корзине
            const existingItem = cart.find(item => item.id === productId);
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    image: product.image,
                    quantity: 1
                });
            }
            
            saveCart();
            updateCart();
            showNotification(`${product.name} добавлен в корзину!`, 'success');
        }
        
        // Удаление из корзины
        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            saveCart();
            updateCart();
            showNotification('Товар удален из корзины', 'error');
        }
        
        // Изменение количества
        function updateQuantity(productId, change) {
            const item = cart.find(item => item.id === productId);
            if (!item) return;
            
            item.quantity += change;
            if (item.quantity < 1) {
                removeFromCart(productId);
                return;
            }
            
            saveCart();
            updateCart();
        }
        
        // Обновление отображения корзины
        function updateCart() {
            const container = document.getElementById('cartItems');
            const countElement = document.getElementById('cartCount');
            const totalElement = document.getElementById('totalPrice');
            
            if (cart.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 30px; background: #f8f9fa; border-radius: 10px;">
                        <p style="color: #666;">Корзина пуста</p>
                        <p>Добавьте товары из каталога</p>
                    </div>
                `;
                countElement.textContent = '0';
                totalElement.textContent = '0';
                return;
            }
            
            let html = '';
            let total = 0;
            
            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                
                html += `
                    <div class="product-item-admin" style="margin-bottom: 10px;">
                        <div class="product-image">
                            <img src="${item.image}" alt="${item.name}" style="width: 60px; height: 60px;">
                        </div>
                        <div class="product-info">
                            <h4 style="margin: 0;">${item.name}</h4>
                            <div style="display: flex; align-items: center; gap: 15px; margin-top: 10px;">
                                <button onclick="updateQuantity(${item.id}, -1)" style="background: #ddd; border: none; width: 30px; height: 30px; border-radius: 5px; cursor: pointer;">-</button>
                                <span style="font-weight: bold;">${item.quantity} шт</span>
                                <button onclick="updateQuantity(${item.id}, 1)" style="background: #ddd; border: none; width: 30px; height: 30px; border-radius: 5px; cursor: pointer;">+</button>
                                <span style="color: #e74c3c; font-weight: bold; margin-left: 20px;">${itemTotal.toLocaleString()} руб</span>
                            </div>
                        </div>
                        <div class="product-actions">
                            <button class="btn btn-danger" onclick="removeFromCart(${item.id})">Удалить</button>
                        </div>
                    </div>
                `;
            });
            
            container.innerHTML = html;
            countElement.textContent = cart.reduce((sum, item) => sum + item.quantity, 0).toString();
            totalElement.textContent = total.toLocaleString();
        }
        
        // Оформление заказа
        function checkout() {
            if (cart.length === 0) {
                showNotification('Добавьте товары в корзину', 'error');
                return;
            }
            
            let orderDetails = '📦 ЗАКАЗ С VIBESHOP 📦\n\n';
            let total = 0;
            
            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                orderDetails += `• ${item.name} - ${item.quantity} шт × ${item.price} руб = ${itemTotal} руб\n`;
            });
            
            orderDetails += `\n💰 ИТОГО: ${total.toLocaleString()} руб\n`;
            orderDetails += `📅 ${new Date().toLocaleString()}\n\n`;
            orderDetails += 'Для подтверждения заказа свяжитесь с менеджером!';
            
            if (confirm(`Подтвердить заказ на ${total.toLocaleString()} руб?\n\nДетали заказа будут сохранены.`)) {
                // Сохраняем историю заказов
                const orders = JSON.parse(localStorage.getItem('vibeshop_orders')) || [];
                orders.push({
                    date: new Date().toISOString(),
                    items: [...cart],
                    total: total
                });
                localStorage.setItem('vibeshop_orders', JSON.stringify(orders));
                
                // Очищаем корзину
                cart = [];
                saveCart();
                updateCart();
                
                showNotification('Заказ оформлен! С вами свяжутся.', 'success');
                alert(orderDetails);
            }
        }
        
        // ==================== ВСПОМОГАТЕЛЬНЫЕ ФУНКЦИИ ====================
        
        // Показать уведомление
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${type}`;
            notification.style.display = 'block';
            
            setTimeout(() => {
                notification.style.display = 'none';
            }, 3000);
        }
        
        // Сохранить товары в LocalStorage
        function saveProducts() {
            localStorage.setItem('vibeshop_products', JSON.stringify(products));
        }
        
        // Сохранить корзину в LocalStorage
        function saveCart() {
            localStorage.setItem('vibeshop_cart', JSON.stringify(cart));
        }
        
        // ==================== ИНИЦИАЛИЗАЦИЯ ====================
        document.addEventListener('DOMContentLoaded', function() {
            // Загружаем начальные данные
            loadAdminProducts();
            
            // Добавляем несколько демо-товаров если пусто
            if (products.length === 0) {
                products = [
                    {
                        id: 1,
                        name: "Кроссовки Model X",
                        price: 5500,
                        image: "https://via.placeholder.com/300x300/3498db/ffffff?text=Кроссовки",
                        description: "Стильные и удобные кроссовки для повседневной носки",
                        composition: "Кожа, текстиль, резиновая подошва",
                        createdAt: new Date().toLocaleString()
                    },
                    {
                        id: 2,
                        name: "Худи Oversized",
                        price: 3200,
                        image: "https://via.placeholder.com/300x300/2ecc71/ffffff?text=Худи",
                        description: "Модное худи свободного кроя",
                        composition: "Хлопок 80%, полиэстер 20%",
                        createdAt: new Date().toLocaleString()
                    }
                ];
                saveProducts();
                loadAdminProducts();
            }
            
            showNotification('Админ-панель загружена!', 'success');
        });
    </script>
</body>
</html>
