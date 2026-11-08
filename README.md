# OpenType Professional Studio

**A browser-based OpenType feature editor for Bengali (Bangla) font
development.**

OpenType Professional Studio is an independent, client-side tool for
inspecting and editing OpenType layout data. It provides a visual
workflow for working with glyphs, scripts, languages, features, GSUB
substitutions, GPOS positioning, glyph groups, and GDEF glyph classes.

The project is intended to help Bengali font developers build and manage
OpenType layout rules, including conjunct-related substitutions and mark
positioning. It can also be used for selected Latin and other script
workflows supported by the application.

> **Status:** Experimental / development-stage software. Always validate
> exported fonts in professional font tools and real shaping engines
> before production use.

## Features

-   Open an existing font and inspect its glyphs and available OpenType
    layout data.
-   Work with script, language-system, and feature assignments.
-   Create and edit GSUB substitution lookups.
-   Create and edit GPOS positioning lookups.
-   Manage glyph groups and GDEF glyph classes.
-   Create anchor-based positioning data.
-   Filter lookups, including a Bengali conjunct-focused view.
-   Preview glyphs and proof text using the loaded font where supported.
-   Test lookup rules with the built-in lookup test tool.
-   Validate project data with the built-in validation tool.
-   Export OpenType feature source (`.fea`).
-   Export an updated TrueType font (`.ttf`) for supported lookup types.
-   Save and import editable project files (`.voltproj` / JSON).
-   Undo and redo edits, with browser-based session recovery.
-   Light and dark interface themes.

## Bengali / Bangla workflow

The application includes Bengali-oriented script and feature support.
The interface includes a conjunct lookup filter and templates for
Bengali conjunct work.

A typical workflow is:

1.  Open a compatible `.ttf` or `.otf` font.
2.  Inspect the imported glyph names and existing layout data.
3.  Create or select the `beng` script and the appropriate language
    system.
4.  Add the OpenType features needed by the font.
5.  Create GSUB lookups for substitutions, such as ligature and conjunct
    rules.
6.  Create GPOS lookups for mark and other positioning rules.
7.  Attach lookups to the correct features and arrange their execution
    order.
8.  Run the project's validation and lookup test tools.
9.  Save the editable project file.
10. Export the `.fea` source or a new `.ttf`, then test the result in
    external shaping software.

Feature requirements and lookup order vary by font design and shaping
behavior. Do not assume that one feature recipe is correct for every
Bengali font.

## Getting started

### Run locally

This is a standalone HTML application.

1.  Download or clone this repository.
2.  Open `index.html` in a modern desktop browser.
3.  Use **Open Font** to load a font, or choose **Load Template** to
    start with a template.
4.  Edit the project and save your work as a project file.

No application server or database is required for the basic browser
workflow.

### External library

The current HTML loads
[opentype.js](https://github.com/opentypejs/opentype.js) version `1.3.4`
from cdnjs:

``` html
<script src="https://cdnjs.cloudflare.com/ajax/libs/opentype.js/1.3.4/opentype.min.js"></script>
```

An internet connection is therefore needed to load that dependency when
using the current CDN-based version. Check the library's own license and
notices before redistributing or bundling it.

## File formats

  -----------------------------------------------------------------------
  Format                              Purpose
  ----------------------------------- -----------------------------------
  `.ttf`                              Font input and TrueType export

  `.otf`                              Font input

  `.woff` / `.woff2`                  Accepted by the file picker; actual
                                      support depends on the browser and
                                      decoder path

  `.fea`                              Exported OpenType feature source

  `.voltproj`                         Editable project data in JSON
                                      format

  `.json`                             Project import
  -----------------------------------------------------------------------

**Important:** The project file stores the editor's working data. It is
not itself an installable font.

## Current implementation scope and limitations

The application's built-in compilation notes describe the following
scope:

### Supported or partially supported

-   GSUB lookup types 1--4, 7 (extension), and 8 (reverse chaining).
-   GPOS lookup types 1--6 and 9 (extension).
-   Anchor subtable decoding for GPOS types 3--6.
-   Contextual GSUB types 5 and 6 can be stored as text, but are not
    compiled to binary.
-   TTF export with GSUB/GPOS binary compilation for the supported
    implementation paths.

### Known limitations

-   Contextual GSUB types 5 and 6 are not compiled into font binary
    tables.
-   GDEF ClassDef ranges are simplified.
-   WOFF2 requires an external decoder.
-   The application does not include HarfBuzz shaping verification.
-   WOFF 1.0 cannot be re-exported through the current export path.
-   Importing or exporting a font does not guarantee that every OpenType
    table or feature is preserved or supported.

Because font compilation is complex, treat exported files as development
builds until they have been checked independently.

## Validation and production testing

Before distributing a font:

1.  Keep an untouched backup of the source font.
2.  Save the editor project separately from the exported font.
3.  Inspect the exported font with a professional font editor or font
    inspection utility.
4.  Compile and test feature source with a trusted OpenType toolchain
    where appropriate.
5.  Test shaping with HarfBuzz or another target shaping engine.
6.  Test actual Bengali text, including vowel signs, combining marks,
    reph, half forms, conjuncts, and mark-to-mark behavior as applicable
    to the font.
7.  Test in the applications and operating systems where the font will
    be used.

The editor is not a replacement for FontTools, Adobe FDK for OpenType,
HarfBuzz, or a professional font editor.

## Privacy

The application is designed to run in the browser. The supplied source
contains no application backend or account system. Font files and
project data are processed by the browser workflow; browser storage is
used for local theme and session-recovery data.

The current version loads an external JavaScript library from a CDN.
Network requests to that CDN are separate from local font editing.
Review the source code and any dependencies before using the tool with
confidential font files.

## Technology

-   HTML
-   CSS
-   JavaScript
-   [opentype.js](https://github.com/opentypejs/opentype.js)

## Contributing

Contributions are welcome.

Suggested areas for improvement:

-   More complete OpenType table import and export.
-   Better contextual GSUB compilation.
-   More comprehensive GDEF support.
-   WOFF2 decoding and export workflows.
-   HarfBuzz-based shaping tests.
-   Expanded Bengali feature templates and test cases.
-   Automated regression tests for font parsing and compilation.
-   Documentation and sample projects.

When submitting a change:

1.  Explain the problem or feature.
2.  Include a small reproducible project or font test case when
    possible.
3.  Describe how the change was tested.
4.  Avoid including fonts or glyph artwork unless you have permission to
    share them.

## License

**The license for this project has not yet been specified.**

Before publishing this repository as open source, choose a license and
add its full text in a `LICENSE` file. Do not describe the project as
MIT-licensed, GPL-licensed, or otherwise licensed until that file has
been added and the project owner has confirmed the choice.

Also retain and follow the notices and license terms for third-party
dependencies, including opentype.js.

## Disclaimer

OpenType Professional Studio is an independent project. It is not
affiliated with, endorsed by, or an official product of Microsoft,
Adobe, FontLab, or the developers of HarfBuzz, FontTools, or
opentype.js.

OpenType is a font technology specification. Product and project names
are used only to describe compatibility or related workflows.

------------------------------------------------------------------------

**Project:** OpenType Professional Studio\
**Focus:** Bengali / Bangla OpenType font development\
**Type:** Browser-based, client-side editor
