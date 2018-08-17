---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: OperaTaxonomyBundle
body_class: body-pink
---

The bundle [OperaTaxonomyBundle](https://github.com/opera-project/OperaTaxonomyBundle){:target="_blank"} provide a easy way to manage tags for opera-project cms

## Installation

````
composer require opera-project/taxonomy-bundle
````

```yaml
# config/packages/easy_admin.yaml
imports:
    - { resource: "@OperaTaxonomyBundle/Resources/config/easy_admin.yaml" }

easy_admin:
    design:
        menu:
            #...
            - { label: 'Taxonomy', children: ['Tag'] }

```


## Usage

```php
namespace App\Entity;

use Opera\TaxonomyBundle\Taggable\Traits\TaggableEntity;

class Article
{
    use TaggableEntity;
}
```

Now you can use tags for example with the [OperaListBlockBundle](/OperaListBlockBundle)