---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: OperaTwigBlockBundle
body_class: body-pink
---

This bundle [OperaTwigBlockBundle](https://github.com/opera-project/OperaTwigBlockBundle){:target="_blank"} will help you to easily add twig code in your blocks

## Installation

````
composer require opera-project/twig-block-bundle
````

## Usage

You can already add some js, static content like ads, or image using a [OperaTextBlockBundle](OperaTextBlockBundle)...
Well, with the OperaTwigBlockBundle you can also add twig code.

Instead of some static code like 

```html
<div class="container">
    <div class="row">
        <div class="col-lg-12">
            <h1 class="text-center">Hello This is my static title</h1>
            <a href='/my_link'>
        </div>
    </div>
</div>
```

You can use the twig variables available on the current page context

```html
{% raw %}
<div class="container">
    <div class="row">
        <div class="col-lg-12">
            <h1 class="text-center">{{ block.name }} - {{ _opera_page.title }}</h1>
        </div>
    </div>
</div>
{% endraw %}
```

<!-- todo doc how to add variable in context of page -->
