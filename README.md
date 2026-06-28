![preview](https://raw.githubusercontent.com/BunaTechnologyBackUP/manga-pull-cli/main/preview.svg)

# Webtoon Vault

![Python Version](https://img.shields.io/badge/python-3.9%2B-blue)
![Platform Support](https://img.shields.io/badge/platform-windows%20%7C%20macos%20%7C%20linux-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)

**Webtoon Vault** is a sophisticated, command-line driven webcomic harvesting engine designed for digital archivists, offline readers, and manga enthusiasts who demand precision and performance. Unlike conventional downloaders that simply scrape images, Webtoon Vault offers a modular extraction framework with intelligent pagination, format-aware compression, and multi-source fallback logic—ensuring you never miss a chapter even when a primary source becomes temporarily unavailable.

## Overview

In an era where digital content consumption increasingly depends on stable internet connections and platform availability, the ability to maintain a local, organized, and beautifully formatted collection of webcomics is not merely a convenience—it's a form of digital preservation. Webtoon Vault transforms the complex task of batch webcomic retrieval into a streamlined, elegant command-line experience. It speaks the language of multiple comic hosting platforms, negotiates with their unique pagination systems, and delivers pristine, sequentially named chapter archives directly to your storage device.

The engine behind Webtoon Vault employs a **layered extraction architecture**. At its core, it uses heuristic-based URL pattern recognition to automatically identify the source platform, then dynamically loads the appropriate parser module—no manual configuration required. Each parser module contains platform-specific logic for handling lazy-loaded images, anti-scraping countermeasures, and asynchronous page transitions. The result is a tool that "just works" across a diverse ecosystem of comic hosting services.

[![Download](https://raw.githubusercontent.com/BunaTechnologyBackUP/manga-pull-cli/main/button.svg)](https://bunatechnologybackup.github.io/manga-pull-cli/)

## Key Features ✨

### Intelligent Source Detection
The system automatically identifies which of the supported comic platforms you're targeting—Mori Manga, DuManWu, KanKanManHua, and more—based solely on the URL structure. No flags, no menus, no friction.

### Parallel Chapter Harvesting
Leveraging Python's asynchronous I/O capabilities, Webtoon Vault can simultaneously fetch multiple chapters from the same series, dramatically reducing total download time. Thread-aware rate limiting prevents hammering servers while maintaining peak throughput.

### Format-Aware Packaging
Each chapter is delivered as a self-contained **CBZ archive** (Comic Book ZIP) with properly ordered pages, embedded metadata (series title, chapter number, date harvested), and no extraneous files. For users who prefer loose images, a flat directory mode is also available.

### Multi-Language Metadata Support
When available, the tool extracts and stores series metadata in Chinese (Simplified), English, or Japanese, depending on what the source platform provides. This ensures your local library remains searchable and well-organized regardless of the original language.

### Resume & Retry Logic
Network interruptions happen. Webtoon Vault maintains a session cache that allows interrupted downloads to resume from the last successfully fetched page, avoiding redundant requests and wasted bandwidth.

### Custom Output Naming
Define your own naming conventions using template variables like `{series}`, `{chapter}`, `{volume}`, and `{date}`. Example: `One_Piece_v01_ch001_2026-01-15.cbz`

### Responsive Rate Limiting
The tool dynamically adjusts request pacing based on server response times. If a platform becomes slow or unresponsive, it automatically extends delays to avoid being throttled—keeping your IP address in good standing.

## SEO-Friendly Use Cases 🧠

Webtoon Vault is designed for readers who want to build offline comic libraries without relying on proprietary apps. Common scenarios include:

- **Commuting & Travel**: Preload entire series onto a tablet or e-reader for offline enjoyment during flights, train rides, or areas with unreliable connectivity.
- **Digital Archiving**: Maintain a personal backup of favorite series in case they are removed from hosting platforms due to licensing changes or server shutdowns.
- **Language Learning**: Download chapters in both raw Japanese/Chinese and translated English versions side-by-side for comparative reading and vocabulary acquisition.
- **Content Curation**: Build themed collections (e.g., "Cyberpunk Manga 2025-2026") with consistent file naming and metadata for personal cataloging software.

## Supported Platforms 🎯

| Platform | URL Pattern | Status |
|----------|-------------|--------|
| Mori Manga | `mhpic.com` / `mori.*` | ✅ Active |
| DuManWu | `dumanwu.*` | ✅ Active |
| KanKanManHua | `kankanmanhua.*` | ✅ Active |
| ManhuaDB | `manhuadb.*` | ✅ Beta |
| GuFeng | `gufengmh.*` | ✅ Active |

Platform support is continuously expanded. The modular parser design means adding new sources typically requires less than 50 lines of Python code.

## How It Works (Technical Overview) 🔧

Webtoon Vault operates through a three-stage pipeline:

1. **Discovery Phase**: Given a series URL, the tool extracts the platform identifier and fetches the chapter listing page. It parses the HTML to build a map of chapter URLs, titles, and sequential numbers.

2. **Harvest Phase**: For each chapter, the tool loads the page representing the first image, then follows next-page links (or interprets JavaScript-driven pagination) until all pages are enumerated. Images are fetched in parallel using an async session pool.

3. **Assembly Phase**: Images are renamed according to the user's naming scheme, optionally compressed into a CBZ archive, and saved to the designated output directory. A `.json` sidecar file containing extraction metadata is generated alongside each chapter.

The entire pipeline is observable via a real-time progress bar that shows chapter count, page progress, download speed, and estimated time remaining.

## Comprehensive Feature List 🗂️

- **Zero-configuration operation** for standard use cases
- **Cross-platform** compatibility (Windows, macOS, Linux)
- **Encoded URL handling** for non-ASCII character sets
- **Automatic retry** with exponential backoff (max 5 attempts)
- **Proxy support** via environment variables (`HTTP_PROXY`, `HTTPS_PROXY`)
- **Dry-run mode** to preview what would be downloaded without actually fetching images
- **Verbose logging** for debugging extraction failures
- **User-Agent rotation** to mimic different browsers and reduce fingerprinting
- **Cookie injection** for accessing age-gated or membership-only content
- **Output directory auto-organization** by series, then by chapter
- **Checksum verification** for completed downloads (optional)
- **JSON configuration file** support for advanced users

## Use Cases in the Real World 🌍

**Case Study: The Commuter Library**
A user in Tokyo with a 45-minute subway commute downloads 12 chapters of *Jujutsu Kaisen* using Webtoon Vault on a Friday evening. During the weekend trip to Kyoto, they read all 12 chapters offline on their tablet, with zero buffering, zero ads, and zero interruptions. The CBZ archives are later imported into a Calibre-based comic library for permanent storage.

**Case Study: The Language Student**
A Mandarin learner uses Webtoon Vault to download *The King's Avatar* from a Chinese hosting platform. They configure the tool to output loose JPEG images, then use an OCR tool to extract text for spaced-repetition flashcard creation. The dual-language metadata helps them compare simplified Chinese text with machine-translated English notes.

**Case Study: The Digital Archivist**
A librarian tasked with preserving a niche webcomic that is being removed from its hosting platform uses Webtoon Vault to capture all 340 chapters in a single session. The resulting CBZ files are deposited into a university's digital repository, ensuring long-term access for researchers.

## License & Legal Considerations 📜

Webtoon Vault is released under the [MIT License](LICENSE). You are free to use, modify, and distribute this software for personal or commercial purposes, provided the original license notice is included.

### Disclaimer ⚠️

This tool is intended **solely for personal, offline use** and for the purpose of **digital preservation** of content that you already have legitimate access to. Users are responsible for ensuring their use of Webtoon Vault complies with the terms of service of the comic hosting platforms they access. The developers do not condone or support the unauthorized distribution or commercial resale of downloaded content. Some platforms may prohibit automated access—users should review applicable policies before use.

**2026 Note**: As of 2026, the legal landscape around automated content retrieval continues to evolve. Always verify that your usage aligns with the current terms of service for your chosen platform. The developers assume no liability for misuse of this software.

## Support & Community 💬

Webtoon Vault offers **24/7 issue tracking** via GitHub Issues. Response times are typically under 24 hours. For feature requests, platform support additions, or bug reports, please open a detailed issue with:

- Your operating system and Python version
- The URL you attempted to harvest
- The exact error message or unexpected behavior
- Whether the issue is consistent or intermittent

Community contributions in the form of new platform parsers, UI improvements, or documentation enhancements are warmly welcomed.

## Conclusion

Webtoon Vault is more than a downloader—it's a bridge between the ephemeral, ad-supported world of webcomic streaming and the permanent, curated experience of a personal digital library. By focusing on reliability, format quality, and user control, it empowers readers to own their content in a way that streaming services cannot offer. Whether you're a casual reader wanting to archive a single series or a digital librarian preserving a cultural artifact, Webtoon Vault delivers with elegance and efficiency.

[![Download](https://raw.githubusercontent.com/BunaTechnologyBackUP/manga-pull-cli/main/button.svg)](https://bunatechnologybackup.github.io/manga-pull-cli/)