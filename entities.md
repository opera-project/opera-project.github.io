---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: Entities
toc: true
body_class: body-purple
---

# Create your entity

## command make:entity

Let's say you want to create an Article Entity.

Use `make:entity` command to create your entity Article

`./bin/console make:entity Article`

The command will ask you some questions - answer them to add your properties like title and body.

```
New property name (press <return> to stop adding fields):
 > title

 Field type (enter ? to see all types) [string]:
 > string

 Field length [255]:
 > 255

 Can this field be null in the database (nullable) (yes/no) [no]:
 > no



 Add another property? Enter the property name (or press <return> to stop adding fields):
 > body   

 Field type (enter ? to see all types) [string]:
 > text

 Can this field be null in the database (nullable) (yes/no) [no]:
 > yes
```

To add a field relation between Article and the Media class from the `OperaMediaBundle`:
```
 Add another property? Enter the property name (or press <return> to stop adding fields):
 > image

 Field type (enter ? to see all types) [string]:
 > relation

 What class should this entity be related to?:
 > Opera\MediaBundle\Entity\Media

Relation type? [ManyToOne, OneToMany, ManyToMany, OneToOne]:
 > ManyToOne

 Is the Article.image property allowed to be null (nullable)? (yes/no) [yes]:
 > yes
```

This will create a `Entity/Article.php` and `Repository/ArticleRepository.php`

## Update the database schema
`./bin/console database:schema:update --force`

## Add your entity to easy admin

```yaml
# in the File config/packages/easy_admin.yaml
# more info for this configuration on https://symfony.com/doc/master/bundles/EasyAdminBundle/book/edit-new-configuration.html
easy_admin:

    design:
        menu:
            # [...]
            - { label: 'Content', children: ['Article'] } # Add an 'Article' link in the admin menu

    entities:
        Article:
            class: App\Entity\Article # Add 'Article' class to easy admin entities
            form:
                fields: # customise the shown fields
                    - title
                    - slug
                    - { property: body, type: FOS\CKEditorBundle\Form\Type\CKEditorType }
                    - tags
                    - intro
                    - { property: image, type: Opera\MediaBundle\Form\MediaEntityType }

```

## What to do with your entity

### Listable

If you want to have a block of "top 10 articles", "last 5 articles" or "Articles about XYZ" in your website you can use the ListableContent Block: you have to make your entity listable following the [OperaListBlockBundle](/OperaListBlockBundle) documentation.

It will consist of having your newly created `ArticleRepository` to implements an Interface.

### Create your Custom Block

If you want to create a custom block for your new entity you can follow the [Block System](/blocks) documentation