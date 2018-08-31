---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: Quick Setup
body_class: body-green
---

## From project

The easyiest way to try playing is clone the sample project here `https://github.com/opera-project/opera-cms`

add the opera pages to your routing file `config/routes.yaml`
```
_opera_page:
  path: /{_opera_page_path}
  defaults:
      _opera_page_path: /
  requirements:
      _opera_page_path: .+
```

---
## From composer with flex

Waiting PR in merge

---
## From composer without flex


### Create an Opera project

In your command console execute the following command:

```
composer create-project -s dev opera-project/skeleton:1.0.x-dev example
```

This command creates a new directory called `example` that contains a new symfony project using opera.

### Configure database

Presently, your database is not configured, you will not have permission.
You must edit the `DATABASE_URL` in your `.env` file

### Finish install

You can now use `make init` command in your project folder. It will create the database according to your `DATABASE_URL` and load the schema and fixtures.

### Run Server

You can now start the web server:
`./bin/console server:run`

The admin will be available on [http://localhost:8000/admin](http://localhost:8000/admin){:target="_blank"} using `cedric` as username and `demo` as password.

### Next steps

**This skeleton contains these bundles:**

- [OperaTextBlockBundle](/OperaTextBlockBundle) (Manage block of text, script, static contents)
- [OperaListBlockBundle](OperaListBlockBundle) (Manage block of list of content)
- [OperaMediaBundle](OperaMediaBundle) (Manage media, upload files)
- [OperaTaxonomyBundle](OperaTaxonomyBundle) (Manage tags)

You can now:
- [create your own entities](/entities)
- [implement a layout](/layouts) for your website
- [create your own block](/blocks)

### Things to know

Opera Project use EasyAdmin admin generator. You might want to take a look at their [documentation](https://symfony.com/doc/current/bundles/EasyAdminBundle/index.html){:target="_blank"} in the near futur.
