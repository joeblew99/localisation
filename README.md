# Gitea Translation


The is a system to build GUI's and Servers that fully support i18N and l10n.

Designed for Hugo, Golang Server and Flutter Clients ( Mobile, Desktop and Web).



## Quick Summary


Integration with Flutter and golang:

- 100% matches into the FLutter and golang way of plugging into localisation. Not reinventing the wheel there.

i18n:

- plurals 
- codegen for flutter and golang

i10n:

- codegen for flutter and golang
- Data time
- Currency
- SI Units ( temperature, ec etc etc )
- Extensible for now things because its code gen based.

Workflow:

- for teams
- not reliant on third parties if you dont want it.
- extensible: So use CSV, Use Web GUI, use what makes sense. 
- Translation memory
- plug into different machine translation as needed.

Golang:

- Can be used with any golang server code. Not dependent on Gin, Echo, etc.

Code generated:

- To make it easy to manage and extend, uses lots of code gen.
- See: https://github.com/joeblew99/gitea-trans/blob/master/pkg/protoc-gen-dart-ext/Makefile
- Stil unstable, but getting there.

Test Harness:

- Using Gitea FLutter as a test harness, and because it will be good for Gitea.
- Their project: https://github.com/pd4d10/git-touch
- See: https://github.com/joeblew99/gitea-trans/blob/master/gui/flutter/flutter-git-gui/

## Status

Parts of this work, however the libraries need to be integrated and refined.

## i18n & l10n

For any Application or Server its quite complex to get it working for many different locales. Its often over looked how complex it is to get it smoothly working and to have it work with CI because of the many actors.

i18n is related to language translation. Plurals is important here.


l10n is related to Dates, Currencies, etc.

- Clients need to convert the values from the Neutral values to what the Client locale is.

- Servers should store all l10n related data in a neural format and for each locale it needs to convert the values from the client locale to the global neutral values.

- Examples:

	- DateTime as UTC values
	- Currency as Floats.
	- SI Units as Metric values


## CMD

A Web based Dashboard and CLI to make it easy for both Developers and Translators to use the system.

See the [Workflow GUI folder](/cmd/workflow/) for more information.

Its provides:

- For Developers the tools for the code generation to make it easy to manage their GUI and generate the required i18n and l10n files.

- For Translators the tools to do the translation work for each language.

- A Server to run the workflow as part of any CI process.


## GUI

These are the libraries the Developer uses in their Apps and GUI's.

There are also examples.

There are 3 GUI's needed:

- Mobile and Desktop using Flutter for the Gitea App.
	- See the [Flutter GUI folder](/gui/flutter/)

- Web using Hugo for the docs web site and main website.
	- See the [Hugo GUI folder](/gui/hugo/)
