Step 1: Install Content bundle
---------------------------

Content bundle is installed using [Composer](https://getcomposer.org).

```bash
$ php composer.phar require ongr/content-bundle "~1.0"
```

> ### Elasticsearch bundle
> Please note that this requires Elasticsearch bundle, guide on how to install it
 can be found [here](https://github.com/ongr-io/ElasticsearchBundle/tree/master/Resources/doc/setup.md).


Step 2: Enable Content bundle
---------------------------

Enable Content bundle in your AppKernel:

```php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        // Elasticsearch bundle - should be already added.
        new ONGR\ElasticsearchBundle\ONGRElasticsearchBundle(),
        // The line you need to add.
        new ONGR\ContentBundle\ONGRContentBundle(),
    );  
}
```

Step 3: Add configuration for bundle
-----------------------------

Add minimal configuration for Content bundle.

```yaml
#app/config/config.yml
ongr_content:
    es:
        repositories:
            product: es.manager.default.product
            content: es.manager.default.content
            category: es.manager.default.category
```


In this example, we have set repositories which will be used to fetch data.
> Repositories are being generated by ElasticsearchBundle. To learn more about repositories, click [here](https://github.com/ongr-io/ElasticsearchBundle/blob/master/Resources/doc/usage.md)


Step 4: Adding category fields
------------------------------

To let our services work with your documents you have to include CategoryTrait into your category document.

```php
class Category
{
    use CategoryTrait; 
    // Above adds public properties like: active, hidden, parentId, etc.

    // Other fields ...
}
```


Step 5: Use your new bundle
-----------------------------

Usage documentation for the Content bundle is available [here](index.md).