# 🔧 FIX: Napraw deployment na Vercel

## Problem który masz:
- ❌ 404: NOT_FOUND
- ❌ "Automatic publicPath is not supported in this browser"

## ✅ ROZWIĄZANIE - Krok po kroku:

### Opcja 1: Zmień branch deployment w Vercel (NAJSZYBSZE)

1. **Wejdź na swój projekt w Vercel:**
   - https://vercel.com/dashboard
   - Wybierz projekt `blazorTest`

2. **Settings → Git:**
   - Kliknij "Git"
   - W sekcji "Production Branch" zmień z `main` na: **`vercel-deploy`**
   - Save

3. **Deployments → Redeploy:**
   - Wejdź w zakładkę "Deployments"
   - Wybierz ostatni deployment
   - Kliknij "Redeploy"
   - LUB po prostu kliknij "Deploy" → wybierz branch `vercel-deploy`

4. **Gotowe!** 🎉
   - Aplikacja powinna działać w ~1-2 minuty

---

### Opcja 2: Zmień Output Directory w Vercel

1. **Vercel Dashboard → Settings → General**

2. **Build & Development Settings:**
   - Framework Preset: **Other**
   - Build Command: **ZOSTAW PUSTE** (lub usuń)
   - Output Directory: zmień na: **`output/wwwroot`**
   - Install Command: **ZOSTAW PUSTE**

3. **Save**

4. **Deployments → Redeploy ostatni deployment**

---

### Opcja 3: Nowy projekt z poprawnym branchem

Jeśli powyższe nie działa:

1. **Usuń obecny projekt z Vercel** (opcjonalnie)

2. **Import na nowo:**
   - https://vercel.com/new
   - Import: `Paula066/blazorTest`
   - **WAŻNE:** Wybierz branch: **`vercel-deploy`**
   - Output Directory: `output/wwwroot`
   - Build Command: ZOSTAW PUSTE
   - Deploy!

---

## 🤔 Co się dzieje?

Branch `vercel-deploy` zawiera **już zbudowane pliki** gotowe do deploy:
- Wszystkie pliki .dll (skompilowane)
- WebAssembly runtime
- Statyczne pliki (HTML, CSS, JS)

Branch `main` zawiera tylko **kod źródłowy C#**, który Vercel nie umie zbudować (bo nie ma .NET SDK).

---

## 🔄 W przyszłości - jak aktualizować?

Gdy wprowadzisz zmiany w kodzie:

```bash
# 1. Wróć do main
git checkout main

# 2. Wprowadź zmiany w plikach .razor, .cs
# (edytuj pliki...)

# 3. Commit zmian
git add .
git commit -m "Opis zmian"
git push

# 4. Zbuduj nową wersję
dotnet publish -c Release -o output

# 5. Przejdź do branch vercel-deploy
git checkout vercel-deploy

# 6. Merge zmian z main
git merge main

# 7. Dodaj zbudowane pliki
git add -f output/wwwroot/
git commit -m "Update built files"
git push

# 8. Vercel automatycznie wdroży nową wersję! 🚀
```

---

## ⚡ PRO TIP: Automatyzacja z GitHub Actions

Możesz też użyć GitHub Actions do automatycznego buildowania i pushowania do `vercel-deploy`.

Jeśli chcesz, mogę to skonfigurować!

---

## 📝 Szybkie sprawdzenie

Po wdrożeniu, otwórz w przeglądarce i sprawdź:
- ✅ Strona główna się ładuje
- ✅ Routing działa (`/counter`, `/fetchdata`, `/komponenty`)
- ✅ Brak błędów 404 w console

---

**Pytania?** Daj znać jeśli coś nie działa!
