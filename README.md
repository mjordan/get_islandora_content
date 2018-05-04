# Get Islandora Content

Command-line tool to harvest Islandora objects through OAI-PMH or REST and save them to disk ready to ingest into Drupal 8 using Migrate Plus. More of a proof of concept than anything else, but works as advertised. For background, see https://github.com/Islandora-CLAW/CLAW/issues/452.

## Requirements

* On the target Islandora instance
  * [Islandora OAI](https://github.com/Islandora/islandora_oai) or
  * [Islandora REST](https://github.com/discoverygarden/islandora_rest)
* On the system where the script is run
  * PHP 5.5.0 or higher.
  * [Composer](https://getcomposer.org)

## Installation

1. `git clone https://github.com/mjordan/get_islandora_content.git`
1. `cd get_islandora_content`
1. `php composer.phar install` (or equivalent on your system, e.g., `./composer install`)

## Overview and usage

Run `./get_islandora_content --help` to get help usage information:

```
-d/--dsid <argument>
     Datastream ID to harvest. Default is "OBJ".

-c/--collection <argument>
     A collection PID to harvest.

-h/--host <argument>
     The Islandora server's hostname, including the "http(s)://". The trailing "/" is optional.

-m/--mimetype <argument>
     A MIME type to restrict harvested objects to.

-o/--output_directory <argument>
     The full path to the output directory.

-s/--source <argument>
     Required. Either "oai" or "rest".
```

Examples of running the script include:

`./get_islandora_content -h http://digital.lib.sfu.ca -c hbc:collection -o /tmp/testing --s oai`
`./get_islandora_content -h http://digital.lib.sfu.ca -c hbc:collection -o /tmp/testing --s rest -d PDF`
`./get_islandora_content -h http://digital.lib.sfu.ca -c hbc:collection -o /tmp/testing -m image/jpeg`

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

The `metadata.xml` file contains all of the MODS datastreams retrieved from the OAI harvest, concatenated together and wrapped in a `<modsCollection>` element, e.g.:

```xml
<modsCollection>
<record xmlns="http://www.openarchives.org/OAI/2.0/"><header><identifier>oai:digital.lib.sfu.ca:hbc_2</identifier><datestamp>2017-08-01T11:02:59Z</datestamp><setSpec>hbc_collection</setSpec></header><metadata><mods xmlns="http://www.loc.gov/mods/v3" xmlns:mods="http://www.loc.gov/mods/v3" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink">
  <titleInfo>
    <title>A view of a rope bridge, (2) showing traffic</title>
  </titleInfo>
  <name>
    <namePart>Harrison Brown</namePart>
    <role>
      <roleTerm type="code" authority="marcrelator">pht</roleTerm>
      <roleTerm type="text" authority="marcrelator">Photographer</roleTerm>
    </role>
  </name>
  <originInfo>
    <dateIssued encoding="w3cdtf" keyDate="yes">1936-11-12</dateIssued>
  </originInfo>
  <abstract>Kwan Hsian</abstract>
  <genre authority="lcsh">photographs</genre>
  <accessCondition type="use and reproduction">Reproduction of the material is subject to the approval of the Special Collections and Rare Books Librarian</accessCondition>
  <identifier type="local"/>
  <typeOfResource>still image</typeOfResource>
  <identifier type="uuid">f7bc0c20-9bc6-4499-b1f3-7fda4eafeaf0</identifier>
  <identifier type="uri" invalid="yes" displayLabel="Migrated From">http://content.lib.sfu.ca/cdm/ref/collection/hbc/id/1</identifier>
</mods></metadata></record>

<!-- more MODS records here -->

</modsCollection>
```

Using the REST option, the `metadata.xml` file contains just the MODS content, and not any OAI-PMH content:

```
<modsCollection>
<mods xmlns="http://www.loc.gov/mods/v3" xmlns:mods="http://www.loc.gov/mods/v3" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink">
  <titleInfo>
    <title>A view of a rope bridge, (2) showing traffic</title>
  </titleInfo>
  <name>
    <namePart>Harrison Brown</namePart>
    <role>
      <roleTerm type="code" authority="marcrelator">pht</roleTerm>
      <roleTerm type="text" authority="marcrelator">Photographer</roleTerm>
    </role>
  </name>
  <originInfo>
    <dateIssued encoding="w3cdtf" keyDate="yes">1936-11-12</dateIssued>
  </originInfo>
  <abstract>Kwan Hsian</abstract>
  <genre authority="lcsh">photographs</genre>
  <accessCondition type="use and reproduction">Reproduction of the material is subject to the approval of the Special Collections and Rare Books Librarian</accessCondition>
  <identifier type="local"/>
  <typeOfResource>still image</typeOfResource>
  <identifier type="uuid">f7bc0c20-9bc6-4499-b1f3-7fda4eafeaf0</identifier>
  <identifier type="uri" invalid="yes" displayLabel="Migrated From">http://content.lib.sfu.ca/cdm/ref/collection/hbc/id/1</identifier>
</mods>
<!-- more MODS records here -->

</modsCollection>
```

## To do

* Confirm that the filenames are suitable for use by Migrate Plus
* More, better error handling

## Contributing

* Testing, bug reporting, and questions are welcome. Please open an issue.
* Pull requests are welcome, but if you want to open a pull request, please open an issue first.

## Maintainer

* [Mark Jordan](https://github.com/mjordan)

## License

The Unlicense
