# Usage

This repo is a Jekyll site and theme using the GitHub Pages build pipeline. The site is published from the `master` branch, and the `origin` remote is set to `https://github.com/quidscio/quidscio.github.io.git`.

Do NOT edit/commit from Windows. Use WSL instead to ensure action script execute bits remain set. 

## Prerequisites

- Ruby 3.2 (matches CI)
- Bundler (`gem install bundler`)

## Local preview workflow

1) Install dependencies:

   `script/bootstrap`

2) Run the local server:

   `bundle exec jekyll serve`

3) Open the preview:

   `http://127.0.0.1:4000/`

Jekyll rebuilds as you edit files; refresh the browser to see updates.

## Publish workflow (GitHub Pages)

1) Check changes:

   `git status`

2) Commit:

   `git add -A`
   `git commit -m "Update site"`

3) Push to GitHub:

   `git push origin master`

GitHub Pages will build and publish the site at `https://quidscio.github.io/`.

## Workflow coexistence 

Local preview runs locally w/o impacting GH publishing. 
Publishing happens with a push to `origin` on `master`.

## Known issues and notes

- none? 