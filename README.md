# Rahul Bera - Resume

This repository contains the LaTeX source code for my resume, along with a CI/CD pipeline to automate the generation and release of PDF versions across different tailored variants.

## Branching Strategy

The repository follows a branch-per-variant model:
- Each branch represents a distinct resume variant tailored for specific roles (e.g., `main` for generic, `robotics`, `backend`, `frontend`).
- Normal commits are tracked on these branches but remain unpublished.

## Local Setup & Building

The resume is built using LaTeX. The primary source file is located at `latex/resume.tex`.

### Prerequisites
- A LaTeX distribution (e.g., TeX Live, MacTeX, MiKTeX).
- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension for VSCode (Recommended).

### Building
The repository is configured via `.vscode/settings.json` to handle compilation automatically. When building locally, the output is configured to generate `rahul-bera-resume.pdf`.

You can also build it manually from the terminal:
```bash
cd latex
latexmk -pdf resume.tex
```

## Release Flow

This repository uses GitHub Actions to automate PDF generation. PDFs are **not** committed to version control; instead, they are attached as versioned build artifacts to GitHub Releases.

To publish a new resume version:

1. **Commit your changes** to the appropriate branch (e.g., `robotics`).
2. **Create a Git tag** specifying the date and variant.
3. **Push the tag** to GitHub.

### Example

```bash
# Ensure you are on the correct branch
git checkout robotics

# Tag the snapshot
git tag 20260905-robotics

# Push the tag to trigger the GitHub Action
git push origin 20260905-robotics
```

The GitHub Actions workflow will automatically:
- Trigger on the tag push.
- Checkout the exact commit associated with the tag.
- Compile the LaTeX document into a PDF.
- Rename the output file to `rahul-bera-resume.pdf` (configurable in `.github/workflows/release.yml`).
- Create a GitHub Release and attach the PDF as an asset.

You can then download or link directly to the PDF from the GitHub Releases page.
