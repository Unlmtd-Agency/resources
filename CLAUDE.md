# CLAUDE.md — Unlmtd Agency: Resources

This file provides guidance for AI assistants working in this repository.

---

## Repository Overview

**Repository**: `Unlmtd-Agency/resources`
**Purpose**: Print and digital design resources for Unlmtd Agency, an Australian graphic design and branding studio.

This repository hosts standalone HTML-based design tools and reference documents used by the Unlmtd Agency team and their clients.

---

## Repository Structure

```
resources/
├── README.md                          # Minimal project description
├── CLAUDE.md                          # This file
└── Unlmtd Agency design resources    # Interactive Logo Design Checklist (HTML)
```

### File: `Unlmtd Agency design resources`

A self-contained, interactive HTML document titled **"Logo Design Checklist | Unlmtd Agency"**. It is a single-file web application (no build step required) intended to guide graphic designers through a professional logo design workflow.

**Key features:**
- 7 collapsible workflow sections, each with required and optional checklist items
- Real-time progress bar tracking total and required items
- Quick reference panel (brand specs, file counts)
- Colour modes reference table with expandable detail cards
- File format reference table (vector vs raster)
- Design tips section (Scalability Test, Squint Test, Versatility Check, Licensing Reminder)
- State persisted to `localStorage` under the key `unlmtd-logo-checklist`
- No framework or bundler — pure HTML, CSS, and vanilla JavaScript in one file

---

## Checklist Sections & Items

The checklist data lives in the JavaScript constant `checklistData` (approx. line 767 of the HTML file):

| Section ID | Section Title | Items | Required |
|---|---|---|---|
| `discovery` | Discovery & Research | 8 | 6 |
| `concept` | Concept Development | 8 | 7 |
| `design` | Design Execution | 10 | 9 |
| `testing` | Testing & Refinement | 8 | 6 |
| `approval` | Client Approval | 6 | 5 |
| `delivery` | File Preparation & Delivery | 10 | 8 |
| `guidelines` | Brand Guidelines | 8 | 6 |

Each item object has the shape:
```js
{ id: 'string', text: 'string', required: boolean }
```

---

## Brand Design Tokens

Defined as CSS custom properties in `:root`:

```css
/* Core palette */
--unlmtd-blue:   #21409a
--unlmtd-yellow: #FFDE17
--unlmtd-red:    #BE1E2D
--unlmtd-black:  #1D1D1D
--unlmtd-white:  #ffffff

/* Extended palette */
--blue-light:    #e8ecf5
--blue-medium:   #3a5bb8
--yellow-light:  #fff9db
--red-light:     #fceaec
--grey-100:      #f7f7f7
--grey-200:      #eeeeee
--grey-300:      #d4d4d4
--grey-500:      #737373
--grey-700:      #404040
```

**Typography:**
- Body / UI: `Instrument Sans` (400, 500, 600, 700) — loaded from Google Fonts
- Headings: `Instrument Serif` (400, 700; italic variants) — loaded from Google Fonts
- Monospace fallback: `SF Mono`, `Monaco`, `Consolas`

---

## Conventions

### Language
- Australian English spelling throughout (e.g., "colour", "recognisable", "analysed", "finalising")
- Maintain this convention for all text content edits

### HTML File Naming
- The main resource file has no extension: `Unlmtd Agency design resources`
- Do not rename this file without updating any references to it
- New resource files should follow the same naming pattern: `Unlmtd Agency <resource name>`

### File Architecture
- Resources are self-contained single HTML files — no external JS/CSS dependencies except Google Fonts
- Do not introduce npm, bundlers, or build tools
- CSS lives in a `<style>` block in `<head>`; JavaScript lives in a `<script>` block before `</body>`

### CSS Structure
The stylesheet is organised with section comment banners:
```css
/* ============================================
   SECTION NAME
   ============================================ */
```
Follow this pattern when adding new style blocks.

### JavaScript
- Pure vanilla ES6+; no frameworks or libraries
- Checklist state is managed with a plain object (`checkedItems`) and persisted via `localStorage`
- DOM rendering is done by string-based `innerHTML` injection (`render()` function pattern)
- All interactive data (checklist items, colour specs, file formats) is defined as JS constants near the top of the `<script>` block

---

## Development Workflow

### Making Changes

1. Edit the HTML file directly — there is no build step
2. Open in a browser to verify changes
3. Test checklist interactions: toggling items, section collapse/expand, progress bar updates
4. Verify `localStorage` persistence works across page reloads

### Adding a New Checklist Section

1. Add an entry to `checklistData` array with a unique `id`, `title`, and `items[]`
2. The render functions are data-driven — the new section will appear automatically
3. Update progress logic if required item counts change

### Adding a New Resource File

1. Create a new self-contained HTML file following the existing file's structure
2. Use the same CSS custom properties (`--unlmtd-blue`, etc.) for brand consistency
3. Use Instrument Sans / Instrument Serif from Google Fonts
4. Name the file without an extension: `Unlmtd Agency <resource name>`
5. Update `README.md` to list the new resource

### Git Workflow

- Default branch: `master`
- Feature/task branches: use the `claude/` prefix (e.g., `claude/feature-name-sessionid`)
- Commit messages should be descriptive and imperative mood (e.g., `Add print export section to Logo Design Checklist`)
- Always push with `-u` flag: `git push -u origin <branch-name>`

---

## Key Constraints

- **No build tooling**: keep resources as single, self-contained HTML files
- **No external JS**: avoid CDN-loaded JavaScript libraries to keep files portable and offline-friendly
- **Brand fidelity**: always use the defined CSS custom properties — do not hardcode colour hex values in new rules
- **Australian English**: maintain consistent spelling in all user-facing text
- **Accessibility**: maintain semantic HTML structure; checklist items use interactive elements with appropriate labels
