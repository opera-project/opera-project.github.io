---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: The block System
toc: true
body_class: body-pink
---

## How to create a new kind of block

Run the symfony command : `bin/console make:block sample` (write name of block in lower case)

This will generate the service block And the twig template sample

In the service u have to implements :

- `getVariables(Block $block)` : array to return the twig variables needed for template
- `getType(Block $block)` : string the type of block for db stored name
- `createAdminConfigurationForm(FormBuilderInterface $builder)` the configurable part of your bundle

### The getVariables method

The getVariables define the variables that can be used in the template.

```` php
    public function getVariables(Block $block) : array
    {
        return [
            'article' => $this->requestStack->getCurrentRequest()->get('article'),
        ];
    }
````

The `$block` is automatically also passed inside your template to give u the way to get the current block instance. 


With the given example in your twig u can use

```` twig
dump(article) - To get the article
dump(block.configuration) - To get the article configuration
````

## Define a custom template 

Just override : `getTemplate(Block $block)`

