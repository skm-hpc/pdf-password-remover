# PrimeRonin PDF Unlocker

A privacy-first, browser-based PDF password remover that processes PDF
files locally in the browser.

**Live application:**
<https://skm-hpc.github.io/pdf-password-remover/>  
**GitHub repository:** <https://github.com/skm-hpc/pdf-password-remover>

> **Author:** PrimeRonin  
> **License:** MIT  
> **Runtime:** Modern web browser  
> **Processing model:** Client-side / browser-only

------------------------------------------------------------------------

## Overview

**PrimeRonin PDF Unlocker** is a standalone web application for removing
password protection from PDF documents when the user has the right or
permission to process those documents.

The application is designed around direct PDF decryption rather than
converting document pages into images. The unlocked result remains a
PDF, avoiding the quality and structural limitations associated with
PNG/JPEG page reconstruction.

No backend, database, application server, or build system is required.

------------------------------------------------------------------------

## Main Features

### 🔐 Direct PDF Password Removal

The primary unlock workflow removes the PDF encryption through a
browser-based PDF decryption engine.

- PDF remains a PDF.
- No PNG conversion.
- No JPEG conversion.
- No canvas-based page reconstruction for the normal unlock path.
- Text remains PDF text.
- Vector content remains PDF content.
- PDF objects are retained as part of the decrypted PDF structure.
- The resulting file can be downloaded directly from the browser.

### 📄 Single PDF Mode

Single PDF mode is enabled by default.

1.  Select one PDF.
2.  Enter its password.
3.  Click **Unlock File**.
4.  Download the unlocked PDF.

This keeps the normal workflow simple for users who only need to process
one document.

### 📚 Multiple PDF Mode

Enable **Multiple PDFs** when several protected documents need to be
processed.

Multiple mode allows the user to:

- Select multiple PDF files in one upload action.
- Display every selected PDF as an individual file entry.
- Enter a separate password for every PDF.
- Match each password directly with its corresponding PDF.
- Remove individual files from the queue.
- Process all queued PDFs independently.
- Continue processing other files if one file fails.

Example:

``` text
invoice.pdf          Password: ********
statement.pdf        Password: ********
report.pdf            Password: ********
document.pdf          Password: ********
```

Each document has its own password, so different PDFs can use different
passwords.

### 📥 Individual Downloads

Every successfully unlocked PDF receives its own **Download** button.

This allows users to download only the documents they need.

### 📦 Download All Files

After multiple PDFs have been successfully unlocked, **Download All
Files** is available.

The feature:

- Collects all successfully unlocked PDFs.
- Packages them into a ZIP archive.
- Keeps the individual Download buttons available.
- Excludes files that failed to unlock.
- Provides one convenient download for the complete successful batch.

The generated archive uses a PrimeRonin-specific filename such as:

``` text
PrimeRonin_Unlocked_PDFs_2026-09-27.zip
```

### 🖱️ Drag and Drop

PDF files can be selected through the file picker or dragged into the
upload area where supported by the active mode.

### 👁️ Password Visibility

Password fields include a Show/Hide control so the entered password can
be verified before processing.

### 🌓 Dark and Light Themes

The interface supports both dark and light visual themes.

The selected theme is remembered locally in the browser.

### 📊 Processing Feedback

The interface provides:

- Processing status.
- Progress information where available.
- Success messages.
- Error messages.
- Cancellation support.
- Individual batch processing results.

### 📱 Responsive Interface

The application is designed for:

- Desktop browsers.
- Laptop browsers.
- Tablets.
- Mobile browsers.

------------------------------------------------------------------------

## How It Works

The normal processing architecture is:

``` text
Protected PDF
     +
Password
     ↓
Browser-side PDF decryption
     ↓
Unlocked PDF
     ↓
Browser download
```

The application does **not** intentionally upload the user's PDF or
password to an application server.

The important distinction is that the normal output is generated as PDF
data rather than rendering every page into an image.

------------------------------------------------------------------------

## PDF Preservation

The normal unlock workflow is intended to preserve the PDF as PDF data.

Unlike image-based reconstruction, the normal path does not
intentionally:

- Render pages to PNG.
- Render pages to JPEG.
- Convert text into page images.
- Rebuild every page with jsPDF.
- Rasterize the document.

The output is nevertheless a newly written/decrypted PDF file, so it
should not be expected to be byte-for-byte identical to the encrypted
source file.

PDFs containing digital signatures may require special consideration
because rewriting a PDF can affect signature validity.

------------------------------------------------------------------------

## Privacy

PrimeRonin PDF Unlocker is designed for client-side processing.

### Local processing

The selected PDF and password are handled by JavaScript running in the
user's browser.

The application does not intentionally send the document to a
PDF-processing backend.

### No password storage

PDF passwords are not intended to be stored in:

- LocalStorage.
- Cookies.
- URLs.
- Analytics systems.

### Third-party resources

The application may load required JavaScript libraries from public CDN
resources.

Therefore:

- A network connection may be required to load the application
  dependencies.
- The PDF itself is processed in the browser.
- Users requiring a completely offline environment can self-host the
  required dependencies.

------------------------------------------------------------------------

## Security and Responsible Use

This tool should only be used for documents that you own or are
explicitly authorized to process.

Do not use it to bypass access controls on documents without permission.

The application is a document-processing utility, not a
password-cracking or password-guessing system.

------------------------------------------------------------------------

## Technologies

| Technology       | Purpose                                               |
|------------------|-------------------------------------------------------|
| HTML5            | Application structure                                 |
| CSS3             | Responsive interface, themes and animations           |
| JavaScript       | Application logic and state management                |
| QPDF WebAssembly | Direct PDF decryption in the browser                  |
| ZIP generation   | Packaging successfully unlocked PDFs for Download All |

The application is intentionally implemented as a single-page HTML
application.

------------------------------------------------------------------------

## Project Structure

``` text
pdf-password-remover/
├── index.html
├── README.md
└── LICENSE
```

The main application is contained in `index.html`.

No Node.js project or build pipeline is required for the basic
application.

------------------------------------------------------------------------

## Running Locally

### Option 1 — Open the HTML file

Clone the repository:

``` bash
git clone https://github.com/skm-hpc/pdf-password-remover.git
cd pdf-password-remover
```

Then open:

``` text
index.html
```

in a modern browser.

### Option 2 — Use a local HTTP server

A local HTTP server is recommended for consistent browser behavior.

Using Python:

``` bash
python3 -m http.server 8080
```

Then open:

``` text
http://localhost:8080
```

------------------------------------------------------------------------

## GitHub Pages

The project is configured as a static web application and can be
published through GitHub Pages.

Current repository:

``` text
https://github.com/skm-hpc/pdf-password-remover
```

Current live application:

``` text
https://skm-hpc.github.io/pdf-password-remover/
```

### GitHub Pages configuration

In GitHub:

``` text
Repository
→ Settings
→ Pages
→ Build and deployment
→ Deploy from a branch
→ main / root
→ Save
```

`index.html` is the website entry point.

------------------------------------------------------------------------

## Development Workflow

Check the working tree:

``` bash
git status
```

Review changes:

``` bash
git diff
```

View history:

``` bash
git log --oneline --decorate --graph --all
```

Pull the latest remote changes:

``` bash
git pull --rebase origin main
```

After making changes:

``` bash
git add .
git commit -m "feat: describe the main feature"
git push origin main
```

### Recommended commit message style

Use feature-oriented messages for user-visible functionality.

Examples:

``` bash
git commit -m "feat: add multiple PDF unlock with individual passwords"
```

``` bash
git commit -m "feat: add download all unlocked PDFs as ZIP"
```

``` bash
git commit -m "fix: improve encrypted PDF password handling"
```

``` bash
git commit -m "ui: improve PDF upload workflow"
```

``` bash
git commit -m "docs: update project documentation"
```

------------------------------------------------------------------------

## Batch Processing Workflow

Multiple PDF mode follows this sequence:

``` text
Enable Multiple PDFs
        ↓
Upload multiple PDFs
        ↓
Create individual PDF entries
        ↓
Enter password for each PDF
        ↓
Unlock All Files
        ↓
Process each PDF independently
        ↓
Display individual results
        ↓
 ┌───────────────┐
 │ Download      │ ← individual file
 └───────────────┘
        +
 ┌─────────────────────┐
 │ Download All Files  │ ← ZIP archive
 └─────────────────────┘
```

A password belongs only to the PDF entry where it was entered.

------------------------------------------------------------------------

## Error Handling

### Incorrect password

Verify that the password is correct.

PDF passwords are case-sensitive.

If a batch contains several PDFs, an incorrect password for one PDF
should be reported against that specific file rather than silently
applying that password to every document.

### Corrupted or unsupported PDF

A PDF may fail if it is:

- Corrupted.
- Incomplete.
- Non-standard.
- Using an encryption configuration not supported by the browser-side
  processing engine.

Try opening the source PDF in a trusted desktop PDF viewer first to
verify that the document itself is readable.

### Browser memory

Large PDFs and large multi-file batches can consume significant browser
memory.

For very large batches:

- Process fewer files at a time.
- Close unnecessary browser tabs.
- Allow the browser time to release memory after large operations.

### Download All

Only successfully generated unlocked PDFs are included in the batch ZIP.

Individual Download buttons remain available even when Download All is
used.

------------------------------------------------------------------------

## Limitations

PrimeRonin PDF Unlocker does not guarantee successful processing of
every possible PDF.

Potential limitations include:

- Unsupported or unusual PDF encryption configurations.
- Corrupted PDF files.
- Extremely large documents.
- Browser memory limitations.
- Browser compatibility differences.
- Digital-signature validity after PDF rewriting.
- External CDN availability when dependencies are not self-hosted.

The output is a rewritten decrypted PDF rather than a byte-for-byte copy
of the encrypted source.

------------------------------------------------------------------------

## Code Organization

The application is intentionally self-contained in `index.html`.

The source is organized into:

### HTML

Defines:

- Application layout.
- PDF upload controls.
- Single/multiple mode controls.
- Password inputs.
- Batch file entries.
- Processing buttons.
- Individual download controls.
- Download All control.
- Status and progress areas.
- Theme controls.
- Informational dialogs.
- Privacy/legal notices.

### CSS

Contains:

- Application theme variables.
- Dark/light themes.
- Responsive layouts.
- Upload states.
- File cards.
- Password controls.
- Modern action buttons.
- Progress indicators.
- Result cards.
- Download controls.
- Toast notifications.
- Modal dialogs.

### JavaScript

Handles:

- PDF validation.
- File selection.
- Multiple-file queue management.
- Individual password management.
- PDF decryption.
- Batch processing.
- Cancellation.
- Progress updates.
- Blob creation.
- Individual downloads.
- ZIP generation.
- Download All.
- Theme persistence.
- UI state management.

------------------------------------------------------------------------

## Design Principles

The project follows several core principles:

1.  **PDF stays PDF** — avoid unnecessary image conversion.
2.  **Client-side processing** — keep document processing in the
    browser.
3.  **Password isolation** — each queued PDF has its own password.
4.  **Single mode by default** — keep the common workflow simple.
5.  **Batch when needed** — enable multiple processing explicitly.
6.  **Individual control** — every batch result can be downloaded
    independently.
7.  **Batch convenience** — provide a single ZIP download for successful
    results.
8.  **No unnecessary persistence** — do not store document passwords.
9.  **Responsive UI** — maintain usability across screen sizes.
10. **Transparent errors** — report failures against the relevant PDF.

------------------------------------------------------------------------

## License

This project is released under the MIT License.

See [`LICENSE`](LICENSE) for the complete license text.

------------------------------------------------------------------------

## Disclaimer

This software is provided **as-is**, without warranty.

Users are responsible for ensuring that they have the legal right or
explicit permission to remove protection from every document they
process.

PrimeRonin does not condone unauthorized access to protected documents.

------------------------------------------------------------------------

## Author

**PrimeRonin**

GitHub:

<https://github.com/skm-hpc/pdf-password-remover>

Live application:

<https://skm-hpc.github.io/pdf-password-remover/>

© 2026 PrimeRonin.
