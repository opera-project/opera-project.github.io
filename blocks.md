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

This will generate the service block and the twig template sample

In the service you have to implements :

- `getVariables(Block $block)` : array to return the twig variables needed for template
- `getType()` : string the type of block for db stored name
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

The `$block` is automatically also passed inside your template to give you the way to get the current block instance. 


With the given example in your twig you can use

```` twig
dump(article) - To get the article
dump(block.configuration) - To get the article configuration
````

### The getType method

This method have to return one unique name that is the identifier of your block inside the database. This will also be the translation key for your block to have one human name inside the backend.

```` php
public function getType() : string
{
    return 'article';
}
````

### The createAdminConfigurationForm(FormBuilderInterface $builder)

Sometime, your block require configuration, that means it does not just use the request context but for example have to be filtered on one category. So to build your `getVariables` you need to get some user defined configuration.

To do that, just configure the admin form with :

```` php
use Opera\CoreBundle\Form\Type\CkEditorOrTextareaType;

public function createAdminConfigurationForm(FormBuilderInterface $builder)
{
    $builder->add('text', CkEditorOrTextareaType::class);    
}
````

You can use all of the symfony [form types](https://symfony.com/doc/current/forms.html) and all of this configuration will be persisted inside `$block->getConfiguration()`

## Define a custom template 

By default the getTemplate return `sprintf('blocks/%s.html.twig', $this->getType());` so the template is something like `templates/blocks/article.html.twig`

Just override : `getTemplate(Block $block)`

For exemple if you want a template that depend of configuration :

```` php
use Symfony\Component\Form\Extension\Core\Type\ChoiceType;

public function createAdminConfigurationForm(FormBuilderInterface $builder)
{
    $builder->add('template', ChoiceType::class, [
        'choices' => [
            'Super template' => 'example.html.twig',
            'Super template 2' => 'example2.html.twig',
        ],
    ]);    
}

public function getTemplate(Block $block)
{
    return sprintf('blocks/my-block/%s', $block->getConfiguration()['template']);    
}
````
