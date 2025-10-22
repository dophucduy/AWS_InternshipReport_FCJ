# GitHub Pages Deployment Setup

## Issue Resolution

The question "why I cant see any deployment, is there a different choice: root or docs" has been addressed.

## What Changed

1. **Hugo Configuration Updated**: The `config.toml` now includes `publishDir = "docs"` to ensure Hugo builds the site into the `docs` directory instead of the default `public` directory.

2. **Docs Directory Created**: All site content has been generated in the `docs` directory, which is one of the two options GitHub Pages supports for branch-based deployments.

## GitHub Pages Configuration

GitHub Pages allows you to deploy from either:
- **Root directory** (`/`) - deploys from the repository root
- **Docs directory** (`/docs`) - deploys from the docs folder (recommended for Hugo sites)

This repository is now configured to use the **docs directory** option.

## Setup Steps

To enable GitHub Pages deployment, follow these steps:

1. Navigate to your repository on GitHub: https://github.com/dophucduy/AWS_WorkShop_FCJ

2. Click on **Settings** (in the repository menu)

3. In the left sidebar, click on **Pages**

4. Under **Source**:
   - Select "Deploy from a branch"
   
5. Under **Branch**:
   - Select your main branch (e.g., `main` or `master`)
   - Select `/docs` from the folder dropdown
   - Click **Save**

6. GitHub will start deploying your site. After a few moments, you'll see a message with your site's URL (typically: https://dophucduy.github.io/AWS_WorkShop_FCJ/)

## Verification

Once deployed, you should be able to access your AWS System Manager workshop at:
- https://dophucduy.github.io/AWS_WorkShop_FCJ/

The site includes both English and Vietnamese language versions.

## Future Updates

When you make changes to the workshop content:

1. Edit the markdown files in `000058-SessionManager/000058-SessionManager/content/`
2. Rebuild the site using `hugo` command (from the Hugo project directory)
3. Commit and push the changes in the `docs` directory
4. GitHub Pages will automatically redeploy the updated site

## Troubleshooting

If you don't see the deployment option:
- Make sure the repository is public (GitHub Pages requires a paid plan for private repositories)
- Ensure you have the necessary permissions on the repository
- Check that the `docs` folder exists in your repository

For more information, see: https://docs.github.com/en/pages/getting-started-with-github-pages
