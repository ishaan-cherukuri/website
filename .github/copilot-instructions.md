# Copilot Instructions for MkDocs Portfolio Site

## Project Overview
A personal portfolio website built with **MkDocs Material** that showcases Ishaan's competitive programming, hackathons, ML projects, and music. The site uses Material Design theme with custom extensions for timelines, cards, and Mermaid diagrams.

## Architecture & Key Files

### Core Configuration
- **[mkdocs.yml](mkdocs.yml)**: Main site configuration including theme, plugins, markdown extensions, and navigation structure
  - Uses Material theme with dark/light mode toggle
  - Enables custom extensions: `neoteroi.timeline`, `neoteroi.mkdocsoad` (for API docs)
  - Custom CSS in `docs/css/` for neoteroi components
  - Key plugins: `glightbox` (image galleries), `search`, `pymdownx.*` (superfences, tasklist, emoji)

### Content Structure
- **docs/**: Source markdown files organized by category
  - `index.md`: Home page with about section and project overview
  - `cp.md`: Competitive programming achievements (USACO, contests)
  - `hack.md`: Hackathon projects
  - `kaggle.md`: ML/Kaggle competitions
  - `music.md`: Piano and music portfolio
- **docs/assets/images/**: Images referenced in markdown files (use relative paths `./assets/images/filename`)
- **docs/css/**: Custom stylesheets for neoteroi components (timeline, cards, etc.)
- **[cards.yml](cards.yml)** & **[timeline.yml](timeline.yml)**: YAML data files defining card and timeline content used with custom extensions

### Generated Site
- **site/**: Build output directory (auto-generated via `mkdocs build`, commit to version control if needed for GitHub Pages)

## Build & Deployment Workflow

### Local Development
```bash
uv sync                    # Install dependencies (uses uv package manager)
mkdocs serve              # Start live dev server at http://127.0.0.1:8000
```

### Build for Production
```bash
mkdocs build              # Generate static site in site/ directory
```

The site is likely deployed via **GitHub Pages** (check `.github/workflows/` for CI/CD).

## Content Authoring Conventions

### Markdown Extensions in Use
1. **Code Blocks**: Use ` ```language ` syntax; content.code.copy enabled
2. **Admonitions**: `!!! type "Title"` or `???+ type "Title"` (collapsible)
3. **Mermaid Diagrams**: ` ```mermaid ` blocks render flowcharts/diagrams
4. **Inline Highlights**: `pymdownx.inlinehilite` for inline code highlighting
5. **Task Lists**: `- [x] Task` syntax with custom checkboxes
6. **Superfences**: Custom fence types like mermaid with custom rendering

### Image Handling
- Store images in `docs/assets/images/`
- Reference with relative paths: `![Alt text](./assets/images/filename)`
- Use `{ loading=lazy width="400" }` attributes for lazy loading and sizing

### Navigation & Organization
- Update `mkdocs.yml` `nav:` section to add/modify page structure
- Nested navigation creates dropdown menus (see "Machine Learning" section with `kaggle.md` nested)

## Custom Extensions & Styling

### Neoteroi Components
- **Timeline** (`neoteroi.timeline`): Render timeline.yml events with icons from material/fontawesome
- **Cards** (custom CSS): Display card.yml content in `docs/css/neoteroi-cards.css`
- **Stylesheets**: Extra CSS in `docs/stylesheets/extra.css` for site-wide customizations

### Material Theme Features Enabled
- Instant page loading (`navigation.instant`)
- Tabbed content (`pymdownx.tabbed`)
- Code annotation (`content.code.annotate`)
- Search suggestions (`search.suggest`)

## Dependencies & Python Version
- **Python**: >=3.11
- **Key Packages**: mkdocs (1.6.1+), mkdocs-material (9.7.1+), pymdown-extensions (10.19.1+)
- **Package Manager**: uv (see `pyproject.toml`)
- Build tool: None specified (plain static generation)

## Critical Patterns

### When Adding Content
1. Create markdown file in `docs/` with kebab-case naming
2. Update `mkdocs.yml` navigation if creating a new page
3. Use existing pages (cp.md, hack.md) as templates for structure
4. Reference images and assets with relative paths from `docs/` root

### When Modifying Design
1. CSS changes go in `docs/css/` (site-wide) or `docs/stylesheets/extra.css`
2. Material theme colors configured in `mkdocs.yml` theme.palette section
3. Custom extensions require understanding neoteroi-specific syntax in markdown
