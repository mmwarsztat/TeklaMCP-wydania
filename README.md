# TeklaMCP Dashboard — wydania

To repozytorium trzyma **wyłącznie gotowe instalatory** dashboardu. Kod źródłowy siedzi
osobno, w prywatnym repozytorium `mmwarsztat/TeklaMCP`.

## Po co osobne repozytorium

Dashboard sam sprawdza, czy jest nowsza wersja, i sam ją instaluje. Musi więc mieć dostęp
do miejsca z wydaniami — a nie chcemy, żeby miał dostęp do repozytorium z kodem i całą jego
historią. Stąd podział: program dostaje token uprawniony **tylko do tego repozytorium**,
i tylko do odczytu.

## Co jest w wydaniu

| Plik | Do czego |
|---|---|
| `TeklaMCP-Setup-X.Y.Z.exe` | instalator (osadzony Python + dashboard + binarki wtyczki dla Tekla 2023-2026) |
| `latest.json` | manifest: numer wersji, nazwa pliku, suma SHA-256, rozmiar — to jego czyta dashboard |

Instalacja jest per-użytkownik (`%LOCALAPPDATA%\TeklaMCP`), bez praw administratora.

## Jak powstaje wydanie

W repozytorium z kodem:

```
python scripts/build_release.py --version X.Y.Z
gh release create vX.Y.Z --repo mmwarsztat/TeklaMCP-wydania dist/TeklaMCP-Setup-X.Y.Z.exe dist/latest.json
```
