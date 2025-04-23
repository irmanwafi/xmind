# XMind Smart Converter

> Transform raw tabular data into mind maps and presentations

![XMind Logo](public/static/faviconX.png)

## 🌟 Overview

XMind Smart Converter is a web application that provides a step-by-step tutorial for transforming raw data from spreadsheets into structured mind maps and PowerPoint SmartArt. This tool bridges the gap between unstructured tabular data and visual representations that are easier to understand and present.

## 🛠️ Features

- **Data Transformation**: Convert raw spreadsheet data into hierarchical structures
- **ChatGPT Integration**: Utilize AI prompts to structure your data intelligently
- **Markdown Conversion**: Transform data into hierarchical markdown format
- **XMind Visualization**: Create beautiful mind maps from structured data
- **SmartArt Export**: Generate PowerPoint presentations with SmartArt diagrams
- **Complete Tutorial**: Step-by-step guide with examples and templates

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- [pnpm](https://pnpm.io/) package manager

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd xmind
   ```

2. Install dependencies:
   ```bash
   cd public
   pnpm install
   ```

3. Start the development server:
   ```bash
   pnpm dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

## 📋 How to Use

The application guides you through the following steps:

1. **Import Raw Data**: Start with your tabular data from a Google Sheet or Excel file
2. **Use ChatGPT**: Transform your data with the provided intelligent prompt templates
3. **Convert to Markdown**: Format your data as hierarchical markdown
4. **Import to XMind**: Create a mind map visualization of your structured data
5. **Finalize in SmartArt**: Export to PowerPoint for presentations

## 🧪 Testing

Run the tests to ensure everything is working correctly:

```bash
pnpm test
```

This will run both end-to-end tests and unit tests.

## 🏗️ Built With

- [SvelteKit](https://kit.svelte.dev/) - The web framework
- [TailwindCSS](https://tailwindcss.com/) - For styling
- [Vite](https://vitejs.dev/) - Build tool
- [TypeScript](https://www.typescriptlang.org/) - Type safety
- [Playwright](https://playwright.dev/) - End-to-end testing
- [Vitest](https://vitest.dev/) - Unit testing