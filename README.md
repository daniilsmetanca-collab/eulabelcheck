# EU Label Check

**EU Food Label Regulatory Screening Tool**

A free, open-source, browser-based tool that screens food product labels against 11 EU regulations and directives. It runs 22 automated checks, classifies each finding by how decidable it is, and maps results to enforcement consequence archetypes — so you know not just what might be wrong, but what would happen if an inspector found it.

Everything runs locally in your browser. No backend, no login, no data collection.

---

## What it does

You enter your product's label information (name, ingredients, nutrition, claims, etc.) and the tool returns a structured regulatory screening report containing:

- **22 checks** covering mandatory particulars, allergens, nutrition declaration, claims, origin, GI status, organic certification, novel food status, GMO declarations, lot identification, date marking, font size/legibility, language requirements, and more.
- **Truth-type classification** for each check — one of four categories:
  - **Structural**: decidable from the data you entered (missing fields, threshold violations, format requirements)
  - **Trigger**: applicability logic — whether a rule applies at all given your product's characteristics
  - **Evidence**: the rule is clear but the answer depends on information this tool can't verify (lab results, physical label measurements, national law)
  - **Interpretive**: consumer perception risk under Art. 7 or the Unfair Commercial Practices Directive — no binary answer exists
- **Enforcement consequence archetypes** as the headline output — not a score, but what an enforcement authority would likely do:
  - Health protection risk (allergen/safety gaps — recall/RASFF plausible)
  - Marketability stop risk (missing mandatory info — corrective action)
  - Fraud/authenticity scrutiny risk (origin/GI/organic issues)
  - Misleadingness dispute risk (Art. 7 / UCPD interpretive zone)
  - Claims review required (Reg. 1924/2006 verification needed)
  - Administrative correction likely (minor format/language items)
  - Evidence required (findings needing external verification)
- **Triage score** (0–100) as a secondary signal, not the headline.
- **Nutri-Score estimation** using the 2023 updated algorithm (beverage and solid food categories).
- **14-allergen keyword scanning** against Annex II of Reg. 1169/2011, with cross-referencing between ingredient text and declared allergens.
- **Micronutrient claim verification** for vitamins and minerals against Reference Intake thresholds (Annex XIII, Reg. 1169/2011).
- **PDF and JSON export** of the full report.

---

## Regulatory coverage

| Instrument | Short name | Coverage |
|---|---|---|
| Reg. (EU) 1169/2011 | FIC | Mandatory labelling for all food on the EU market |
| Reg. (EC) 1924/2006 | Claims | Nutrition and health claims conditions |
| Reg. (EU) 2019/787 | Spirits | Spirit drink categories, minimum ABV, GI for spirits |
| Reg. (EU) 1308/2013 | Wine CMO | Wine ingredient/nutrition labelling (since Dec 2023) |
| Dir. 2011/91/EU | Lot | Lot identification and traceability |
| Reg. (EU) 1151/2012 | GI | PDO, PGI, TSG quality schemes |
| Reg. (EU) 2015/2283 | Novel Food | Pre-market authorisation for novel ingredients |
| Reg. (EU) 2018/848 + 2018/775 | Organic / Origin | Organic certification and primary ingredient origin |
| Reg. (EC) 1829/2003 + 1830/2003 | GMO | GMO labelling and traceability |
| Dir. 2005/29/EC | UCPD | Unfair commercial practices (marketing claims) |
| Dir. 2002/46/EC | Supplements | Food supplement specific labelling |

All legal references link to EUR-Lex consolidated texts. Verified as of February 2026.

---

## How it works

### The epistemic model

Most compliance tools treat regulation as binary: pass or fail. This tool treats it as a layered epistemic structure where the boundary between what's decidable and what's not is itself the most valuable output.

The four truth-types map to what a competent regulatory advisor does when reviewing a label:

1. **Structural checks** answer questions the tool can resolve from your inputs alone. If your product has no ingredient list and isn't exempt, that's a BLOCK. No ambiguity.

2. **Trigger checks** determine whether a rule even applies. Does QUID apply? Do alcohol claim prohibitions kick in? Is origin disclosure mandatory for this category? The tool evaluates the trigger condition and tells you whether you're in scope.

3. **Evidence checks** are where the tool reaches its limit honestly. Font size compliance requires measuring the physical label. GI status requires the eAmbrosia database. Organic certification requires documentation. The tool flags these as requiring external verification rather than pretending to resolve them.

4. **Interpretive checks** sit in the zone where no deterministic answer exists. "Handcrafted" on a product made partly by machine — is that misleading under Art. 7? The tool identifies the risk and frames it as a dispute probability, not a verdict.

### Consequence archetypes replace the risk score as headline

A scalar score (72/100) tells you nothing about what to do. Consequence archetypes tell you what an enforcement authority would do:

- A missing allergen declaration is not the same kind of problem as a missing lot code, even if both are "non-compliant."
- The first can trigger a RASFF notification and product recall. The second gets a corrective action notice.
- The tool maps findings to enforcement actions so you can triage by consequence, not by count.

---

## Who this is for

**QA managers and food technologists** — Quick pre-check before sending to your regulatory advisor. Catches structural issues so your advisor's time goes to the interpretive questions that actually need expertise.

**Small and medium food businesses** — Craft producers, startups, or small-batch manufacturers placing products on the EU market for the first time. Structured picture of what's required, what's missing, and where you need professional help.

**Regulatory consultants and food lawyers** — Structured checklist mapping findings to legal basis with article-level traceability. Truth-type classification separates what you can sign off on from what needs investigation. PDF export for client delivery.

**Students and researchers** — The Legal Basis tab maps every check to source articles with EUR-Lex links. The methodology section explains the epistemic model.

---

## What it does not do

This tool provides regulatory pre-screening, not legal advice or compliance certification. It cannot:

- Verify the physical label (font measurements, field of vision, contrast)
- Check additive legality under Reg. 1333/2008 (ingredient scan is for allergens and list structure, not additive permissibility)
- Confirm GI registration or organic certification documentation
- Determine national language requirements or Member State implementing measures
- Evaluate Art. 7 misleadingness with case-law depth
- Replace laboratory analysis for nutritional values or contaminant limits

Evidence-type checks are flagged as requiring external verification. Interpretive checks are framed as risk assessments, not verdicts.

---

## Technical details

- **Single file**: `index.html` — no build step, no framework, no npm
- **Checks**: 22 automated, across 11 regulation groups
- **Algorithms**: Nutri-Score 2023, 14-allergen keyword scanner (200+ keywords), micronutrient RI verification
- **Export**: PDF (print-optimised HTML), JSON (structured data)
- **Privacy**: All processing client-side. Google Fonts loaded on page load (no product data in request). No cookies, analytics, or tracking.
- **Browser**: Any modern browser

## Deployment

```bash
# GitHub Pages
git add index.html
git commit -m "Deploy EU Label Check v2"
git push origin main
```

No server, no database, no environment variables.

---

## Author

**Daniil Smetanca**
MSc Student Food Safety, Wageningen University & Research
[LinkedIn](https://www.linkedin.com/in/daniil-smetanca)

## License

MIT

---

*Regulatory references verified against EUR-Lex consolidated texts, February 2026.*
