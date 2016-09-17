# CacheTags - Laravel blade partial caching

[![Build Status](https://travis-ci.org/Perturbatio/CacheTags.svg?branch=master)](https://travis-ci.org/Perturbatio/CacheTags)
[![Latest Stable Version](https://poser.pugx.org/perturbatio/cachetags/v/stable?format=flat)](https://packagist.org/packages/perturbatio/cachetags)
[![Latest Unstable Version](https://poser.pugx.org/perturbatio/cachetags/v/unstable?format=flat)](https://packagist.org/packages/perturbatio/cachetags)
[![License](https://poser.pugx.org/perturbatio/cachetags/license?format=flat)](https://packagist.org/packages/perturbatio/cachetags)
[![Total Downloads](https://poser.pugx.org/perturbatio/cachetags/downloads?format=flat)](https://packagist.org/packages/perturbatio/cachetags)

This package is intended to allow you to cache portions of a web page by marking them using blade directives.

You can specify how long the partial will be cached for as well as naming it (to allow you to invalidate it if needed).

## Installation

Install it as a composer package with

```
composer require perturbatio/cachetags
```

Add `Perturbatio\CacheTags\CacheTagsProvider::class` to your config/app.php providers array

Add `'CacheTags' => Perturbatio\CacheTags\CacheTags::class` to your aliases

Then publish the config file with `php artisan vendor:publish --tag=config` this will create a `cachetag.php` config file in `/config`

## Usage

### Caching items

#### Blade

```Blade
@cachetagStart('super-cool-widget', 15) <!-- menu cached for 15 minutes -->
<?=superCoolWidgetThatTakesTooLongToGenerate();?>
@cachetagEnd()
```

#### PHP

```PHP
if ( cachetagHas('super-cool-widget') ){
  echo cachetagGet('super-cool-widget');
} else {
  cachetagStart('super-cool-widget', 15);
  echo superCoolWidgetThatTakesTooLongToGenerate();
  echo cachetagEnd();
}
```

### Clearing items

#### Blade

```Blade
@cachetagClear('super-cool-widget')
```

#### PHP

```PHP
//clear the cache for a specific key
cachetagClear('super-cool-widget');
````
