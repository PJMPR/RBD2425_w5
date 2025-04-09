# 🎓 Mixowanie komend SQL – INSERT, UPDATE, DELETE z SELECT

Dziś przyjrzymy się **praktycznemu łączeniu komend SQL** takich jak `INSERT`, `UPDATE` i `DELETE` z zapytaniami `SELECT`. Ten temat jest niesamowicie użyteczny w codziennej pracy z bazą danych – pozwala dynamicznie modyfikować dane na podstawie innych danych.

---

## 🎯 Po co są takie zapytania?

Zanim przejdziemy do komend, warto zrozumieć, **dlaczego warto łączyć `SELECT` z komendami `INSERT`, `UPDATE` czy `DELETE`**. Tego typu zapytania pozwalają na automatyczne i kontekstowe zarządzanie danymi. Oto przykłady problemów, które można w ten sposób rozwiązać:

- 🔁 **Zarchiwizuj klientów** z wybranego kraju do osobnej tabeli – bez ręcznego kopiowania danych.
- 🏷️ **Dodaj do promocji** tylko te produkty, które spełniają określone kryteria (np. aktywność i cena).
- 📈 **Zwiększ ceny** produktów, które były zamawiane w ostatnich 30 dniach.
- 🧹 **Usuń dane**, które nie mają powiązań – np. adresy klientów bez żadnego zamówienia.

Takie zapytania są przydatne wszędzie tam, gdzie **logika biznesowa zależy od innych danych w bazie** – a nie od z góry znanych ID czy wartości.

Dzięki tej technice SQL staje się bardziej elastyczny, automatyczny i skalowalny. 💡

- Zobaczymy **jak SELECT może pomóc przy modyfikowaniu danych** 🧠
- Poznamy dwa style pisania zapytań:
  - Nowoczesny: dynamiczny z `SELECT`
  - Klasyczny: ręczny z `VALUES`, `IN`, itd.
- Będziemy pracować na bazie pełnej relacji: klienci, produkty, zamówienia 📦

---

## 🧠 Co już powinniście znać?

- Podstawowe zapytania SQL (`SELECT`, `INSERT`, `UPDATE`, `DELETE`)
- Jak działa relacyjna baza danych
- Czym są klucze główne i obce

---

## 🗂️ O czym będziemy mówić?

### 1. `CREATE TABLE AS SELECT`
- Tworzymy nową tabelę na podstawie istniejących danych.
- Zobaczymy jak szybko utworzyć tabelę z klientami z wybranego kraju.
- Porównamy to z klasycznym podejściem: `CREATE TABLE` + `INSERT INTO ... VALUES (...)`

### 2. `INSERT INTO ... SELECT`
- Pokażemy jak można wstawić wiele rekordów dynamicznie – np. kopiując tanie produkty do tabeli promocyjnej.
- Dla porównania, wstawimy te same dane ręcznie, bez `SELECT`.

### 3. `UPDATE ... IN (SELECT ...)`
- Zaktualizujemy dane (np. podniesiemy ceny) tylko tam, gdzie wystąpiły określone warunki – np. produkt był w ostatnich zamówieniach.
- Następnie zrobimy to samo ręcznie, wskazując konkretne ID.

### 4. `DELETE ... IN (SELECT ...)`
- Usuniemy dane powiązane – np. adresy klientów bez zamówień lub pozycje nieaktywnych produktów.
- Porównamy to z klasycznym podejściem, gdzie usuwamy dane po identyfikatorach.

---

# 🎤 Q&A: SQL – Mixowanie komend i widoki

Zestaw pytań do dyskusji, analizy i wspólnego rozwiązywania podczas wykładu o `INSERT`, `UPDATE`, `DELETE` z `SELECT`, a także o `VIEW`. Format pasuje do prezentacji Markdown lub prowadzenia zajęć interaktywnych.

---

## 🔁 INSERT ... SELECT

### ❓ Czy `INSERT INTO ... SELECT` to zawsze najlepsze rozwiązanie?
- Co tracimy, a co zyskujemy?
- Kiedy warto użyć `VALUES`, a kiedy `SELECT`?

### ❓ Czy można przypadkiem zduplikować dane przy takim insercie?
- Jak to zabezpieczyć?

---

## 🔄 UPDATE ... SELECT

### ❓ Czy `UPDATE` z `SELECT` może być niebezpieczny?
- Co się stanie, jeśli `SELECT` zwraca za dużo?
- Co jeśli nie ma `WHERE`?

### 💬 Zadanie: Podaj przykład UPDATE, który może się „wymsknąć spod kontroli”.

---

## 🧹 DELETE ... SELECT

### ❓ Czy `DELETE FROM ... WHERE ... IN (SELECT ...)` to dobra praktyka?
- Jak sprawdzić, co usuniemy, zanim klikniemy ENTER?
- Co z relacjami i kluczami obcymi?

### 💬 Zadanie: Zaprojektuj zapytanie DELETE, które usuwa dane niepowiązane z żadną inną tabelą.

---

📌 Te pytania nie mają „jednej dobrej odpowiedzi” – celem jest dyskusja, analiza i rozwijanie intuicji SQL.


