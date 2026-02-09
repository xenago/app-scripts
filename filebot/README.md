# filebot

File-renaming software.

## Disable x-attr

To avoid modifying the files, run with the flag `-no-xattr`. Otherwise, extended attributes will be modified:

https://www.filebot.net/forums/viewtopic.php?t=324#usage

## Preset

Create a preset as follows for proper naming:

* Files: `Use Original Files selection`
* Format: `{n} - {sxe} - {t}`
* Datasource: `TheTVDB`
* Episode Order: `Airdate`
* Match Mode: `Opportunistic`
* Rename Action: `Rename`
