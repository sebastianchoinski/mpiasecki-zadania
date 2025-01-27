# Napisz funkcję wyznaczającą wartość średnią z ciągu liczb typu rzeczywistych (double) zapisanych na dysku w pliku binarnym "dane.dat".

```c
double wyznaczSrednia(const char *nazwaPliku) {
    FILE *plik = fopen(nazwaPliku, "rb");
    if (plik == NULL) {
        printf("Nie można otworzyć pliku");
        return 0.0;
    }
    double liczba, suma = 0.0;
    size_t licznik = 0;
    // Odczyt liczb z pliku
    while (fread(&liczba, sizeof(double), 1, plik) == 1) {
        // fread: wskaznik na zmienna do zapisania, rozmiar jednego elementu, liczba elementow do dczytania, wskaznik do pliku
        suma += liczba;
        licznik++;
    }

    fclose(plik);
    if (licznik == 0) {
        printf("Plik jest pusty lub brak danych.");
        return 0.0;
    }
    return suma / licznik;
}

```

---

# Dany jest plik tekstowy, o nazwie "dane.txt", zawierający liczby rzeczywiste. Napisz funkcję kopiującą zawartość tego pliku do nowego (tekstowego) pliku "wyniki.dat", ale z pominięciem liczb ujemnych.

```c
void kopiujDodatnie(const char *plikWe, const char *plikWy) {
    FILE *we = fopen(plikWe, "r");
    if (we == NULL) {
        perror("Nie można otworzyć pliku wejściowego");
        return;
    }

    FILE *wy = fopen(plikWy, "w");
    if (wy == NULL) {
        perror("Nie można otworzyć pliku wyjściowego");
        fclose(we);
        return;
    }

    double liczba;

    // Odczyt liczb z pliku wejściowego i zapis liczb dodatnich do wyjściowego
    while (fscanf(we, "%lf", &liczba) == 1) {
        if (liczba >= 0) {
            fprintf(wy, "%.2f\n", liczba);
        }
    }

    fclose(we);
    fclose(wy);
}

```

---

# Dany jest plik binarny, o nazwie "liczby.bin", zawierający nieznaną ilość czterobajtowych liczb całkowitych. Napisz funkcję odwracającą kolejność liczb w tym pliku tzn., że pierwsza liczba znajdzie się na końcu pliku a ostatnia liczba na pierwszej pozycji, druga liczba na przedostatniej pozycji a przedostatnia na drugiej, itd.

```c
int znajdzMaksymalnaPozycja(const char *plik) {
    FILE *f = fopen(plik, "r"); // Tryb odczytu tekstowego
    if (f == NULL) {
        perror("Nie można otworzyć pliku");
        return -1;
    }

    int liczba, max, pozycja = -1, aktualnaPozycja = 0;
    if (fscanf(f, "%d", &max) == 1) {
        pozycja = 0;
    }

    while (fscanf(f, "%d", &liczba) == 1) {
        aktualnaPozycja++;
        if (liczba > max) {
            max = liczba;
            pozycja = aktualnaPozycja;
        }
    }

    fclose(f);
    return pozycja;
}

```

# Napisz funkcję wyznaczającą liczbę wystąpień sekwencji liter: 'aa' , 'bb' lub 'cc' w ciągu znaków zapisanych na dysku w binarnym pliku "dane.dat".

```c
int liczWystapieniaSekwencji(const char *plik) {
    FILE *f = fopen(plik, "rb"); // Tryb odczytu binarnego
    if (f == NULL) {
        perror("Nie można otworzyć pliku");
        return -1;
    }

    char poprzedni = 0, aktualny;
    int licznik = 0;

    // Czytaj znaki z pliku
    while (fread(&aktualny, sizeof(char), 1, f) == 1) {
        // Sprawdzaj, czy sąsiadujące znaki tworzą 'aa', 'bb' lub 'cc'
        if ((poprzedni == 'a' && aktualny == 'a') ||
            (poprzedni == 'b' && aktualny == 'b') ||
            (poprzedni == 'c' && aktualny == 'c')) {
            licznik++;
        }
        poprzedni = aktualny; // Przesuń "okno"
    }

    fclose(f);
    return licznik;
}

```
