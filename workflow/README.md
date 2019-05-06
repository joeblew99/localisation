# Workflow

The MOST important aspect here is that this is NOT driven by Git differences.
Its idempotent, in that you can run this workflow at any time and it will only do work that is actually new.
SO your not reliant on Git and the CI system detecting the things that changes. This does not really work with translation because of the parametric nature of real world translation and code gen.

We need a basic workflow:

1. CI Server

- Any CI server can be used. On build, you alwas run the Trans first and and code gen.

2. File Cache

- This is where all translations are stored as files and stored in git.
- It does NOT store the files used by the Gitea system at runtime that are JSON, markdown and ARB, because these are in a different form
- It is just the simple list of Names to Values to record what is a correct translation.
- The Machine and Human Translation stages uses this as its Ground Truth.


3. Machine Translation

- The Application source files are parsed.
- The strings are sent for translation.
	- Uses the Cache and if it gets a cache miss it calls the Google server.
- The result is saved in the Cache.
- See the Google-trans project
	- A simple Google translator to run anything through google translator.
	- Need to extend to handle:
		- ARB files for Flutter Mobile, Desktop and Web
		- Parse them and send each thing into Google
	- HTML files for HUGO
		- Will be a mixture of Markdown and JSON.

4. Human Translation

- Anything new in the cache requires checking by a human.

- See the i18n-Indexer project
	- A simple Indexer for files related to i18n
	- Needs to handle:
		- ARB files for Flutter Mobile, Desktop and Web
		- HTML files for HUGO
