# WP Rest Schema Builder

....

![alt text](https://img.shields.io/badge/Current_Version-0.0.1-yellow.svg?style=flat " ") 
[![Open Source Love](https://badges.frapsoft.com/os/mit/mit.svg?v=102)]()
[![WordPress 6.1 Test Suite [PHP7.2-8.1]](https://github.com/Pink-Crab/WP_Rest_Schema/actions/workflows/WP_6_1.yaml/badge.svg?branch=master)](https://github.com/Pink-Crab/WP_Rest_Schema/actions/workflows/WP_6_1.yaml)
[![codecov](https://codecov.io/gh/Pink-Crab/WP_Rest_Schema/branch/master/graph/badge.svg?token=4yEceIaSFP)](https://codecov.io/gh/Pink-Crab/WP_Rest_Schema) [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/Pink-Crab/WP_Rest_Schema/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/Pink-Crab/WP_Rest_Schema/?branch=master)

## Version 0.1.0-beta3 ##

****

## Why? ##

Defining valid JSON rest schema in WordPress is a little messy and easy to make a mistake with it being lots of nested arrays. This library attempts to make this process cleaner and simpler with a fully fluent, object driven interface.

****

## Setup ##

To install, you can use composer
```bash
$ composer require pinkcrab/wp-rest-schema-builder
```
for_meta_data
## Basic Usage ##

> This can be used for Register Post Meta
```php
register_post_meta( 'post', 'fixed_in', array(
    'type'         => 'string',
    'show_in_rest' => array(
        'single' => true,
        'schema' => Argument_Parser::for_meta_data(
            String_Type::on('fixed_in')
                ->min_length(10)
                ->max_length( 42 )
                ->required()
                ->description('This is a required string value, that must be between 10 and 42 chars long.')
        ),
    ),
) );
```
> Can also be used with the [Perique Registerable](https://github.com/Pink-Crab/Perique-Registerables) library
```php
    $meta_data = (new Meta_Data('fixed_in'))
        ->post_type('post')
        ->type('string')
        ->rest_schema(
            Argument_Parser::for_meta_data(
                String_Type::on( 'fixed_in' )
                    ->min_length(10)
                    ->max_length( 42 )
                    ->required()
                    ->description('This is a required string value, that must be between 10 and 42 chars long.')
            )
        );
```


The WP Rest Schema Builder can be used in various places where you would normally define a schema, such as Rest Routes, Registering Post Types, Taxonomies and Meta Data.

## Change Log ##
* 0.1.0 Inital version