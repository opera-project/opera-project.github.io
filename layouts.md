---
layout: doc
title: The layout
body_class: body-blue
---

The layout is the html structure of your view, it is composed of *areas*

The layout is composed of :

- 1 twig file
- 1 entry in database (table layout)

## The database entry

See [https://github.com/opera-project/opera-cms/blob/master/src/DataFixtures/LayoutFixtures.php](https://github.com/opera-project/opera-cms/blob/master/src/DataFixtures/LayoutFixtures.php)

```` php
$layout = new Layout();
$layout->setName('default');
$layout->setConfiguration([
    'areas' => [
        'H' => 'header',
        'B' => 'body'
    ],
    'layout' => [
        'H H H H',
        'B B B B',
        'B B B B',
    ]
]);
$manager->persist($layout);
$manager->flush();
````

- setName : have to be unique inside of your project, it correspond to the twig file name that will be setted inside `templates/layouts/NAME.html.twig`
- setConfiguration : is the area configuration

The configuration declare some areas that will be used inside of the template. And associate them to one letter.
After you have to configure the layout representation using this letters. The syntax is based on css grid-template.

## The template


### Layout template

```twig
{% raw %}
{# in file templates/layouts/NAME.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    {{ cms_area('header', _opera_page) }}
    {{ cms_area('header') }}

    <hr />
    {{ cms_area('body', _opera_page) }}

{% endblock %}
{% endraw %}
```

The twig function `cms_area(area_name, ?page)` will show the list of blocks attached to the given area name. If page is not given it will call the area for `_global` page usefull for common elements like menu for example.

**the _global page**

You must have a `global` page. The `_global` page doesn't have a layout and will never be rendered.
The global page have all the commons block that are used on all the page (menu, footer...) so you don't have to configure them on all the pages.

### Base template

```twig
{% raw %}
{# in file templates/base.html.twig #}
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}{{ cms_render(_opera_page.title) }}{% endblock %}</title>
        <meta name="description" content="{{ _opera_page.metaDescription }}" />
        <meta name="keywords" content="{{ _opera_page.metaKeyword }}" />

        {% block stylesheets %}{% endblock %}
    </head>
    <body>
        {% block body %}{% endblock %}
        {% block javascripts %}{% endblock %}
    </body>
</html>
{% endraw %}
```

You can also directly show all elements of page object. But for title, or other if you want, we recommand you to use the `cms_render` function: this call will enable your user to save twig template inside of the page to render elements that depends of PageController context. Eg the title of the current article we will save in database `{% raw %}$page->setTitle('{{ article.title }}');{% endraw %}` and this will render the article title.

