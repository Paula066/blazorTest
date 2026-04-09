# FAQ - Często zadawane pytania

## Ogólne

### Czy Blazor WASM działa na Vercel?
✅ **TAK!** Blazor WebAssembly działa na Vercel jako statyczne pliki. Blazor Server NIE działa na Vercel.

### Ile kosztuje hosting na Vercel?
- **Hobby (darmowy)**: Idealny do projektów osobistych i testowych
- **Pro**: ~$20/miesiąc - dla profesjonalnych projektów
- **Enterprise**: Custom pricing

### Jak duża jest aplikacja Blazor WASM?
Typowa aplikacja: **~2-3 MB** (pobierane przy pierwszym załadowaniu)
- .NET runtime: ~1.5 MB
- Twój kod: ~0.5-1 MB
- Zależności: reszta

## Performance

### Czy mogę poprawić czas ładowania?
Tak! Kilka opcji:

1. **Lazy loading** - ładuj komponenty na żądanie
```xml
<Project Sdk="Microsoft.NET.Sdk.BlazorWebAssembly">
  <PropertyGroup>
    <BlazorWebAssemblyLoadAllGlobalizationData>false</BlazorWebAssemblyLoadAllGlobalizationData>
  </PropertyGroup>
</Project>
```

2. **Compression** - Vercel automatycznie kompresuje pliki (gzip/brotli)

3. **AOT Compilation** - kompilacja Ahead-of-Time (zwiększa performance)
```xml
<PropertyGroup>
  <RunAOTCompilation>true</RunAOTCompilation>
</PropertyGroup>
```

### Czy mogę użyć PWA?
✅ **TAK!** Szablon Blazor WASM już zawiera podstawową konfigurację PWA:
- `manifest.json` - w `wwwroot/`
- Service Worker - opcjonalny

## Deployment

### Jak często mogę wdrażać?
Bez limitu! Każdy push do Git automatycznie wdraża nową wersję.

### Czy mogę mieć różne wersje (staging/production)?
✅ **TAK!** 
- `main` branch → produkcja
- Inne branche → preview deployments

### Jak podłączyć własną domenę?
1. Vercel Dashboard → Settings → Domains
2. Dodaj swoją domenę
3. Skonfiguruj DNS (Vercel pokaże instrukcje)

## Rozwój

### Jak dodać autentykację?
Użyj zewnętrznego providera:
- Auth0
- Azure AD B2C
- Firebase Auth
- Własny API endpoint

Przykład:
```csharp
@inject AuthenticationStateProvider AuthenticationStateProvider

@code {
    private async Task<AuthenticationState> GetAuthenticationStateAsync()
    {
        var state = await AuthenticationStateProvider.GetAuthenticationStateAsync();
        var user = state.User;
    }
}
```

### Jak połączyć się z bazą danych?
Blazor WASM nie może bezpośrednio łączyć się z bazą danych (działa w przeglądarce).

✅ **Rozwiązanie**: Stwórz backend API
- ASP.NET Core Web API (hostuj na Azure/AWS)
- Node.js API (hostuj na Vercel Serverless Functions)
- Firebase, Supabase (Backend-as-a-Service)

### Czy mogę używać Entity Framework?
NIE bezpośrednio. EF działa tylko po stronie serwera. Musisz stworzyć API endpoint.

### Jak testować lokalnie?
```bash
# Development server z hot reload
dotnet watch

# Lub standardowy run
dotnet run
```

## Problemy

### "Failed to find a valid digest"
**Rozwiązanie:**
```bash
dotnet clean
rm -rf bin obj
dotnet restore
dotnet publish -c Release -o output
```

### Aplikacja nie ładuje się na Vercel
**Sprawdź:**
1. ✅ `vercel.json` jest w głównym folderze?
2. ✅ Build command jest poprawny?
3. ✅ Output directory to `output/wwwroot`?
4. ✅ Logi w Vercel Dashboard pokazują błędy?

### 404 na podstronach po odświeżeniu
To normalne dla SPA. `vercel.json` powinien zawierać routing:
```json
{
  "routes": [
    { "handle": "filesystem" },
    { "src": "/.*", "dest": "/index.html" }
  ]
}
```

### Długie pierwsze ładowanie
To normalne dla Blazor WASM. Opcje:
1. Dodaj ładny loading screen w `index.html`
2. Użyj AOT compilation
3. Włącz lazy loading dla rzadko używanych komponentów

## Bezpieczeństwo

### Czy mogę przechowywać API keys w kodzie?
❌ **NIE!** Wszystko w Blazor WASM jest widoczne w przeglądarce.

✅ **Rozwiązanie**: Użyj backend API do zarządzania sekretami.

### Jak zabezpieczyć API calls?
1. **CORS** - skonfiguruj na serwerze API
2. **Authentication** - użyj JWT tokens
3. **HTTPS** - zawsze!

## Skalowanie

### Czy Vercel automatycznie skaluje?
✅ **TAK!** Vercel używa CDN Edge Network - twoja aplikacja jest dystrybuowana globalnie.

### Ile użytkowników może obsłużyć?
Jako statyczne pliki - praktycznie **nieograniczona liczba** (dzięki CDN).

### Jak monitorować performance?
1. Vercel Analytics (wbudowane)
2. Google Analytics
3. Application Insights (Azure)

## Koszty

### Jaki jest koszt bandwidth na Vercel?
- **Hobby (Free)**: 100 GB/miesiąc
- **Pro**: 1 TB/miesiąc
- **Enterprise**: Custom

### Co się stanie jak przekroczę limit?
Vercel powiadomi Cię emailem. Możesz upgrade'ować plan.

## Inne

### Czy mogę użyć innych platform niż Vercel?
✅ **TAK!** Blazor WASM działa wszędzie gdzie można hostować statyczne pliki:
- **Netlify** - podobny do Vercel
- **GitHub Pages** - darmowy
- **Azure Static Web Apps** - integracja z Azure
- **Firebase Hosting** - Google
- **AWS S3 + CloudFront** - Amazon

### Jak przełączyć się na inną platformę?
Build lokalnie i wdróż pliki z `output/wwwroot/`:
```bash
dotnet publish -c Release -o output
# Następnie wdróż zawartość output/wwwroot/ gdziekolwiek
```

### Czy mogę używać Blazor Hybrid zamiast WASM?
Blazor Hybrid jest dla **desktop/mobile apps** (MAUI, Electron), nie dla web hostingu.

---

**Nie znalazłeś odpowiedzi?**
- [Dokumentacja Blazor](https://docs.microsoft.com/aspnet/core/blazor/)
- [Vercel Docs](https://vercel.com/docs)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/blazor)
