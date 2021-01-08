# counting-translations
Translations files for counting.

## About
These are the translations for the Discord bot [counting](https://counting.duckgroup.xyz/invite). I understand that it is not in a standard translations format. Just how we decided to implement it, as there were no libraries which we
determined to be good contenders.

## File Structure
Anyway, the format is pretty simple. All normal strings should be referenced from `en-US.json`. If an English string is changed, we will be removing all existing translations expecting them to be rewritten.

The file `booleanSubstitutions.json` is specifically for boolean command argument processing. It defines strings and their appropriate boolean representations. Items in the `global` section are always checked for, and the other sections
are for specific languages.

## Internal Processing Notes
String translations are processed as most systems normally do. Counting takes these simple steps when processing a translation:

- Get guild's current translation language
- Search appropriate language translation file for matching translation ID
  - If ID is found, return translated string
  - If ID is not found, return string recorded in `en-US.json`
- Determine if retreived string is a redirect and replace. (Eg. `__helpMessage__`)
- Return string

Counting will then do further string replacement for variables.

## Contributing
Contributing is simple. If you are fluent in a language, we could use your help!

### Translating the help message or adding boolean substitutions
- Fork the repository
- Create a new branch for your changes (Eg. `update-fr-FR`)
- For the help message, create or modify the appropriate file for your language (Eg. `helpMessage/fr-FR.txt`)
- For boolean substitutions, edit `booleanSubstitutions.json`
- Commit the changes to your fork
- Open a PR for your changes to be merged!

### Translating the rest of the bot strings
- Go to https://crowdin.com/project/counting-translations
- Click on your language
- Click on the `en-US.json` file
- Go through and translate whichever strings you feel

If you are new to using Crowdin, the interface should give you a helpful walkthrough. We understand that this is a fairly high barrier to entry, however this is the best way for us to stay organized.

Notes:
- Be sure not to translate string replacements! String replacements are anything within `{}` brackets. Example: `{authorId}`
- Discord limits messages to a maximum of 2000 characters. At the moment, the only relevant string for this is the help message, so be careful when translating to stay under this limit!
 - If translation pushes the character count of a linked file (Eg. `__helpMessage__`) to over 2000 characters, find a suitable part of the translation that can be broken, and add `__MESSAGE_BREAK__` to its own line where you want to split. This will tell the bot to send multiple messages.
