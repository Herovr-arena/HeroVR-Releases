# HeroVR Releases

Publiczne repozytorium **tylko z gotowymi wydaniami** programu HeroVR Master Launcher.

Kod źródłowy i dokumentacja znajdują się w osobnym, prywatnym repozytorium. Tutaj
trafiają wyłącznie pliki wykonywalne i informacja o najnowszej wersji.

## Co tu jest

| Plik | Przeznaczenie |
|---|---|
| `latest.json` | informacja o najnowszym wydaniu — **ten plik czyta launcher** |
| `releases/<wersja>/HeroVR_Launcher.exe` | plik wykonywalny danego wydania |
| `README.md` | ten opis |

## Jak launcher sprawdza aktualizacje

Launcher pobiera `latest.json` i porównuje numer wersji ze swoim:

```
https://raw.githubusercontent.com/Herovr-arena/HeroVR-Releases/main/latest.json
```

Jeżeli wersja w pliku jest nowsza, w nagłówku launchera pojawia się przycisk
aktualizacji. Jeżeli pliku nie ma, nie ma internetu albo numer jest nieczytelny —
launcher nie robi nic i nie pokazuje operatorowi żadnego komunikatu.

### Zawartość `latest.json`

```json
{
  "version": "1.11.22",
  "url": "https://github.com/Herovr-arena/HeroVR-Releases/raw/main/releases/1.11.22/HeroVR_Launcher.exe",
  "sha256": "…",
  "size": 33287229,
  "date": "2026-10-04",
  "notes": "krótki opis zmian dla operatora",
  "min_version": "1.11.0"
}
```

| Pole | Znaczenie |
|---|---|
| `version` | najnowsza dostępna wersja |
| `url` | bezpośredni adres pliku `.exe` |
| `sha256` | suma kontrolna pliku — launcher **nie uruchomi** pliku, który się nie zgadza |
| `size` | rozmiar w bajtach, do sprawdzenia po pobraniu |
| `notes` | jedna–trzy linie opisu, pokazywane operatorowi |
| `min_version` | od jakiej wersji działa ten mechanizm aktualizacji |

## Jak wydać nową wersję

W repozytorium z kodem:

```
powershell -ExecutionPolicy Bypass -File tools\release_to_public.ps1 -Version 1.11.23 -Notes "opis zmian"
```

Skrypt kopiuje zbudowany plik do `releases/<wersja>/`, liczy `sha256`, aktualizuje
`latest.json` i wysyła zmiany tutaj. Numer wersji musi być zgodny z tym w kodzie
(`LAUNCHER_VERSION`), inaczej skrypt przerwie pracę.

## Czego tu nie ma

W tym repozytorium **nie ma** kodu źródłowego, konfiguracji, danych klientów ani
żadnych informacji o działalności. Wyłącznie pliki wykonywalne programu i informacja
o wersji.
