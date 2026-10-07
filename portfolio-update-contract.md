# Portfolio Update Rules

## Purpose

This file defines the rules for automatically adding new project cards
or updating existing project cards in the portfolio.

The automation must follow these rules exactly.

When processing a project update, the automation must determine whether
the project already exists in the portfolio.

If the project does not exist, a new project card must be created.

If the project already exists, its project card and required translations
must be synchronized with the current information provided in the project's
`portfolio-update.md`.

The automation must not modify unrelated projects or their translations.

---

## Source

Project information must be read from the project's `portfolio-update.md`.

The `portfolio-update.md` must contain the following information:

- Project name
- Project description in English and Polish
- Technologies used

If any required information is missing, the process must stop
and return an error describing what is missing.

The automation must not invent or assume missing information.

---

## Project Detection

The automation must determine whether the project already exists
in the portfolio before modifying the portfolio.

The project must be identified using the repository that triggered
the portfolio update.

The repository name must be converted to PascalCase and used to
generate the project's translation key.

For example:

```text
terraform-first-project
```

becomes:

```text
TerraformFirstProject
```

The generated project key must be used consistently when identifying
the project's existing translations and project card.

If the project already exists, the automation must update that project
instead of creating a duplicate project card.

If the project does not exist, the automation must create a new project card.

---

## Project Card

### New Project

Every new project must be added as a new:

```html
<li class="project-item">
```

The new project card must be added at the end of the existing
project list inside the `Projects` section.

The card must contain:

- Project name
- Project description
- Technologies used
- Project status
- GitHub repository link

### Existing Project

If the project already exists, the automation must synchronize its
existing project card with the current information from
`portfolio-update.md`.

The automation must:

- update the project name when it changes
- update the project description when it changes
- add technologies that were added to `portfolio-update.md`
- remove technologies that no longer exist in `portfolio-update.md`
- update the required Polish and English translations
- preserve the project's current status
- preserve the project's current position in the project list

The automation must not create duplicate project cards.

---

## Project Name

The project name must be taken from the project's `portfolio-update.md`.

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

The same naming convention must be used for every project.

The repository-based project key is the stable identifier for the project.

Changing the project name in `portfolio-update.md` must not create
a new project card or change the project's repository-based identity.

---

## Description

The project description must be taken from the project's
`portfolio-update.md`.

The description must have separate Polish and English translations.

The translation keys must follow the project naming convention:

```text
<ProjectKey>ProjectDescription
```

For example:

```text
TerraformFirstProjectDescription
```

When creating a new project, the required translation keys must be added.

When updating an existing project, the existing project translation keys
must be synchronized with the current information from `portfolio-update.md`.

If the description changes, the old project description must be replaced
with the new description.

The description must not be invented if it is missing from
the `portfolio-update.md`.

---

## Technologies

Technologies must be taken from the project's `portfolio-update.md`.

Technology names must remain in their original form.

Do not translate technology names.

If a technology has a corresponding Devicon icon available,
use the appropriate Devicon icon.

If no Devicon icon exists, display the technology name without an icon.

Do not invent technologies or icons that are not present in the project
information.

For existing projects, the technology list must be synchronized with
the current contents of `portfolio-update.md`.

If a technology is added to `portfolio-update.md`, it must be added
to the project card.

If a technology is removed from `portfolio-update.md`, it must be removed
from the project card.

If the Devicon availability changes, the automation must use the current
appropriate Devicon when available and otherwise display the technology
name without an icon.

---

## Status

Every newly added project must automatically receive:

```html
<p data-i18n="StatusInProgress">
    Status: In progress
</p>
```

When updating an existing project, its current status must be preserved.

The automation must never automatically change the status of an
existing project.

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

When updating an existing project, the repository link must continue
to point to the repository that triggered the update.

---

## Translations

Every user-facing project name and description must have
Polish and English translations.

Use the existing `translations` object in:

```text
js/language.js
```

Use `data-i18n` attributes for translatable HTML elements.

For a new project, the required translation keys must be created.

For an existing project, the project's existing translation keys
must be synchronized with the current information from
`portfolio-update.md`.

If the project name changes, the corresponding project name translation
must be updated.

If the project description changes, the corresponding Polish and English
description translations must be updated.

Existing translation keys belonging to unrelated projects must not
be modified.

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

The generated or updated project card must follow the existing
`.project-item` structure used by the portfolio.

The automation must preserve the existing formatting and indentation
style of the HTML file.

Do not redesign or restructure the `Projects` section.

New projects must be appended to the end of the existing project list.

Existing projects must remain in their current position.

The automation must not modify unrelated project cards.

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
ERROR: Project name is missing from portfolio-update.md.
Portfolio update aborted.
```

```text
ERROR: Project description is missing from portfolio-update.md.
Portfolio update aborted.
```

```text
ERROR: Technologies are missing from portfolio-update.md.
Portfolio update aborted.
```

```text
ERROR: Biome validation failed.
Portfolio update aborted.
```

The automation must never continue after an error.

---

## Existing Projects

Existing project cards must not be removed or reordered.

If an existing project is being updated, only that project's
defined information and required translations may be modified.

The automation must synchronize the existing project with the current
contents of `portfolio-update.md`.

This means that project name, descriptions, technologies and their
required translations may be added, updated or removed as necessary.

The project's current status must be preserved.

The automation must not modify unrelated project cards,
translations, or other portfolio content.

An existing project must be updated in place.

A new project must always be appended to the end of the project list.

The automation must never create a duplicate project card for
an existing project.

The purpose of this automation is to add new projects or synchronize
existing projects and their required translations with
`portfolio-update.md`.
