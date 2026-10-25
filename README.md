# C-Lab3

![C](https://img.shields.io/badge/Language-C99-A8B9CC?style=flat&logo=c&logoColor=black)
![Linux](https://img.shields.io/badge/Target-Linux-FCC624?style=flat&logo=linux&logoColor=black)
![GitHub Codespaces](https://img.shields.io/badge/Environment-GitHub%20Codespaces-181717?style=flat&logo=github&logoColor=white)
![Educational](https://img.shields.io/badge/Purpose-Educational-6A5ACD?style=flat)

Trzecie laboratorium z języka C, przygotowane do pracy w środowisku GitHub Codespaces.

## Cel laboratorium

Celem zajęć jest zapoznanie studenta z:

- definiowaniem i wywoływaniem funkcji,
- przekazywaniem argumentów i zwracaniem wyników,
- konwersją tekstu na typ `float` za pomocą `strtof`,
- sprawdzaniem poprawności danych wejściowych,
- wyborem działania na podstawie operatora,
- zapisem działania w odwrotnej notacji polskiej,
- podziałem programu na odczyt, walidację, obliczenia i wyświetlanie wyniku.

## Struktura projektu

```text
.
├── .devcontainer/
│   └── devcontainer.json
├── .vscode/
│   ├── launch.json
│   └── tasks.json
├── src/
│   └── main.c
├── tests/
├── build/
├── Makefile
└── README.md
```

Najważniejsze elementy projektu:

- `src/main.c` — główny plik źródłowy programu; to plik edytowany przez studenta,
- `tests/` — katalog zawierający pliki pomocnicze związane z testami projektu,
- `Makefile` — plik sterujący budowaniem i uruchamianiem programu,
- `.vscode/launch.json` — konfiguracja debugowania,
- `.vscode/tasks.json` — konfiguracja zadań,
- `.devcontainer/` — konfiguracja środowiska GitHub Codespaces,
- `build/` — katalog na pliki wynikowe kompilacji.

## Budowanie programu

Program można zbudować poleceniem:

```bash
make
```

Po poprawnej kompilacji plik wykonywalny znajduje się w:

```text
build/app
```

Kod przygotuj w standardzie C99. Kompilacja powinna wykorzystywać flagi:

```text
-std=c99 -Wall -Wextra -Wpedantic -g
```

## Uruchamianie programu

Program można uruchomić poleceniem:

```bash
make run
```

Można również wykorzystać zadania skonfigurowane w `.vscode/tasks.json`.

## Program startowy

Plik `src/main.c` zawiera program dodający dwie zmienne typu `float` i wypisujący wynik.

```c
#include <stdio.h>

int main(void)
{
    float a = 20.0f;
    float b = 6.0f;
    float result = a + b;

    printf("result: %.4f\n", result);

    return 0;
}
```

Oczekiwane wyjście:

```text
result: 26.0000
```

## Funkcje wykorzystywane w laboratorium

### `strtof`

Nagłówek: `<stdlib.h>`.

Konwertuje początkową część tekstu na liczbę typu `float`.

Pomija początkowe białe znaki. Przez argument `endptr` zapisuje adres pierwszego znaku niewykorzystanego w konwersji.

Jeżeli nie wykonano konwersji, zwraca `0`, a wskaźnik końca wskazuje początek przekazanego tekstu. Błąd zakresu sygnalizuje przez ustawienie `errno` na `ERANGE`.

Sama wartość `0` nie oznacza błędu — zero może być poprawnym wynikiem konwersji.

### `isfinite`

Nagłówek: `<math.h>`.

Sprawdza, czy wartość zmiennoprzecinkowa jest skończona. Zwraca wartość różną od zera dla wartości skończonej, a zero dla nieskończoności i NaN.

## Funkcje w języku C

Funkcja jest wydzieloną częścią programu wykonującą określone zadanie. Może przyjmować argumenty i zwracać wynik.

Definicja funkcji składa się z:

- typu zwracanego wyniku,
- nazwy funkcji,
- listy parametrów wraz z ich typami,
- ciała funkcji, czyli instrukcji zapisanych w nawiasach klamrowych.

Ogólny schemat:

```text
typ_wyniku nazwa_funkcji(typ parametr_1, typ parametr_2)
{
    instrukcje;
    return wynik;
}
```

### Parametry i argumenty

Parametry to zmienne wymienione w definicji funkcji. Argumenty to wartości przekazywane podczas jej wywołania.

Argumenty przyporządkowuje się parametrom według kolejności. Pierwszy argument trafia do pierwszego parametru, drugi do drugiego.

W języku C argumenty są przekazywane przez wartość. Funkcja otrzymuje kopie przekazanych wartości. Zmiana parametru wewnątrz funkcji nie zmienia zmiennej użytej jako argument.

### Zwracanie wyniku

Instrukcja `return` kończy wykonanie funkcji i przekazuje wynik do miejsca jej wywołania.

Zwróconą wartość można przypisać do zmiennej, wykorzystać w wyrażeniu albo przekazać jako argument innej funkcji.

Funkcja, która nie zwraca wartości, ma typ wyniku `void`.

### Deklaracja i definicja

Deklaracja funkcji, nazywana również prototypem, określa jej nazwę, typ wyniku i typy parametrów. Kończy się średnikiem i nie zawiera ciała funkcji.

Definicja zawiera również ciało funkcji.

Przed wywołaniem funkcji kompilator musi znać jej deklarację. Możesz:

- umieścić definicję funkcji przed miejscem wywołania,
- umieścić prototyp przed `main`, a definicję poniżej `main`.

### Zmienne lokalne

Parametry i zmienne zadeklarowane w ciele funkcji są lokalne dla tej funkcji. Nie można odwoływać się do nich po nazwie z innej funkcji.

Różne funkcje mogą mieć zmienne o takich samych nazwach — są to odrębne zmienne.

## Przykład: odejmowanie dwóch liczb typu `float`

```c
#include <stdio.h>

float subtract(float a, float b)
{
    return a - b;
}

int main(void)
{
    float first = 15.5f;
    float second = 4.25f;
    float result = subtract(first, second);

    printf("result: %.4f\n", result);

    return 0;
}
```

## Odwrotna notacja polska

W odwrotnej notacji polskiej operator znajduje się po operandach.

Obowiązuje format:

```text
[pierwsza_liczba] [druga_liczba] [operator]
```

Separatorem jest **dokładnie jedna spacja**. Nie dodawaj spacji na początku ani na końcu wyrażenia podobnie jak tabulatoró i wielokrotnych spacji

Przykłady:

```text
20 6 +
20 6 -
20 6 *
20 6 /
```

## Format wyjścia

Wynik każdego działania wypisuj z czterema miejscami po przecinku, używając `%.4f`.

Przykład:

```text
result: 26.0000
```

Nie wypisuj zaproszeń do wpisania danych, nagłówków ani dodatkowych pustych linii.

Po wykryciu błędu wypisz jeden komunikat i zakończ program.

## Zadania

### 1. Uruchomienie programu startowego

1. Zbuduj i uruchom program.
2. Sprawdź wynik dodawania.
3. Zmień wartości `a` i `b` na `15.5f` oraz `4.25f`.
4. Sprawdź, czy program wypisuje:

   ```text
   result: 19.7500
   ```

### 2. Dwie liczby w osobnych liniach

Zastąp wartości wpisane w kodzie danymi odczytywanymi z klawiatury.

1. Odczytaj pierwszą linię przez `fgets`.
2. Przekonwertuj ją na `float` przez `strtof` i zapisz wynik w `a`.
3. Odczytaj drugą linię przez osobne wywołanie `fgets`.
4. Przekonwertuj ją na `float` i zapisz wynik w `b`.
5. Dodaj liczby i wypisz wynik.

Przykładowe wejście:

```text
15.5
4.25
```

Oczekiwane wyjście:

```text
result: 19.7500
```

Zastosuj tablice o rozmiarze 128 elementów. Wykorzystaj kontrolę odczytu całej linii z poprzedniego laboratorium. Przyjmij limit 127 znaków przed końcem linii.

Dla każdej liczby sprawdź:

- czy odczyt się powiódł,
- czy linia nie przekroczyła limitu,
- czy wykonano konwersję,
- czy wystąpił błąd `ERANGE`,
- czy wynik jest skończony,
- czy po liczbie pozostały wyłącznie białe znaki.

Przed każdą konwersją ustaw `errno` na `0`.

Sprawdź m.in. wejścia:

```text
abc
```

```text
15.5abc
```

```text
15.5 4.25
```

```text
1e9999
```

Odrzuć również `nan` i `inf`.

Nie używaj `scanf`, `sscanf` ani `atof` do konwersji.

### 3. Wydzielenie obliczeń do funkcji

Dodaj funkcje:

- `add`,
- `subtract`,
- `multiply`,
- `divide`.

Każda funkcja ma przyjmować dwie liczby typu `float` i zwracać wynik działania.

Zastąp dodawanie w `main` wywołaniem `add`.

Następnie sprawdź pozostałe funkcje dla `a = 15.5f` i `b = 4.25f`. Na tym etapie wywołaj je kolejno i wypisz:

```text
add: 19.7500
subtract: 11.2500
multiply: 65.8750
divide: 3.6471
```

Nie wywołuj `divide`, jeżeli drugi argument jest równy zero.

### 4. Operator w trzeciej linii

Dodaj trzecie wywołanie `fgets`, które odczytuje operator.

Kolejność wejścia na tym etapie:

1. pierwsza liczba,
2. druga liczba,
3. operator.

Przykładowe wejście:

```text
15.5
4.25
*
```

Oczekiwane wyjście:

```text
result: 65.8750
```

Obsługuj operatory:

| Operator | Funkcja |
|---|---|
| `+` | `add` |
| `-` | `subtract` |
| `*` | `multiply` |
| `/` | `divide` |

Wybierz funkcję za pomocą instrukcji `switch`.

Sprawdź, czy linia operatora zawiera jeden dozwolony znak, ewentualnie otoczony białymi znakami. Odrzuć dodatkowe znaki.

Przykłady niepoprawnego operatora:

```text
++
```

```text
abc
```

```text
%
```

Przed dzieleniem sprawdź, czy `b` jest równe zero. Dotyczy to również wartości `-0.0`.

Po obliczeniu sprawdź, czy wynik jest skończony.

Usuń wypisywanie wszystkich czterech działań z zadania 3. Program ma wypisywać wyłącznie wynik wybranego działania albo jeden komunikat błędu.

### 5. Jedna linia w odwrotnej notacji polskiej

Zastąp trzy osobne odczyty jednym odczytem linii przez `fgets`.

Dane mają mieć postać:

```text
pierwsza_liczba druga_liczba operator
```

Przykładowe wejście:

```text
15.5 4.25 *
```

Oczekiwane wyjście:

```text
result: 65.8750
```

Zachowaj funkcje arytmetyczne oraz wybór działania z poprzednich zadań. Zmień odczyt i interpretację wejścia.

Sprawdzaj elementy w kolejności:

1. pierwsza liczba,
2. dokładnie jedna spacja,
3. druga liczba,
4. dokładnie jedna spacja,
5. operator,
6. koniec wyrażenia.

Wykorzystaj wskaźniki końca konwersji zwracane przez `strtof`, aby ustalić, gdzie kończy się każda liczba.

Wymagania:

- operator musi być jednym z `+`, `-`, `*`, `/`,
- separatorem jest dokładnie jedna spacja,
- spacje na początku i na końcu wyrażenia są niedozwolone,
- tabulatory i inne białe znaki wewnątrz wyrażenia są niedozwolone,
- liczby mogą być ujemne lub poprzedzone znakiem `+`,
- dopuszczalny jest zapis wykładniczy, np. `1.5e2`,
- separatorem dziesiętnym jest kropka,
- bezpośrednio po operatorze musi wystąpić koniec tekstu albo końcowy znak nowej linii odczytany przez `fgets`,
- po operatorze nie mogą występować dodatkowe elementy,
- odrzucaj liczby spoza zakresu konwersji, NaN i nieskończoności.

Nie polegaj na automatycznym pomijaniu białych znaków przez `strtof`. Przed każdą konwersją sprawdź, czy liczba rozpoczyna się w wymaganym miejscu.

### 6. Komunikaty programu docelowego

Zastosuj następujące komunikaty:

| Sytuacja | Wyjście |
|---|---|
| Poprawne działanie | `result: wartość` |
| Niepoprawny układ wyrażenia, separator lub zapis liczby | `error: invalid input` |
| Nieobsługiwany operator | `error: invalid operator` |
| Błąd zakresu konwersji, NaN lub nieskończoność na wejściu | `error: invalid number` |
| Dzielenie przez zero | `error: division by zero` |
| Nieskończony wynik obliczenia lub NaN | `error: invalid result` |
| Zbyt długa linia | `error: input too long` |
| EOF bez danych | `error: no input` |
| Błąd odczytu | `error: read failure` |

Najpierw sprawdź odczyt i długość linii. Następnie sprawdzaj wyrażenie od lewej do prawej. Po znalezieniu błędu wypisz komunikat i zakończ program.

Nie wykonuj działania przed sprawdzeniem całego wyrażenia.

### 7. Sprawdzenie programu

Sprawdź następujące przykłady dla wersji z jednym odczytem:

| Wejście | Oczekiwane wyjście |
|---|---|
| `15.5 4.25 +` | `result: 19.7500` |
| `15.5 4.25 -` | `result: 11.2500` |
| `15.5 4.25 *` | `result: 65.8750` |
| `15.5 4.25 /` | `result: 3.6471` |
| `4.25 15.5 -` | `result: -11.2500` |
| `-2.5 4 +` | `result: 1.5000` |
| `1.5e2 2 +` | `result: 152.0000` |
| `10 0 /` | `error: division by zero` |
| `10 2 %` | `error: invalid operator` |
| `abc 2 +` | `error: invalid input` |
| `1 2abc +` | `error: invalid input` |
| `1 2 + 3` | `error: invalid input` |
| `1 +` | `error: invalid input` |
| `1 2+` | `error: invalid input` |
| `nan 2 +` | `error: invalid number` |
| `1e9999 2 +` | `error: invalid number` |
| `15.5  4.25 +` — dwie spacje między liczbami | `error: invalid input` |
| `15.5 4.25  +` — dwie spacje przed operatorem | `error: invalid input` |
| ` 15.5 4.25 +` — spacja na początku | `error: invalid input` |
| `15.5 4.25 + ` — spacja na końcu | `error: invalid input` |
| Tabulator zamiast którejkolwiek spacji | `error: invalid input` |

### 8. Debugowanie

1. Ustaw breakpoint po odczytaniu linii.
2. Dodaj do WATCH:

   - bufor z wyrażeniem,
   - `operation`,
   - `a`,
   - `b`,
   - wskaźnik końca konwersji.

3. Uruchom program dla:

   ```text
   15.5 4.25 /
   ```

4. Wykonuj program krokowo.
5. Sprawdź, gdzie kończy się odczyt pierwszej i drugiej liczby.
6. Wejdź do funkcji `divide` klawiszem `F11`.
7. Sprawdź wartości argumentów i zwracany wynik.

Powtórz dla:

```text
15.5abc 4.25 +
```

Wskaż warunek, który odrzuca to wejście.


_Last updated: 2026-10-25_