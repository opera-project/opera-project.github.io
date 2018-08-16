---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: doc
title: OperaMediaBundle
body_class: body-pink
---

The bundle [OperaMediaBundle](https://github.com/opera-project/OperaMediaBundle){:target="_blank"} provides a way to manage media for opera-project cms:
- media manager
- upload of files
- media picker widget for form and also ckeditor

## Installation

````
composer require opera-project/media-bundle
````

## Configuration

### Configure require bundle Gaufrette and LiipImagine

The OperaMediaBundle use [KnpGaufretteBundle](https://github.com/KnpLabs/KnpGaufretteBundle){:target="_blank"} and [LiipImagineBundle](https://github.com/liip/LiipImagineBundle){:target="_blank"}.

You must configure your adapters and filesystems that will be used.

```yaml
# exemple
knp_gaufrette:
    stream_wrapper: ~
    adapters:
        images:
            local:
                directory: '%kernel.project_dir%/images'
                
    filesystems:
        images:
            adapter: images

liip_imagine:
    data_loader: opera_media.chain_loader
    filter_sets:
        opera_thumbnail:
            quality: 75
            filters:
                thumbnail: { size: [120, 120], mode: outbound }
```

### Configure OperaMediaBundle

Configure the list of sources your project will use and the filesystem that will be used

```yaml
# config.packages/opera_media.yaml
opera_media:
    sources:
        images:
            filesystem: gaufrette.images_filesystem
            wrapper: gaufrette://images/
```

## Media Manager

You will now have a media manager on the route `opera_admin_media_list` with the list of your configured sources (here, 'image' and 'toto') and their folders and media.

![MediaManager](images/OperaMediaBundle/manager.png)

## Form Types, Image picker

There is two media form type used for the media picker:
- `Opera\MediaBundle\Form\MediaEntityType`
- `Opera\MediaBundle\Form\MediaTextType`

`MediaEntityType` is an EntityType of Media entity.
`MediaTextType` is the same but act as a TextType but use the path of the media.

Both use a custom widget design to show the MediaManager.

## Add Media Picker plugin to CKEDITOR

To add a button in your CKEditor to open a MediaPicker to insert a image you must add the `opera_media_picker` plugin in your plugins list and used config:

```yaml
fos_ck_editor:
    default_config: opera
    plugins:
        opera_media_picker:
            path:     "/bundles/operamedia/opera_media_picker/" # with trailing slash
            filename: "plugin.js"
    configs:
        opera:
            extraPlugins: "opera_media_picker"
```