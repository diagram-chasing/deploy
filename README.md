# Deploy

Sample repository for a GitHub Actions workflow to deploy `Preview` and `Production` site builds on Cloudflare Pages. Template site used [here](https://github.com/thedivtagguy/starter/)

## New project setup

- In the GitHub repository, create 2 secrets inside the repository `Settings`:
    - `CLOUDFLARE_ACCOUNT_ID` 
    - `CLOUDFLARE_API_TOKEN`
- In Cloudflare, create a Pages project with a name `$PROJECT_NAME` and default branch as `master`. Project creation can be done using the `wrangler` CLI provided by Cloudflare: `wrangler pages project create`
- In the GitHub repository, copy over the files under `.github/workflows` from this repository.
- Edit the `projectName: 'diagram-chasing'` line near the bottom, replacing `diagram-chasing` with the Pages project name (`$PROJECT_NAME`)

## Using the workflow

- Go to the `Actions` section of the GitHub repository to view the configured workflows.
- `Preview Deploy` workflow automatically runs on every commit to `master`. Manual trigger can be done from the `Actions` section of the GitHub repository, or using the [`gh` CLI](https://cli.github.com/manual/gh_workflow_run)
- `Production Deploy` workflow needs to be manually triggered.

## Deployment URL format

- Preview: `https://preview.$PROJECT_NAME.pages.dev`
- Production: `https://$PROJECT_NAME.pages.dev`

## Publishing the site

On the main site, create a `_redirects` file that points the required subpath to the Production deploy on Cloudflare
