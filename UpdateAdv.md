# 📘 SQL: UPDATE z SELECT – i wersje klasyczne

Poniżej znajdziesz dwa przykłady użycia komendy `UPDATE` z podzapytaniami `SELECT`, a także ich klasyczne wersje bez `SELECT`. Obie metody pozwalają aktualizować dane, ale mają inne zastosowania dydaktyczne i praktyczne.

---

## 🧪 Przykład 1: Aktualizacja daty ostatniej zmiany w magazynie 📦

### ✅ UPDATE z SELECT
```sql
UPDATE inventory
SET last_updated = NOW()
WHERE product_id IN (
    SELECT DISTINCT product_id
    FROM order_items
);
```
📌 **Opis**: Ustawia aktualną datę dla produktów, które wystąpiły w jakimkolwiek zamówieniu.

### 🧱 UPDATE bez SELECT
```sql
UPDATE inventory
SET last_updated = '2024-04-01 12:00:00'
WHERE product_id IN (3, 5, 7);
```
📌 **Opis**: Ręczna aktualizacja dla znanych produktów.

---

## 🧪 Przykład 2: Podwyżka cen dla zamawianych produktów 💸

### ✅ UPDATE z SELECT
```sql
UPDATE products
SET price = price * 1.10
WHERE product_id IN (
    SELECT DISTINCT oi.product_id
    FROM order_items oi
    JOIN orders o ON oi.order_id = o.order_id
    WHERE o.order_date >= NOW() - INTERVAL 1 MONTH
);
```
📌 **Opis**: Zwiększa ceny o 10% dla produktów zamawianych w ostatnich 30 dniach.

### 🧱 UPDATE bez SELECT
```sql
UPDATE products
SET price = price * 1.10
WHERE product_id IN (8, 9, 12);
```
📌 **Opis**: Ręczne zwiększenie cen wybranych produktów.

---

