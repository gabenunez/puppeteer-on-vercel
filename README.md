# Puppeteer on Vercel

A demonstration of how to run [Puppeteer](https://pptr.dev/) on [Vercel](https://vercel.com).

<img width="1546" height="874" alt="Puppeteer on Vercel" src="https://github.com/user-attachments/assets/e94645f2-9095-414d-8032-410182ae6543" />

## Deploy on Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/gabenunez/puppeteer-on-vercel)

## Purpose

This repository demonstrates how to successfully deploy and run Puppeteer on Vercel. Puppeteer is a powerful Node.js library that provides a high-level API to control headless Chrome/Chromium browsers, commonly used for:

- 📸 Taking screenshots of web pages
- 📄 Generating PDFs from web content
- 🧪 Automated testing
- ⚡ Performance testing

Running Puppeteer on Vercel requires special configuration due to the large size of the Chromium binary and the size constraints of functions. This project shows you exactly how to do it.

## What It Does

This Next.js application provides a simple web interface where you can:

1. Enter any URL (e.g., `https://vercel.com`)
2. Click "Capture" to take a screenshot
3. View the generated screenshot instantly

Behind the scenes, the app:

- Uses **regular Puppeteer** with bundled Chromium for local development
- Uses **`@sparticuz/chromium-min`** with a pre-packaged Chromium binary for Vercel deployment
- Automatically caches the Chromium executable path to improve cold start performance
- Handles URL validation and error management
- Defaults to the provided example Chromium .tar file if no production deployment is found to allow you to use the application without a publically accessible version.

## How It Works

### Local Development

- Uses `puppeteer` package with its bundled Chromium binary
- Works out of the box with no special configuration

### Vercel Deployment

1. **Build Time**: The `postinstall` script extracts Chromium binaries from `@sparticuz/chromium` and packages them into `public/chromium-pack.tar`
2. **Runtime**: The API route uses `@sparticuz/chromium-min` to download and extract the Chromium binary from the hosted tar file
3. **Caching**: The executable path is cached in memory to avoid re-downloading on subsequent requests

## Troubleshooting

### Timeout errors on Vercel

Note that Vercel functions have a 10-second timeout on the Hobby plan. If screenshots are taking too long, consider upgrading to Pro for higher limits.
