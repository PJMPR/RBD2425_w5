# 📘 Przykłady użycia widoków w SQL (MariaDB)

Widoki w SQL pozwalają uprościć dostęp do danych, zapisać złożone zapytania jako wirtualne tabele i wielokrotnie wykorzystywać je w innych miejscach.

---

## 🔧 Dokumentacja: `CREATE VIEW`

### 🧱 Składnia
```sql
CREATE [OR REPLACE] VIEW view_name AS
SELECT ...;
```

- `view_name` – nazwa tworzonego widoku,
- `SELECT` – dowolne zapytanie, które ma zwracać dane jak tabela.

### 🧠 Co warto wiedzieć:
- Widok nie przechowuje danych – działa jak zapisane zapytanie.
- Możesz wykonywać `SELECT` na widoku, jakby to była zwykła tabela.
- Widoku nie można zaindeksować.
- Niektóre widoki mogą być edytowalne (`UPDATE`, `INSERT`, `DELETE`), ale nie te z `GROUP BY`, `DISTINCT`, itp.
- Widoki można nadpisywać (`OR REPLACE`) lub usuwać (`DROP VIEW`).

---

## 📌 Przykład 1: Klienci z Francji 🇫🇷

### ✅ Tworzenie widoku
```sql
CREATE VIEW french_customers_view AS
SELECT c.customer_id, c.first_name, c.last_name, a.city, a.country
FROM customers c
JOIN addresses a ON c.customer_id = a.customer_id
WHERE a.country = 'France';
```

### 🔍 Użycie
```sql
SELECT * FROM french_customers_view;
```

### ❌ Usunięcie
```sql
DROP VIEW french_customers_view;
```

---

## 📌 Przykład 2: Produkty dostępne i aktywne 🟢

### ✅ Tworzenie widoku
```sql
CREATE VIEW available_products_view AS
SELECT p.product_id, p.name, p.price, i.quantity
FROM products p
JOIN inventory i ON p.product_id = i.product_id
WHERE p.active = TRUE AND i.quantity > 0;
```

### 🔍 Użycie
```sql
SELECT * FROM available_products_view ORDER BY price ASC;
```

### ❌ Usunięcie
```sql
DROP VIEW available_products_view;
```

---

## 📌 Przykład 3: Podsumowanie zamówień 🧾

### ✅ Tworzenie widoku
```sql
CREATE VIEW order_summary_view AS
SELECT o.order_id, o.customer_id, o.order_date,
       SUM(oi.quantity * oi.unit_price) AS total_amount
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY o.order_id, o.customer_id, o.order_date;
```

### 🔍 Użycie
```sql
SELECT * FROM order_summary_view WHERE total_amount > 100;
```

### ❌ Usunięcie
```sql
DROP VIEW order_summary_view;
```

---

## 📌 Przykład 4: Pozycje z nieaktywnymi produktami ❌

### ✅ Tworzenie widoku
```sql
CREATE VIEW deprecated_product_orders AS
SELECT oi.order_id, oi.product_id, oi.quantity
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
WHERE p.active = FALSE;
```

### 🔍 Użycie
```sql
SELECT * FROM deprecated_product_orders;
```

### ❌ Usunięcie
```sql
DROP VIEW deprecated_product_orders;
```

---

📌 Widoki pomagają czytelnie prezentować dane, ukrywać złożoność i organizować logikę zapytań SQL.

