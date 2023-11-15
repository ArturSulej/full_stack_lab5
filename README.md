# full_stack_lab5
Rozwiązanie zadań dla laboratorium5 z przedmiotu Programowanie Full Stack w Chmurze Obliczeniowej

# Wprowadzenie
Przed przystąpieniem do poniższych zadań, należy utworzyć przestrzeń nazw zad5 <br>
`kubectl create namespace zad5` <br>

# Zadanie 1
Plik `zad5-resource-quota.yaml` pozwala na utworzenie zestawu ograniczeń, zgodnie z wytycznymi z zadania. Aby użyć pliku, należy wykonać polecenie: <br>
`kubectl apply -n zad5 -f zad5-resource-quota.yaml`

# Zadanie 2
Plik `worker-pod.yaml` pozwala na utworzenie poda w przestrzeni nazw zad5 na obrazie nginx, o nazwie worker, który posiada ograniczenia zdefiniowane w poleceniu. Aby wykorzystać plik, należy wykonać polecenie: <br>
`kubectl apply -n zad5 -f worker-pod.yaml`

# Zadanie 3
Plik ` php-apache-deployment-service.yaml` tworzy obiekty Deployment i Service i odpowiednio ogranicza ich zasoby. Polecenie: <br>
`kubectl apply -n zad5 -f php-apache-deployment-service.yaml`

# Zadanie 4
Plik `php-apache-hpa.yaml` pozwala na utworzenie obiektu HPA, pozwalającego na autoskalowanie wdrożenia php-apache. Polecenie: <br>
`kubectl apply -n zad5 -f php-apache-hpa.yaml`

### Uwaga
W tym zadaniu maksymalna liczba replik została ustawiona na 8. Takie ustawienie pozwala zachować pewnego rodzaju bezpieczną strefę, dzięki czemu 2 pody będą dostępne, dopóki administrator ich ręcznie nie skonfiguruje.

# Zadanie 5
Poniższe polecenia pozwalają stwierdzić, czy powyższe pliki i polecenia działają, a obiekty są tworzone. <br>
`kubectl get pods -n zad5` - Sprawdzenie czy pody są utworzone <br>
`kubectl get services -n zad5` - Sprawdzenie czy usługa jest utworzona prawidłowo <br>
`kubectl get hpa -n zad5` - Sprawdzenie czy hpa się utworzył poprawnie
