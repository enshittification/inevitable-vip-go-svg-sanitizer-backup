# svg-sanitizer

## Note

This fork is currently in use by [vip-go-ci](https://github.com/automattic/vip-go-ci).

# Introduction

This is my attempt at building a decent SVG sanitizer in PHP. The work is laregely borrowed from [DOMPurify](https://github.com/cure53/DOMPurify).

## Installation

Either require `enshrined/svg-sanitize` through composer or download the repo and include the old way!

## Usage

Using this is fairly easy. Create a new instance of `enshrined\svgSanitize\Sanitizer` and then call the `sanitize` whilst passing in your dirty SVG/XML

**Basic Example**

```php
use enshrined\svgSanitize\Sanitizer;

// Create a new sanitizer instance
$sanitizer = new Sanitizer();

// Load the dirty svg
$dirtySVG = file_get_contents('filthy.svg');

// Pass it to the sanitizer and get it back clean
$cleanSVG = $sanitizer->sanitize($dirtySVG);

// Now do what you want with your clean SVG/XML data

```

## Output

This will either return a sanitized SVG/XML string or boolean `false` if XML parsing failed (usually due to a badly formatted file).

## Options

You may pass your own whitelist of tags and attributes by using the `Sanitizer::setAllowedTags` and `Sanitizer::setAllowedAttrs` methods respectively.

These methods require that you implement the `enshrined\svgSanitize\data\TagInterface` or `enshrined\svgSanitize\data\AttributeInterface`.

## Remove remote references 

You have the option to remove attributes that reference remote files, this will stop HTTP leaks but will add an overhead to the sanitiser.

This defaults to false, set to true to remove references.

`$sanitizer->removeRemoteReferences(true);`

## Minification

You can minify the XML output by calling `$sanitiser->minify(true);`.

## Demo
There is a demo available at: [http://svg.enshrined.co.uk/](http://svg.enshrined.co.uk/)

## WordPress

I've just released a WordPress plugin containing this code so you can sanitize your WordPress uploads. It's available from the WordPress plugin directory: [https://wordpress.org/plugins/safe-svg/](https://wordpress.org/plugins/safe-svg/)

## Drupal

[Michael Potter](https://github.com/heyMP) has kindly created a Drupal module for this library which is available at: [https://www.drupal.org/project/svg_sanitizer](https://www.drupal.org/project/svg_sanitizer)

## Tests

You can run these by running `phpunit`

## To-Do

More extensive testing for the SVGs/XML would be lovely, I'll try and add these soon. If you feel like doing it for me, please do and make a PR!
