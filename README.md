# PDF Diff Viewer

A browser-based PDF comparison library with intelligent visual diff highlighting. Compare PDFs instantly without installation or system dependencies. Works as both a standalone app and an embeddable library.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node Version](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen.svg)

## ✨ Features

- **🌐 Browser-Based** - Runs entirely in the browser using PDF.js
- **📦 Embeddable Library** - Import and use in your own applications
- **🚀 Zero Setup** - No GraphicsMagick, ImageMagick, or GhostScript required
- **🔒 Privacy First** - PDFs never leave your machine, all processing is client-side
- **🎯 Smart Alignment** - Auto-alignment algorithm handles minor layout shifts
- **📝 Word-Level Detection** - Intelligent text extraction with word-level highlighting
- **⚡ Instant Feedback** - Real-time visual diff with color-coded differences
- **🎨 Visual Overlay** - Side-by-side comparison with highlighted changes
- **💻 Cross-Platform** - Works on any OS with a modern browser
- **🔧 Configurable** - Extensive options for customization

## 🚀 Quick Start

### Installation

```bash
npm install pdf-diff-viewer
```

### Programmatic Usage (Embed in Your App)

```javascript
// Import the library
import PDFDiffViewer from 'pdf-diff-viewer';

// Or in browser (after including the script)
// <script src="node_modules/pdf-diff-viewer/src/PDFDiffViewer.js"></script>

// Create an instance
const viewer = new PDFDiffViewer('#results-container', {
  scale: 3.0,
  labelA: 'Original',
  labelB: 'Modified',
  highlightAlpha: 0.32
});

// Compare PDFs (accepts File objects, ArrayBuffers, or Uint8Arrays)
const fileA = document.getElementById('fileA').files[0];
const fileB = document.getElementById('fileB').files[0];

viewer.compare(fileA, fileB)
  .then(results => {
    console.log('Comparison complete:', results);
    console.log('Total pages:', results.totalPages);
    console.log('Total diff pixels:', results.totalDiffPixels);
  })
  .catch(error => {
    console.error('Comparison failed:', error);
  });
```

### HTML Setup

```html
<!DOCTYPE html>
<html>
<head>
  <title>PDF Comparison</title>
  <!-- Include PDF.js -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
</head>
<body>
  <input type="file" id="fileA" accept="application/pdf">
  <input type="file" id="fileB" accept="application/pdf">
  <button onclick="comparePDFs()">Compare</button>
  
  <div id="results"></div>

  <!-- Include PDFDiffViewer -->
  <script src="node_modules/pdf-diff-viewer/src/PDFDiffViewer.js"></script>
  <script>
    function comparePDFs() {
      const viewer = new PDFDiffViewer('#results');
      const fileA = document.getElementById('fileA').files[0];
      const fileB = document.getElementById('fileB').files[0];
      
      viewer.compare(fileA, fileB);
    }
  </script>
</body>
</html>
```

### Standalone Server Mode

Run as a standalone web server:

```bash
npx pdf-diff-viewer
```

Then open your browser to `http://localhost:3000`

**Custom port:**

```bash
PORT=8080 npx pdf-diff-viewer
```

### Direct Browser Use (No npm)

Simply open `public/index.html` directly in your browser - no server or npm required!

## 📖 How It Works

1. Select two PDF files using the file inputs (or pass them programmatically)
2. Click "Compare PDFs" (or call `viewer.compare(pdfA, pdfB)`)
3. View the visual diff with highlighted differences
4. Red highlights show changed or different content
5. Auto-alignment compensates for minor layout shifts

## 📚 API Reference

### Constructor

```javascript
new PDFDiffViewer(container, options)
```

**Parameters:**
- `container` (string|HTMLElement) - CSS selector or DOM element to render results
- `options` (Object) - Configuration options

**Options:**
- `scale` (number) - PDF rendering scale, default: 3.0 (~300 DPI)
- `maxShift` (number) - Max pixel shift for alignment, default: 3
- `colorTolerance` (number) - Color difference threshold, default: 120
- `minHighlightArea` (number) - Min area to highlight in pixels, default: 60
- `minWordSize` (number) - Min word box size in pixels, default: 8
- `highlightAlpha` (number) - Highlight transparency, default: 0.32
- `labelA` (string) - Label for first document, default: 'Document A'
- `labelB` (string) - Label for second document, default: 'Document B'
- `showPageNumbers` (boolean) - Show page numbers, default: true
- `cropRegions` (Array) - Regions to crop: `[{ page: 1, x, y, width, height }]`
- `maskRegions` (Array) - Regions to mask/ignore: `[{ page: 1, x, y, width, height }]`

### Methods

#### `compare(pdfA, pdfB)`

Compare two PDFs and render results.

**Parameters:**
- `pdfA` (File|ArrayBuffer|Uint8Array) - First PDF
- `pdfB` (File|ArrayBuffer|Uint8Array) - Second PDF

**Returns:** Promise<Object> - Comparison results with:
- `totalPages` - Number of pages compared
- `totalDiffPixels` - Total different pixels across all pages
- `pageResults` - Array of per-page results

#### `getResults()`

Get the most recent comparison results.

**Returns:** Object|null - Last comparison results

#### `clear()`

Clear the viewer and remove all rendered content.

#### `destroy()`

Destroy the viewer instance and clean up resources.

## 🔧 Technical Details

### Architecture

- **Frontend**: AngularJS with PDF.js for rendering
- **PDF Rendering**: PDF.js at 3x scale (~300 DPI)
- **Comparison Engine**: Custom pixel-diff algorithm with alignment
- **Text Detection**: Word-level text box extraction
- **Highlighting**: Intelligent dilation and area filtering

### Configuration

Key parameters in `public/app.js`:

```javascript
const SCALE = 3.0;              // Rendering DPI (3x = ~300 DPI)
const MAX_SHIFT = 3;            // Pixel search radius for alignment
const COLOR_TOLERANCE = 120;    // Color difference threshold
const MIN_HIGHLIGHT_AREA = 60;  // Minimum area to highlight (pixels)
const MIN_WORD_SIZE = 8;        // Minimum word box size (pixels)
const HIGHLIGHT_ALPHA = 0.32;   // Highlight transparency
```

## 📦 Project Structure

```
pdf-diff-viewer/
├── src/
│   └── PDFDiffViewer.js    # Main embeddable library
├── public/
│   ├── index.html          # Standalone app interface
│   └── app.js              # AngularJS standalone app
├── example/
│   └── index.html          # Usage example
├── bin/
│   └── cli.js              # CLI entry point
├── server.js               # Express server (optional)
├── package.json
└── README.md
```

## 💡 Usage Examples

### Basic Usage

```javascript
const viewer = new PDFDiffViewer('#container');
await viewer.compare(pdfFileA, pdfFileB);
```

### With Custom Options

```javascript
const viewer = new PDFDiffViewer('#container', {
  scale: 2.5,
  labelA: 'Version 1',
  labelB: 'Version 2',
  highlightAlpha: 0.4,
  colorTolerance: 100
});
```

### With Crop Regions (Compare Specific Areas)

```javascript
const viewer = new PDFDiffViewer('#container', {
  cropRegions: [
    { page: 1, x: 100, y: 150, width: 400, height: 200 }
  ]
});
```

### With Mask Regions (Ignore Dynamic Content)

```javascript
const viewer = new PDFDiffViewer('#container', {
  maskRegions: [
    { page: 1, x: 50, y: 30, width: 200, height: 60 }  // Ignore date field
  ]
});
```

### Using ArrayBuffers

```javascript
const bufferA = await fetch('/path/to/doc-a.pdf').then(r => r.arrayBuffer());
const bufferB = await fetch('/path/to/doc-b.pdf').then(r => r.arrayBuffer());

await viewer.compare(bufferA, bufferB);
```

## � Key Highlights

- **Client-Side Processing** - All PDF comparison happens in your browser, no server uploads needed
- **Zero System Dependencies** - No need for GraphicsMagick, ImageMagick, or GhostScript
- **Instant Setup** - Just open the HTML file in a browser, or run `npx pdf-diff-viewer` for the server version
- **Visual Feedback** - Interactive overlay showing exactly what changed and where
- **Privacy-Focused** - Your PDFs never leave your local machine
- **Lightweight** - Pure JavaScript solution without heavy binary dependencies

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [PDF.js](https://mozilla.github.io/pdf.js/) (v3.11.174) by Mozilla for PDF rendering
- [AngularJS](https://angularjs.org/) (v1.6.0) for the frontend framework
- [Express.js](https://expressjs.com/) for the optional web server

## 📧 Support

For issues and questions, please open an issue on [GitHub](https://github.com/a-subhaneel/pdf-diff-viewer/issues).

## 🔗 Links

- [GitHub Repository](https://github.com/a-subhaneel/pdf-diff-viewer)
- [NPM Package](https://www.npmjs.com/package/pdf-diff-viewer)
- [Report Bug](https://github.com/a-subhaneel/pdf-diff-viewer/issues)
- [Request Feature](https://github.com/a-subhaneel/pdf-diff-viewer/issues)

---

Made with ❤️ for developers who need visual PDF comparison
