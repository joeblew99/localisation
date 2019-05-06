# Gitea Translation


Because of this need in Gitea !!
https://github.com/go-gitea/gitea/issues/6552#issuecomment-483582189

## i18n & l10n

You need to do both to have a decent app that works in many locales.

i18n is mostly related to the language translation. Plurals is important here.

l10n is related to the runtime conversion of Dates, Currencies, etc

## GUI

There are 3 GUI's needed:

- Mobile and Desktop using Flutter.
	- See the [Flutter folder](../blob/master/flutter/README.md)
- Hugo for the docs web site and main website. 
- A Web based Dashboard and CLI to make it easy for both Developers and Translators to use the system.
	- For Developers some tools for the code generation to make it easy for developers to manage their GUI and generate the required i18n and l10n files.
	- For Translators some tools to do the translation work for each languages.

## Parts of the system

3 aspects to make it work

1. Design time
- The process for a developer.
- The libraries Hugo, Web and Flutter app need to use.

2. CI Time

- The workflow to get the data properly translated.
- See the Workflow folder ...

3. Runtime

- Gitea web and flutter app can use the ARB and Dart files so that it works in many languages
- Gitea hugo web site uses the translated files itself.

- See the Hugo and Flutter folders ...


