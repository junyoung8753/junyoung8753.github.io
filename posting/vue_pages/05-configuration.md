---
title: "Configuration"
permalink: /vue/configuration/
excerpt: "Settings for configuring and customizing the theme."
last_modified_at: 2020-08-04T11:26:21-04:00
toc: true
---

Settings that affect your entire site can be changed in [Jekyll's configuration file](https://jekyllrb.com/docs/configuration/): `_config.yml`, found in the root of your project. If you don't have this file you'll need to copy or create one using the theme's [default `_config.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml) as a base.

**Note:** for technical reasons, `_config.yml` is NOT reloaded automatically when used with `jekyll serve`. If you make any changes to this file, please restart the server process for them to be applied.
{: .notice--warning}

Take a moment to look over the configuration file included with the theme. Comments have been added to provide examples and default values for most settings. Detailed explanations of each can be found below.

## Site settings

### Theme

If you're using the Ruby gem version of the theme you'll need this line to activate it:

```yaml
theme: minimal-mistakes-jekyll
```

### Skin

Easily change the color scheme of the theme using one of the provided "skins":
