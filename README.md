# eBook Template Repository

[![CI](https://github.com/isaac-cf-wong/mdbook-template/actions/workflows/CI.yml/badge.svg)](https://github.com/isaac-cf-wong/mdbook-template/actions/workflows/CI.yml)
[![Publish](https://github.com/isaac-cf-wong/mdbook-template/actions/workflows/publish.yml/badge.svg)](https://github.com/isaac-cf-wong/mdbook-template/actions/workflows/publish.yml)
[![mdBook](https://img.shields.io/badge/mdBook-v0.4.40-blue)](https://github.com/rust-lang/mdBook)
[![MathJax](https://img.shields.io/badge/MathJax-v3.2.2-blue)](https://www.mathjax.org/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen)](https://pre-commit.com/)
[![Codespell](https://img.shields.io/badge/Spellcheck-Codespell-blue)](https://github.com/codespell-project/codespell)
[![Detect-Secrets](https://img.shields.io/badge/Security-Detect--Secrets-blue)](https://github.com/Yelp/detect-secrets)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Template](https://img.shields.io/badge/GitHub-Template-blue)](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

This repository serves as a template for creating and maintaining an eBook using mdBook, a tool for building books from Markdown files. It is designed to streamline the process of authoring, building, and publishing technical documentation or eBooks, with support for features like MathJax 3.2 for rendering mathematical equations (including the physics package). The repository includes pre-commit hooks and GitHub Actions workflows to ensure code quality, security, and automated publishing.

## Getting Started

### Creating Your eBook Repository
1. **Use This Template**:
   - Click the green **"Use this template"** button and select **"Create a new repository"**.
   - Choose a name for your new repository (e.g., `my-ebook`), select its visibility (public/private), and create it.
   - This copies the template’s structure (mdBook setup, pre-commit hooks, workflows) into your new repository without linking to the original template.

2. **Clone Your New Repository**:
   ```bash
   git clone https://github.com/your-username/my-ebook.git
   cd my-ebook
   ```

### Prerequisites
- [mdBook](https://github.com/rust-lang/mdBook): Install with `cargo install mdbook`.
- [Python](https://www.python.org/): For running pre-commit hooks (e.g., `detect-secrets`, `codespell`).
- A GitHub personal access token (PAT) named `WORKFLOW_SECRET` with the `workflow` scope for the `github-actions-version-updater` workflow. Add it in your repository’s Settings > Secrets and variables > Actions.

### Installation
1. Install mdBook:
   ```bash
   cargo install mdbook
   ```

2. Install pre-commit hooks:
   ```bash
   pre-commit install
   ```
3. Build and serve the eBook locally:
   ```bash
   mdbook build
   mdbook serve --open
   ```
   Open `http://localhost:3000` in your browser to preview the eBook.

### Project Structure
- `book.toml`: mdBook configuration, enabling MathJax support.
- `src/`: Markdown files for your eBook content.
- `theme/`: Custom theme files (e.g., `index.hbs` for MathJax 3.2 configuration).
- `.pre-commit-config.yaml`: Defines pre-commit hooks for quality and security.
- `.github/workflows/`: GitHub Actions workflows for CI, publishing, and maintenance.
- `.github/template-sync.yml`: Lists files to synchronize with this template repository.
- `.gitignore`: Includes `.secrets.baseline` to prevent committing the `detect-secrets` baseline file.

### MathJax Support
The template includes MathJax 3.2 with the `physics` package for rendering mathematical equations. Use `\\(...\\)` for inline equations and `\\[ ... \\]` for display equations in Markdown files. Example:
```markdown
The state vector \\(\ket{\psi}\\) is used in quantum mechanics.
\\[
\grad \cdot \vec{E} = \frac{\rho}{\epsilon_0}
\\]
```

## Pre-Commit Hooks
The template includes the following pre-commit hooks (defined in `.pre-commit-config.yaml`) to ensure code quality and prevent accidental commits of sensitive information:
- **check-yaml**: Validates YAML files for correct syntax.
- **check-toml**: Validates TOML files (e.g., `book.toml`) for correct syntax.
- **trailing-whitespace**: Removes trailing whitespace from files.
- **end-of-file-fixer**: Ensures files end with a newline.
- **check-added-large-files**: Prevents committing large files that could bloat the repository.
- **codespell**: Checks for common spelling mistakes in text and code.
- **detect-secrets**: Scans for sensitive information (e.g., API keys, passwords). Maintain a local `.secrets.baseline` file to ignore false positives (e.g., MathJax equations). Do **not** commit `.secrets.baseline` to the repository; it’s included in `.gitignore`.

To set up the hooks:
```bash
pre-commit install
```
To generate a local `.secrets.baseline` file for `detect-secrets`:
```bash
detect-secrets scan > .secrets.baseline
detect-secrets audit .secrets.baseline
```
- Audit the `.secrets.baseline` file to mark false positives (e.g., MathJax equations like `\ket{\psi}`).
- **Do not commit `.secrets.baseline`**. Ensure it’s in `.gitignore` to keep it local.

## GitHub Actions Workflows
The template includes the following GitHub Actions workflows (in `.github/workflows/`):

1. **CI**:
   - **Purpose**: Runs on every push and pull request to check spelling with `codespell`.
   - **Details**: To ignore specific words, add them to the `.codespellignore` file.

2. **publish**:
   - **Purpose**: Publishes the eBook when a release is created (e.g., via a GitHub release).
   - **Details**: Builds the mdBook project and deploys the output (e.g., to GitHub Pages or another hosting service). Configure the deployment target in the workflow file as needed.

3. **github-actions-version-updater**:
   - **Purpose**: Keeps GitHub Actions dependencies up to date (e.g., `actions/checkout`, `actions/setup-python`).
   - **Details**: Requires a personal access token named `WORKFLOW_SECRET` with the `workflow` scope. Add it to your repository’s Settings > Secrets and variables > Actions.

4. **semantic-pr-check**:
   - **Purpose**: Ensures pull request titles use a valid semantic prefix (e.g., `feat:`, `fix:`, `docs:`) for consistency.
   - **Details**: Fails the PR if the title doesn’t follow the configured convention.

5. **template-sync**:
   - **Purpose**: A dispatch workflow to synchronize your repository with this template repository.
   - **Details**: Before running, review `.github/template-sync.yml` to verify the list of files to be synchronized (e.g., workflows, pre-commit config). Trigger manually via the Actions tab or configure automatic synchronization.

## Usage
This repository is a GitHub template for creating your own eBook. **Do not fork or use this repository directly** for your eBook content, as it is meant to be a reusable template. Instead, follow these steps:

1. **Create Your Repository**:
   - Use the **"Use this template"** button on GitHub to create a new repository under your account or organization.
   - Clone your new repository:
     ```bash
     git clone https://github.com/your-username/my-ebook.git
     cd my-ebook
     ```

2. **Customize Content**:
   - Edit Markdown files in `src/` to add your eBook content.
   - Update `book.toml` to set the book title, author, and other settings.
   - Modify `theme/index.hbs` if you need custom MathJax configurations (e.g., additional packages).

3. **Add Equations**:
   - Use MathJax syntax for equations (e.g., `\\(\ket{\psi}\\)` for inline, `\\[ \grad \cdot \vec{E} \\]` for display).
   - If equations trigger `detect-secrets` locally, mark them as false positives in your local `.secrets.baseline` or add `# pragma: allowlist secret` comments:
     ```markdown
     \\(\ket{\psi}\\)  # pragma: allowlist secret
     ```

4. **Build and Test**:
   - Build the eBook: `mdbook build`
   - Preview locally: `mdbook serve --open`
   - Verify equations render correctly at `http://localhost:3000`.

5. **Commit Changes**:
   - The pre-commit hooks will validate files and scan for secrets.
   - Maintain a local `.secrets.baseline` for `detect-secrets` and ensure it’s not committed (check `.gitignore`).
   - Update `.secrets.baseline` if false positives (e.g., MathJax equations) are flagged:
     ```bash
     detect-secrets audit .secrets.baseline
     ```

6. **Push and Publish**:
   - Push changes to trigger the `CI` workflow, which checks for spelling.
   - Create a GitHub release to trigger the `publish` workflow and deploy your eBook.
   - Use the `template-sync` workflow to pull updates from this template, checking `.github/template-sync.yml` first to verify synchronized files.

## Contributing to Your eBook
To add content or features to your eBook repository:
1. Create a branch with a semantic name (e.g., `feat/add-chapter`).
2. Commit changes, ensuring pre-commit hooks pass.
3. Open a pull request with a title using a valid semantic prefix (e.g., `docs: Update README`).

## Contributing to This Template
To improve this template repository (e.g., update hooks or workflows):
1. Fork the repository.
2. Create a branch with a semantic name (e.g., `feat/add-hook`).
3. Commit changes, ensuring pre-commit hooks pass.
4. Open a pull request with a semantic title to this repository.

## Troubleshooting
- **MathJax Equations Not Rendering**: Ensure `mathjax-support = true` in `book.toml` and verify the MathJax 3.2 script in `theme/index.hbs`.
- **Pre-Commit Hook Failures**: For `detect-secrets`, update your local `.secrets.baseline` or use `# pragma: allowlist secret` in Markdown. For spelling, add custom words to `.codespellignore`.
- **Workflow Failures**: Check the Actions tab for logs. Ensure `WORKFLOW_SECRET` is set for `github-actions-version-updater`. For `template-sync`, verify `.github/template-sync.yml`.
- **GitHub Page**: Set Settings > Pages > Build and deployment > Source to `GitHub Actions`.

---
For questions or issues, open an issue in your eBook repository or this template repository.
---
