---
comments: true
tags:
  - howto
---
# How to upgrade

Upgrade to the latest version with:

```
pip install --upgrade --force-reinstall mkdocs-material
```

Show the currently installed version with:

```
pip show mkdocs-material
```

## Upgrading from 8.x to 9.x

This major release includes a brand new search implementation that is faster
and allows for rich previews, advanced tokenization and better highlighting.
It was available as part of Insiders for over a year, and now that the funding
goal was hit, makes its way into the community edition.

### Changes to `mkdocs.yml`

#### `content.code.copy`

The copy-to-clipboard buttons are now opt-in and can be enabled or disabled
per block. If you wish to enable them for all code blocks, add the following
lines to `mkdocs.yml`:

``` yaml
theme:
  features:
    - content.code.copy
```

#### `content.action.*`

A "view source" button can be shown next to the "edit this page" button, both
of which must now be explicitly enabled. Add the following lines to
`mkdocs.yml`:

``` yaml
theme:
  features:
    - content.action.edit
    - content.action.view
```

#### `navigation.footer`

The _previous_ and _next_ buttons in the footer are now opt-in. If you wish to
keep them for your documentation, add the following lines to `mkdocs.yml`:

``` yaml
theme:
  features:
    - navigation.footer
```

#### `theme.language`

The Korean and Norwegian language codes were renamed, as they were non-standard:

- `kr` to `ko`
- `no` to `nb`

#### `feedback.ratings`

The old, nameless placeholders were removed (after being deprecated for several
months). Make sure to switch to the new named placeholders `{title}` and `{url}`:

```
https://github.com/.../issues/new/?title=[Feedback]+{title}+-+{url}
```

### Changes to `*.html` files

The templates have undergone a series of changes. If you have customized
Material for MkDocs with theme extension, be sure to incorporate the latest
changes into your templates. A good starting point is to [inspect the diff].

!!! warning "Built-in plugins not working after upgrade?"

    If one of the built-in plugins (search or tags) doesn't work anymore without
    any apparent error or cause, it is very likely related to custom overrides.
    [MkDocs 1.4.1] and above allow themes to namespace built-in plugins, which
    Material for MkDocs 9 now does in order to allow authors to use third-party
    plugins with the same name as built-in plugins. Search your overrides for
    [`"in config.plugins"`][in config.plugins] and add the `material/` namespace.
    Affected partials:

    - [`content.html`][content.html]
    - [`header.html`][header.html]

  [inspect the diff]: https://github.com/squidfunk/mkdocs-material/pull/4628/files#diff-3ca112736b9164701b599f34780107abf14bb79fe110c478cac410be90899828
  [MkDocs 1.4.1]: https://github.com/mkdocs/mkdocs/releases/tag/1.4.1
  [in config.plugins]: https://github.com/squidfunk/mkdocs-material/search?q=%22in+config.plugins%22
  [content.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/content.html
  [header.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/header.html
