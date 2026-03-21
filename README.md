Lab 3 punkt

Skonfigurować i uruchomić lokalny rejestr obrazów wykorzystując samodzielnie

podpisany certyfikat. Wykonane działania proszę krótko opisać.


W pierwszej kolejności wygenerowany został klucz prywatny oraz certyfikat TLS za pomocą narzędzia OpenSSL dla lab3rejest.local. 

Należało zapewnić zaufane połączenie w tym celu zmapowany został adres 127.0.0.1 w plikach hosts systemu WSL i Windows. 

Na koniec uruchomiony został kontener z rejestrem który wskazał mu pliki certyfikatow i włączając szyfrowanie HTTPS oraz funkcję usuwania obrazów.


Dla potwierdzenia wykonania następnego punktu został podesłany załącznik w formie obrazu.


Lab4

punkt: 

• wprowadzone zmiany b. krótko uzasadnić

Dockerfile modyfikacja:

Jako obraz bazowy wykorzystano Ubuntu:latest.

Dodano dane autora za pomocą instrukcji LABEL aby obraz zawierał metadane dotyczące twórcy.

Optymalizacja: Połączono komendy apt-get update oraz apt-get install w jedną instrukcję RUN i dodano czyszczenie pamięci podręcznej. 

Zredukowało to liczbę warstw i zmniejszyło rozmiar końcowy obrazu.

punkt:

• sprawdzić czy na podstawie tego Dockerfile-a można zbudować obraz a na podstawie

poznanych narzędzi należy wskazać, ile warstw posiada opracowany obraz


Opracowany obraz posiada 3 warstwy funkcjonalne (dane z Ubuntu, instalacja Apache oraz plik strony WWW). Pozostałe instrukcje (jak EXPOSE czy CMD) stanowią jedynie metadane konfiguracji kontenera (0B).


ETAP 3

Zbudowany obraz został pomyślnie udostępniony w dwóch lokalizacjach:

DockerHub: Przesłano obraz do publicznego repozytorium pod nazwą pejas/laboratoria:lab4.

Integracja z Lab 3: Wykorzystując bezpieczny, lokalny rejestr z poprzedniego laboratorium, obraz został przesłany na adres lab3rejestr.local:5000/web100:v1.


pejas@Kacper1:~/lab4$ docker tag web100 lab3rejestr.local:5000/web100:v1

pejas@Kacper1:~/lab4$ docker push lab3rejestr.local:5000/web100:v1

The push refers to repository [lab3rejestr.local:5000/web100]

7875c714dbc8: Pushed

817807f3c64e: Pushed

329327692e6a: Pushed

bc43777f8e31: Pushed

v1: digest: sha256:92ee851ad57ccc67ef6fafd8bb41e87fc788a33123eef7c5b19fd077321c1c60 size: 855

pejas@Kacper1:~/lab4$ curl -k https://lab3rejestr.local:5000/v2/_catalog

{"repositories":["lab3alpine","web100"]}

pejas@Kacper1:~/lab4$
