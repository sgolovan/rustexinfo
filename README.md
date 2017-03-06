# rustexinfo

A weekend project which implements support for Russian language in GNU Texinfo

## Requirements

* **GNU Texinfo** 6.0 or newer
* **LuaTeX** 0.85 or newer
* **Tcl** 8.6 or newer (for the **rutexindex** postprocessor)

## Usage

* Use the UTF-8 encoding for your Texinfo document.

* Put the following as the very first lines to ypur Texinfo
  source:

      \input texinfo
      @include russian.itexi

* Use **LuaLaTeX** to actually build the PDF document from the source, and use
  the supplied **rutexindex** script to postprocess the index files (it takes
  care about sorting Russian words):

      PDFTEX=luatex TEXINDEX=./rutexindex texi2pdf filename.texi

## Implementation details

* First, the **russian.itexi** replaces the default Computer Modern fonts
  which don't have cyrillic characters by the Computer Modern Unicode fonts.
  It's done via the `luaotfload` package, hence **LuaTeX** is a requirement.

* Second, the new language `@russian` is created and the hyphenation patterns
  for it are loaded (another reason why the LuaTeX is used, as it can load
  hyphenation patterns dynamically).
