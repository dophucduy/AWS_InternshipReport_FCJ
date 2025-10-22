# AWS System Manager Workshop

This is a Hugo-based workshop site for AWS System Manager.

## GitHub Pages Deployment

This site is configured to deploy to GitHub Pages using the `docs` directory.

### Setup Instructions

1. Go to your repository's Settings > Pages
2. Under "Source", select "Deploy from a branch"
3. Under "Branch", select your main branch and choose `/docs` as the folder
4. Click "Save"

The site will be automatically deployed from the `docs` directory.

## Local Development

To build the site locally:

```bash
hugo
```

This will generate the site in the `docs` directory (as configured in `config.toml`).

To serve the site locally:

```bash
hugo server
```

Then visit http://localhost:1313 in your browser.
