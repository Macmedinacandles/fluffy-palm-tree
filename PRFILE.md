# Puppeteer Installation

Puppeteer is a Node.js library which provides a high-level API to control Chrome/Chromium over the DevTools Protocol.

## Installation Options

### Full Installation (with Chrome)
Install Puppeteer with a compatible Chrome browser downloaded automatically during installation:
```bash
npm i puppeteer
```

### Library Only (without Chrome)
Alternatively, install Puppeteer as a library without downloading Chrome:
```bash
npm i puppeteer-core
```

Use `puppeteer-core` when you want to manage the browser installation yourself or use an existing browser installation.

## Usage Example

Here's a basic example of using Puppeteer to automate browser interactions:

```javascript
import puppeteer from 'puppeteer';
// Or import puppeteer from 'puppeteer-core';

// Launch the browser and open a new blank page.
const browser = await puppeteer.launch();
const page = await browser.newPage();

// Navigate the page to a URL.
await page.goto('https://developer.chrome.com/');

// Set screen size.
await page.setViewport({width: 1080, height: 1024});

// Open the search menu using the keyboard.
await page.keyboard.press('/');

// Type into search box using accessible input name.
await page.locator('::-p-aria(Search)').fill('automate beyond recorder');

// Wait and click on first result.
await page.locator('.devsite-result-item-link').click();

// Locate the full title with a unique string.
const textSelector = await page
  .locator('::-p-text(Customize and automate)')
  .waitHandle();
const fullTitle = await textSelector?.evaluate(el => el.textContent);

// Print the full title.
console.log('The title of this blog post is "%s".', fullTitle);

await browser.close();
```
