# PoC: reviewcommentaar op ReSpec → GitHub-issue

Selecteer tekst op een gepubliceerde ReSpec-pagina → klik **💬 Reviewcommentaar** →
GitHub opent een vooraf ingevuld issue form (model, versie, sectie, citaat, deeplink).
Geen backend; reviewers hebben alleen een (gratis) GitHub-account nodig.

## Bestanden

| Bestand | Doel |
|---|---|
| `review.js` | Selectieknop + bouwt de issue-URL. Eén `<script>`-regel in het document. |
| `.github/ISSUE_TEMPLATE/review.yml` | Issue form met de reviewvelden. |
| `.github/workflows/review-labels.yml` | Zet labels `review`, `status: nieuw`, `type: …`, `model: …`, `versie: …`. |
| `demo/index.html` | Testdocument, los van wat Ontologica publiceert. |

## Opzetten

1. **Pages aanzetten**: Settings → Pages → *Deploy from a branch* → `main` / `(root)`.
2. **Ontologica-export**: voeg in de `<head>` toe:
   ```html
   <script src="https://xcalibur1978.github.io/temp/review.js" defer
           data-repo="xcalibur1978/temp"></script>
   ```
   Model en versie worden uit het pad gehaald (`/temp/<model>/<versie>/`).
   Wijkt het pad af, zet dan `data-model` en `data-version` expliciet.
3. **Project-board** (optioneel): maak een Project, zet de workflow *Auto-add to project*
   aan met filter `is:issue label:review`, en kolommen als
   *Nieuw → In behandeling → Besloten → Verwerkt in versie*.

## Testen

Open `https://xcalibur1978.github.io/temp/demo/` met een account dat **geen** lid is van de repo:
tekst selecteren → knop → issue indienen → controleer velden, labels en of de link
in "Directe link naar de passage" naar de juiste tekst springt.

## Bekende beperkingen

- Citaat wordt afgekapt op 500 tekens (URL-lengte).
- Text fragments (`:~:text=`) springen niet in oudere Firefox-versies; dan valt de link terug op de sectie.
- Op touch-apparaten verschijnt de knop na het loslaten van de selectie.
