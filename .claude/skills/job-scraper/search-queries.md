# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary (Colombia):
- **linkedin.com/jobs** - LinkedIn (filtro: Medellín, Antioquia, Colombia); también vía CLI `linkedin-search` con `--location "Medellín, Antioquia, Colombia"`
- **co.computrabajo.com** - bolsa de empleo más grande de Colombia
- **elempleo.com** - bolsa general colombiana
- **co.indeed.com** - agregador
- **serviciodeempleo.gov.co / SISE** - Servicio Público de Empleo (incluye cajas de compensación: Comfama, Comfenalco Antioquia)
- **cnsc.gov.co (SIMO)** - concursos de carrera administrativa (ICBF y otras entidades públicas)
- **icbf.gov.co/trabaja-con-nosotros** y **SECOP II** - contratos de prestación de servicios con el ICBF y la Alcaldía

Secondary (company career pages via Google):
- Operadores del ICBF en Antioquia, Alcaldía de Medellín, fundaciones, IPS de salud mental

## Query Categories

### Priority 1: Psicóloga en protección / restablecimiento de derechos

```
site:co.computrabajo.com psicólogo "restablecimiento de derechos" Medellín
site:co.computrabajo.com psicóloga ICBF Medellín
site:linkedin.com/jobs psicólogo "Defensoría de Familia" OR "Comisaría de Familia" Antioquia
site:elempleo.com psicólogo ICBF Antioquia
"psicólogo" "PARD" OR "restablecimiento de derechos" Medellín vacante
```

### Priority 2: Psicóloga social comunitaria y psicosocial

```
site:co.computrabajo.com "psicólogo social" OR "psicóloga social" Medellín
site:co.computrabajo.com "profesional psicosocial" Medellín
site:linkedin.com/jobs "psicosocial" psicólogo Medellín
site:elempleo.com "psicólogo comunitario" OR "atención psicosocial" Antioquia
```

### Priority 3: Psicóloga en salud / salud mental

```
site:co.computrabajo.com psicólogo IPS Medellín
site:co.computrabajo.com psicóloga "salud mental" Medellín
site:linkedin.com/jobs psicólogo "salud mental" Medellín
```

### Priority 4: Red más amplia (recién egresada, gestión humana)

```
site:co.computrabajo.com psicólogo "sin experiencia" OR "recién egresado" Medellín
site:co.computrabajo.com "psicólogo de selección" OR "analista de selección" Medellín
site:linkedin.com/jobs "psicólogo" "talento humano" Medellín
site:elempleo.com psicólogo Medellín
```

## Location Filter

Verificar que la vacante esté en un lugar razonable desde Medellín:
- Medellín (ideal)
- Área Metropolitana: Bello, Itagüí, Envigado, Sabaneta (aceptable)
- La Estrella, Caldas, Copacabana, Girardota (aceptable)
- Oriente cercano: Rionegro, Marinilla, La Ceja (borderline - ~1 h; pendiente confirmar)
- Otros departamentos / municipios lejanos de Antioquia (demasiado lejos, salvo que Dayerlis diga lo contrario)
- Remoto / teleorientación psicológica: aceptable

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
