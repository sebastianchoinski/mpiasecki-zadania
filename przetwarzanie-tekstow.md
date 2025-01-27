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
