# Portfolio Update Rules

## Purpose

This file defines the rules for automatically adding new project cards
to the portfolio.

The automation must follow these rules exactly and must not modify
existing project cards.

---

## Source

Project information must be read from the project's `README.md`.

The README must contain the following information:

- Project name
- Project description
- Technologies used

If any required information is missing, the process must stop
and return an error describing what is missing.

The automation must not invent or assume missing information.

---

## Project Card

Every new project must be added as a new:

```html
<li class="project-item">
```

The new project card must be added at the end of the existing
project list inside the `Projects` section.

Existing project cards must not be modified.

The card must contain:

- Project name
- Project description
- Technologies used
- Project status
- GitHub repository link

---

## Project Name

The project name must be taken from the project's `README.md`.

A unique translation key must be generated from the repository name.

The repository name must be converted to PascalCase.

For example:

```text
terraform-first-project
```

becomes:

```text
TerraformFirstProject
```

The translation keys must be:

```text
TerraformFirstProject
TerraformFirstProjectDescription
```

The same naming convention must be used for every new project.

---

## Description

The project description must be taken from the project's `portfolio-update.md`.

The description must have separate Polish and English translations.

The translation keys must follow the project naming convention:

```text
<ProjectName>ProjectDescription
```

The description must not be invented if it is missing from the README.

---

## Technologies

Technologies must be taken from the project's `README.md`.

Technology names must remain in their original form.

Do not translate technology names.

If a technology has a corresponding Devicon icon available,
use the appropriate Devicon icon.

If no Devicon icon exists, display the technology name without an icon.

Do not invent technologies or icons that are not present in the project
information.

---

## Status

Every newly added project must automatically receive:

```html
<p data-i18n="StatusInProgress">
    Status: In progress
</p>
```

The status of existing projects must never be changed automatically.

Project status changes after the initial addition are performed manually.

---

## GitHub Repository

The GitHub repository link must be obtained automatically from
the repository that triggered the portfolio update.

The URL must be placed in the project card's GitHub button:

```html
<a href="REPOSITORY_URL"
   target="_blank"
   class="btn">
    GitHub
</a>
```

The repository URL must not be manually entered when the automation
can obtain it automatically.

---

## Translations

Every user-facing project name and description must have
Polish and English translations.

Use the existing `translations` object in:

```text
js/language.js
```

Use `data-i18n` attributes for translatable HTML elements.

Existing translation keys must not be modified.

The existing shared translation keys, such as:

```text
Projects
TechnologiesUsed
StatusInProgress
StatusFinished
StatusCompleted
```

must be reused when applicable instead of creating duplicates.

---

## HTML Structure

The generated project card must follow the existing
`.project-item` structure used by the portfolio.

The automation must preserve the existing formatting and indentation
style of the HTML file.

Do not redesign or restructure the `Projects` section.

Do not modify existing project cards.

---

## Validation

After modifying the portfolio, run the project's validation process.

The following checks must pass:

1. Biome
2. Ruff
3. `check.bat`

If any validation step fails, the process must stop.

No commit or Pull Request must be created when validation fails.

The error must clearly identify which validation step failed.

---

## Error Handling

If required project information cannot be obtained,
the process must stop.

Errors must clearly describe the problem.

Examples:

```text
ERROR: Project name is missing from README.md.
Portfolio update aborted.
```

```text
ERROR: Project description is missing from README.md.
Portfolio update aborted.
```

```text
ERROR: Technologies are missing from README.md.
Portfolio update aborted.
```

```text
ERROR: Biome validation failed.
Portfolio update aborted.
```

The automation must never continue after an error.

---

## Existing Projects

Existing project cards and existing translations must not be modified,
removed, reordered, or overwritten.

A new project must always be appended to the end of the project list.

The purpose of this automation is only to add the new project
and its required translations.
