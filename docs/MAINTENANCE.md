# Resume Maintenance & CI/CD Workflow

## Overview

This repository uses an automated "Documentation as Code" pipeline to generate professional PDFs from Markdown source files. It is architected to minimize technical debt and ensure that the "Technical Craftsmanship" and "Enterprise Platform Architecture" details remain the single source of truth.

## Infrastructure

* **Engine:** Pandoc via GitHub Actions.
* **Docker Image:** `pandoc/extra:latest` (required for Koma-Script dependencies like `scrartcl.cls`).
* **Template:** Eisvogel LaTeX template located in `./templates/eisvogel.tex`.
* **Deployment:** GitHub Pages (configured to use GitHub Actions as the source).

## Standard Procedures

### Adding a New Resume Version

To create a tailored version (e.g., for a specific job description):

1. Create a new Markdown file in the root (e.g., `resume-manager.md`).
2. Update the `index.html` landing page to include a link to the new PDF.
3. Update `.github/workflows/deploy.yml` to include the new render command:
```yaml
-o ./public/resume-manager.pdf resume-manager.md

```



### Local Development (WSL2/Lando)

While the build happens in the cloud, you can preview changes locally if Pandoc is installed in your WSL2 environment.

```bash
# Example local build command
pandoc resume.md -o resume.pdf --template ./templates/eisvogel.tex --pdf-engine=pdflatex

```

## Troubleshooting

* **LaTeX Errors:** If a "file not found" error occurs for a `.cls` or `.sty` file, ensure the GitHub Action is using the `extra` version of the Pandoc Docker image, as the `latex` version is often too stripped down.
* **Pathing:** Always use relative paths (e.g., `./templates/`) to ensure the Docker container can resolve file locations correctly.

## Philosophy

> "If you don't have time to do it right, when are you going to have time to do it again?"
> — Adhering to the Musgrave Rule for personal infrastructure ensures this system remains functional with zero maintenance for years.
>
>

---
