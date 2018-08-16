---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: OperaTextBlockBundle
body_class: body-pink
---

This bundle [OperaTextBlockBundle](https://github.com/opera-project/OperaTextBlockBundle){:target="_blank"} will help you to easily manage static texts usefull to add some js, static content like ads, or image... 

## Installation

````
composer require opera-project/text-block-bundle
````

### Want a ckeditor because static html is not so funny ?

````
composer require friendsofsymfony/ckeditor-bundle
php bin/console ckeditor:install
php bin/console assets:install public
````

## And after ?

Thats all refresh your admin and you will see the text block is ready to use !!