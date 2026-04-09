# 🚀 DEPLOY NA VERCEL - KROK PO KROKU

## Masz 2 opcje - wybierz jedną:

---

## ✅ OPCJA 1: Przez Dashboard Vercel (BEZ GitHub Actions)

### To zrób teraz:

1. **Otwórz:** https://vercel.com/new
2. **Zaloguj się** przez GitHub
3. **Import repository:** Paula066/blazorTest
4. **Konfiguracja:**
   - Framework: **Other**
   - Build Command: **`dotnet publish -c Release -o output`**
   - Output Directory: **`output/wwwroot`**
   - Install Command: **ZOSTAW PUSTE**
5. **Kliknij Deploy**

⚠️ **PROBLEM:** Vercel nie ma .NET SDK, więc build może się nie udać.

### Rozwiązanie - build lokalnie:

```bash
# W terminalu (tam gdzie jest projekt):
dotnet publish -c Release -o output
cd output/wwwroot

# Zainstaluj Vercel CLI (tylko raz):
npm install -g vercel

# Deploy:
vercel --prod
```

---

## ⭐ OPCJA 2: GitHub Actions (AUTOMATYCZNE) - ZALECANE

GitHub Actions zbuduje aplikację za Ciebie!

### Kroki:

#### 1. Utwórz projekt na Vercel
- Idź na https://vercel.com/new
- Import: **Paula066/blazorTest**
- Framework: **Other**
- **NIE KLIKAJ DEPLOY JESZCZE!**

#### 2. Zdobądź tokeny Vercel

**Token:**
- https://vercel.com/account/tokens
- "Create Token" → Nazwij "GitHub Actions"
- **Skopiuj token!**

**Project ID i Org ID:**
- Otwórz projekt na Vercel
- Settings → General
- Przewiń w dół, znajdziesz:
  - `Project ID`
  - `Organization ID`

#### 3. Dodaj sekrety w GitHub

- Idź na: https://github.com/Paula066/blazorTest/settings/secrets/actions
- Kliknij "New repository secret" 3 razy i dodaj:

| Name | Value |
|------|-------|
| `VERCEL_TOKEN` | Token z kroku 2 |
| `VERCEL_ORG_ID` | Organization ID |
| `VERCEL_PROJECT_ID` | Project ID |

#### 4. Trigger deployment

```bash
# Zrób dowolną zmianę i push:
git commit --allow-empty -m "Trigger deployment"
git push
```

**GitHub Actions automatycznie:**
- Zbuduje aplikację z .NET
- Wdroży na Vercel
- Gotowe w ~3-5 minut!

#### 5. Sprawdź status

- GitHub: https://github.com/Paula066/blazorTest/actions
- Zobacz czy workflow działa ✅

---

## 🎯 Co wybrać?

| | Opcja 1: Lokalny build | Opcja 2: GitHub Actions |
|---|---|---|
| **Czas setupu** | 2 min | 10 min |
| **Automatyzacja** | ❌ Musisz ręcznie | ✅ Automatyczne |
| **Każdy push** | ❌ Ręczny deploy | ✅ Auto deploy |
| **Wymaga** | Vercel CLI | GitHub Secrets |
| **Zalecane dla** | Szybki test | Produkcja |

---

## ✅ Po deployment

Aplikacja będzie dostępna na:
- **Production:** `https://blazor-test.vercel.app` (lub podobny URL)
- **Dashboard:** https://vercel.com/dashboard

---

## 📝 Helpful URLs

- Twój GitHub: https://github.com/Paula066/blazorTest
- Vercel Dashboard: https://vercel.com/dashboard
- Vercel Tokens: https://vercel.com/account/tokens
- GitHub Secrets: https://github.com/Paula066/blazorTest/settings/secrets/actions

---

**Pytania?** Zobacz `VERCEL_DEPLOY.md` lub `FAQ.md`
