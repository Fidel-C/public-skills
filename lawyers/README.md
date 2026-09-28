# Legal Case Timeline

**A free skill for Claude that builds a dated, source-cited chronology from your case documents.**

Give it a folder, a list of files, or a zip. It reads the documents and gives you a Word table you can check and use.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license)
[![Free to use](https://img.shields.io/badge/Price-Free-blue.svg)](#license)

---

## Contents

1. [What it does](#what-it-does)
2. [What you get](#what-you-get)
3. [Install the skill](#install-the-skill)
4. [How to use it](#how-to-use-it)
5. [How it handles dates and facts](#how-it-handles-dates-and-facts)
6. [Limits](#limits)
7. [Need more? Get in touch](#need-more-get-in-touch)
8. [License](#license)
9. [Follow and contact](#follow-and-contact)

---

## What it does

Legal Case Timeline reads your case documents and lists every significant event in date order. For each event it records:

- The event date, kept separate from the date of the document that mentions it
- What happened, in plain and neutral words
- A category, such as Notice, Payment or Court step
- The source document and page number
- Notes for anything a lawyer should check

It also merges repeat mentions of the same event into one row and keeps all the sources. It flags dates that conflict or are unclear. It shows whether each event is established or only alleged.

## What you get

A Word document (landscape) with this table:

| Date | Event | Category | Source | Review/Notes |
|---|---|---|---|---|

Events are sorted by date. Events with no usable date go in a separate table after the main one. The document ends with a **Potential Date Conflicts** section that lists each conflicting source and the date it gives.

You also get a Markdown copy of the same table.

Files it can read:

| Type | Notes |
|---|---|
| PDF | Read page by page. Scanned pages are read with OCR. |
| Word, ODT, RTF, PowerPoint | Converted to PDF first so page numbers exist. |
| Email (.eml) | Headers are kept, including the sent date. |
| Images (PNG, JPG, TIFF and others) | Read with OCR. |
| Spreadsheets (XLSX, CSV and others) | Cited by sheet and row, not by page. |
| Plain text | Cited by paragraph, not by page. |
| Zip files | Opened for you, including zips inside zips. |

---

## Install the skill

You need the file **`legal-case-timeline.skill`** (or the folder `legal-case-timeline`). Skills need a paid Claude plan with code execution turned on. Menu names change from time to time. If a step does not match your screen, check the [Claude Help Center](https://support.claude.com) for the current wording.

### Claude.ai on the web

1. Sign in at [claude.ai](https://claude.ai).
2. Click your name or profile icon, then open **Settings**.
3. Go to **Capabilities** and turn on **Code execution and file creation**.
4. Open the **Skills** section. It may be under **Customize** in the menu.
5. Click **Upload skill** and choose `legal-case-timeline.skill`. If Claude asks for a zip file, zip the `legal-case-timeline` folder and upload that.
6. Switch the skill on.
7. Start a new chat and follow the steps in [How to use it](#how-to-use-it).

Shortcut: if someone sends you the skill inside a Claude chat, the file card has a **Save skill** button. Click it and the skill installs in your account.

### Claude Desktop app and Claude mobile app

Skills you add on the web are tied to your account, so they also show up in the desktop and mobile apps. Install it on the web using the steps above, then open the app and start a chat. On desktop, make sure code execution and file creation is turned on in **Settings**. In the mobile app the `/` skill menu may not appear. See [Where the `/` skill menu works](#where-the--skill-menu-works).

### Claude Code (command line)

1. Copy the folder `legal-case-timeline` into your personal skills folder:
   - Mac or Linux: `~/.claude/skills/legal-case-timeline/`
   - Windows: `%USERPROFILE%\.claude\skills\legal-case-timeline\`
2. To use it for one project only, copy it to `.claude/skills/legal-case-timeline/` inside that project.
3. Install the tools the scripts need on your computer:
   - Python 3.9 or newer
   - `python-docx` (run `pip install python-docx pytesseract pillow`)
   - Poppler (gives you `pdftotext` and `pdftoppm`)
   - Tesseract OCR
   - LibreOffice (only needed to get page numbers for Word files)
4. Restart Claude Code. Type `/legal-case-timeline` and tell it which files to use.

### Claude API

Upload the skill through the Skills feature of the Claude API and attach it to your request with code execution turned on. The API rules change often, so follow the current guide at [docs.claude.com](https://docs.claude.com).

### Other platforms

The skill follows the standard Agent Skills format: a folder with a `SKILL.md` file and some scripts. Any tool that supports this format can load it. Check that tool's documentation for where skills go.

---

## How to use it

1. Start a new chat in Claude with the skill switched on.
2. **Select the skill first.** In the message box, type a forward slash `/`. A list of your skills appears. Pick **legal-case-timeline** (you can type `/legal` to filter the list). This tells Claude exactly which skill to use. Do this before you attach any documents.
3. Attach your documents. You can attach:
   - A zip file of the whole bundle
   - Several files at once
   - Files taken from a folder (select them all and drag them in)
4. Type a plain request. For example:
   - "Build a chronology from these case documents."
   - "Make a timeline from this zip and show me any date conflicts."
   - "Prepare a dated chronology for mediation from these files."
5. Wait while Claude reads the files. Large bundles take longer.
6. Claude gives you a Word document. Download it and open it.
7. Read the **Review/Notes** column first. Rows shaded amber need a human check. Rows shaded green are established.
8. Check the result against your original documents before you rely on it.

### Where the `/` skill menu works

| Where you use Claude | Slash menu | What to do |
|---|---|---|
| Claude.ai on the web | Yes, according to Anthropic's Help Center | Type `/` and pick **legal-case-timeline** |
| Claude desktop app | Yes, it uses the same menu as the web | Type `/` and pick **legal-case-timeline** |
| Claude Code (command line) | Yes | Type `/legal-case-timeline`, then describe the task and name the files |
| Claude mobile app (iPhone and Android) | Not confirmed | Skip the menu and write the skill name in your message (see below) |

I have not been able to confirm that the `/` menu works in the mobile app, and it may change between app versions. If you do not see the menu on your phone, it is fine. Claude also picks the skill on its own when your request matches it. To be sure, start your message with this line:

> Use the legal-case-timeline skill to build a chronology from the attached documents.

On mobile, installing and managing skills may also be limited. If you cannot find the **Skills** page in the app, install the skill on the web first. It will then be tied to your account.

Tips for better results:
- Give one matter at a time. Do not mix cases in one upload.
- Tell Claude which party you act for if it matters to how events are described.
- Say which country's date style you expect (for example day/month/year) if your documents use numbers like 03/04/2021.
- For very large bundles, upload in batches by document type (pleadings, then emails, then records) and ask Claude to merge the results.

---

## How it handles dates and facts

- **It never invents a date.** "March 2021" stays "March 2021". "Before 12 June 2021" stays open-ended.
- **Event date and document date are separate.** A witness statement signed in May 2023 about something in March 2022 is placed at March 2022. The May 2023 date shows in the Source column.
- **Duplicates are merged.** One event, many sources. If two sources give different dates, the row shows both, and the event is also listed under Potential Date Conflicts.
- **Allegations are labelled.** Each event is marked ESTABLISHED, ALLEGED (party), STATED (witness), DISPUTED or UNVERIFIED. A party repeating a claim in many papers does not make it established.
- **Checks it runs.** It compares stated weekdays to the calendar, looks for events in an impossible order, and flags unclear numeric dates and doubtful OCR digits.

---

## Limits

Please read this section before you use the output on a real matter.

**Accuracy and review**
- This is a first-pass tool. It can miss events, mistake a date, or pick the wrong source. A lawyer must check every row that matters against the original document.
- It gives no legal advice. It does not judge whether an event is legally important. It uses a broad rule and may include or leave out items you would decide differently.
- Its "established" and "alleged" labels are a starting point. You decide what is proven.

**Reading the documents**
- Handwriting is not read reliably. Poor scans, stamps, faxes and photos of paper may be read wrongly or not at all. OCR pages are marked so you can check them.
- Page numbers for Word files come from a converted copy and may differ from Word's own pages. Emails, spreadsheets and plain text have no pages, so they are cited another way.
- Password-protected files and encrypted zips cannot be opened. Outlook `.msg` files, audio and video files are not supported. Convert them first (for example, save emails as `.eml` or PDF).
- If a printed page number or Bates number differs from the PDF page, the tool may not always find it.
- Text is read best in English. Other languages may work, but date formats and results can be less reliable.

**Size and speed**
- Claude has a limit on how much it can read in one chat. Very large bundles (many thousands of pages) will not fit in one go. Split them into batches.
- Your Claude plan limits how much you can upload and how often you can run big jobs.

**Scope**
- It works only from the files you give it. It does not check court dockets, registries or the internet.
- It builds one timeline per run. It does not save your matter, learn from past matters or connect to case-management, e-discovery or document-management systems.
- It offers one fixed table layout and a default set of categories. Firm templates, branding, multi-user review, audit trails and secure storage are not included.
- It does not redact documents.

**Confidentiality**
- You are uploading case documents to an AI service. Before you do, check your client's consent, your firm's policy and your professional rules on confidentiality and AI tools. Check the terms and data settings of your Claude plan.

---

## Need more? Get in touch

If your work goes past these limits, I can help. I build specialised software for law firms and offices, made around how you work. Examples of what can be built:

- A standalone app that runs on your own systems, so documents stay in your control
- Support for very large document sets
- Your own categories, templates and branding
- Connections to your case-management or document-management system
- Multi-user review, sign-off and audit records
- Support for more languages and file types

Email me at **fidelchukwunyere@gmail.com** with a short note about your office and what you need.

---

## License

**MIT License**

Copyright (c) 2026 fidelcmedia

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

In plain words: it is free. You can use it, share it and change it, for personal or commercial work, at no cost. Keep the copyright line with it. There is no warranty, and you are responsible for checking the results.

---

## Follow and contact

**Follow @fidelcmedia**

[![Facebook](https://img.shields.io/badge/Facebook-@fidelcmedia-1877F2?logo=facebook&logoColor=white)](https://www.facebook.com/fidelcmedia)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-@fidelcmedia-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fidelcmedia)
[![YouTube](https://img.shields.io/badge/YouTube-@fidelcmedia-FF0000?logo=youtube&logoColor=white)](https://www.youtube.com/@fidelcmedia)
[![TikTok](https://img.shields.io/badge/TikTok-@fidelcmedia-000000?logo=tiktok&logoColor=white)](https://www.tiktok.com/@fidelcmedia)
[![X](https://img.shields.io/badge/X-@fidelcmedia-000000?logo=x&logoColor=white)](https://x.com/fidelcmedia)

**Email:** [fidelchukwunyere@gmail.com](mailto:fidelchukwunyere@gmail.com)
