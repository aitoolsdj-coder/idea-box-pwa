# 💡 Idea Box PWA

Zmodernizowana wersja kolektora pomysłów na automatyzacje. Działa jako aplikacja progresywna (PWA) z synchronizacją w chmurze (Supabase).

## 🚀 Szybki Start

1.  Otwórz `index.html` i wprowadź swoje `SUPABASE_URL` oraz `SUPABASE_ANON_KEY`.
2.  Zdeployuj folder na **Netlify**.
3.  Otwórz stronę na telefonie i wybierz **"Dodaj do ekranu głównego"**.

## 🛠 Konfiguracja Supabase

Stwórz nową bazę i uruchom następujący SQL w edytorze zapytań:

```sql
create table public.ideas (
  id uuid default gen_random_uuid() primary key,
  title text not null,
  area text not null,
  author text not null,
  description text,
  status text default 'NEW',
  created_at timestamp with time zone default now()
);

-- Włącz dostęp publiczny (jeśli nie używasz Auth)
alter table public.ideas enable row level security;
create policy "Allow public read" on public.ideas for select using (true);
create policy "Allow public insert" on public.ideas for insert with check (true);
```

## 🌐 Deploy na Netlify (Zmienne Środowiskowe)

Aby nie trzymać kluczy w kodzie po deployu:
1. W kodzie JS zmień stałe na:
   ```javascript
   const SUPABASE_URL = window.location.hostname === 'localhost' ? 'TWOJ_LOCAL_URL' : ''; 
   // Docelowo najlepiej użyć narzędzia typu Vite/Webpack, 
   // ale dla prostego HTML możesz użyć pola w panelu Netlify (Snippet Injection).
   ```
2. **UWAGA**: W tym prostym projekcie (bez build-stepu) klucze są trzymane w pliku `index.html`. Dla pełnego bezpieczeństwa zaleca się użycie frameworka (np. Vite) i zmiennych `.env`.

## 📱 Funkcje PWA
- **Tryb pełnoekranowy** na iOS i Android.
- **Ikona aplikacji** na pulpicie.
- **Mobile-first UI** dopasowany do ekranów dotykowych.
