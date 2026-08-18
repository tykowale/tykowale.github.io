# tykowale.github.io

This is Ty Kowalewski's personal site, built with [Hugo](https://gohugo.io/) using the [Congo](https://jpanther.github.io/congo/) theme and deployed to GitHub Pages with GitHub Actions.

## How the Site Is Organized

- `content/` contains site pages and blog posts.
- `content/posts/` contains blog posts written in Markdown.
- `config/_default/` contains Hugo and Congo theme configuration.
- `themes/congo/` is the Congo theme, installed as a Git submodule.
- `layouts/` contains small local theme overrides, if needed.
- `static/` contains files copied directly into the published site.
- `static/CNAME` preserves the custom GitHub Pages domain.
- `.github/workflows/hugo.yaml` builds and deploys the site on every push to `main`.

## Local Setup

Install Hugo Extended:

```sh
brew install hugo
```

If this is a fresh clone, initialize the theme submodule:

```sh
git submodule update --init --recursive
```

Run the local development server:

```sh
hugo server -D --renderToMemory
```

Then open the local URL printed by Hugo, usually `http://localhost:1313/`.

The development config in `config/development/` makes local asset URLs point at the Hugo server instead of the production domain. `--renderToMemory` keeps local preview output separate from the production `public/` build.

## Writing a Blog Post

Create a new post:

```sh
hugo new content posts/my-post-title.md
```

Edit the new file in `content/posts/`. Hugo creates new posts as drafts by default:

```yaml
draft: true
```

Set `draft: false` when the post is ready to publish.

## Publishing

Commit and push changes to `main`:

```sh
git add .
git commit -m "Update site"
git push origin main
```

GitHub Actions will build the Hugo site and deploy the generated `public/` output to GitHub Pages.

In the repository settings, GitHub Pages should use **GitHub Actions** as the deployment source.

## Updating the Theme

Congo is installed as a Git submodule. To update it:

```sh
git submodule update --remote --merge themes/congo
hugo --gc --minify
```

Commit the submodule pointer update if the build looks good.

## Custom Domain

The custom domain file lives at `static/CNAME` so Hugo includes it in the published site. Keep this file when changing the site structure.
