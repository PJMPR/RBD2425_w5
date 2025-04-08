# 📘 Widoki w SQL

Widoki (ang. **views**) to jedno z najpotężniejszych narzędzi w SQL. Pozwalają tworzyć wirtualne tabele, które bazują na zapytaniach SELECT. W tym pliku poznasz:

- czym są widoki,
- po co się je tworzy,
- jak działają w kontekście przykładowej bazy danych,
- jaki mają wpływ na wydajność,
- i kiedy warto (lub nie warto) ich używać.

---

## 🧠 Co to jest widok?

**Widok to zapamiętane zapytanie SELECT, które działa jak wirtualna tabela.** Nie przechowuje fizycznie danych, ale udostępnia dane w takim samym stylu, jakby były w prawdziwej tabeli.

Można na nim wykonywać `SELECT`, czasami też `UPDATE`, `INSERT` czy `DELETE` – ale nie zawsze.

---

## 🎯 Po co tworzymy widoki?

### ✅ Upraszczanie złożonych zapytań
Zamiast pisać długie zapytania z JOIN-ami i filtrami – tworzysz widok raz, i używasz go jak tabeli.

### ✅ Abstrakcja i porządek
Użytkownik nie musi znać struktury bazy, wystarczy że widzi widok z gotowymi danymi.

### ✅ Ograniczenie dostępu
Możesz zrobić widok, który pokazuje tylko część danych – np. tylko aktywne zamówienia albo tylko kolumny bez danych wrażliwych.

### ✅ Standaryzacja logiki
Jeśli wiele zapytań, raportów czy aplikacji ma korzystać z tych samych danych – lepiej zamknąć tę logikę w widoku.

---

## 📦 Widoki a nasza baza

Twoja baza zawiera:
- `customers`, `addresses`, `orders`, `order_items`, `products`, `inventory`

To świetny kontekst do tworzenia widoków np.:
- `french_customers_view` – klienci z Francji
- `active_products_view` – produkty aktywne i dostępne
- `order_summary_view` – uproszczone informacje o zamówieniach

Widok może łączyć kilka tabel, filtrować dane lub agregować (np. suma zamówień).

---

## ⚙️ Wydajność – czy widoki ją pogarszają?

Widok sam **nie przechowuje danych** – za każdym razem jego zapytanie `SELECT` jest wykonywane od nowa. Dlatego:

- Prosty widok (np. bez JOIN-ów) nie wpływa negatywnie
- Złożony widok (JOIN + GROUP BY + podzapytania) może spowolnić działanie
- Niektóre widoki można zamienić na **materializowane** (w MariaDB przez ręczne tworzenie tabel z danymi)

---

## 🛑 Ograniczenia

- Widok **nie zawsze jest edytowalny** – np. jeśli zawiera `GROUP BY`, `DISTINCT`, funkcje agregujące.
- Nie można na nim założyć indeksu.
- Czasami nie zadziała `INSERT`, `UPDATE`, `DELETE` – to zależy od zapytania bazowego.

---
