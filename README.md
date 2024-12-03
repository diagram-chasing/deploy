# Deploy

Sample repository for a GitHub Actions workflow to deploy `Preview` and `Production` site builds on Cloudflare Pages or Netlify. Template site used [here](https://github.com/thedivtagguy/starter/)

## New project setup

### Cloudflare Pages

- In the GitHub repository, create 2 secrets inside the repository `Settings`:
  - `CLOUDFLARE_ACCOUNT_ID`
  - `CLOUDFLARE_API_TOKEN`
- In Cloudflare, create a Pages project with a name `$PROJECT_NAME` and default branch as `master`. Project creation can be done using the `wrangler` CLI provided by Cloudflare: `wrangler pages project create`
- In the GitHub repository, copy over the `cf-pages-*` files under `.github/workflows` from this repository.
- Edit the `projectName: 'diagram-chasing'` line near the bottom, replacing `diagram-chasing` with the Pages project name (`$PROJECT_NAME`)

### Netlify

- In Netlify, create a Site with a name `$SITE_NAME`. Site creation can be done using the `netlify` CLI provided by Netlify: `netlify sites:create`
- In the GitHub repository, create 2 secrets inside the repository `Settings`:
  - `NETLIFY_AUTH_TOKEN`
  - `NETLIFY_SITE_ID`
- In the GitHub repository, copy over the `netlify-*` files under `.github/workflows` from this repository.

- Replace the `baseURL` and `analyticsID` in `package.json` with the Netlify URL and Plausible Analytics ID. Base URL corresponds to where the site is being deployed on Netlify, (no prefix like `preview--`).

## Using the workflow

- Go to the `Actions` section of the GitHub repository to view the configured workflows.
- `Preview Deploy` workflow automatically runs on every commit to `master`. Manual trigger can be done from the `Actions` section of the GitHub repository, or using the [`gh` CLI](https://cli.github.com/manual/gh_workflow_run)
- `Production Deploy` workflow needs to be manually triggered.

## Deployment URL format

### Cloudflare Pages

- Preview: `https://preview.$PROJECT_NAME.pages.dev`
- Production: `https://$PROJECT_NAME.pages.dev`

### Netlify

- Preview: `https://preview--$SITE_NAME.netlify.app`
- Production: `https://$SITE_NAME.netlify.app`

## Publishing the site

On the main site, create a `_redirects` file to configure the required redirect.
