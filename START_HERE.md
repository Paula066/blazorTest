# ⚡ SZYBKI START - Automatyczny deployment na Vercel

## 🎯 Co masz teraz:

✅ Aplikacja Blazor WASM działa lokalnie: http://localhost:5090  
✅ Kod jest na GitHub: https://github.com/Paula066/blazorTest  
✅ GitHub Actions gotowe do automatycznego buildowania  

## 🚀 Co musisz zrobić (5 minut):

### 1. Utwórz projekt na Vercel (jeśli jeszcze nie masz)

- Wejdź na: https://vercel.com/new
- Import: **Paula066/blazorTest** z GitHub
- Framework: **Other**
- **NIE ZMIENIAJ** Build/Output settings (GitHub Actions to zrobi)
- Kliknij **Deploy** (pierwsze wdrożenie może się nie udać - to OK!)

### 2. Pobierz tokeny z Vercel

Otwórz te 2 linki w nowych kartach:

📍 **Token:** https://vercel.com/account/tokens
   - Create Token → Nazwij "GitHub Actions"
   - **SKOPIUJ I ZAPISZ TOKEN!**

📍 **Project Settings:** https://vercel.com/dashboard
   - Wybierz projekt `blazorTest`
   - Settings → General → przewiń w dół
   - Skopiuj **Project ID** i **Organization ID**

### 3. Dodaj sekrety w GitHub

Otwórz: https://github.com/Paula066/blazorTest/settings/secrets/actions

Kliknij **"New repository secret"** 3 razy i dodaj:

| Name | Value | Gdzie znaleźć |
|------|-------|---------------|
| `VERCEL_TOKEN` | Token z kroku 2 | https://vercel.com/account/tokens |
| `VERCEL_ORG_ID` | Twój Organization ID | Vercel → Settings → General |
| `VERCEL_PROJECT_ID` | Twój Project ID | Vercel → Settings → General |

### 4. Trigger deployment

W terminalu (w folderze projektu):

```bash
git commit --allow-empty -m "Trigger auto deployment"
git push
```

### 5. Sprawdź status

**GitHub Actions:** https://github.com/Paula066/blazorTest/actions
- Zobacz workflow "Build and Deploy to Vercel"
- Powinien być zielony ✅ po ~3-5 min

**Vercel:** https://vercel.com/dashboard
- Zobacz nowy deployment z GitHub Actions

**Twoja aplikacja:** URL znajdziesz w:
- Vercel Dashboard
- Lub w logach GitHub Actions (na końcu)

---

## ✅ GOTOWE!

Od teraz każdy `git push` do `main` automatycznie wdroży nową wersję! 🎉

---

## 📚 Więcej info:

- Szczegóły o sekretach: [GITHUB_SECRETS.md](GITHUB_SECRETS.md)
- Troubleshooting: [FIX_VERCEL.md](FIX_VERCEL.md)
- FAQ: [FAQ.md](FAQ.md)

---

## 💡 Przydatne linki:

- 🔑 Vercel Tokens: https://vercel.com/account/tokens
- ⚙️ GitHub Secrets: https://github.com/Paula066/blazorTest/settings/secrets/actions
- 🚀 GitHub Actions: https://github.com/Paula066/blazorTest/actions
- 📊 Vercel Dashboard: https://vercel.com/dashboard
- 📖 Repository: https://github.com/Paula066/blazorTest

---

**Problemy?** Zobacz [GITHUB_SECRETS.md](GITHUB_SECRETS.md) dla szczegółowych instrukcji!
