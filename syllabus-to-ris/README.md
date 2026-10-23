# Syllabus to RIS

*Version 2.2*

A small browser tool that turns a course syllabus into a RIS file that's ready to import into **VU Reading Lists**. Lecturers paste or upload their syllabus. The tool splits it into readings, keeps them in order under their week headings, reads each reading's importance and notes, and adds a DOI, ISBN or link wherever one can be found. The result imports straight into VU Reading Lists as a new list.

**Author:** Eran Keidar, Vrije Universiteit Amsterdam
**Contact:** e.keidar@vu.nl

---

## What it does

- **Reads the syllabus.** You can paste text or upload a PDF, Word (.docx) or text file. Files are read in the browser and never uploaded to a server.
- **Finds the readings.** It splits the text into separate references, keeps headings as sections, and reads each reading's importance (Required reading, Recommended reading or Optional reading). See [Marking sections and importance](#marking-sections-and-importance-in-your-syllabus).
- **Keeps the notes.** Remarks such as "PDF in Canvas", page counts and "Introduction and Chapter 1" go into each reading's note.
- **Adds identifiers.**
  - It uses DOIs already in the text and converts library proxy links (e.g. `doi-org.vu-nl.idm.oclc.org`) to normal `doi.org` links.
  - It searches **Crossref**, then **OpenAlex**, for missing DOIs. OpenAlex is searched by title first. For papers without a DOI (working papers, reports), it takes the web link OpenAlex has for them.
  - It searches **Google Books**, then **Open Library**, for the ISBN of books and book chapters.
  - Readings with only a web link are typed as web pages or reports, so VU Reading Lists handles them correctly.
- **Lets you check everything.** Each reading has a status:
  - 🟢 **DOI / ISBN**: identified, so the library can link it to its holdings
  - 🔵 **Web link**: imports as a web page or report
  - 🟠 **Needs a look**: no identifier found, or an uncertain match (for example a different edition) for you to accept or reject

  Every field can be edited. You can merge two lines that belong together, add readings, and retry all amber readings with one click.
- **Exports RIS.** Download one file for the whole list, or one file per week.

## How to use it

1. Open `syllabus-to-ris.html` in Chrome, Edge, Firefox or Safari. Double-clicking the file is enough; an internet connection is needed for the lookups.
2. Paste the reading list (or the whole syllabus), or upload the file.
3. Fill in your email address. Crossref and OpenAlex answer faster and more reliably when it's included, and it is only sent to them.
4. Click **Find readings** and wait for the searches to finish (about 1–3 minutes for 20–30 readings).
5. Check the amber readings. Accept or reject suggested matches, or paste a DOI or ISBN under **Edit**.
6. Download the .ris file.

## How links to the full text are found

- **Readings with a DOI or ISBN** link to the library's holdings. With your email address filled in, the tool also asks [Unpaywall](https://unpaywall.org) for a free, legal full-text copy and adds it as a second link.
- **Readings without a DOI or ISBN** (working papers, reports, policy briefs) are looked up in OpenAlex. The tool then picks the best link it can find, in this order:
  1. **Open full text**: a copy OpenAlex marks as openly available.
  2. **Archived copy of the full text**: a copy of the original PDF saved by the Internet Archive's Wayback Machine. Older working papers often move or disappear from their publisher's site, but the archived copy stays available.
  3. **PDF link (not checked)**: a PDF address the tool couldn't check.
  4. **Record page**: a catalogue or repository page, which may not include the full text.
- **Each reading shows its link type.** For a PDF link or record page, a **Replace with a better link** field appears.
- **Google Scholar fallback.** Google Scholar can't be searched automatically. If the tool finds nothing at all, the reading gets a **Google Scholar search link** for its main title (in quotes, the part before any colon) and first author, as an extra online link.
  - VU Reading Lists also tries to link every reading through the library after import: it matches ISBNs against the catalogue and, for journal articles, uses DOIs or the library's link service (OpenURL). Students then see buttons such as **Check availability** or **Check for full text**. Talis doesn't document what happens to readings without any identifier, so check those in your list after importing.
  - It's on by default; turn it off under **Import settings** if you'd rather leave such readings without a link.
  - A direct link is better for students, so paste one when you can.

## Marking sections and importance in your syllabus

VU Reading Lists has three importance levels:

- **Required reading**
- **Recommended reading**
- **Optional reading**

The tool reads them from the syllabus, so lecturers only need to write their syllabus in a recognisable way.

### Importance: the options

| Where | How to write it | Example |
|---|---|---|
| One reading, label at the start | Start with a label and a colon | `Required: Putnam, R. D. (1995). Bowling alone…` |
| One reading, tag anywhere | Add the label in square or round brackets | `Anderson, B. (2006). Imagined Communities. Verso. [optional]` |
| A group of readings | A heading on its own line; it applies to the readings below it until the next section or group heading | `Required readings`, `Recommended reading`, `Further reading` |
| Readings with no label | In the check step, choose a level and click **Set for all unmarked** | e.g. set them all to Required reading |

Words that are recognised:

| Level | English | Dutch |
|---|---|---|
| Required reading | Required, Essential, Core, Compulsory, Mandatory, Obligatory | Verplicht, Verplichte literatuur |
| Recommended reading | Recommended, Suggested | Aanbevolen, Aanbevolen literatuur |
| Optional reading | Optional, Further reading, Additional reading, Background reading, Extra reading | Optioneel, Facultatief |

In the check step you can change the importance of any reading with the menu on its card. **Set for all unmarked** gives every reading without importance the same level in one click.

### Sections: the options

Write each heading on its own line:

| Kind | Example |
|---|---|
| Numbered sessions | `Week 2: Social capital`, `Session 3`, `Lecture 4`, `Seminar 1`, `Tutorial 2`, `College 5`, `Bijeenkomst 6` |
| Named themes | `Section: Theories of capital`, `Theme: Inequality`, `Thema: Ongelijkheid` |
| Markdown headings | `## Global goals` |

### Example

This example uses every way of marking importance. It's also the list that **Load example** puts into the tool.

```
Week 1: Introduction
Required: Putnam, R. D. (1995). Bowling alone: America's declining social capital. Journal of Democracy, 6(1), 65–78.
Recommended: Granovetter, M. S. (1973). The strength of weak ties. American Journal of Sociology, 78(6), 1360–1380.
Optional: Anderson, B. (2006). Imagined Communities: Reflections on the Origin and Spread of Nationalism. Verso. Introduction (12 pages)

Week 2: Forms of capital
Required readings
Bourdieu, P. (1986). The forms of capital. In J. Richardson (Ed.), Handbook of Theory and Research for the Sociology of Education (pp. 241–258). Greenwood. (PDF in Canvas)
Coleman, J. S. (1988). Social capital in the creation of human capital. American Journal of Sociology, 94, S95–S120.
Further reading
Lin, N. (2001). Social Capital: A Theory of Social Structure and Action. Cambridge University Press.

Week 3: Global goals
United Nations (2015). Transforming our world: the 2030 Agenda for Sustainable Development. https://sdgs.un.org/2030agenda [recommended]
```

What the tool makes of it:

| Reading | Section | Importance | Why |
|---|---|---|---|
| Putnam (1995) | Week 1: Introduction | Required reading | starts with `Required:` |
| Granovetter (1973) | Week 1: Introduction | Recommended reading | starts with `Recommended:` |
| Anderson (2006) | Week 1: Introduction | Optional reading | starts with `Optional:` |
| Bourdieu (1986) | Week 2: Forms of capital | Required reading | below the heading `Required readings` |
| Coleman (1988) | Week 2: Forms of capital | Required reading | below the heading `Required readings` |
| Lin (2001) | Week 2: Forms of capital | Optional reading | below the heading `Further reading` |
| United Nations (2015) | Week 3: Global goals | Recommended reading | tag `[recommended]` at the end |

### What reaches VU Reading Lists

- **Importance is imported.** It's written to the RIS field `U1`, using VU Reading Lists' exact labels: `Required reading`, `Recommended reading` and `Optional reading`. A list exported from VU Reading Lists uses the same field and wording. The label must match exactly, or the reading arrives with "Importance not set", so the tool doesn't let you change it.
- **Sections are not imported, but headings are.**
  - VU Reading Lists can't create real sections from a RIS file.
  - The tool writes each section heading as a *paragraph* (the Talis RIS record `TY - NOTE`) placed above that section's readings. Imported into a new list, the list arrives in order with its week headings.
  - To turn the headings into real sections, use **Add section** at each heading and move the readings into it.
  - Each reading's note also starts with its section, and you can download one file per section.
- **Creating sections automatically** would need the Talis Reading Lists API. It requires credentials that Talis issues to the institution, a server to run on, and a Talis user account to act as. That's a project for the library or IT, not something a page like this can do.

## Importing into VU Reading Lists

1. Sign in to VU Reading Lists and open **My Bookmarks**.
2. Choose **Add → Import citations** and select the .ris file.
3. Tick **Add imported resources to a new list** and click **Import**. The readings keep their order, and each week heading appears as a paragraph above its readings. (Without the tick, the readings only go to My Bookmarks, and the order and headings are lost.)
4. To create real sections, use **Add section** at each heading paragraph and move that week's readings into it.

A few things to know about the import:

- Readings with a DOI or ISBN are matched to the library's holdings. Their details may be updated from the catalogue.
- A file can hold up to 300 readings.
- For readings marked "PDF in Canvas", upload the file or request a digitisation from the list item.

### Import settings (in the tool)

Under **Import settings** (closed by default) there are four switches. All are on by default, and most lecturers can leave them as they are:

- **Headings as paragraphs:** add each section heading to the list as a paragraph above its readings.
- **Google Scholar fallback:** link readings with no DOI, ISBN or other link to a Google Scholar search.
- **Section in the note:** start each reading's *note for students* with its section.
- **Importance:** set the importance level. When off, the level is added to the note instead.

The importance labels can't be changed: they are VU Reading Lists' fixed wording (Required reading, Recommended reading, Optional reading).

See also the [Manual VU Reading Lists](https://maken.wikiwijs.nl/218892/Manual_VU_Reading_Lists).

## Good to know

- **Searches are paced on purpose.** The free services limit how many searches they accept per minute. If some readings show "Couldn't reach …", wait a minute and click **Search again for amber readings**.
- **Free allowances are shared.**
  - OpenAlex gives one small free daily allowance to everyone on the same network, such as the VU network. If its searches start failing, get a free personal key at openalex.org/settings/api and paste it under **OpenAlex API key** in the tool. The key is kept only in that browser.
  - Google Books also has a shared daily limit. When it's reached, the tool uses Open Library instead.
- **Check ISBNs for the right edition.** ISBNs found through Google Books or Open Library are the best match for the year in the syllabus. Confirm it's the edition students should use.
- **Some readings have no identifier.** Working papers, reports, policy briefs and dissertation summaries often have no DOI or ISBN. The tool then looks them up in OpenAlex, which lists many of them with a web link, and adds that link. Google Scholar can't be searched automatically (it offers no public search service), so if OpenAlex doesn't have it, you can copy a link from Google Scholar into the **Paste a link, DOI or ISBN** field on an amber reading. With a link, the reading imports as a report or web page.
- **Unusual layouts may need a manual fix.** The syllabus parser handles common citation styles (APA, Harvard, Chicago, Vancouver). For unusual layouts, use **Edit → Original text → Read original text again**, or **Merge up**.

## Privacy

The tool runs in your browser and your syllabus file is never uploaded. It does need an internet connection.

- To find identifiers and full-text links, it sends the title, authors and DOI of each reading to Crossref, OpenAlex, Google Books, Open Library, Unpaywall and the Internet Archive.
- If you fill in your email address, it goes to Crossref, OpenAlex and Unpaywall.
- Fonts and the PDF and Word readers are loaded from Google Fonts and cdnjs.
- Nothing is stored or sent anywhere else.

The README is also available inside the tool: click **Read the README** in the footer.

## Technical details

- A single, self-contained HTML file with no installation and no server.
- Libraries are loaded from cdnjs: mammoth.js for Word files and pdf.js for PDFs.
- Services queried from the browser:
  - `api.crossref.org`
  - `api.openalex.org`
  - `www.googleapis.com/books`
  - `openlibrary.org`
  - `api.unpaywall.org` (free full-text copies of readings with a DOI; only when an email address is filled in)
  - `archive.org/wayback/available` (archived copies of PDFs whose original address may no longer work)
- The only data sent is reading titles, authors and DOIs, plus the email address if one is filled in.
- RIS fields follow Talis Aspire's [Mapping RIS fields to Talis Aspire](https://support.talis.com/hc/en-gb/articles/17338816364189-Mapping-RIS-fields-to-Talis-Aspire):
  - Types: `JOUR` article, `CHAP` chapter, `BOOK` book, `ELEC` web page, `RPRT` report, `THES` thesis, `CONF` proceedings, `ABST` document. `GEN` isn't used, because Talis rejects records with it.
  - `TI` title; `T2` journal or book title; `AU` authors; `A2` editors of the book a chapter is in; `ED` editors of a whole book.
  - `PY` year; `VL`, `IS`, `SP`, `EP` for volume, issue and pages; `PB` publisher.
  - `SN` ISBN; `DO` DOI; `UR` link; `U1` importance; `N1` Study Note.
  - Tags Talis ignores (`KW`, `JO`, `T3`, `CY`) aren't written.
- **Hosting:** the file can be put on any static web host (for example a faculty site or GitHub Pages) so lecturers can use a link instead of a file. Canvas file previews usually block scripts, so link to the hosted page from Canvas rather than uploading the file there.

## Questions and feedback

Contact Eran Keidar at **e.keidar@vu.nl**.
