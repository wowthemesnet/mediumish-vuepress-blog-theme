
# Demo 

https://wowthemesnet.github.io/vuepress-theme-mediumish/

[mediumish vuepress blogging theme!](https://wowthemesnet.github.io/vuepress-theme-mediumish/assets/img/screenshot.jpg)

# Install

Install packages

```
yarn
```

Run server

```
vuepress dev docs
```

## Use

Go to Docs and start editing or adding MD posts. 

For some reason, you might need to re-run `vuepress dev docs --no-cache` if you don't see the changes.

// To do: extended documentation on use.

## Ready for Production

Build for production

```
vuepress build docs
```

## Or even better, I have prepared an automatic deployment to Github if you want to use Github pages:

1. Create your Github repo.
2. Go to `docs/.vuepress/config.js` and edit `base: '/vuepress-theme-mediumish/'` with your own REPO
3. Go to `deploy.sh` and edit `git push -f git@github.com:wowthemesnet/vuepress-theme-mediumish.git master:gh-pages` with your own Github username & REPO.
4. From your terminal `bash deploy.sh`.



