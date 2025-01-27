# Zdefiniuj typ strukturalny oraz 100-elementową tablicę pozwalającą przechowywać informacje o książkach w bibliotece (tytuł, autor, indeks, cena) oraz napisz funkcję, która wyświetli na ekranie wszystkie dane tanich książek (tzn. cena<10zł)

```c
typedef struct {
    char tytul[100];
    char autor[100];
    int indeks;
    float cena;
} Ksiazka;

Ksiazka biblioteka[100];


for (size_t i = 0; i < rozmiar; i++) {
    if (biblioteka[i].cena < 10.0) {
        printf("Tytuł: %s, Autor: %s, Indeks: %d, Cena: %.2f zł\n",
                biblioteka[i].tytul,
                biblioteka[i].autor,
                biblioteka[i].indeks,
                biblioteka[i].cena);
    }
}



```

# Zdefiniuj strukturę przechowującą dane katalogowe ksiażki w bibliotece (tytuł = 50 znaków; autor = 30 znaków; liczba stron = liczba całkowita dodatnia; wypożyczona = zmienna logiczna) oraz 200-elementową tablicę takich struktur. Napisz funkcję drukującą na ekranie spis wszystkich niewypożyczonych książek, które mają więcej niż 100 stron.

```c
typedef struct {
char tytul[50];
char autor[30];
int strony;
bool wypozyczona;

} Ksiazka;

Ksiazka biblioteka[200];


for(size_t i = 0; i<rozmiar; i++){
    if(biblioteka[i].wypozyczona==0 && biblioteka[i].strony>100 ){
        printf("%d"biblioteka[i].tytul);
    }
}
```

# Zdefiniuj typ strukturalny oraz 100-elementową tablicę pozwalającą przechowywać informacje o samochodach w auto-komisie (marka, przebieg, kolor, cena) oraz napisz funkcję, która wyświetli na ekranie wszystkie dane samochodu o najmniejszym przebiegu.

```c
typedef struct {
char marka[100];
int przebieg;
char kolor[20];
int cena;

} Komis;
Komis samochody[100];
int najmniejszy = samochody[0].przebieg;
int indeks = 0;
for(int i = 1; i<rozmiar; i++){
    if(samochody[i].przebieg<najmniejszy){
        najmniejszy=samochody[i].przebieg;
        indeks = i;
    }
for(int i = 0; i<rozmiar; i++){
    if(samochody[i].indeks==najmniejszy){
        printf("%s", samochody[i].marka);
    }
}
}
```
