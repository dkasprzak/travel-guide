# Travel Guide

Przewodnik wyjazdowy w jednym pliku HTML: plan dnia, dojazd, jedzenie, puby, sklepy i checklista dokumentów. Działa na telefonie, w trybie jasnym i ciemnym, i nie potrzebuje żadnego builda.

**Aktualny wyjazd:** Newcastle Weekend 2026
**Strona:** `https://dkasprzak.github.io/travel-guide/`


## Nowy wyjazd w 5 krokach

1. **Skopiuj plik.** Najprościej założyć nowe repo (np. `lizbona-2027`) i wrzucić do niego kopię `index.html`. Możesz też trzymać wszystko w jednym repo w folderach: `/newcastle-2026/index.html`, `/lizbona-2027/index.html` itd.
2. **Podmień nagłówek.** Zmień `<title>`, `<h1>` i linijkę `.eyebrow` (kto jedzie, ile osób, jakie dni).
3. **Podmień treść sekcji.** Kolejność sekcji i ich `id` opisuje tabela niżej.
4. **Zmień klucz checklisty.** Na dole pliku w skrypcie jest prefiks `'ncl-'`. Ustaw nowy, np. `'lis-'`, żeby odhaczone punkty z poprzedniego wyjazdu nie przeszły na nowy.
5. **Wrzuć plik i sprawdź.** Otwórz stronę na telefonie, kliknij każdy link do map i sprawdź godziny.

## Mapa pliku

| Sekcja w stronie | Czego szukać w `index.html` | Co zmieniasz |
|---|---|---|
| Nagłówek | `<header>` | tytuł, opis, liczba osób |
| Nocleg | `class="base"` (pierwsza karta) | adres, opis okolicy, link do map, tekst kopiowany przyciskiem (`var text=` w skrypcie) |
| Stadion / główny punkt | `class="base stadium"` | nazwa miejsca, adres, link do trasy |
| Menu skrótów | `<nav class="jump">` | etykiety; `href="#..."` musi pasować do `id` sekcji |
| Plan | `id="plan"` | dni (`.day`) i godziny (`<li><time>`); `class="key"` zaznacza godzinę na żółto |
| Dojazd | `id="dojazd"` | linia, przystanki (`.stops li`), notatka o biletach |
| Jedzenie | `id="jedzenie"` | miejsca w `ul.places` |
| Piwo | `id="piwo"` | jw. |
| Sklepy | `id="sklepy"` | jw. |
| Papiery | `id="papiery"` | punkty checklisty; każdy `input` potrzebuje unikalnego `id` |

### Gotowe kawałki do kopiowania

**Miejsce (knajpa, pub, sklep):**
```html
<li>
  <div class="name">Nazwa miejsca</div>
  <div class="meta">Jedno, dwa zdania: co to jest i po co tam iść.</div>
  <div class="tags"><span class="tag">tag</span><span class="tag">drugi tag</span></div>
  <a class="map" href="https://maps.google.com/?q=Nazwa+Miejsca+Miasto" target="_blank" rel="noopener">Mapa →</a>
</li>
```

**Punkt planu:**
```html
<li><time>12:00</time><span>Co się dzieje</span></li>
<li class="key"><time>17:00</time><span>Ważna godzina (podświetlona)</span></li>
```

**Punkt checklisty:**
```html
<label><input type="checkbox" id="c-cos"><div><b>Nazwa</b><span>Krótki opis.</span></div></label>
```

**Przystanek na trasie:**
```html
<li><span>Nazwa stacji</span></li>
<li class="end"><span>Stacja docelowa</span><em>ok. 20 min · wysiadka</em></li>
```

### Linki do map
- Pinezka: `https://maps.google.com/?q=Adres+lub+Nazwa+Miasto` (spacje zamieniasz na `+`)
- Trasa pieszo:
  `https://www.google.com/maps/dir/?api=1&origin=SKAD&destination=DOKAD&travelmode=walking`
  (`travelmode` może być też `transit` albo `driving`)

## Kolory i wygląd

Wszystkie kolory są na górze `<style>`, w bloku `:root`. Każdy kolor jest wpisany trzy razy: raz dla trybu jasnego i dwa razy dla ciemnego.

- `--accent` to żółte podświetlenie godzin i obwódka focusu,
- `--green` to kolor linii metra (zmień na kolor linii w danym mieście),
- `--stripe-a` / `--stripe-b` to pasy na samej górze (np. barwy klubu).

Pod inny klub zwykle wystarczy zmienić pasy i `--accent`.

## Wrzucanie zmian (z telefonu)

1. Wejdź w repo na github.com.
2. Kliknij **Add file → Upload files**, wybierz nowy `index.html` i kliknij **Commit changes**. Stary plik zostanie nadpisany.
3. Odczekaj 1–2 minuty i odśwież stronę.

Drobne poprawki możesz robić od razu w przeglądarce: otwórz `index.html` w repo, kliknij ikonę ołówka, popraw tekst i kliknij **Commit changes**.

## Uwagi

- **Repo i strona są publiczne.** Każdy z linkiem widzi adres noclegu, więc nie wpisuj kodów do drzwi, numerów rezerwacji ani numerów telefonów.
- **Bez internetu** strona nie otworzy się z linku. Na wyjazd warto zapisać `index.html` w telefonie albo zrobić zrzut ekranu z planem.
- **Checklista** zapisuje się tylko w przeglądarce danej osoby. Każdy odhacza u siebie, a inni tego nie widzą.
