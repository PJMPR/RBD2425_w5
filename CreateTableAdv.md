
# 📘 SQL: Tworzenie tabel na podstawie SELECT

W tym dokumencie przedstawione są dwa podejścia do tworzenia i wypełniania tabel w bazie danych:

- **Szybka metoda**: `CREATE TABLE ... AS SELECT`
- **Tradycyjna metoda**: `CREATE TABLE` + `INSERT` z ręcznie podanymi danymi

---

## 🧪 Przykład 1: Klienci z Francji 🇫🇷

### 📝 Opis
Chcemy utworzyć nową tabelę `french_customers`, zawierającą tylko klientów, którzy mają przypisany adres we Francji.

---

### ✅ Szybko: `CREATE TABLE AS SELECT`

```sql
CREATE TABLE french_customers AS
SELECT c.customer_id, c.first_name, c.last_name, c.email, c.registration_date
FROM customers c
JOIN addresses a ON c.customer_id = a.customer_id
WHERE a.country = 'France';
```

📌 **Opis**: Tworzy tabelę `french_customers` i od razu wypełnia ją wynikami zapytania `SELECT`.

---

### 🧱 Tradycyjnie: `CREATE TABLE` + `INSERT`

```sql
CREATE TABLE french_customers (
    customer_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    registration_date DATETIME
);

INSERT INTO french_customers (customer_id, first_name, last_name, email, registration_date)
VALUES 
    (1, 'Jean', 'Dupont', 'jean.dupont@example.com', '2023-01-15 10:00:00'),
    (2, 'Marie', 'Curie', 'marie.curie@example.com', '2023-02-20 14:30:00');
```

📌 **Opis**: Najpierw tworzymy tabelę, potem ręcznie wstawiamy dane za pomocą `INSERT`.

---

## 🧪 Przykład 2: Tanie produkty 💰

### 📝 Opis
Chcemy stworzyć tabelę `cheap_products`, zawierającą aktywne produkty, których cena jest mniejsza niż 50.

---

### ✅ Szybko: `CREATE TABLE AS SELECT`

```sql
CREATE TABLE cheap_products AS
SELECT product_id, name, price
FROM products
WHERE active = TRUE AND price < 50;
```

📌 **Opis**: Tabela `cheap_products` tworzona na podstawie filtrowanego zestawu produktów.

---

### 🧱 Tradycyjnie: `CREATE TABLE` + `INSERT`

```sql
CREATE TABLE cheap_products (
    product_id INT,
    name VARCHAR(100),
    price DECIMAL(10,2)
);

INSERT INTO cheap_products (product_id, name, price)
VALUES
    (10, 'Wireless Mouse', 29.99),
    (15, 'Notebook', 12.50),
    (22, 'USB Cable', 8.90);
```

📌 **Opis**: Klasyczne podejście – pełna kontrola nad strukturą i zawartością.

---

## ℹ️ Podsumowanie

| Podejście              | Zalety                                      | Wady                                      |
|------------------------|---------------------------------------------|-------------------------------------------|
| `CREATE TABLE AS`      | ✅ Szybkość<br>✅ Jedno polecenie            | ⚠️ Mniejsza kontrola nad typami danych    |
| `CREATE` + `INSERT`    | ✅ Pełna kontrola<br>✅ Czytelność            | ⚠️ Więcej kodu<br>⚠️ Manualne wstawianie  |

---
