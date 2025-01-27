# Napisz program, który wczyta łańcuch znaków z klawiatury, a następnie usunie z tego łańcucha pierwszą małą literę.

```c
int main() {
    char str[100];
    int i, j;

    printf("Wprowadź łańcuch znaków: ");
    fgets(str, sizeof(str), stdin);

    // Usuń znak nowej linii, jeśli istnieje
    size_t len = strlen(str);
    if (len > 0 && str[len - 1] == '\n') {
        str[len - 1] = '\0';
    }

    // Znajdź i usuń pierwszą małą literę
    for (i = 0; str[i] != '\0'; i++) {
        if (islower(str[i])) {
            for (j = i; str[j] != '\0'; j++) {
                str[j] = str[j + 1];
            }
            break;
        }
    }

    printf("Łańcuch po usunięciu pierwszej małej litery: %s\n", str);

    return 0;
}
```

---

# Napisz funkcję, która usunie wszystkie początkowe spacje w łańcuchu tekst, który powinien być parametrem wejściowo/wyjściowym tej funkcji.

```c
void trimLeadingSpaces(char *tekst) {
    size_t len = strlen(tekst);
    for (size_t i = 0; i < len; i++) {
        if (tekst[i] != ' ') {
            // Przepisanie reszty tekstu na początek
            memmove(tekst, &tekst[i], len - i + 1);
            break;
        }
    }
}
```

# Napisz funkcję formatującą tekst poprzez usunięcie wszystkich początkowych i końcowych spacji z łańcucha zadanego jako parametr wejściowy tej funkcji.

```c
void trimSpaces(char *tekst) {
    size_t len = strlen(tekst);

    // Usuń początkowe spacje
    size_t start = 0;
    while (start < len && tekst[start] == ' ') {
        start++;
    }

    // Usuń końcowe spacje
    size_t end = len;
    while (end > start && tekst[end - 1] == ' ') {
        end--;
    }

    // Przepisz tekst bez początkowych i końcowych spacji
    // memmove przesuwa dane z obszaru źródłowego (&tekst[start]) do obszaru docelowego (tekst).
    // Parametry:
    // - tekst: wskaźnik do miejsca docelowego, gdzie zostanie zapisany wynikowy tekst bez spacji.
    // - &tekst[start]: wskaźnik na pierwszy znak, który nie jest spacją, w oryginalnym łańcuchu.
    // - end - start: liczba bajtów do skopiowania, obliczona jako różnica między końcem a początkiem tekstu bez spacji.
    // memmove działa poprawnie nawet wtedy, gdy obszary źródłowy i docelowy częściowo zachodzą na siebie.
    memmove(tekst, &tekst[start], end - start);
    tekst[end - start] = '\0'; // Dodaj znak końca ciągu
}

```

# Napisz funkcję usuwającą (poprzez skrócenie tekstu)wszystkie spacje z łańcucha podawanego jako parametr tej funkcji.

```c
void removeAllSpaces(char *tekst) {
    size_t len = strlen(tekst);
    size_t j = 0;


    for (size_t i = 0; i < len; i++) {
        if (tekst[i] != ' ') {
            tekst[j++] = tekst[i];
        }
    }

    tekst[j] = '\0';
}

```

# Napisz funkcję usuwającą z zadanego łańcucha (poprzez skrócenie tekstu) wszystkie bezpośrednie powtórzenia liter np. zamieniającą tekst “kommputter” na ”komputer”.

```c
void usun(char *tekst) {
    size_t len = strlen(tekst);
    size_t j=0;
    for (size_t i = 1; i < len; i++) {
        if(tekst[j]!=tekst[i]) {
            tekst[++j]=tekst[i];
        }
    }
    tekst[j+1] = '\0';
}
```

# Napisz funkcję dodającą zadaną ilość spacji na początku zadanego łańcucha tekst(wcześniejsza zawartość tekstu przesuwana jest na dalsze pozycje)

```c
void dodaj_spacje(int ile, char *tekst) {
    size_t len = strlen(tekst);

    memmove(tekst+ile, tekst, len+1);

    for(size_t i = 0; i<ile; i++){
        tekst[i] = ' ';
    }
}

```

# Napisz funkcję usuwającą z łańcucha tekst wszystkie litery poczynając od pozycji pocz do litery na pozycji kon.

```c
void usun_od(int pocz, int konc, char *tekst) {
    size_t len = strlen(tekst)

    size_t przesun = konc - pocz +1;
    memmove(&tekst[pocz], &tekst[konc+1], len-konc); // przesun na pozycje pocz,
    // rzeczy od momentu pierwszego znaku po konc,
    // rzeczy o rozmiarze len-kon

    tekst[len-przesun]='\0';


}
```

# Napisz funkcję wyrównującą długość zadanego tekst'u do N znaków, poprzez dodanie odpowiedniej ilości spacji na końcu tego łańcucha.

```c
void wyrownaj(int N, char *tekst) {
    size_t len = strlen(tekst);

    for(size_t i = len; i<=N; i++) {
        tekst[i] = ' ';
    }
    tekst[N] = '\0';

}

```

# Napisz funkcję sprawdzającą czy zadany łańcuch znaków ma symetryczną zawartość tzn, pierwszy znak jest równy ostatniemu, drugi przedostatniemu itd.

```c
void sprawdz_symetrie(char *tekst) {
    size_t len = strlen(tekst);
    size_t ostatni = len - 1;

    for (size_t i = 0; i < len / 2; i++) {
        if (tekst[i] != tekst[ostatni - i]) {
            printf("niesymetryczny\n");
            return;
        }
    }

    printf("symetryczny\n");
}
```
