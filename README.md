# Twig components extension

[![Latest Version on Packagist](https://img.shields.io/packagist/v/performing/twig-components.svg?style=flat-square)](https://packagist.org/packages/performing/twig-components)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/giorgiopogliani/twig-components/Tests)](https://github.com/giorgiopogliani/twig-components/actions?query=workflow%3ATests+branch%3Amaster)
[![Total Downloads](https://img.shields.io/packagist/dt/performing/twig-components.svg?style=flat-square)](https://packagist.org/packages/performing/twig-components)

This is a twig extension for automatically create components as tags. The name of the tag is based on files in a directory. This is highly inspired from blade components.  

## Installation

You can install the package via composer:

```bash
composer require performing/twig-components
```

## Usage

You can create the twig extension that will find all the files in the given directory and create the component tag.
```php
$extension = new \Performing\TwigComponents\ComponentExtension(
    '/absoulute/path/to/components/directory',
    '/relative/twig/components/directory',
);
```

For example, Craft CMS users can do the following:
```php
Craft::$app->view->registerTwigExtension(
    new \Performing\TwigComponents\ComponentExtension(
        CRAFT_BASE_PATH . '/templates/components',
        '/components',
    )
);
```

Next you can create a file in the components directory like this.
```twig
{# /components/button.twig #}
<button {{ attributes.merge({ class:'text-white rounded-md px-4 py-2' })|raw }}>
  {{ slot }}
</button>
```

Use the new created tag.
```twig
{# /index.twig #}
{% button with {class:'bg-blue-600'} %}
  <span class="text-lg">Click here!</span>
{% endbutton %}
```

The output generated will be like this.
```html
<button class="bg-blue-600 text-white rounded-md px-4 py-2">
  <span class="text-lg">Click here!</span>
</button>
```

## Testing

``` bash
composer test
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
