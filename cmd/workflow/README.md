# Workflow 


Tools to facilitate the following.

If the logic and packages are right, the tooling is quite easy to build.

## Flow and Actors

At a high level this is the flow of who is involved.

1. Design Time

	- The process for a developer.

2. Translation Time

	- The workflow to get the data properly translated.

3. Build Time

	- The normal build of any Apps and GUI.

3. Run Time

	- Gitea Web and Flutter apps use the packages in the app to enable them to easily support the i18n and l10n.

	- These packages are designed to use the translated files that the cli tools produces, and these use the raw translated language files.

	- Gitea Hugo web site uses the translated files that the workflow produces


## Artifacts

The developers files are Markdown, JSON and ARB files.

- These are tightly coupled to their code, which is what you want so you know that if it compiles everything works.


The translation system uses a global Key Value File Cache.

- These keys and values are derived from the Developers files. The developers never need to touch this.

## Translation system

The Server is a simple File Cache that holds all Name values pairs.

Its just a denormalized Key Value store of all the data derived from the Developer's MarkDown, JSON, ARB files that their App's use.

- This is where all translations are stored as files in git.

- This is the Ground Truth in terms of what is the correct Translation.

- The files are simple Key / Values pairs.

- The Machine and Human Translation stages use this data.

- It does NOT store the developers JSON, markdown and ARB.

- It parses the Developers files to generate the Key Value pairs.

- Indexing and Search to make it easy to manage.
	- See the  [i18n-indexer package](/pkg/i18n-indexer/README.md) for more info ...

## Logic

The MOST important aspect here is that this is NOT driven by Git differences.

Its idempotent, in that you can run this workflow at any time and it will only do work that is actually needed.


The basic workflow is:

1. Developer

	- If they changed existing GUI or Markdown.

		- They just add it like normal.

	- If they added new GUI.

		- They use the tooling to code generator the skeleton code.

	- They commit their changes like normal.

2. Server Parse

	- The Server parses the Files and sees whats needed to be translated.

		- It know this from looking at the Developers.

	- It then kicks off the Machine Translation.

	- Then based on the outputs it notified each Human Translator for work to be done by email.

	- Then it watches for git commits from each Human Translator, and runs the Merge.


3. Machine Translation

	- The Application files are parsed. These are JSON, Markdown and ARB files.
		- TODO: Need to write parsers for Markdown, JSON, ARB

	- Now the translation starts:

		- If it gets a cache miss it calls the Google server to get the Value.
		
			- The result is saved in the Cache with a "IsDirty" Flag so the next stage of the workflow know whats needed to be checked.

		- If it does NOT get a cache miss

			- Just use the value found in the cache.

	- See the google-trans [google-trans package](/pkg/google-trans/README.md) for more info ...


4. Human Translation

	- Anything "Dirty" in the cache requires checking by a human.

	- The person checks its ok.

	- If its not ok:
	
		- They correct it, and the file in the Cache is flagged as "Not Dirty" and as "HIL Fixed", with a DateTime stamp.

	- If its OK:

		- The correct it, and the file in the Cache is flagged as "Not Dirty" and as "HIL No Changes", with a DateTime stamp.

	
5. Merge

	- The Name files are sitting there in the File Cache all ready.

	- The system will code generate the JSON, MarkDown, ARB files from the values in the File Cache.

6. Build

	- Now any App's and GUI can be compiled like normal.
