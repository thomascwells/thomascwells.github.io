---
title: "Steps for publishing"
editor_options: 
  chunk_output_type: console
engine: knitr
---

# Setup R session

These things get the R session ready to run the commands below.

Check the versions of your R packages to make sure nothing has changed.

```{r}
renv::status()
```

Load useful libraries

```{r}
library('quarto')
library('rmarkdown')
library('knitr')
library('httpuv')
```


# Make edits

Make your edits to local files and save changes.

Use the `quarto_preview()` command below to view the output locally. 

Changes you make and save to local files should trigger automatic updates of the preview window.

```{r}
quarto::quarto_preview()
```

```{r}
quarto_preview_stop()
```

# Render 

After you're satisfied with your changes, but before commiting changes and publishing, use the `quarto_render()` command below or the `Render` button in the toolbar to check that everything works (one more time).

The render command below will just render the site. 

The Render button in the toolbar will render the site then attempt to launch a preview window of that rendered site so you can QC it.

If you want to use the Render button, make sure you're viewing the `index.qmd` file when you do.

```{r}
quarto::quarto_render()
```

# Publish - first time

The first time you publish your site, you will have extra steps to get it setup. 

First, save any changes, then commit and push those changes.

## Set up site for publishing

Follow the instructions here: 

https://quarto.org/docs/publishing/github-pages.html#publish-command

Make sure the `.gitignore` file is updated. 

Also make sure the `publish.yml` github action file is added to the `.github` dir.

One key part of the instructions above will be running this command.

```{r}
system2('quarto', "publish gh-pages")
```

After the publish happens, check that it worked by going to this url: 

https://{{you_gh_user_name}}.github.io

If that looks good, proceed to setting up the redirect to point your domain to that published site.

## Set up domain for publishing

- Add domain to cloudflare
- follow github instructions for creating CNAME and A records for github
- Add domain to gh-pages portion of repo settings 

# Publish - every time after first time

After the initial publish is configured, any edits you make to the files in the main branch should trigger an automatic re-render and publish on github (no need to republish yourself). 

You can either make edits in RStudio, then commit and push those changes, or you can make edits directly to the files in github. 

