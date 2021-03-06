# Getting Started With FrameworkSettingsBundle

## Installation

    composer require sumocoders/framework-settings-bundle

Enable the bundle in the kernel.

```php
<?php
// app/AppKernel.php

public function registerBundles()
{
    // ...
    $bundles = array(
        // ...
        new SumoCoders\FrameworkSettingsBundle\SumoCodersFrameworkSettingsBundle(),
    );
}
```

Make sure your database-schema is updated, or at least your migrations are
generated:

    php app/console doctrine:migrations:diff
    php app/console doctrine:migrations:migrate

## Usage

The SettingsManager is available as a service, therefore you can grab it with
the code below

```php
$settingsManager = $this->getContainer()->get('framework.settings_manager');
```

As the code implements (partially) the ParameterBagInterface you are able to
`add`, `set`, `get` settings.

On the `get`-call a extra parameter is added which contains a default-value,
which will be returned when the setting doesn't exists. Warning: it wont be
stored if the default-value is returned.

```php
$settingsManager = $this->getContainer()->get('framework.settings_manager');
$willReturnDefaultValue = $settingsManager->get(
    'this.does.not.exists',
    'Default Value'
);
```

## Usage in templates

Also added is a Twig function so you can easily access settings in the templates.
You can do this as follows:

```html
{{ setting('this.is.a.setting.key') }}
```
