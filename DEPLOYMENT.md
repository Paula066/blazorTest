# 🚀 Szybki Start - Wdrożenie na Vercel

## Krok 1: Przygotowanie

Upewnij się, że masz:
- ✅ Konto na [Vercel](https://vercel.com) (możesz zalogować się przez GitHub)
- ✅ Repository Git (GitHub, GitLab, lub Bitbucket)

## Krok 2: Push do Git

```bash
# Inicjalizuj git (jeśli jeszcze nie zrobione)
git init

# Dodaj pliki
git add .

# Commit
git commit -m "Initial Blazor WASM app"

# Dodaj remote (zamień na swój repository)
git remote add origin https://github.com/TWOJ-USERNAME/TWOJ-REPO.git

# Push
git push -u origin main
```

## Krok 3: Wdróż na Vercel

### Metoda A: Przez Dashboard (najprostsza)

1. Wejdź na [vercel.com/new](https://vercel.com/new)
2. Kliknij "Import Project"
3. Wybierz swój repository
4. Vercel automatycznie wykryje `vercel.json`
5. Kliknij **"Deploy"**
6. Gotowe! 🎉

### Metoda B: Przez CLI

```bash
# Zainstaluj Vercel CLI
npm install -g vercel

# Zaloguj się
vercel login

# Wdróż
vercel

# Lub od razu produkcyjnie
vercel --prod
```

## Krok 4: Testowanie

Po wdrożeniu otrzymasz URL typu: `https://twoj-projekt.vercel.app`

Otwórz w przeglądarce i sprawdź, czy aplikacja działa!

## 🔄 Automatyczne wdrożenia

Po podłączeniu z Git, każdy push do branch'a automatycznie wdroży nową wersję:

- Push do `main` → Wdrożenie produkcyjne
- Push do innego brancha → Preview deployment

## 🛠️ Lokalne testowanie przed wdrożeniem

```bash
# Uruchom lokalnie
dotnet run

# Lub z auto-reload
dotnet watch

# Zbuduj wersję produkcyjną
dotnet publish -c Release -o output

# Sprawdź pliki w: output/wwwroot/
```

## ⚡ Pro Tips

1. **Domena własna**: W Vercel Dashboard → Settings → Domains
2. **Environment Variables**: Settings → Environment Variables
3. **Analytics**: Settings → Analytics (włącz bezpłatne statystyki)
4. **Logi**: Sprawdzaj logi wdrożenia w zakładce "Deployments"

## ❓ Problemy?

### "Build failed"
- Sprawdź, czy `vercel.json` jest w głównym folderze
- Upewnij się, że .NET SDK jest dostępny

### "404 na podstronach"
- `vercel.json` zawiera routing dla SPA
- Wszystkie ścieżki przekierowują do `index.html`

### "Długie ładowanie"
- To normalne dla Blazor WASM (2-3 MB przy pierwszym ładowaniu)
- Rozważ dodanie ekranu ładowania w `index.html`

---

**Gotowe!** Twoja aplikacja Blazor jest teraz live na Vercel! 🚀
