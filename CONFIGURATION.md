# Konfiguracja środowisk dla Blazor WASM na Vercel

## Environment Variables

Blazor WebAssembly nie obsługuje tradycyjnych environment variables jak aplikacje serwerowe, ponieważ działa w przeglądarce. Zamiast tego możesz użyć:

### 1. appsettings.json

Utwórz pliki konfiguracyjne w folderze `wwwroot`:

```
wwwroot/
  appsettings.json                    # Domyślna konfiguracja
  appsettings.Development.json        # Dla developmentu
  appsettings.Production.json         # Dla produkcji
```

### 2. Przykład appsettings.json

```json
{
  "ApiBaseUrl": "https://api.example.com",
  "AppName": "Elevato",
  "EnableAnalytics": true
}
```

### 3. Użycie w kodzie

```csharp
@inject HttpClient Http
@inject IConfiguration Configuration

@code {
    protected override void OnInitialized()
    {
        var apiUrl = Configuration["ApiBaseUrl"];
        var appName = Configuration["AppName"];
    }
}
```

### 4. Build time variables (Vercel)

W Vercel Dashboard możesz ustawić environment variables, które są dostępne podczas build:

1. Project Settings → Environment Variables
2. Dodaj zmienne, np:
   - `API_URL` = `https://api.production.com`
   - `ENABLE_FEATURES` = `true`

### 5. Dostęp przez MSBuild properties

W pliku `.csproj` możesz użyć build-time variables:

```xml
<PropertyGroup>
  <ApiUrl>$(API_URL)</ApiUrl>
</PropertyGroup>
```

## ⚠️ Ważne uwagi

1. **Wszystkie dane w Blazor WASM są publiczne** - kod i konfiguracja są widoczne w przeglądarce
2. **NIE przechowuj sekretów** w appsettings.json (API keys, hasła, itp.)
3. **Dla sekretów** używaj backend API, które zarządza nimi bezpiecznie
4. Vercel environment variables są dostępne tylko podczas build, nie w runtime

## Bezpieczne wzorce

### ❌ NIE RÓB TAK:
```json
{
  "DatabasePassword": "super-secret-password",
  "ApiKey": "sk_live_123456789"
}
```

### ✅ RÓB TAK:
```json
{
  "ApiEndpoint": "https://your-backend-api.com/api",
  "PublicAnalyticsId": "GA-123456"
}
```

Backend API powinno zarządzać sekretami i autentykacją.
