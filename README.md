# Get Islandora Content

Command-line tool to harvest Islandora objects through OAI-PMH.

## Requirements

* On the target Islandora instance
  * [Islandora OAI](https://github.com/Islandora/islandora_oai)
* On the system where the script is run
  * PHP 5.5.0 or higher.
  * [Composer](https://getcomposer.org)

## Installation

1. `git clone https://github.com/mjordan/get_islandora_content.git`
1. `cd get_islandora_content`
1. `php composer.phar install` (or equivalent on your system, e.g., `./composer install`)

## Overview and usage

To use this script, edit the following three variables:

```
$output_directory = '/tmp/hbc_output';
$host = 'http://digital.lib.sfu.ca';
$set = 'hbc_collection';
```

The value of `$set` is a collection PID with its colon replaced by an underscore (e.g., `hbc:collection` becomes `hbc_collection`).

Then run the script:

`./get_islandora_content`

The output will contain a `metadata.xml` file and and file corresponding to each retrieved objects' OBJ datastream. For example, a small collection of images results in the following output:

```
/tmp/test/
├── hbc_10.jpeg
├── hbc_11.jpeg
├── hbc_12.jpeg
├── hbc_13.jpeg
├── hbc_14.jpeg
├── hbc_15.jpeg
├── hbc_16.jpeg
├── hbc_17.jpeg
├── hbc_18.jpeg
├── hbc_19.jpeg
├── hbc_1.jpeg
├── hbc_20.jpeg
├── hbc_2.jpeg
├── hbc_3.jpeg
├── hbc_4.jpeg
├── hbc_5.jpeg
├── hbc_6.jpeg
├── hbc_7.jpeg
├── hbc_8.jpeg
├── hbc_9.jpeg
└── metadata.xml
```

The `metadata.xml` file contains all of the MODS datastreams retrieved from the OAI harvest, concatenated together and wrapped in a `<modsCollection>` element.

## Maintainer

* [Mark Jordan](https://github.com/mjordan)

## License

The Unlicense
