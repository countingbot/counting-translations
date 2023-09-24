# counting-translations
Translations files for counting.

## About
These are the translations for the Discord bot [counting](https://countingbot.com/invite). I understand that it is not in a standard translations format. Just how we decided to implement it, as there were no libraries which we determined to be good contenders.

## File Structure
Anyway, the format is pretty simple. All normal strings should be referenced from `en-US.json`. If an English string is changed, we will be removing all existing translations expecting them to be rewritten.

The file `booleanSubstitutions.json` is specifically for boolean command argument processing. It defines strings and their appropriate boolean representations. Items in the `global` section are always checked for, and the other sections
are for specific languages.

## Internal Processing Notes
String translations are processed as most systems normally do. Counting takes these simple steps when processing a translation:

- Get guild's current translation language
- Search appropriate language translation file for matching translation string ID
  - If ID is found, return translated string
  - If ID is not found, return string recorded in `en-US.json`
- Determine if retreived string is a redirect and replace with value if so. (Eg. `__helpMessage__`)
- Return string

Counting will then do further string replacement for variables.

## Contributing
Contributing is simple. If you are fluent in a language, we could use your help!

### Translating bot strings or the `c!help` message
- Go to https://crowdin.com/project/counting-translations
- Click on your language
- Click on the `en-US.json` file
- Go through and translate whichever strings you feel
  - We take advantage of Discord's markdown formatting. Be mindful of things like [links](https://google.com) `[links](https://google.com)` and `code boxes` \`code boxes\`.
  - We perform string replacement on the translated values. Be sure that your strings contain all string replacements that the original English string does. String replacements are encapsulated within `{}`, like `{authorId}`. Be sure not to translate string replacements!
  - For organizational purposes, we have variable features in our translation files. This allows one string ID to link to another within the same file. You can see this being used in the help message, as `__helpMessage__` gets replaced with the value of the `variable.helpMessage` string ID.

### Adding boolean substitutions
- Fork the repository
- Create a new branch for your changes (Eg. `update-fr-FR`)
- Edit `locale/booleanSubstitutions.json`
- Commit the changes to your fork
- Open a PR for your changes to be merged!

If you are new to using Crowdin, the interface should give you a helpful walkthrough. We understand that this is a fairly high barrier to entry, however this is the best way for us to stay organized.

Notes:
- Discord limits messages to a maximum of 2000 characters. At the moment, the only relevant string for this is the help message, so be careful when translating to stay under this limit!
 - If a string/variable is over 2000 characters, find a suitable part of the translation that can be split, and add `__MESSAGE_BREAK__` to its own line where you want to split. This will tell the bot to send multiple messages.
