---
layout: post
title:  "Deploy React App to GitHub Pages"
date:   2023-08-17 12:10:00 +0100
categories: react github pages
tags: [github, pages, react, github actions]
---
It is possible to deploy a React app to GitHub pages.  In this post we will do this using the [gh-pages](https://github.com/tschaub/gh-pages){:target="_blank"} npm package.

<!--more-->

If you want to see these steps in action take a look at this [sample GitHub repository](https://github.com/zjcz/gh-pages-app){:target="_blank"} created for this post.

Note: The following instructions are for deploying a React app created using Create React App.  If you are using a different package to create and manage your React app you may need to make some changes.  The [gh-pages](https://github.com/tschaub/gh-pages){:target="_blank"} documentation contains information for working with Vite and Next.js.

## Prerequisites

Lets assume you already have a React app in GitHub repository.  If not, quickly do it now:

```bash
npx create-react-app gh-pages-app --template typescript
cd gh-pages-app

# - create-react-app will initialise a git repository, 
# - as well as add and commit the initial files
# git init
# git add .
# git commit -m "Initial commit"

git remote add origin <GitHub Repository URL>
git push -u origin main
```

## Deploy to GitHub Pages

To deploy our React app to GitHub Pages, we are going to use an npm package called [gh-pages](https://github.com/tschaub/gh-pages){:target="_blank"}.  This package will copy the static files from the build folder to a branch called gh-pages.  From here GitHub will then copy the files from this branch to the GitHub Pages site.

Lets start by installing the gh-pages package:

```bash
npm install --save gh-pages
```

Next, we need to set the homepage parameter in package.json.  This is required to ensure the correct path is used when your React app is built:

```json
  "homepage": "https://<GitHub Username>.github.io/<Repository Name>",
```

For example:

```json
  "homepage": "https://ghuser.github.io/gh-pages-app",
```

Note: If you want to host your site as a user or organisation site your GitHub repository must be named as your GitHub username + "github.io".  For example, if your GitHub username is ghuser and to host a site at https://ghuser.github.io, the repository must be named "ghuser.github.io".  See [GitHub Pages](https://pages.github.com/) documentation for more information.

Add the following to the "scripts" section of package.json:

```json
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build",
```

To deploy your site, run the following command:

```bash
npm run deploy
```

This will build the app and push the static files to the gh-pages branch on GitHub.  It will also set the relevent GitHub Pages settings for you.  To view these settings, go to the settings page of your GitHub repository and select the Pages option under Code and automation.  The Source is set to "Deploy from a branch" and the branch will be set to our new "gh-pages".

Everytime you want to deploy your site to GitHub Pages simply run the `npm run deploy` command.

## Using GitHub Actions

To automatically deploy the site when you push changes to your GitHub repository, you can use GitHub Actions.

Create a file named .github/workflows/deploy-to-gh-pages.yml in your React project and add the following:

```yaml
name: Deploy to GitHub Pages

on:
  # Runs on pushes to main branch
  push:
    branches:
      - main

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: "Checkout"
        uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: node #latest version
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy with gh-pages
        run: |
          git remote set-url origin https://git:${GITHUB_TOKEN}@github.com/${GITHUB_REPOSITORY}.git
          npx gh-pages -d build -u "github-actions-bot <support+actions@github.com>"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

This will:
- Checkout the code 
- Install Node.js
- Install dependencies
- Build the app
- Deploy the app to GitHub Pages with the gh-pages package

This action will run when you push changes to the main branch of your GitHub repository (either push directly or via a pull request).  If you want to use a different branch, or your main branch is called something else you will need to edit line 7.

Before we commit this, we need to check the permissions within GitHub to make sure the workflow runner has read and write permissions.  Go to the Settings page of your GitHub repository and select the Actions option under Code and automation, then General.  Scroll down to Workflow Permissions and make sure the "Read and write permissions" option is selected.

![Workflow permissions](/assets/images/2023-08-17-github-actions-workflow-permissions-screenshot.png)

Now commit the changes and push to GitHub.  GitHub Actions will automatically run the workflow and deploy.  You can monitor the progress via the "Actions" tab in the GitHub repository project.  Don't forget it is a two part process; the first part is running our action above to copy the files to the gh-pages branch, the second part is GitHub Actions copying the files from the branch to GitHub Pages.  This can take a few minutes and you will see two separate actions running.

## Conclusion

In this post we have seen how to deploy a React app to GitHub Pages using the gh-pages npm package.  We have also seen how to use GitHub Actions to automatically deploy the app when changes are pushed to GitHub.

Remember to take a look at the [sample repository](https://github.com/zjcz/gh-pages-app){:target="_blank"} for this post if you run into any problems.

## Further Reading
- [gh-pages GitHub Repository](https://github.com/tschaub/gh-pages){:target="_blank"}
- [How to use with GitHub Actions? Issue](https://github.com/tschaub/gh-pages/issues/345){:target="_blank"}
- [Deployment - Create React App](https://create-react-app.dev/docs/deployment/#github-pages){:target="_blank"}
- [Sample Repository](https://github.com/zjcz/gh-pages-app){:target="_blank"}
