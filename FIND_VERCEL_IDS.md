# 🎯 NAJPROSTSZY SPOSÓB - Pobierz wartości bezpośrednio z Vercel

## Krok 1: Znajdź swoje wartości w Vercel Dashboard

### A. VERCEL_ORG_ID

**SPOSÓB 1 - Z URL projektu:**
1. Wejdź na: https://vercel.com/dashboard
2. Kliknij na **dowolny** swój projekt
3. Pokaż URL w przeglądarce, wygląda tak:
   ```
   https://vercel.com/TUTAJ_JEST_ORG_ID/nazwa-projektu
   ```
   Przykład: `https://vercel.com/paula066/blazortest`
   → Org ID = `paula066`

**SPOSÓB 2 - Z Settings:**
1. Kliknij na swój **avatar** (prawy górny róg)
2. Zobacz swoją nazwę użytkownika
3. **To jest Twój Org ID**

### B. VERCEL_PROJECT_ID

1. Otwórz projekt: https://vercel.com/dashboard
2. Kliknij na **blazorTest** (lub jak nazwałeś projekt)
3. Settings → General
4. Przewiń w dół - znajdziesz:
   ```
   Project ID: prj_xxxxxxxxxxxxxxxxxxxxx
   ```
5. **Skopiuj to całe ID** (razem z `prj_`)

### C. VERCEL_TOKEN

Już masz - ten z https://vercel.com/account/tokens

---

## Krok 2: Sprawdź czy projekt istnieje na Vercel

**WAŻNE:** Czy utworzyłeś już projekt na Vercel?

Jeśli **NIE**, zrób to teraz:
1. https://vercel.com/new
2. Import z GitHub: **Paula066/blazorTest**
3. Framework: **Other**
4. Build Command: **zostaw puste**
5. Output Directory: `output/wwwroot`
6. **Deploy**

Po utworzeniu projektu - pobierz Project ID z Settings!

---

## Krok 3: Zaktualizuj sekrety w GitHub

https://github.com/Paula066/blazorTest/settings/secrets/actions

Sprawdź czy wszystkie 3 są dodane:
- ✅ VERCEL_TOKEN
- ✅ VERCEL_ORG_ID (bez `prj_`, tylko username lub `team_xxx`)
- ✅ VERCEL_PROJECT_ID (z `prj_` na początku)

---

## 📝 Przykład poprawnych wartości:

```bash
VERCEL_TOKEN=abc123xyz...    # długi token
VERCEL_ORG_ID=paula066       # twój username (lowercase)
VERCEL_PROJECT_ID=prj_abc123xyz...   # zaczyna się od prj_
```

---

## ⚡ ALTERNATYWA - Deploy bez GitHub Actions

Jeśli to nie działa, możemy wdrożyć inaczej:

```bash
# Zbuduj lokalnie
dotnet publish -c Release -o output

# Deploy z Vercel CLI
cd output/wwwroot
vercel --prod
```

---

**Powiedz mi:**
1. Czy masz już projekt utworzony na Vercel Dashboard?
2. Jaki jest URL Twojego projektu (lub profilu) na Vercel?

Na podstawie tego dokładnie Ci powiem jakie wartości użyć! 🚀
