# Gitea Translation


Because of this need in Gitea:

https://github.com/go-gitea/gitea/issues/6552#issuecomment-483582189

The is a system to build GUI's and Servers that fully support i18N and l10n.

Its designed for Hugo, Golang Server and Flutter Clients ( Mobile, Desktop and Web).


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

See the [Workflow gui folder](/cmd/workflow/) for more information.

Its provides:

- For Developers the tools for the code generation to make it easy to manage their GUI and generate the required i18n and l10n files.

- For Translators the tools to do the translation work for each language.

- A Server to run the workflow as part of any CI process.


## GUI

These are the libraries the Developer uses in their Apps and GUI's.

There are also examples.

There are 3 GUI's needed:

- Mobile and Desktop using Flutter for the Gitea App.
	- See the [Flutter gui folder](/gui/flutter/)

- Web using Hugo for the docs web site and main website.
	- See the [Hugo gui folder](/gui/hugo/)
