- [About pdMarkdown](#about-pdmarkdown)
- [About this document](#about-this-document)
- [Definition linking](#definition-linking)
- [Definitions article](#definitions-article)
- [Article inline elements](#article-inline-elements)
- [Article content styling](#article-content-styling)
- [Article properties](#article-properties)
- [List item properties](#list-item-properties)
- [Automatic properties (WIP)](#automatic-properties-wip)
- [Programming article properties](#programming-article-properties)
  - [Automatic programming properties](#automatic-programming-properties)
- [Advanced settings (WIP)](#advanced-settings-wip)

# About pdMarkdown
pdMarkdown is a superset markdown containing features that make it painless to write long documents containing multiple articles.

Since pdMarkdown is in the initial specifications stage, issues providing feedback at this point can make large differences. So please do provide your constructive criticisms and interesting implementation ideas ❤

# About this document
- Serves as both a technical specification and 'how to use' manual; formatted in pdMarkdown. It will be split if deemed necessary.
- pdMarkdown specifications most likely to change are marked (WIP). Work-in-progress discussion is considered meta and belongs in external issue trackers, not within this document.

# Definition linking
aka: anchor, anchors, references

- Anchors are generated for:
  - headings
  - list items starting with text wrapped in backticks. ex:``` -`Title` content```
- Anchors are NOT case sensitive.
- Article text matching an anchor (case insenstive) is linked except:
  - article self-references
  - within backtick scopes
- All discovered document/project definitions are given definition tooltips, trimmed to X characters.
- Long definitions and definitions including formatting are additionally linked to definition within the definition article.

internals: HTML HREF anchors are derived from title, replacing spaces with underscores and discard all incompatible characters.

Although not recommended, automatic linking can be disabled and `abr:` could be used instead.

# Definitions article
aka: glossary

Used for all acronyms, abbreviations, definitions and jargon not covered by other articles.

A definition article is set by placing the `##DEFINITIONS` heading on the line below the decided article heading. There can only be one.

internals: Should pdMarkdown output a console notice for any undefined acronyms (all cap words) found in the document?
Could use `ignore:` An optional list of acronyms (all capital letters) separated by commas to be ignored when pdMarkdown files are parsed. 

# Article inline elements
Can be used anywhere.

- `key:` Keyboard key styling. Example: key:Esc
- ~~`see:` Link to an article/sub-article/list element by title. See definition linking.~~

# Article content styling
aka: box styles

Various styles for content that should stand out. If you are composing a large block of content, it's recommended you start on a separate line with a single tab.

- `try:` Experiment/challenge 🔨

try: Can you use all the different box styles?

- `notice:` Notice that... 👀

notice: It's quite easy to use pdMarkdown!  

- `warning:` aka:caution. Important information that must be recognized ⚠

warning:
  Your noticing of the demonstration notice above has been noted and any continuing participation in noticing new notices will be noted and potentially reported to notable authorities.

- `internals:` Additional details and rational concerning a project's internal functionality 🤓

internals: pdMarkdown was born out of writing documentation and tutorials for an internal project. We noticed repeating textual themes throughout (`try:`, `notice:`, etc) and thought it would be best to standardize it.

# Article properties
aka: Article property, Sub-article properties, Sub-article property

- `tags:` aka:taxonomy,grouping. Article tags/taxonomy/group links. 
  - A project-wide tag list is placed in an article named 'Tag Index', if you want to rename it, create an empty article with your chosen heading directly followed by`##TAGLIST`.
- `slug:` (WIP) specific alternative word or phrase that anchors the article/reference.
- `aka:` alternative titles, names, synonyms, or pseudonyms.

If you are having issues ensure that:

- Properties must be listed after the anchor AND before any article content.
- Property names always start with a lowercase character, end with a key:: colon character and may have a space prior to its first value.
- Property values containing the key:, comma character must be wrapped in single quotes. ex:`aka: foo, 'bar? bizz, buzz'`

# List item properties
Same as article properties however they must also:
- be located directly after the anchor or previous property.
- end with the key:. period character

```md
-`Foo` aka:bar. tags:fizz,buzz. Lorem ipsum sit amet...
```

# Automatic properties (WIP)

- `previously:` human relevant list of previous titles for renamed articles. (sufficiently different, <6 characters?)
  - ~~data-priorTitles: all previous titles, hidden when rendered for use by 'definition linking'.~~
- `authors:` major article contributors. Calculated via non-whitespace contributions adding/changing at least 25% of article. Is this prone to abuse?
- `contributors:` list of all contributors
- `creator:` initial contributor

internals: could use git commit names within repo context.

# Programming article properties
- `usedBy:` (WIP) other articles that utilize this one property/function.
- `depreciated:` aka:absolete. reason for removal and name of replacement if any exists. Heading/list item titles gain `depreciated` class. Date of depreciation prepended automatically if vcs-auto-tags is enabled.

## Automatic programming properties
- `vcs-removed:` git tag/commit removed in, see depreciated.
- `vcs-added:` git tag/commit introduced in

# Advanced settings (WIP)
- auto-link-case-sentitive: default false
- tooltip-length: default 128 characters?
- vcs-auto-tags: default true
- disable-tag-index: default false