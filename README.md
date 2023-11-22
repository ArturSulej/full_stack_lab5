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
W tym zadaniu maksymalna liczba replik została ustawiona na 7. Zakładając że pojedyncza replika będzie wykorzystywana do maksimum tj. 250m CPU i 250Mi pamięci, a quota ustawia ograniczenia na 2000m CPU i 1,5Gi pamięci, to chcąc wyznaczyć ile maksymalnie replik może zostać uruchomionych, wystartczy podzielić maksymalne ograniczenie przez maksymalne wykorzystywanie CPU, w tym przypadku jest to 2000/250, co w przybliżeniu do całości daje 7.

# Zadanie 5
Poniższe polecenia pozwalają stwierdzić, czy powyższe pliki i polecenia działają, a obiekty są tworzone. <br>
`kubectl get pods -n zad5` - Sprawdzenie czy pody są utworzone <br>
`kubectl get services -n zad5` - Sprawdzenie czy usługa jest utworzona prawidłowo <br>
`kubectl get hpa -n zad5` - Sprawdzenie czy hpa się utworzył poprawnie

# Zadanie 6
Polecenie `kubectl get services -n zad5` pozwala dowiedzieć się, pod jakim adresem IP operuje utworzona usługa. Adres ten należy wykorzystać w poleceniu: <br>
`kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- <ADRES_IP>; done"` <br>
Po uruchomieniu powyższego polecenia, należy uruchomić nowe okno konsoli i wywołać polecenie `kubectl get hpa -n zad5 --watch`. Pozwala ono na obserwowanie w czasie rzeczywistym jak zmienia się liczba replik oraz zużycie zasobów.
