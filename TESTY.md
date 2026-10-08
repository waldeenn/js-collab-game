## Mapa ma cztery pokoje, tylko jeden zaznaczony. Informacje są bezpłatne.


próba: mapa()
oczekiwane: 4 pomieszczenia, jedno zaznaczone

otrzymane: 4 pomieszczenia, jedno zaznaczone

## Lewo z pokoju 1 i nieznany kierunek nie zmieniają danych.

próba: idz("lewo"), (gdy pokoj===1)

oczekiwane: uderzenie w ściane

otrzymane: uderzenie w ściane

próba: idz("nigdzie")

oczekiwane: nieznany kierunek

otrzymane: nieznany kierunek

# Prawo przesuwa o jeden pokój i zużywa jedną energię.

próba: idz("prawo")

oczekiwano: zmiana stanu pokoju o 1 więcej, zmiana stanu energii o 1 mniej

otrzymano: zmiana stanu pokoju o 1 więcej, zmiana stanu energii o 1 mniej

# Tego samego przedmiotu nie da się zabrać dwa razy.

próba: `
akcja("karta")
akcja("karta")
`

oczekiwano: poprawne zebranie karty przy pierwszej próbie i 
brak sukcesu przy 2 próbie

otrzymano: poprawne zebranie karty przy pierwszej próbie i 
brak sukcesu przy 2 próbie

próba: `
akcja("bezpiecznik")
akcja("bezpiecznik")
`
(gdy pokoj===2)

oczekiwano: poprawne zebranie bezpiecznika przy pierwszej próbie i 
brak sukcesu przy 2 próbie

otrzymano: poprawne zebranie bezpiecznika przy pierwszej próbie i 
brak sukcesu przy 2 próbie


próba: `
akcja("napraw")
akcja("napraw")
`
(gdy pokoj===2 i spelnione warunki bezpiecznik=true i karta=true)

oczekiwano: poprawne naprawienie przy pierwszej próbie i 
brak sukcesu przy 2 próbie

otrzymano: poprawne naprawienie przy pierwszej próbie i 
brak sukcesu przy 2 próbie

próba `
akcja("wyjdz")
akcja("wyjdz")
`

(gdy pokoj===3 i spelnione warunki karta=true zasilanie=true)

oczekiwano: zakonczenie gry przy pierwszej próbie i 
brak komunikatu przy drugiej

otrzymano: zakonczenie gry przy pierwszej próbie i 
brak komunikatu przy drugiej

# Nie da się naprawić zasilania bez bezpiecznika ani otworzyć drzwi bez obu wymagań.

próba `
    akcja('napraw')
`
gdy pokoj===3 i !bezpiecznik

oczekiwane: brak możliwości naprawienia zasilania

otrzymane: brak możliwości naprawienia zasilania

próba `
akcja('wyjdz')
`
gdy pokoj===4 i karta===True, zasilanie===True

oczekiwane: brak możliwości zakończenia gry

otrzymane: brak możliwości zakończenia gry

# Da się wygrać, wykonując potrzebne czynności w rozsądnej kolejności.

próba `
akcja("karta")
idz("prawo")
akcja("bezpiecznik")
idz("prawo")
akcja("napraw")
idz("prawo")
akcja("wyjdz")
`

oczekiwane: zakończenie gry

otrzymane: zakończenie gry

# Po dziesięciu poprawnych ruchach bez wygranej następuje porażka. Kolejny ruch nie zmienia już stanu.

próba: nie chce mi się tego pisać


oczekiwano: przegrana

otrzymane: przegrana

# start() przywraca energię, pozycję oraz wszystkie flagi.

próba: start()

oczekiwano: przywrócenie początkowych wartości

otrzymano: przywrócenie początkowych wartości