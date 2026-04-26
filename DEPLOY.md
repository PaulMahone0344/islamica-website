# Deploy

`islamica.tech` wordt geserveerd door een **Cloudflare Worker** (project
`islamica-website`) die gekoppeld is aan deze GitHub-repo. Iedere push
naar `main` triggert een auto-deploy binnen 30–60 seconden.

> ⚠️ **NIET** `wrangler pages deploy --project-name islamica` gebruiken —
> dat is een ander Pages-project zonder custom domain. Deploy gaat
> ALTIJD via git push.

## Standaard deploy (na een wijziging)

1. Wijzigingen maken in deze folder
2. `git status` om te checken wat er gewijzigd is
3. `git add <files>` (of `git add .` als alles bedoeld is)
4. `git commit -m "korte omschrijving"`
5. `git push origin main`
6. Wacht 30–60 sec → check `https://islamica.tech/`

## Cache-issues na deploy

Als de wijziging niet zichtbaar is na 1 minuut:

1. Cloudflare dashboard → zone **islamica.tech** → tab **Caching**
2. Knop **Purge Everything** → bevestigen
3. Refresh met cache-bust: `https://islamica.tech/?cb=1` (of `Cmd+Shift+R`)

## URL-structuur

- `islamica.tech/` → hoofdsite (`index.html`)
- `islamica.tech/admin/` → moskee admin panel (`admin/`)
- `islamica.tech/tarteel/` → Tarteel landing (`tarteel/index.html`)
- `islamica.tech/tarteel/privacy` → privacybeleid
- `islamica.tech/tarteel/terms` → voorwaarden
- `islamica.tech/support` → support pagina

## Repo info

- Lokaal: `/Users/h/Desktop/Projecten/islamica-website/`
- Remote: `PaulMahone0344/islamica-website` (branch `main`)
- Cloudflare account: `brahprive200@gmail.com`
- Worker-project: `islamica-website` (Git-connected)
