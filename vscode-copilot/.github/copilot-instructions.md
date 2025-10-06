# GitHub Copilot - Project Instructions

> **Auto-loaded:** Diese Instructions werden automatisch bei jedem Copilot Chat oder Agent Request geladen.

## Project Overview

Dieses Projekt implementiert einen **strukturierten Requirements Engineering Workflow** mit GitHub Copilot. Es nutzt Custom Chat Modes, spezifische Instructions und Templates, um hochqualitative Requirements mit vollständiger Testbarkeit (Gherkin-Szenarien) und bidirektionaler Hierarchie zu erstellen.

**Hauptziel:** Transformiere vage Geschäftsideen in präzise, GitHub-native Requirements (Epic → Feature → Issue) die von Architecture und Development Teams direkt genutzt werden können.

---

## ⚠️ Requirements Engineering Rules (ALWAYS ACTIVE)

> **Wichtig:** Wenn du als Requirements Engineer arbeitest (Chatmode `@requirements-engineer` aktiv ODER in `requirements/` Dateien arbeitest), wende **IMMER** die vollständigen Regeln aus `.github/instructions/requirements-engineer.instructions.md` an.

---

## 🏗️ Architecture Engineering Rules (ALWAYS ACTIVE)

> **Wichtig:** Wenn du als Architect arbeitest (Chatmode `@architect` aktiv ODER in `architecture/` Dateien arbeitest), wende **IMMER** die vollständigen Regeln aus `.github/instructions/architect.instructions.md` an.

### Quick Reference - Architecture Standards

**Diese Standards gelten für ALLE Architecture-Operationen:**

#### ✅ ADR (Architecture Decision Record)

**Dateiname-Pattern:**
```
architecture/decisions/ADR-XXX-descriptive-slug.md

Beispiele:
✅ ADR-001-deployment-architecture.md
✅ ADR-015-database-selection.md
✅ ADR-023-caching-strategy.md

❌ adr-1.md                      (Nummer nicht 3-stellig)
❌ ADR-001-Database_Selection.md (Underscores statt Dashes)
```

**Required Sections:**
- ✅ **Status:** Proposed | Accepted | Deprecated | Superseded
- ✅ **Date:** YYYY-MM-DD
- ✅ **Decision Makers:** Names/Roles
- ✅ **Context:** Problem statement (klar und präzise)
- ✅ **Decision Drivers:** List of factors
- ✅ **Considered Options:** **MIN. 3 Options** mit Analysis
- ✅ **Decision:** Chosen option (eindeutig)
- ✅ **Rationale:** Why this option (detailliert)
- ✅ **Consequences:** Positive + Negative (beide erforderlich!)
- ✅ **Research Links:** MIN. 2 valid URLs (context7 + web_search)

**Qualitätsstandards:**
- ✅ **context7 MCP Research FIRST** (offizielle Dokumentation)
- ✅ **web_search Research SECOND** (Community Insights, Benchmarks)
- ✅ **Decision Matrix** für Optionen-Vergleich
- ❌ **KEINE Platzhalter:** `[X]`, `TODO`, `TBD`, `[to be decided]`
- ❌ **KEINE vagen Formulierungen:** "might be good", "probably works"

#### ✅ arc42 Documentation

**Datei:** `architecture/arc42-architecture.md`

**Required Sections (12/12):**
1. ✅ Introduction and Goals
2. ✅ Constraints
3. ✅ Context and Scope
4. ✅ Solution Strategy
5. ✅ Building Block View
6. ✅ Runtime View
7. ✅ Deployment View
8. ✅ Cross-Cutting Concepts
9. ✅ Architecture Decisions
10. ✅ Quality Requirements
11. ✅ Risks and Technical Debt
12. ✅ Glossary

**Minimum Requirements:**
- ✅ **MIN. 5 Mermaid Diagrams** (Context, Container, Component, Sequence, Deployment)
- ✅ **MIN. 10,000 words** (comprehensive documentation)
- ✅ **Links to ALL ADRs** (bidirektional)
- ✅ **No placeholders** in final version
- ✅ **Each section >100 words**

#### ✅ Task Decomposition

**Dateiname-Pattern:**
```
requirements/tasks/TASK-XXX-descriptive-slug.md

Beispiele:
✅ TASK-001-setup-database-schema.md
✅ TASK-042-implement-user-authentication.md

❌ task-1.md                     (Nummer nicht 3-stellig)
❌ TASK-001-Setup_Database.md   (Underscores statt Dashes)
```

**Atomic Task Requirements:**
- ✅ **MAX. 4 hours** estimation (sonst Task splitten!)
- ✅ **Epic/Feature/Issue References** im Header
- ✅ **Specific File Paths** (welche Dateien erstellt/geändert werden)
- ✅ **Complete Code Examples** (KEIN Pseudo-Code!)
- ✅ **Test Plan** mit Unit + Integration Tests
- ✅ **MIN. 5 Acceptance Criteria** (messbar)
- ✅ **MIN. 5 Definition of Done Items** (checklist)
- ❌ **KEINE Platzhalter:** `[implement logic here]`, `TODO`, `...`

#### ✅ Mermaid Diagrams

**Dateiname-Pattern:**
```
architecture/diagrams/[type]-[name].mmd

Types:
- context-*      (C4 Level 1)
- container-*    (C4 Level 2)
- component-*    (C4 Level 3)
- sequence-*     (Sequence Diagrams)
- deployment-*   (Deployment Views)
```

**Quality Standards:**
- ✅ **Valid Mermaid Syntax** (testbar via Mermaid Live Editor)
- ✅ **Descriptive Labels** (keine kryptischen Abkürzungen)
- ✅ **MIN. 5 Nodes/Participants** pro Diagram
- ✅ **Readable** (sinnvolle Gruppierung, Layout)
- ❌ **KEINE Platzhalter:** `[?]`, `TODO`, `TBD`

#### ✅ Environment Setup

**Datei:** `architecture/ENVIRONMENT-SETUP.sh`

**Required Elements:**
- ✅ **Shebang:** `#!/bin/bash`
- ✅ **Error Handling:** `set -e` (exit on error)
- ✅ **Phase Headers:** Clear sections (# Phase 1: ...)
- ✅ **Progress Messages:** `echo "✅ [message]"`
- ✅ **Verification Section:** Test all created resources
- ✅ **Non-Interactive:** No user prompts (fully automated)
- ✅ **Executable:** `chmod +x` gesetzt

---

### 🔍 Research Requirements (Architecture)

**CRITICAL: ALWAYS Research in This Order:**

1. **context7 MCP FIRST** (Official Documentation)
   ```
   @context7 Latest [Technology] version and features
   @context7 [Technology] best practices
   @context7 [Technology] compatibility with [OtherTech]
   ```

2. **web_search SECOND** (Community Insights)
   ```
   web_search: "[Technology] production guide 2025"
   web_search: "[Technology] benchmark comparison"
   web_search: "[Technology] real-world experiences"
   ```

3. **Decision Matrix** (Combine Results)
   ```
   | Criterion | Option A | Option B | Option C |
   |-----------|----------|----------|----------|
   | Performance | 9/10 | 7/10 | 8/10 |
   | Complexity | 6/10 | 8/10 | 7/10 |
   | Cost | 7/10 | 9/10 | 6/10 |
   ```

**Validation:**
- ❌ **ADR ohne context7 Research** → FEHLER
- ❌ **ADR ohne web_search Research** → FEHLER
- ❌ **ADR ohne Decision Matrix** → WARNUNG

---

### 🎯 Quality Gate 2 (QG2) Validation Checklist

**Bevor du Architecture Phase abschließt, prüfe:**

1. **arc42 Documentation:**
   - [ ] Alle 12 Sections vollständig
   - [ ] MIN. 5 Mermaid Diagrams
   - [ ] MIN. 10,000 words
   - [ ] Keine Platzhalter

2. **Architecture Decisions:**
   - [ ] MIN. 10 ADRs erstellt
   - [ ] Alle ADRs haben 3+ Options
   - [ ] Alle ADRs haben context7 + web_search Research
   - [ ] Alle ADRs haben Decision Matrix
   - [ ] Keine Platzhalter

3. **Task Decomposition:**
   - [ ] MIN. 20 Tasks erstellt
   - [ ] Alle Tasks <4h (atomic)
   - [ ] Alle Tasks haben Complete Code Examples
   - [ ] Alle Tasks haben Test Plans
   - [ ] Alle Tasks haben Specific File Paths

4. **Environment Setup:**
   - [ ] Setup Script existiert und ist executable
   - [ ] Setup Documentation vollständig
   - [ ] Alle Dependencies spezifiziert

5. **BACKLOG Integration:**
   - [ ] BACKLOG.md updated mit Architecture Summary
   - [ ] Alle Tasks integriert
   - [ ] Implementation Plan vorhanden

6. **Handover:**
   - [ ] HANDOVER-TO-IMPLEMENTATION.md erstellt
   - [ ] Alle QG2 Criteria erfüllt
   - [ ] Keine offenen Fragen

---

### 📚 Detaillierte Architecture-Regeln

**Für vollständige Architecture Validierungsregeln siehe:**
`.github/instructions/architect.instructions.md`

Diese Datei wird automatisch geladen wenn du in `architecture/**/*` Dateien arbeitest und enthält:
- Vollständige ADR-Qualitätsstandards
- arc42 Section Requirements
- Task Decomposition Rules
- Mermaid Diagram Standards
- context7 + web_search Integration Guidelines
- QG2 Quality Gate Kriterien
- Automatische Validation Feedback Messages
- Extended Thinking Triggers
- Error Handling & Recovery Strategies

### Quick Reference - Quality Standards

**Diese Standards gelten für ALLE Requirements-Operationen:**

#### ✅ Dateinamen-Konvention
```
Pattern: TYPE-XXX-descriptive-slug.md

Beispiele:
✅ EPIC-001-customer-portal.md
✅ FEATURE-023-user-authentication.md  
✅ ISSUE-142-oauth-google-integration.md

❌ epic-1.md                     (Nummer nicht 3-stellig)
❌ ISSUE-1-login.md              (Nummer nicht 3-stellig)
❌ ISSUE-001-User_Login.md       (Underscores statt Dashes)
```

#### ✅ Gherkin Requirements (für Issues)
```gherkin
Feature: [Feature Name] (FEATURE-XXX)

Scenario: [Descriptive name - NO placeholders]
  Given [konkrete Precondition mit spezifischen Werten]
  And [additional precondition]
  When [konkrete User Action]
  And [additional action]
  Then [erwartetes Outcome mit messbaren Werten]
  And [additional expectation]
```

**Qualitätsstandards:**
- ✅ **Minimum 2 vollständige Scenarios** pro Issue
- ✅ Jedes Scenario hat **Given/When/Then**
- ✅ **Spezifische Werte** in Anführungszeichen: `"user@example.com"`, `"redirected to /dashboard"`
- ✅ **Messbare Outcomes**: `"page loads in less than 2 seconds"`
- ❌ **KEINE Platzhalter**: `[X]`, `TODO`, `TBD`, `...`, `[user does something]`
- ❌ **KEINE vagen Begriffe**: "user does something", "system responds"

#### ✅ Hierarchie (bidirektional)

**Issue → Feature + Epic:**
```markdown
> **Epic:** [EPIC-XXX](EPIC-XXX-name.md)
> **Feature:** [FEATURE-XXX](FEATURE-XXX-name.md)
```

**Feature → Epic + Issues:**
```markdown
> **Epic:** [EPIC-XXX](EPIC-XXX-name.md)

## Related Issues
- [ISSUE-001](ISSUE-001-name.md) - Description (X SP)
- [ISSUE-002](ISSUE-002-name.md) - Description (X SP)
```

**Epic → Features:**
```markdown
## Related Features
| Feature | Story Points | Status | Priority |
|---------|--------------|--------|----------|
| [FEATURE-001](FEATURE-001-name.md) | XX | Status | Priority |
```

#### ✅ Business Value Quantifizierung

**Epic:**
- ✅ ROI dokumentiert (Investment vs. Expected Return)
- ✅ Success Metrics mit **Baseline → Target** (z.B. "0 → 200+ Daily Active Users")
- ✅ Timeline mit Milestones

**Feature:**
- ✅ User Impact messbar (z.B. "50%+ reduction in setup time")
- ✅ Metriken quantifiziert (€, %, Zeit, User-Zahlen)
- ✅ Feature-spezifische Success Metrics

**Issue:**
- ✅ Business Context erklärt **Contribution to Feature**
- ✅ User Story im Format: "Als [Role] möchte ich [Action] damit [Benefit]"

#### ✅ Story Points Konsistenz

**Aggregation Rules:**
```
Feature SP = Σ(alle Issue SP in diesem Feature)
Epic Total SP = Σ(alle Feature SP in diesem Epic)
```

**Bei Änderungen:**
- Issue SP geändert → Feature SP muss aktualisiert werden
- Feature SP geändert → Epic Total SP muss aktualisiert werden

#### ✅ Required Sections (je nach Type)

**EPIC muss haben:**
- [ ] Business Goal & Vision Alignment
- [ ] Business Value & ROI
- [ ] Success Metrics (Baseline → Target)
- [ ] Target Audience & User Personas
- [ ] Related Features (Table mit min. 3 Features)
- [ ] Timeline & Milestones
- [ ] Dependencies & Integration Points
- [ ] Risks & Mitigation Strategies
- [ ] Acceptance Criteria

**FEATURE muss haben:**
- [ ] Epic Referenz (im Header)
- [ ] Business Value (quantifiziert)
- [ ] User Story
- [ ] Success Metrics
- [ ] Related Issues (Table mit min. 3 Issues)
- [ ] Story Points (= Summe aller Issues)
- [ ] Dependencies
- [ ] Acceptance Criteria

**ISSUE muss haben:**
- [ ] Epic UND Feature Referenz (im Header)
- [ ] Business Context (Contribution to Feature)
- [ ] User Story
- [ ] **Acceptance Criteria mit min. 2 Gherkin-Szenarien**
- [ ] Technical Requirements
- [ ] Definition of Done
- [ ] Story Points (Fibonacci: 1, 2, 3, 5, 8, 13, 21)

---

### 🔍 Validation Checklist (vor Commit)

**Bevor du Requirements commitest, prüfe:**

1. **Dateiname korrekt?**
   - [ ] Pattern: `TYPE-XXX-descriptive-slug.md`
   - [ ] Nummer ist 3-stellig (001-999)
   - [ ] Slug ist lowercase mit dashes

2. **Hierarchie vollständig?**
   - [ ] Alle Parent-Links gesetzt (Issue → Feature + Epic)
   - [ ] Alle Child-Links gesetzt (Feature → Issues, Epic → Features)
   - [ ] Links funktionieren (relative Pfade)

3. **Gherkin-Qualität (Issues)?**
   - [ ] Min. 2 vollständige Scenarios
   - [ ] Jedes Scenario hat Given/When/Then
   - [ ] KEINE Platzhalter in Scenarios
   - [ ] Spezifische Werte verwendet

4. **Business Value quantifiziert?**
   - [ ] Epic: ROI dokumentiert
   - [ ] Feature: Metriken messbar
   - [ ] Issue: Contribution to Feature klar

5. **Story Points konsistent?**
   - [ ] Feature SP = Summe aller Issues
   - [ ] Epic Total SP = Summe aller Features

6. **Keine Platzhalter?**
   - [ ] Keine `[X]`, `TODO`, `TBD`, `...`
   - [ ] Keine `[to be defined]`, `[user does X]`

---

### 📚 Detaillierte Validierungsregeln

**Für vollständige Validierungsregeln siehe:**
`.github/instructions/requirements-engineer.instructions.md`

Diese Datei wird automatisch geladen wenn du in `requirements/**/*.md` Dateien arbeitest und enthält:
- Vollständige Gherkin-Qualitätsstandards
- Detaillierte Hierarchie-Checks
- Business-Value-Validierung
- Story-Points-Konsistenz-Rules
- QG1 Quality Gate Kriterien
- Automatische Validation Feedback Messages

---

## Tech Stack & Tools

### Core Technologies
- **Markdown** - Für alle Requirements-Dokumente
- **YAML Frontmatter** - Für Metadata in Chatmodes und Instructions
- **Gherkin** - Für testbare Acceptance Criteria in Issues

### GitHub Copilot Customization
- **Chat Modes** (`.chatmode.md`) - Spezialisierte AI-Personas
- **Instructions** (`.instructions.md`) - Path-spezifische Validierungsregeln
- **Templates** - Strukturierte Vorlagen für Epics, Features, Issues

### Development Environment
- **VS Code** - Primary IDE mit GitHub Copilot Extension
- **Git** - Version Control
- **Shell Scripts** - Für Validierung und Automatisierung

## Project Structure

```
.github/
├── copilot-instructions.md              # Diese Datei - Globale Instructions
├── chatmodes/
│   └── requirements-engineer.chatmode.md # Requirements Engineer Chat Mode
└── instructions/
    └── requirements-engineer.instructions.md # Auto-Validierung für requirements/

requirements/
├── templates/
│   ├── EPIC-TEMPLATE.md                 # Template für strategische Initiativen
│   ├── FEATURE-TEMPLATE.md              # Template für Funktionalitäten
│   ├── ISSUE-TEMPLATE.md                # Template für Implementierungseinheiten
│   └── README.md                        # Template-Dokumentation
├── BACKLOG.md                           # Zentrale Backlog-Übersicht (generiert)
├── HANDOVER.md                          # QG1 → Architecture Übergabe (generiert)
├── EPIC-XXX-*.md                        # Epic-Dateien
├── FEATURE-XXX-*.md                     # Feature-Dateien
└── ISSUE-XXX-*.md                       # Issue-Dateien

scripts/                                  # (Optional) Validation/Automation Scripts
docs/                                     # (Optional) Zusätzliche Dokumentation
```

## Naming Conventions

### Requirements-Dateien

**Alle Requirements folgen diesem Pattern:**
```
TYPE-XXX-descriptive-slug.md

Wobei:
- TYPE: EPIC | FEATURE | ISSUE
- XXX: 3-stellige Nummer (001-999)
- descriptive-slug: lowercase, words mit dashes getrennt
```

**Beispiele:**
```
✅ EPIC-001-customer-portal.md
✅ FEATURE-023-user-authentication.md
✅ ISSUE-142-oauth-google-integration.md

❌ epic-1.md                     (nicht konform)
❌ ISSUE-1-login.md              (Nummer nicht 3-stellig)
❌ ISSUE-001-User_Login.md       (Underscores statt Dashes)
```

### Chat Modes & Instructions

```
chatmodes/: [name].chatmode.md
instructions/: [name].instructions.md
```

## Coding Guidelines

### Markdown Best Practices

**Headers:**
- Nutze `#` für H1, `##` für H2, etc.
- Eine H1 pro Datei (Titel)
- Logische Hierarchie einhalten

**Listen:**
- Nutze `-` für unordered lists
- Nutze `1.` für ordered lists
- Konsistente Einrückung (2 Spaces)

**Code Blocks:**
```markdown
\`\`\`language
code here
\`\`\`
```

**YAML Frontmatter:**
```yaml
---
key: value
list:
  - item1
  - item2
---
```

### Gherkin Best Practices

**Struktur:**
```gherkin
Feature: [Feature Name] ([FEATURE-XXX])

Scenario: [Descriptive scenario name]
  Given [concrete precondition with specific values]
  And [additional precondition]
  When [concrete user action]
  And [additional action]
  Then [expected outcome with specific values]
  And [additional expectation]
  And [additional expectation]
```

**Qualitätsstandards:**
- ✅ Spezifische Werte in Anführungszeichen: `"user@example.com"`
- ✅ Messbare Outcomes: `"redirected to /dashboard"`
- ✅ Konkrete Actions: `"clicks the Login button"`
- ❌ Keine Platzhalter: `[X]`, `TODO`, `...`
- ❌ Keine vagen Begriffe: `"user does something"`

### File Organization

**Templates bleiben Templates:**
- Niemals Templates direkt editieren
- Immer kopieren und umbenennen
- Templates in `requirements/templates/` belassen

**Requirements-Struktur:**
- Alle Epics im root von `requirements/`
- Alle Features im root von `requirements/`
- Alle Issues im root von `requirements/`
- Keine Unterordner für Epics/Features/Issues

**Generated Files:**
- `BACKLOG.md` wird automatisch generiert
- `HANDOVER.md` wird bei QG1 erstellt
- Nicht manuell editieren, sonst gehen Änderungen verloren

## Working with Chat Modes

### Available Modes

**Requirements Engineer** (`@requirements-engineer`)
- Nutze für: Neue Requirements erstellen, Business Intake, QG1 Validation
- Prozess: 7 Phasen von Discovery bis Handover
- Output: Epics, Features, Issues mit Gherkin-Szenarien

### When to Use Which Mode

```
Neue Anforderungen definieren?
  → @requirements-engineer

Technische Architektur planen?
  → @architect (wenn verfügbar)

Code implementieren?
  → Standard Copilot oder @coder (wenn verfügbar)
```

## Quality Standards

### Requirements Quality (QG1)

**Ein Epic ist QG1-ready wenn:**
- [ ] Business Goal klar definiert mit ROI
- [ ] Min. 3 Core Features definiert und verlinkt
- [ ] Success Metrics mit Baseline → Target
- [ ] Timeline mit Milestones
- [ ] Dependencies und Risks dokumentiert

**Ein Feature ist QG1-ready wenn:**
- [ ] Business Value quantifiziert (Metriken!)
- [ ] Epic-Referenz im Header
- [ ] Min. 3 Core Issues definiert und verlinkt
- [ ] Story Points = Summe aller Issues
- [ ] Feature-spezifische Success Metrics

**Ein Issue ist QG1-ready wenn:**
- [ ] Epic UND Feature Referenz im Header
- [ ] Business Context erklärt Contribution to Feature
- [ ] **MIN. 2 vollständige Gherkin-Szenarien**
- [ ] Gherkin: Jedes Scenario hat Given/When/Then
- [ ] **KEINE Platzhalter** in Gherkin-Szenarien
- [ ] Definition of Done vollständig
- [ ] Story Points geschätzt (Fibonacci)

### Hierarchie-Integrität

**Bidirektionale Verlinkung:**
```
Epic → Features (in "Related Features")
Feature → Epic (im Header: "> **Epic:** EPIC-XXX")

Feature → Issues (in "Related Issues")
Issue → Feature (im Header: "> **Feature:** FEATURE-XXX")

Issue → Epic (im Header: "> **Epic:** EPIC-XXX")
```

**Story Points-Konsistenz:**
```
Epic Total SP = Σ(Feature Story Points)
Feature SP = Σ(Issue Story Points)
```

## Development Workflow

### Creating New Requirements

**Schritt 1: Aktiviere Requirements Engineer Mode**
```
@requirements-engineer Ich brauche Requirements für [Feature]
```

**Schritt 2: Business Intake durchführen**
- Beantworte strukturierte Fragen
- Eine Frage nach der anderen
- Sei spezifisch, nicht vage

**Schritt 3: Review & Validate**
- Automatische Validierung läuft
- Prüfe Feedback-Messages
- Korrigiere Fehler vor Commit

**Schritt 4: Commit**
```bash
git add requirements/
git commit -m "feat(requirements): Add [Epic/Feature/Issue] for [what]"
```

### Modifying Existing Requirements

**Wenn Requirements noch nicht QG1-approved:**
- Direkt editieren ist OK
- Validierung läuft automatisch
- Re-Validierung nach jedem Save

**Wenn Requirements bereits QG1-approved:**
- Diskutiere Änderungen mit Team
- Update alle betroffenen Parent/Child Items
- Re-Validierung durchführen
- Update BACKLOG.md wenn nötig

### Git Commit Messages

**Format:**
```
type(scope): subject

body (optional)

footer (optional)
```

**Types für Requirements:**
- `feat(requirements):` - Neue Requirements
- `fix(requirements):` - Korrekturen
- `docs(requirements):` - Dokumentations-Updates
- `refactor(requirements):` - Umstrukturierung

**Beispiele:**
```
feat(requirements): Add EPIC-001 customer portal with 5 features
fix(requirements): Correct Story Points in FEATURE-023
docs(requirements): Update EPIC-001 success metrics
```

## Validation & Automation

### Automatic Validations

**Beim Arbeiten in `requirements/**/*.md`:**
- ✅ Dateinamen-Validierung
- ✅ Hierarchie-Checks
- ✅ Gherkin-Qualitäts-Checks (für Issues)
- ✅ Business-Value-Validierung (für Epics/Features)
- ✅ Story-Points-Konsistenz
- ✅ Platzhalter-Detection

**Bei Git Commit:**
- ✅ Pre-Commit Hook (wenn konfiguriert)
- ✅ Vollständige Validierung
- ✅ Commit nur bei Success

### Quality Gates

**QG1 - Requirements Approved:**
- Alle Validierungen passed
- Label: `requirements:approved`
- `HANDOVER.md` erstellt
- Bereit für Architecture Mode

## Tools & Resources

### Primary Tools

**VS Code Extensions:**
- GitHub Copilot
- GitHub Copilot Chat
- Markdown All in One (empfohlen)
- markdownlint (empfohlen)

### Documentation

- **Process:** `.github/chatmodes/requirements-engineer.chatmode.md`
- **Validation:** `.github/instructions/requirements-engineer.instructions.md`
- **Templates:** `requirements/templates/README.md`
- **Corrections:** `CORRECTIONS-SUMMARY.md`
- **DRY Updates:** `DRY-CONSISTENCY-UPDATES.md`

### Quick Reference

**Aktiviere Requirements Engineer:**
```
@requirements-engineer [Your request]
```

**Check Validation Status:**
- Look for ✅/❌ in Copilot feedback
- Check file for error markers
- Review pre-commit output

**Templates Location:**
```
requirements/templates/
├── EPIC-TEMPLATE.md
├── FEATURE-TEMPLATE.md
└── ISSUE-TEMPLATE.md
```

## Best Practices

### DO ✅

- Nutze Requirements Engineer Mode für neue Requirements
- Beantworte alle Business Intake Fragen vollständig
- Schreibe spezifische, testbare Gherkin-Szenarien
- Halte bidirektionale Hierarchie konsistent
- Quantifiziere Business Value mit Metriken
- Commite nur nach erfolgreicher Validierung
- Update Story Points nach Issue-Änderungen

### DON'T ❌

- Erstelle keine Requirements ohne Business Intake
- Nutze keine Platzhalter in finalen Requirements
- Kopiere keine Gherkin-Szenarien zwischen Issues
- Ignoriere keine Validierungsfehler
- Breche keine bidirektionale Verlinkung
- Editiere keine Templates direkt
- Commite keine QG1-approved Requirements ohne Team-Diskussion

## Team Collaboration

### Onboarding New Members

**Schritt 1:** Lies diese Datei  
**Schritt 2:** Lies Requirements Engineer Chatmode  
**Schritt 3:** Probiere Mode mit Test-Feature  
**Schritt 4:** Review existierender Requirements  
**Schritt 5:** Erstelle erste echte Requirements  

### Code Review Focus

**Bei Requirements PRs prüfe:**
- [ ] Alle Validierungen passed
- [ ] Gherkin-Szenarien sind spezifisch und testbar
- [ ] Business Value ist quantifiziert
- [ ] Hierarchie ist bidirektional korrekt
- [ ] Story Points sind konsistent
- [ ] Commit Messages folgen Convention

### Communication

**Bei Fragen zu:**
- **Prozess:** Frage Team Lead oder prüfe Chatmode-Docs
- **Validierung:** Prüfe Instructions oder Validation Scripts
- **Templates:** Prüfe Template README
- **Git:** Nutze Standard Git Conventions

## Troubleshooting

### Common Issues

**Problem: Validierung schlägt fehl**
```
Lösung:
1. Lies Fehlermeldung sorgfältig
2. Prüfe welcher Check fehlschlug
3. Korrigiere gemäß Feedback
4. Save → Re-Validation
```

**Problem: Gherkin-Scenario nicht akzeptiert**
```
Lösung:
1. Prüfe: Hat Given/When/Then?
2. Prüfe: Enthält Platzhalter?
3. Prüfe: Sind Werte spezifisch?
4. Siehe ISSUE-TEMPLATE.md für Beispiele
```

**Problem: Story Points stimmen nicht**
```
Lösung:
1. Berechne: Summe aller Child-Item Story Points
2. Update Parent-Item Story Points
3. Re-Validate
```

**Problem: Chat Mode lädt nicht**
```
Lösung:
1. Prüfe: Dateiname korrekt (.chatmode.md)?
2. Prüfe: YAML Frontmatter valide?
3. VS Code neu laden: Cmd/Ctrl + Shift + P > Reload Window
```

## Updates & Maintenance

**Diese Datei wird gepflegt von:** [Team/Person]  
**Letzte Überprüfung:** [Datum]  
**Version:** 1.0

**Bei Änderungen am Prozess:**
- Update diese Datei
- Update Chatmode wenn Prozess-Änderung
- Update Instructions wenn Validierungs-Änderung
- Kommuniziere Änderungen ans Team

---

**Hinweis:** Diese Instructions werden automatisch bei jedem Copilot-Request geladen. Du musst nichts manuell aktivieren - arbeite einfach wie gewohnt, und Copilot wird diese Regeln berücksichtigen!

**Feedback:** Hast du Verbesserungsvorschläge für diese Instructions? Erstelle ein Issue oder PR!
