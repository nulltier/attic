# mdbook

Static site generator designed for the online documentation

## Hosting on github pages

Do not forget to add `output.html.cname` property into book.toml if you are hosting site on the 
github pages under a custom domain

```toml

[output.html]
cname = "attic.anzo.me"

```

Without it github pages will be switching your site back on a default domain (example, 
`https://anzome.github.io/attic/`). Manual change after each deployment will be needed.