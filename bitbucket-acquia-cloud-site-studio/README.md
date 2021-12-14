# Bitbucket-Acquia-Cloud-Site-Studio

This project was developed with a team of 7 developers, several QA people.

### Project Set-up

- Bitbucket for Git repository
- Acquia Cloud Enterprise for hosting
    - Note this project had additional non-production environments to support separate QA and UAT, an extra pre-QA environment during development (INTDEV) and a second work stream (DEV2 and INTDEV2).  Most references to the additional environments were removed.
- Acquia Site Studio for theming
- Acquia Pipelines for CI/CD
- Acquia BLT to support development workflows
- Did NOT use Acquia Lightning or Acquia CMS.  The project originally started using Lightning but it was removed early in the project as project requirements diverged from Lightning assumptions.

Documentation was created and maintained in Confluence, exported to PDFs, converted to Word using Adobe Acrobat when I realized Pandoc doesn't accept PDF as an input, converted with Pandoc to Commonmark, then sanitized.  The random directories inside the media directory were generated during the Pandoc conversion to avoid different documents outputting the same file name and overwriting each other.

### Structure on Confluence

The documentation files were organized in Confluence as follows:

- Development
    - Development Process
        - Acquia Spec Tool
        - Custom Module Naming and Packaging
        - Config Split Definition
        - GIT Process
            - GIT Repository Structure (not included here)
            - Git Conventions and Standards
            - Deploying code from the DEVELOP branch to STAGE branch
            - Deploying code from the STAGE branch to MASTER branch
            - Creating and Deploying a HOTFIX for Production
        - Workflows
            - Individual Development Workflow
            - Site Studio Development Process
            - Code Review Process
            - Acquia Deployments
            - Cloud Hooks Code Deployment
            - Initializing an Environment for Migration
            - Drupal Security Core/Module Updates
            - Drupal Core/Module Updates
            - Upgrading the Cohesion Modules
        - Cloud IDEs and Local Development Environments
            - Setting up a Cloud IDE
            - Acquia Cloude IDE Tips and Tricks (not included here)
            - Local Development Environment Setup using DDEV
            - Local Development Environment Setup using Lando
            - VS Code Extensions and Configurations