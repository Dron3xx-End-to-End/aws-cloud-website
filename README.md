# AWS Cloud & DevOps Portfolio

A lightweight, static portfolio website presenting Dawid Bronikowski's Cloud & DevOps skills, certifications, and projects. The portfolio is focused on **AWS, infrastructure as code, automation, and CI/CD**.

**Live website:** https://d3kblsgq3c7ax1.cloudfront.net  
**Source repository:** https://github.com/Dron3xx-End-to-End/aws-cloud-website

## Overview

The site is built with HTML, CSS, and vanilla JavaScript. It is hosted as static content on AWS S3 and delivered through Amazon CloudFront. The page includes Polish and English translations and project cards linking to their source repositories.

The repository also contains maintenance utilities and participates in a GitHub Actions workflow that validates code and updates the portfolio content.

## Features

- Static portfolio website with a responsive layout
- Polish and English interface translations
- Sections for professional introduction, skills, certifications, projects, and contact information
- Project cards showing descriptions, technologies, status, and repository links
- AWS S3 hosting with CloudFront delivery
- GitHub Actions workflows for validation and automated portfolio maintenance
- Python utility for updating the page's last-updated date
- Ruff and Biome checks for code quality

## Technology Stack

- **Cloud:** AWS S3, Amazon CloudFront
- **Automation / CI:** GitHub Actions
- **Frontend:** HTML5, CSS3, JavaScript
- **Maintenance:** Python 3, Beautiful Soup 4
- **Quality checks:** Ruff, Biome

## Repository Structure

```text
aws-cloud-website/
├── index.html
├── css/
│   └── styles.css
├── js/
│   ├── language.js
│   └── projectscroll.js
├── images/
├── scripts/
│   ├── check.bat
│   └── update_last_update.py
├── explained.md
├── README.md
└── LICENSE
```

## Local Development

Clone the repository and open `index.html` in a browser, or start a local static server from the repository root:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>.

## Validation

On Windows, run the repository's validation helper from the project root:

```bat
scripts\check.bat
```

The repository also uses Biome for JavaScript formatting and checks. When running Biome manually, use the project's configured package and run it from the website repository root, for example:

```bash
npx @biomejs/biome format --write ./js
npx @biomejs/biome check ./js
```

## Updating the Footer Date

Run the following command from the repository root:

```bash
python scripts/update_last_update.py
```

The script updates the footer's last-updated date in `index.html`.

## Deployment

The website is hosted on AWS S3 and delivered through Amazon CloudFront. GitHub Actions is used for repository validation and automated maintenance. Deployment settings and AWS resource configuration are managed separately from the static website source.

## Project Direction

This portfolio is focused on **AWS and Cloud/DevOps engineering**. The current learning and project direction prioritizes AWS, Terraform, Ansible, Python, Bash, and GitHub Actions. Azure and Google Cloud Platform are not part of the current roadmap.

## License

This project is licensed under the MIT License. See [`LICENSE`](LICENSE) for details.

## Contact

- Email: dawid.bronikowski@outlook.com
- GitHub: https://github.com/Dron3xx-End-to-End
