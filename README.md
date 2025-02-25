<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aromax - Магазин парфюмов</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: url('https://source.unsplash.com/1600x900/?perfume,fragrance') no-repeat center center fixed;
            background-size: cover;
            color: #333;
            text-align: center;
            transition: background 0.3s, color 0.3s;
        }
        body.dark-mode {
            background: #222;
            color: #fff;
        }
        header {
            background: rgba(255, 255, 255, 0.9);
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
        }
        nav {
            display: flex;
        }
        nav a {
            margin: 0 15px;
            text-decoration: none;
            color: #333;
            font-weight: bold;
            transition: color 0.3s;
        }
        body.dark-mode nav a {
            color: #fff;
        }
        .container {
            padding: 50px 20px;
            background: rgba(255, 255, 255, 0.9);
            margin: 20px auto;
            width: 90%;
            max-width: 800px;
            border-radius: 10px;
            transition: background 0.3s;
        }
        body.dark-mode .container {
            background: rgba(50, 50, 50, 0.9);
        }
        .button {
            display: inline-block;
            padding: 10px 20px;
            background: #333;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            margin-top: 20px;
            transition: background 0.3s;
        }
        .button:hover {
            background: #555;
        }
        .order-form input, .order-form button {
            display: block;
            width: 80%;
            margin: 10px auto;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .orders-list {
            text-align: left;
            margin-top: 20px;
            padding: 20px;
            background: #fff;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Aromax</h1>
        <nav>
            <a href="#about">О нас</a>
            <a href="#men">Мужские духи</a>
            <a href="#women">Женские духи</a>
            <a href="#orders">Заказы</a>
        </nav>
    </header>
    
    <section class="container">
        <h2>Оформление заказа</h2>
        <form class="order-form" onsubmit="submitOrder(event)">
            <input type="text" id="name" placeholder="Ваше имя" required>
            <input type="text" id="phone" placeholder="Телефон" required>
            <input type="text" id="address" placeholder="Адрес доставки" required>
            <button type="submit">Оформить заказ</button>
        </form>
    </section>
    
    <section id="orders" class="container">
        <h2>Список заказов</h2>
        <div class="orders-list" id="orders-list">Нет заказов</div>
    </section>
    
    <script>
        function loadOrders() {
            let ordersList = document.getElementById("orders-list");
            let orders = JSON.parse(localStorage.getItem("orders")) || [];
            ordersList.innerHTML = orders.length ? "" : "Нет заказов";
            orders.forEach(order => {
                let orderItem = document.createElement("p");
                orderItem.textContent = order;
                ordersList.appendChild(orderItem);
            });
        }

        function submitOrder(event) {
            event.preventDefault();
            let name = document.getElementById("name").value;
            let phone = document.getElementById("phone").value;
            let address = document.getElementById("address").value;
            let orderData = `Имя: ${name}, Телефон: ${phone}, Адрес: ${address}`;
            
            let orders = JSON.parse(localStorage.getItem("orders")) || [];
            orders.push(orderData);
            localStorage.setItem("orders", JSON.stringify(orders));
            
            loadOrders();
            document.querySelector(".order-form").reset();
        }
        
        document.addEventListener("DOMContentLoaded", loadOrders);
    </script>
</body>
</html>
