# Changelog for [`HPDF` package](http://hackage.haskell.org/package/HPDF)

## Unreleased (factur-x)

   * PDF/A output, `Graphics.PDF.Archive`: `setPDFA (pdfa3b icc)` writes,
     when the document is saved, an uncompressed XMP metadata stream
     (pdfaid part and conformance, Dublin Core title/creator/description,
     pdf:Producer, and any `XMPExtension` with its PDF/A extension schema
     description), an OutputIntent (GTS_PDFA1) with the given ICC profile,
     a PDF 1.7 header with a binary comment line, and no image
     interpolation.
   * Associated files (PDF/A-3): `embedAssociatedFile` writes an
     EmbeddedFile stream (MIME /Subtype, /Params /Size, optional /ModDate)
     and a Filespec (/F, /UF, /AFRelationship, /Desc), listed in the
     catalog's /AF array and /Names /EmbeddedFiles name tree.
   * Factur-X / ZUGFeRD: `facturXExtension level` is the fx: XMP schema
     (DocumentType, DocumentFileName, Version, ConformanceLevel).
   * `pdfByteStringE` returns the document or the reasons it is not the
     PDF/A it was asked to be (a standard 14 font, which is not embedded).
   * Every document now has a trailer /ID (two copies of a 16-byte hash of
     its objects, so output stays deterministic) and an indirect Info
     dictionary; empty Author/Subject entries are left out and ASCII text
     is written as a literal string.
   * `PDFCatalog` gains a list of extra entries; `PdfState` gains
     `pdfaSettings`, `associatedFiles` and `documentProblems`.

## Unreleased (unicode-truetype)

   * Embedded TrueType fonts with Unicode text: `Graphics.PDF.Fonts.TrueType`
     (`readTrueTypeFont`, `mkTrueTypeFont`) writes a Type0 font over a
     CIDFontType2 with Identity-H encoding, the whole font as FontFile2, /W
     widths and a ToUnicode CMap.
   * `GlyphCode` is now 16 bits; `IsFont` gains `glyphCodeBytes` (default 1)
     and `encodeGlyphs`/`decodeGlyphs`; `fontGlyphs` builds a glyph run for
     any font. Standard 14 and Type1 fonts write the same bytes as before.
   * TrueType fonts are subset by default: when the document is saved, the
     font program keeps only the glyphs shown with it (plus glyph 0 and the
     components of composite glyphs, glyph ids unchanged so CIDToGIDMap stays
     /Identity), /W and ToUnicode cover those glyphs, and the BaseFont gets an
     `ABCDEF+` subset tag. `mkTrueTypeFontWith EmbedWhole` embeds the whole
     font. `subsetTrueType` is exported. Glyphs reach the subset through
     `recordGlyphs`, which `displayGlyphs`, `displayText`, `text` and the
     typesetting code call. `DrawState` gains `usedGlyphs` and `PdfState`
     gains `fontFinalizers`.

## 1.8

   * Added Github CI
   * Allow specifying encodings and merging them (#17)

## 1.7

   * Add transparency support and more function types (#16)

## 1.6.1

   * Fix for building with mtl-2.3

## 1.6.0

   * Allow parsing afm-data from bytestring

## 1.5.3

   * Fixed distribution issue (font files not correctly embedded in the sdist
     archive)

## 1.5.2

   * Embed fonts and encodings

## 1.5.1

   * Fix JPEG support

## 1.5.0

   * Fix build with recent compilers
   * Use hyphenation package
