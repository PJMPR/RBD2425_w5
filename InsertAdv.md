# 📘 SQL: INSERT INTO z SELECT

Poniżej znajdziesz użycia komendy `INSERT INTO ... SELECT`, a także ich klasyczne odpowiedniki z ręcznie podanymi wartościami.

---

## 🧪 Przykład 1: Tanie produkty do promocji 🏷️

### 🏗️ Utworzenie tabeli `promotion_products`
```sql
CREATE TABLE promotion_products (
    product_id INT,
    name VARCHAR(100),
    price DECIMAL(10,2)
);
```

### ✅ INSERT z SELECT
```sql
INSERT INTO promotion_products (product_id, name, price)
SELECT product_id, name, price
FROM products
WHERE active = TRUE AND price < 30;
```

📌 **Opis**: Wybiera tanie produkty z tabeli `products` i dodaje je do promocji.

### 🧱 INSERT bez SELECT
```sql
INSERT INTO promotion_products (product_id, name, price)
VALUES
    (7, 'Notebook', 12.50),
    (14, 'Stylus Pen', 19.99),
    (20, 'USB Cable', 9.90);
```

📌 **Opis**: Ręczne wprowadzenie produktów do tabeli promocji.

---

## 🧪 Przykład 2: Archiwizacja zamówień 🗃️

### 🏗️ Utworzenie tabeli `archived_orders`
```sql
CREATE TABLE archived_orders (
    order_id INT,
    customer_id INT,
    order_date DATETIME
);
```

### ✅ INSERT z SELECT
```sql
INSERT INTO archived_orders (order_id, customer_id, order_date)
SELECT order_id, customer_id, order_date
FROM orders
WHERE customer_id = 101;
```

📌 **Opis**: Archiwizuje zamówienia klienta nr 101.

### 🧱 INSERT bez SELECT
```sql
INSERT INTO archived_orders (order_id, customer_id, order_date)
VALUES
    (201, 101, '2023-03-10 12:45:00'),
    (224, 101, '2023-04-01 09:20:00');
```

📌 **Opis**: Wstawienie przykładowych archiwalnych zamówień.

---

