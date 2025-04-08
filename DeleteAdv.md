# 📘 SQL: DELETE z SELECT – i wersje klasyczne

W tym zestawie znajdziesz przykłady komendy `DELETE` z użyciem `SELECT`, a także tradycyjne wersje z ręcznie wpisanymi wartościami. To bardzo praktyczne podejście np. do czyszczenia danych zależnych od innych tabel.

---

## 🧪 Przykład 1: Usunięcie adresów klientów bez zamówień 📭

### ✅ DELETE z SELECT
```sql
DELETE FROM addresses
WHERE customer_id IN (
    SELECT c.customer_id
    FROM customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id
    WHERE o.order_id IS NULL
);
```
📌 **Opis**: Usuwa adresy klientów, którzy nigdy nie złożyli zamówienia.

### 🧱 DELETE bez SELECT
```sql
DELETE FROM addresses
WHERE customer_id IN (104, 110, 113);
```
📌 **Opis**: Ręczne usunięcie adresów dla wybranych klientów.

---

## 🧪 Przykład 2: Usunięcie pozycji zamówień z nieaktywnymi produktami ❌

### ✅ DELETE z SELECT
```sql
DELETE FROM order_items
WHERE product_id IN (
    SELECT product_id
    FROM products
    WHERE active = FALSE
);
```
📌 **Opis**: Czyści zamówienia z produktów wycofanych z oferty.

### 🧱 DELETE bez SELECT
```sql
DELETE FROM order_items
WHERE product_id IN (7, 9, 15);
```
📌 **Opis**: Usunięcie pozycji z zamówień ręcznie podanych produktów.

---

🧠 **Wskazówka**: `DELETE ... SELECT` pozwala na dynamiczne czyszczenie danych na podstawie powiązań między tabelami – bardzo częsta operacja w realnych systemach.

