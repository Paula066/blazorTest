# Elevato Blazor App

Aplikacja Blazor WebAssembly gotowa do wdrożenia na Vercel.

> **🚀 AUTOMATYCZNY DEPLOYMENT:** Push do `main` automatycznie wdraża na Vercel!  
> **⚙️ Setup:** Zobacz [GITHUB_SECRETS.md](GITHUB_SECRETS.md) - konfiguracja zajmie 5 minut

## 🚀 Cechy

- ✅ Blazor WebAssembly (.NET 7)
- ✅ Routing client-side
- ✅ Gotowa do wdrożenia na Vercel
- ✅ Progressive Web App (PWA)

## 📋 Wymagania

- [.NET 7 SDK](https://dotnet.microsoft.com/download/dotnet/7.0) lub nowszy
- [Node.js](https://nodejs.org/) (dla Vercel CLI - opcjonalnie)
- Konto [Vercel](https://vercel.com/)

## 🛠️ Lokalne uruchomienie

```bash
# Uruchom aplikację lokalnie
dotnet run

# Lub w trybie watch (auto-reload)
dotnet watch
```

Aplikacja będzie dostępna pod adresem: `https://localhost:5001` lub `http://localhost:5000`

## 📦 Build lokalny

```bash
# Zbuduj aplikację w trybie Release
dotnet publish -c Release -o output

# Pliki statyczne będą w folderze: output/wwwroot
```

## 🌐 Wdrożenie na Vercel

### Opcja 1: Przez Dashboard Vercel (najprostsze)

1. Zaloguj się na [vercel.com](https://vercel.com)
2. Kliknij "Add New Project"
3. Zaimportuj ten repository z GitHub/GitLab/Bitbucket
4. Vercel automatycznie wykryje konfigurację z `vercel.json`
5. Kliknij "Deploy"

### Opcja 2: Przez Vercel CLI

```bash
# Zainstaluj Vercel CLI
npm i -g vercel

# Zaloguj się
vercel login

# Wdróż aplikację
vercel

# Lub od razu do produkcji
vercel --prod
```

### Opcja 3: Manualne wdrożenie

```bash
# 1. Zbuduj aplikację
dotnet publish -c Release -o output

# 2. Wdróż folder output/wwwroot
cd output/wwwroot
vercel --prod
```

## 📂 Struktura projektu

```
elevatoBlazor/
├── Pages/              # Strony aplikacji
│   ├── Index.razor     # Strona główna
│   ├── Counter.razor   # Przykładowa strona z licznikiem
│   └── FetchData.razor # Przykładowa strona z danymi
├── Shared/             # Współdzielone komponenty
│   ├── MainLayout.razor
│   ├── NavMenu.razor
│   └── SurveyPrompt.razor
├── wwwroot/            # Pliki statyczne
│   ├── css/
│   ├── sample-data/
│   └── index.html      # Główny HTML
├── App.razor           # Główny komponent aplikacji
├── Program.cs          # Punkt wejścia aplikacji
├── vercel.json         # Konfiguracja Vercel
└── ElevatoBlazorApp.csproj
```

## 🎨 Dostosowywanie

### Dodawanie nowych stron

Utwórz nowy plik `.razor` w folderze `Pages/`:

```razor
@page "/moja-strona"

<h3>Moja nowa strona</h3>

<p>Witaj w Blazor!</p>

@code {
    // Twój kod C#
}
```

### Stylowanie

- Globalne style: `wwwroot/css/app.css`
- Style komponentu: Dodaj sekcję `<style>` w pliku `.razor`

### API Calls

Użyj `HttpClient` do wywoływania API:

```csharp
@inject HttpClient Http

@code {
    private async Task GetData()
    {
        var data = await Http.GetFromJsonAsync<MyData>("https://api.example.com/data");
    }
}
```

## 🔧 Konfiguracja Vercel

Plik `vercel.json` zawiera:
- **buildCommand**: Komenda do zbudowania aplikacji
- **outputDirectory**: Folder z plikami statycznymi
- **routes**: Routing dla SPA (wszystkie ścieżki przekierowują do index.html)

## 📝 Uwagi

- Blazor WASM wymaga pobierania ~2-3 MB przy pierwszym ładowaniu
- Wszystkie pliki `.dll` są pobierane przez przeglądarkę
- Aplikacja działa całkowicie client-side (w przeglądarce)
- Brak automatycznego pre-renderingu (można dodać Blazor WASM z pre-renderingiem)

## 🐛 Troubleshooting

### Błąd: "Failed to find a valid digest in the 'integrity' attribute"

Wyczyść cache przeglądarki lub przebuduj aplikację:
```bash
dotnet clean
dotnet publish -c Release -o output
```

### Aplikacja nie działa na Vercel

Upewnij się, że:
1. `vercel.json` jest w głównym folderze
2. Build command jest poprawny
3. Output directory wskazuje na `output/wwwroot`

## 📚 Dalsze kroki

- [ ] Dodaj więcej stron i komponentów
- [ ] Zintegruj z API
- [ ] Dodaj autentykację (np. Auth0, Azure AD B2C)
- [ ] Włącz PWA dla offline support
- [ ] Dodaj testy jednostkowe

## 🔗 Przydatne linki

- [Dokumentacja Blazor](https://docs.microsoft.com/aspnet/core/blazor/)
- [Dokumentacja Vercel](https://vercel.com/docs)
- [Blazor University](https://blazor-university.com/)

## 📄 Licencja

MIT

---

Wykonane z ❤️ używając Blazor WebAssembly
