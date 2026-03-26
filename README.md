# TopRoxProject — Sistem de Verificare Certificate

Fișiere statice pentru pagina de verificare a certificatelor TopRoxProject SRL.

## Structura Fișierelor

```
toproxproject-verify/
├── certificates.json          ← Baza de date cu certificate
├── verificare/
│   └── index.html             ← Pagina de verificare
├── _redirects                 ← Reguli redirect Cloudflare Pages
├── _headers                   ← CORS headers Cloudflare Pages
└── README.md
```

## Deployment pe Cloudflare Pages (via GitHub)

### Pasul 1 — Creare Repository GitHub
1. Mergi pe [github.com](https://github.com) → **New repository**
2. Denumire: `toproxproject-verify` (sau orice preferi)
3. Vizibilitate: **Public** sau Private (ambele funcționează)
4. Creează repository-ul

### Pasul 2 — Upload Fișiere
Opțiunea simplă (drag & drop):
1. Deschide repository-ul nou creat
2. Click **Add file → Upload files**
3. Drag & drop toate fișierele din acest folder
4. **Important:** păstrează structura de foldere (verificare/ trebuie să rămână subfolder)
5. Commit changes

### Pasul 3 — Conectare Cloudflare Pages
1. Mergi pe [dash.cloudflare.com](https://dash.cloudflare.com)
2. **Pages → Create a project → Connect to Git**
3. Selectează repository-ul GitHub `toproxproject-verify`
4. Setări build:
   - **Framework preset:** None
   - **Build command:** (lasă gol)
   - **Build output directory:** `/` (root)
5. Click **Save and Deploy**

### Pasul 4 — Custom Domain
1. În Cloudflare Pages → Settings → Custom domains
2. Adaugă: `www.toproxproject.com`
3. Sau un subdomeniu: `cert.toproxproject.com`
4. Urmează instrucțiunile DNS (dacă domeniul e deja pe Cloudflare, e automat)

## Adăugare Certificate Noi

Editează `certificates.json` și adaugă un nou obiect în secțiunea `certificates`:

```json
"TRP-GIS1-2025-042": {
  "serie": "TRP-GIS1-2025-042",
  "nume": "Popescu Alexandru",
  "curs": "Bazele GIS",
  "tip": "Curs GIS",
  "durata": "16 ore",
  "perioada": "10–11 Aprilie 2025",
  "data_emiterii": "2025-04-11",
  "formator": "Roxana Giusca, PhD, GISP",
  "status": "valid"
}
```

**Serie-uri recomandate:**
| Curs | Prefix |
|------|--------|
| Bazele GIS | TRP-GIS1-YYYY-NNN |
| GIS Avansat | TRP-GIS2-YYYY-NNN |
| Negociere Antreprenori | TRP-NEG1-YYYY-NNN |
| Negociere PM | TRP-NEG2-YYYY-NNN |
| PM de Elită | TRP-PM1-YYYY-NNN |

## Revocare Certificate

Schimbă `"status": "valid"` în `"status": "revocat"` în `certificates.json`.

## URL-uri de Verificare

Certificatele pot fi verificate prin:
- `https://www.toproxproject.com/verificare/` — căutare manuală
- `https://www.toproxproject.com/verificare/?serie=TRP-GIS1-2025-001` — link direct
- `https://www.toproxproject.com/verificare/TRP-GIS1-2025-001` — URL curat (via _redirects)

Codul QR de pe certificat generează automat al treilea format.
