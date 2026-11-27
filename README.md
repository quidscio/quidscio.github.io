# Quid scio?

This repository is the Markdown source for [Quid scio?](https://quidscio.github.io/), a Jekyll site using the Midnight theme. GitHub Pages builds from the root of `origin/master`. Each post on GitHub Pages is the primary version.

## Author and review posts

Follow the [post-authoring procedure](docs/Post-authoring-procedure_md-pages-LI.md) for filenames, front matter, approval, and preparing LinkedIn Article copy. Keep post sources in `_posts/` and their images in `assets/images/`.

Posts show publication dates above the title and previous/next links at both ends. The desktop reading column is capped at 1,000px and the mobile layout uses Midnight's existing sizing.

## Preview locally in WSL

Use WSL for edits and commits so the executable bits on the build scripts are preserved. The local Ruby version is pinned in `.ruby-version` to 3.2.6. The current WSL bundle uses Bundler 2.6.3, which is also the version used by CI. Install any missing project gems with `bundle install`.

```bash
bundle check
bundle exec jekyll serve --livereload --force_polling
```

Open the [local posts index](http://127.0.0.1:4000/posts/). On a Windows-mounted checkout, polling lets Jekyll detect saves from Windows editors. Restart Jekyll when changing `_config.yml`.

## Validate and publish

Run `script/cibuild` in WSL to build the site in production mode and run HTMLProofer, RuboCop, and W3C HTML and CSS validation. HTMLProofer checks the generated site's internal links and assets. Check important external links separately.

Review the diff and stage only the approved posts and assets. A local commit records the change. Pushing `master` publishes it through GitHub Pages.

After an authorized push, confirm that both CI and the Pages deployment pass for the pushed commit. Open the deployed post and check its visible publication date, canonical URL, and images. [Repository Actions](https://github.com/quidscio/quidscio.github.io/actions)
