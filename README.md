# PlainNotes for Stata & R

This repository adds support for Stata & R with native key bindings to [PlainNotes](https://packagecontrol.io/packages/PlainNotes).

## Installation

You can install this repository either manually or via Package Control. I recommend the latter way since it allows users to install and automatically update packages from GitHub.

0. Remove `PlainNotes` previously installed.
1. Press `ctrl`/`command`+`shift`+`p`, `p`, `c`, `a` and select `Package Control: Add Repository`.
2. Copy & paste [the link to this repository](https://github.com/jh-min/PlainNotes) in the form.  
Note that adding this repository will block installing original `PlainNotes` via Package Control.
3. Press `ctrl`/`command`+`shift`+`p`, `p`, `c`, `i`, `Enter`.
4. Search & install `PlainNotes` from the drop-down list.


## Usage

If opening fence is either ` ```s `, ` ```{s} `, ` ```stata ` or ` ```{stata} `, fenced code block will highlight Stata syntax and support any key bindings working in Stata source(`.do` files).

If opening fence is either ` ```r ` or ` ```{r} `, fenced code block will highlight R syntax and support any key bindings working in R source(`.R` files).

Note that default syntax highlighting scheme is set to [Monokai Pro](https://packagecontrol.io/packages/Theme%20-%20Monokai%20Pro).


## Key Bindings

Below are some example key bindings that you can manually add to `Preferences > Key Bindings`. In order to apply those key bindings, you need to install [Multicommand](https://packagecontrol.io/packages/Multicommand) via package control first. For Stata users, I recommend using [Markstat](https://data.princeton.edu/stata/markdown) to integrate Stata results into Markdown document. For R users, I recommend using [SendCode](https://packagecontrol.io/packages/SendCode) and [Terminus](https://packagecontrol.io/packages/Terminus) to execute R code within Sublime Text.

### for Stata

#### [StataEditor](https://packagecontrol.io/packages/StataEditor) (Windows)

- remapping key bindings to execute Stata code line by line pressing `ctrl`+`d` and whole code pressing `ctrl`+`alt`+`d`:

```json
[ /* the outermost square brackets are only needed if you have never defined Key Bindings before */
  // StataEditor
  { /* remap StataEditor to mimic SendCode */
    "keys": ["ctrl+d"],
    "command": "multicommand",
    "args": {
      "commands": [
        {
          "command": "stata_execute",
          "args": {"Mode": "do", "Selection": "line"},
        },
        {
          "command": "move_to",
          "args": {"to": "hardeol"},
        },
        {
          "command": "move",
          "args": {"by": "lines", "forward": true},
        },
        {
          "command": "move_to",
          "args": {"to": "hardbol"},
        },
      ],
    },
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.stata" }
    ],
  },
  { /* remap StataEditor */
    "keys": ["ctrl+alt+d"],
    "command": "stata_execute",
    "args": {"Mode": "do", "Selection": "default"},
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.stata" }
    ],
  },
] /* the outermost square brackets are only needed if you have never defined Key Bindings before */
```

#### [Improved Stata Editor](https://packagecontrol.io/packages/Stata%20Improved%20Editor) (macOS)

- remapping key bindings to execute Stata code line by line pressing `command`+`d` and whole code pressing `command`+`option`+`d`:

```json
[ /* the outermost square brackets are only needed if you have never defined Key Bindings before */
  // Improved Stata Editor
  { /* remap Improved Stata Editor to mimic SendCode */
    "keys": ["super+d"],
    "command": "multicommand",
    "args": {
      "commands": [
        {
          "command": "lines_to_stata",
        },
        {
          "command": "move_to",
          "args": {"to": "hardeol"},
        },
        {
          "command": "move",
          "args": {"by": "lines", "forward": true},
        },
        {
          "command": "move_to",
          "args": {"to": "hardbol"},
        },
      ],
    },
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.stata" }
    ],
  },
  { /* remap Improved Stata Editor */
    "keys": ["super+option+d"],
    "command": "piu_sign",
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.stata" }
    ],
  },
] /* the outermost square brackets are only needed if you have never defined Key Bindings before */
```

### for R

#### Windows

- remapping key bindings to insert `<-` pressing `alt`+`-` and delete `<-` pressing `backspace` just once:

```json
[ /* the outermost square brackets are only needed if you have never defined Key Bindings before */
  { /* insert R assignment operator easily */
    "keys":["alt+-"],
    "command": "insert",
    "args": {"characters": "<-"},
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.r" },
    ],
  },
  { /* delete R assignment operator easily */
    "keys": ["backspace"],
    "command": "multicommand",
    "args": {
      "commands": [
        {
          "command": "left_delete"
        },
        {
          "command": "left_delete"
        },
      ],
    },
    "context": [
      { "key": "selector", "operator": "equal", "operand": "source.r" },
          { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
          { "key": "preceding_text", "operator": "regex_contains", "operand": "<-$", "match_all": true }
    ],
  },
] /* the outermost square brackets are only needed if you have never defined Key Bindings before */
```

#### macOS

- remapping key bindings to insert `<-` pressing `option`+`-` and delete `<-` pressing `backspace` just once:

```json
[ /* the outermost square brackets are only needed if you have never defined Key Bindings before */
  { /* insert R assignment operator easily */
    "keys":["option+-"],
    "command": "insert",
    "args": {"characters": "<-"},
    "context":
    [
      { "key": "selector", "operator": "equal", "operand": "source.r" },
    ],
  },
  { /* delete R assignment operator easily */
    "keys": ["backspace"],
    "command": "multicommand",
    "args": {
      "commands": [
        {
          "command": "left_delete"
        },
        {
          "command": "left_delete"
        },
      ],
    },
    "context": [
      { "key": "selector", "operator": "equal", "operand": "source.r" },
          { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
          { "key": "preceding_text", "operator": "regex_contains", "operand": "<-$", "match_all": true }
    ],
  },
] /* the outermost square brackets are only needed if you have never defined Key Bindings before */
```

---

# [PlainNotes](https://github.com/aziz/PlainNotes)
Simple and pleasant authoring and note taking for SublimeText.

With PlainNotes you can:
 - Organize notes and thoughts
 - Maintain todo-lists
 - Write documents
 - and probably more

PlainNotes stores and organizes all your notes in a folder and make them
accessible with a single shortcut or mouse click. It also provides you with an
enhanced version of Markdown markup and some good looking color schemes for
note taking.
It's been designed with these ground rules in mind:
 - Plain text is the holy grail
 - Plain text shouldn't be that plain
 - Simple and Sexy is Sublime

<p align="center">
<img src="http://cl.ly/image/21143i2m3e0n/ss2.png" width="727" height="416">
</p>

**Note:** Although PlainNotes works under SublimeText 2, some features might
not be available. We're not actively testing it under SublimeText 2 but will
do our best to make it compatible and usable. We appreciate bug reports and
pull requests.

## Organizing notes

Most of PlainNotes commands are accessible from the SublimeText main menu. You
should have a menu item called `Notes` right after `Help`. Although, there are
faster and easier ways of running those commnads that are mentioned below.

#### Starting a new note (`super+F4`)
- **Command palette**: Open command palette and search for `Notes: new`
  command (typing `nn` will probably find it for you).
  - To save note in a subfolder of the root directory use `/`:
    `"subfolder name"/"note name"`.

- **Shortcut**: By default pressing <kbd>super+F4</kbd> will create a new
  note. For customizing the shortcut see [Keyboard Shortcuts]() section.

#### Opening an existing note (`F4`)
- **Command palette**: Open command palette and search for `Notes: List…`
  command (typing `nl` will probably find it for you), the command will show
  the *Latest Notes quick panel* from which you can select or search for your
  file.
  The *Latest Notes quick panel* is sorting files based on their last-edit
  time, so the note that you have been working on recently should be on top of
  the list.

- **Shortcut**: By default pressing <kbd>F4</kbd> will open the
  *Latest Notes quick panel*. For customizing the shortcut see
  [Keyboard Shortcuts]() section.

#### Jotter (`F1`)
Jotter will let you jot down your thoughts and ideas quickly without
disturbing your work-flow. It opens a *Note Panel* at the bottom of the editor
which is ready to take your note. When you press <kbd>ESC</kbd> it
automatically closes the panel and saves your note with a time stamp in your
*Inbox*.

It can be accessed by pressing <kbd>F1</kbd> (that can be customized in your
Key-bindings if it conflicts with your other key-bindings) or through
`Notes: Jotter` in command palette.
The default color scheme of the jotter panel can be customized in user
settings (`Preferences -> Package Settings -> PlainNotes -> Settings - User`):

```json
{ "jotter_color_scheme": "Packages/PlainNotes/Color Schemes/Sticky-Yellow.tmTheme" }
```

#### Inbox
Inbox is where all your quick notes from *Jotter* live. You can view inbox
through `Notes: Inbox` in command palette or via the Notes main menu.
The date and time format of the note headers in inbox can be customized in user
settings (`Preferences -> Package Settings -> PlainNotes -> Settings - User`):

```json
{
    "jotter_date_format": "%d %b %Y",
    "jotter_time_format": "%I:%M %p"
}
```

#### Notes Index Card (`ctrl+F4`)
Pressing <kbd>ctrl+F4</kbd> or selecting `Notes: Index` from the command
palette will give you the *Notes Index Card* with the list of all notes sorted
alphabetically.
Pressing <kbd>Enter</kbd> on any note will open it in a new tab.

#### Change note color
Open command palette and search for `Note: Change Color…`. it will give you a
list of 10 different colors that is shown in the above image. Pressing up and
down will give you a preview.
Color of the note is remembered by PlainNotes and whenever you open that file,
PlainNotes will set the color-scheme automatically.

#### Archive note
Open command palette and search for `Note: Archive`. This will move the note
into an archive folder than can be specified in the settings -- The default
archive directory is `.archive`. Archiving a note hides it from the Index and
List.

#### Unarchive notes
Open command palette and search for `Note: Unarchive...`. This will open a
list of archived notes sorted by modification date. Selecting one from the
list will unarchive that note.

#### Delete note
Open a note and then open command palette and search for `Note: Delete`.

#### Rename note
Open a note and then open command palette and search for `Note: Rename`.

#### Change note file extension
You can change the note file extension in settings. To do so, go to
`Preferences -> Package Settings -> PlainNotes -> Settings - User` and modify
`"note_save_extension":`. The default note type is `.note` which has the
possibility of setting different note colors and some special markup.
Alternatively you can use any note extension you want such as markdown `.md`.

#### Add yaml front matter to notes
Go to `Preferences -> Package Settings -> PlainNotes -> Settings - User` and
modify `"enable_yaml"`

By default, the following yaml items are added:
```yaml
title:
date:
tags:
```

To add more yaml items you can add them to the settings by modifying `note_yaml:`:

```json
{ "note_yaml" : ["categories"] }
```

#### Other features
- **Open URLs**: place cursor on the link then press `enter` to open a url in
  the browser.
- **Preview images inline**: place cursor on a markdown image with inline image url and press `enter` to a preview popup of that image. You should have ST 3070 or newer for this feature to work.

#### Per-project notes

To have a different notes directory for a project, add the following in your
`.sublime-project` file:

```json
"settings": {
    "PlainNotes": {
        "root": "path/to/notes/dir"
    }
}
```

## Authoring notes
PlainNotes provides an enhanced version of Markdown. It means that you can
write your notes in plain markdown without learning anything new. In addition,
it gives you some extra markups to improve the look and feel of your
documents, since markdown sometime feels too simple to format a real document.

If you are new to markdown here is a cheat-sheet:

|    Markup   |            Markdown Syntax            |
|-------------|---------------------------------------|
| Italic      | `_italic_` or `*italic*`              |
| Bold        | `__bold__` or `**bold**`              |
| Images      | `![Image Title](http://url_to.image)` |
| Links       | `[Link Text](http://link.url)`        |
| Inline Code | `` `code` ``                          |
| Quotes      | `> Here is a quote block`             |
| Separators  | `----` or `*****`                     |
| Heading 1   | `# Heading 1`                         |
| Heading 2   | `## Heading 2`                        |
| Heading 3   | `### Heading 3`                       |
| Heading 4   | `#### Heading 4`                      |

### Extra Markup

#### Admonitions
When writing a note, you might need to distinguish a block or section by
giving it a special title and box. These sections might appear several times
in your document. Some examples would be *Note*, *Tip* or *Caution* blocks in
an article.

Here is how to create an admonition block

    !!! ADMONITION_TYPE "Optional title in quotes"
        Any number of other indented markdown elements.

<img width="640" src="https://cloud.githubusercontent.com/assets/3202/10559318/3d5e5420-74ee-11e5-89b9-0eca42750aca.png" >

By default admonitions block have a purplish background color (that might be
different based on the color scheme), but giving it a specific type from table
below can change the color. Predefined admonition types are listed in table
below and are shown in image above. Note that admonition types can be lower-
case, upper-case or title-case.

| Predefined Admonition Type | Block Color |
|----------------------------|-------------|
| `hint` or `tip`            | bluish      |
| `warning` or `caution`     | yellowish   |
| `danger` or `error`        | reddish     |
| `attention`                | greenish    |

Admonition blocks can have any PlainNotes enhanced markdown inside them and
they customize the look and feel so that everything looks sublime.

<img align="center" width="380" src="https://cloud.githubusercontent.com/assets/3202/10559414/c9a61ff6-74f0-11e5-8209-1c881ebd8506.png" >

## License

Copyright 2014-2015 [Allen Bargi](https://twitter.com/aziz).
Licensed under the MIT License

