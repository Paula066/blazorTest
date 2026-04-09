# 🔐 Konfiguracja GitHub Secrets dla automatycznego deployment

## Teraz branch `main` będzie automatycznie budować i wdrażać! 🚀

### Krok 1: Zdobądź tokeny z Vercel

#### A. VERCEL_TOKEN

1. Wejdź na: https://vercel.com/account/tokens
2. Kliknij **"Create Token"**
3. Nazwij go: `GitHub Actions Token`
4. Scope: Full Account
5. **SKOPIUJ TOKEN** (widoczny tylko raz!)

#### B. VERCEL_ORG_ID i VERCEL_PROJECT_ID

**Metoda 1: Z Dashboard**
1. Otwórz swój projekt na Vercel
2. Settings → General
3. Przewiń na sam dół do sekcji "Project Settings"
4. Znajdziesz tam:
   - **Project ID** (np. `prj_xxxxxxxxxxxxx`)
   - **Team ID** / **Organization ID** (np. `team_xxxxxxxxxxxxx` lub twój username)

**Metoda 2: Z .vercel (jeśli deployowałeś lokalnie)**
```bash
# Jeśli masz folder .vercel lokalnie:
cat .vercel/project.json
```

---

### Krok 2: Dodaj sekrety w GitHub

1. Wejdź na: https://github.com/Paula066/blazorTest/settings/secrets/actions

2. Kliknij **"New repository secret"** trzy razy i dodaj:

   **Secret 1:**
   - Name: `VERCEL_TOKEN`
   - Secret: [wklej token z kroku 1A]

   **Secret 2:**
   - Name: `VERCEL_ORG_ID`
   - Secret: [wklej Organization ID z kroku 1B]

   **Secret 3:**
   - Name: `VERCEL_PROJECT_ID`
   - Secret: [wklej Project ID z kroku 1B]

3. Kliknij "Add secret" dla każdego

---

### Krok 3: Trigger deployment

Teraz każdy push do `main` automatycznie wdroży aplikację!

```bash
# Opcja 1: Zrób jakąś zmianę
# (edytuj dowolny plik)
git add .
git commit -m "Test auto deployment"
git push

# Opcja 2: Empty commit (trigger bez zmian)
git commit --allow-empty -m "Trigger deployment"
git push
```

---

### Krok 4: Sprawdź status

1. **GitHub Actions:**
   - https://github.com/Paula066/blazorTest/actions
   - Zobacz workflow "Build and Deploy to Vercel"
   - Powinien być zielony ✅ po ~3-5 minutach

2. **Vercel Dashboard:**
   - https://vercel.com/dashboard
   - Zobacz nowy deployment

3. **Twoja aplikacja:**
   - URL dostaniesz w logach GitHub Actions
   - Lub sprawdź w Vercel Dashboard

---

## ✅ Gotowe!

Od teraz:
- Push do `main` → automatyczny build → automatyczny deploy na Vercel
- Pull requesty → preview deployments
- Wszystko w pełni zautomatyzowane! 🎉

---

## 🔍 Troubleshooting

### "Error: Vercel token is required"
- Sprawdź czy dodałeś `VERCEL_TOKEN` w GitHub Secrets
- Token musi być z https://vercel.com/account/tokens

### "Error: Project not found"
- Sprawdź `VERCEL_PROJECT_ID` i `VERCEL_ORG_ID`
- Upewnij się że projekt istnieje na Vercel

### "Build failed"
- Sprawdź logi w GitHub Actions
- Aplikacja powinna się budować lokalnie (`dotnet build`)

---

## 📝 Przykładowe wartości (dla referencji)

```
VERCEL_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
VERCEL_ORG_ID=team_xxxxxxxxxxxxxxxx (lub twój username)
VERCEL_PROJECT_ID=prj_xxxxxxxxxxxxxxxx
```

---

**Potrzebujesz pomocy?** Napisz jeśli coś nie działa!
