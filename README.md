# html2md

A bash tool that extracts content from HTML using CSS selectors and converts it to Markdown, supporting both processing of individual HTML documents via stdin and batch processing of multiple URLs from a file.

## Features

- Extract specific content from HTML using CSS selectors
- Convert HTML to well-formatted Markdown
- Process HTML from stdin or from URLs
- Batch process multiple URLs from a file
- Keeps special characters and formatting intact

## Requirements

- `curl` - for downloading web pages
- `pup` - for HTML parsing using CSS selectors
- `perl` - for text processing
- `pandoc` - for HTML to Markdown conversion

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/html2md.git
   ```

2. Make the script executable:
   ```bash
   chmod +x html2md
   ```

3. Consider moving it to your PATH:
   ```bash
   sudo cp html2md /usr/local/bin/
   ```

4. Install dependencies (example for Debian/Ubuntu):
   ```bash
   sudo apt install curl perl pandoc
   # For pup, you may need to install from GitHub:
   # https://github.com/ericchiang/pup
   ```

## Usage

### Basic Usage

```bash
cat page.html | html2md "div.content" > output.md
```

### View Help

```bash
html2md
html2md -h
html2md --help
```

### Process HTML from stdin

```bash
curl -s https://example.com | html2md "main"
```

### Process a single URL

```bash
echo "https://example.com" > urls.txt
html2md --urls=urls.txt "article"
```

### Process multiple URLs

Create a file with URLs, one per line:

```
https://example.com
https://example.org
# This line is a comment and will be skipped
https://example.net
```

Then process them all:

```bash
html2md --urls=urls.txt "div.content"
```

## CSS Selector Syntax

The tool uses [pup](https://github.com/ericchiang/pup) for CSS selection. Some examples:

- `article` - Select all article elements
- `div.content` - Select div elements with class "content"
- `#main-content` - Select element with id "main-content"
- `article p` - Select paragraphs inside article elements

For more details, visit: https://github.com/ericchiang/pup

## Markdown Output Format

The output is formatted using [Pandoc](https://pandoc.org/) with GitHub Flavored Markdown (GFM) plus the following extensions:
- bracketed_spans
- definition_lists
- fancy_lists
- implicit_figures
- smart (for proper quotes and dashes)
- subscript
- superscript

For more information about Pandoc's Markdown extensions, see the [Pandoc documentation](https://pandoc.org/MANUAL.html#pandocs-markdown).

## Examples

Extract the main content from a news article:

```bash
curl -s https://news-site.com/article/12345 | html2md "article.main-content" > article.md
```

Extract titles from multiple pages:

```bash
html2md --urls=blog-posts.txt "h1.title"
```

## License

[MIT License](LICENSE)
