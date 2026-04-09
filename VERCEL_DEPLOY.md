# ⚡ SZYBKIE WDROŻENIE NA VERCEL

## 🚀 Metoda 1: Przez Dashboard (ZALECANA - 5 minut)

### Krok 1: Połącz GitHub z Vercel

1. Wejdź na: **https://vercel.com/new**
2. Zaloguj się przez GitHub (lub utwórz konto)
3. Autoryzuj dostęp Vercel do GitHub

### Krok 2: Import projektu

1. W Vercel kliknij **"Add New..." → "Project"**
2. Znajdź repository: **Paula066/blazorTest**
3. Kliknij **"Import"**

### Krok 3: Konfiguracja (WAŻNE!)

Vercel nie może buildować .NET bezpośrednio, więc użyjemy **GitHub Actions**:

**W ustawieniach projektu na Vercel:**
- Framework Preset: **Other**
- Build Command: **POZOSTAW PUSTE**
- Output Directory: **output/wwwroot**
- Install Command: **POZOSTAW PUSTE**

### Krok 4: Deploy!

Kliknij **"Deploy"** 

⚠️ **UWAGA**: Pierwsze wdrożenie może się NIE UDAĆ - to normalne! Musimy użyć GitHub Actions do budowania.

---

## 🔧 Metoda 2: GitHub Actions + Vercel (Automatyczne)

Ta metoda automatycznie buduje aplikację przy każdym push.

### Już skonfigurowane! ✅

Dodałem plik `.github/workflows/vercel.yml` który:
1. Automatycznie buduje aplikację przy każdym push
2. Wdraża na Vercel
3. Działa bez dodatkowej konfiguracji

**Co musisz zrobić:**

1. Wejdź na GitHub: https://github.com/Paula066/blazorTest/settings/secrets/actions
2. Dodaj dwa sekrety:
   - `VERCEL_TOKEN` - token z https://vercel.com/account/tokens
   - `VERCEL_ORG_ID` - znajdziesz w Vercel Project Settings
   - `VERCEL_PROJECT_ID` - znajdziesz w Vercel Project Settings

### Jak zdobyć tokeny:

**VERCEL_TOKEN:**
1. https://vercel.com/account/tokens
2. Kliknij "Create"
3. Nazwij go np. "GitHub Actions"
4. Skopiuj token

**VERCEL_ORG_ID i VERCEL_PROJECT_ID:**
1. Otwórz swój projekt na Vercel
2. Settings → General
3. Przewiń na dół - znajdziesz tam oba ID

---

## 📦 Metoda 3: Build lokalnie, deploy ręcznie

```bash
# 1. Zbuduj aplikację
dotnet publish -c Release -o output

# 2. Zainstaluj Vercel CLI (tylko raz)
npm install -g vercel

# 3. Wdróż folder wwwroot
cd output/wwwroot
vercel --prod
```

---

## ✅ Weryfikacja

Po wdrożeniu:
1. Otrzymasz URL: `https://twoj-projekt.vercel.app`
2. Otwórz w przeglądarce
3. Sprawdź czy wszystkie strony działają:
   - `/` - Strona główna
   - `/counter` - Licznik
   - `/fetchdata` - Dane
   - `/komponenty` - Komponenty

---

## 🔄 Automatyczne aktualizacje

Po pierwszym wdrożeniu:
- Każdy `git push` do `main` = automatyczne wdrożenie
- Preview deployments dla innych branchy
- Rollback w jednym kliknięciu

---

## ❓ Problemy?

### "Build failed"
- Użyj GitHub Actions (Metoda 2)
- Lub build lokalnie (Metoda 3)

### "404 on refresh"
- Upewnij się że `vercel.json` ma routing dla SPA
- Plik już zawiera poprawną konfigurację ✅

### Długie ładowanie
- To normalne dla Blazor WASM (2-3 MB przy pierwszym ładowaniu)
- Następne wizyty będą szybsze (cache)

---

**Potrzebujesz pomocy?** Zobacz główny README.md lub FAQ.md
