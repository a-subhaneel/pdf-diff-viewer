# PDF Diff Viewer

A browser-based PDF comparison tool with intelligent visual diff highlighting. Compare PDFs instantly without installation or system dependencies.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node Version](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen.svg)

## ✨ Features

- **🌐 Browser-Based** - Runs entirely in the browser using PDF.js
- **🚀 Zero Setup** - No GraphicsMagick, ImageMagick, or GhostScript required
- **🔒 Privacy First** - PDFs never leave your machine, all processing is client-side
- **🎯 Smart Alignment** - Auto-alignment algorithm handles minor layout shifts
- **📝 Word-Level Detection** - Intelligent text extraction with word-level highlighting
- **⚡ Instant Feedback** - Real-time visual diff with color-coded differences
- **🎨 Visual Overlay** - Side-by-side comparison with highlighted changes
- **💻 Cross-Platform** - Works on any OS with a modern browser

## 🚀 Quick Start

### Installation

```bash
npm install pdf-diff-viewer
```

### Usage

```bash
npm start
```

Then open your browser to `http://localhost:3000`

### Manual Usage (No Installation)

Simply open `public/index.html` in your browser - no server required!

## 📖 How It Works

1. Select two PDF files using the file inputs
2. Click "Compare PDFs"
3. View the visual diff with highlighted differences
4. Red highlights show changed or different content
5. Auto-alignment compensates for minor layout shifts

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
├── public/
│   ├── index.html          # Main HTML interface
│   └── app.js              # AngularJS app with comparison logic
├── server.js               # Express server (optional)
├── comparePdfs.js          # Node.js comparison utilities
├── package.json
└── README.md
```

## 🆚 Comparison with Other Tools

### vs. compare-pdf npm package

| Feature | pdf-diff-viewer | compare-pdf |
|---------|----------------|-------------|
| **Environment** | Browser (client-side) | Node.js (server-side) |
| **Dependencies** | None (pure JavaScript) | GraphicsMagick, ImageMagick, GhostScript |
| **Use Case** | Manual visual comparison | Automated testing |
| **Setup Time** | Instant (open HTML) | Install + system deps |
| **Output** | Interactive visual overlay | Pass/fail + saved PNGs |
| **Target Users** | End users, designers | Developers, QA automation |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [PDF.js](https://mozilla.github.io/pdf.js/) by Mozilla for PDF rendering
- [AngularJS](https://angularjs.org/) for the frontend framework
- [pixelmatch](https://github.com/mapbox/pixelmatch) for pixel comparison algorithms

## 📧 Support

For issues and questions, please open an issue on [GitHub](https://github.com/yourusername/pdf-diff-viewer/issues).

## 🔗 Links

- [GitHub Repository](https://github.com/yourusername/pdf-diff-viewer)
- [NPM Package](https://www.npmjs.com/package/pdf-diff-viewer)
- [Report Bug](https://github.com/yourusername/pdf-diff-viewer/issues)
- [Request Feature](https://github.com/yourusername/pdf-diff-viewer/issues)

---

Made with ❤️ for developers who need visual PDF comparison
