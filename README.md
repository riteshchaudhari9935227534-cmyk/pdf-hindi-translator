# PDF Hindi Translator (starter MVP)

A small FastAPI website that accepts an English text-based PDF (up to 150 pages by default), translates text blocks to Hindi through a configured LibreTranslate-compatible API, and attempts to place the Hindi text back into the original page boxes.

## Important limitations

- This is a starter project, not a production-grade typesetting system.
- Exact layout preservation cannot be guaranteed because Hindi text can be longer than English.
- Scanned/image-only PDFs are not translated in this version. OCR (for example Tesseract) must be added.
- Complex tables, columns, equations, headers/footers, and mixed-language pages need manual review.
- Translation quality, speed, and price depend on the translation endpoint. Public free endpoints may rate-limit, be unavailable, or impose daily limits. There is no dependable unlimited free translation API.
- Render free services may sleep, have memory/time limits, and use ephemeral storage. This may not reliably process large 150-page files.

## Run locally

1. Install Python 3.11 or newer.
2. Install a Devanagari font:
   - Ubuntu/Debian: `sudo apt-get install fonts-noto-core`
   - Windows: install Noto Sans Devanagari and set `HINDI_FONT_PATH` to the `.ttf` file.
3. Create and activate a virtual environment:
   - Windows: `python -m venv .venv` then `.venv\\Scripts\\activate`
   - macOS/Linux: `python3 -m venv .venv` then `source .venv/bin/activate`
4. Install packages: `pip install -r requirements.txt`
5. Configure `LIBRETRANSLATE_URL` to a translation endpoint you are allowed to use. If it requires a key, set `LIBRETRANSLATE_API_KEY`.
6. Start: `uvicorn app:app --reload`
7. Open `http://127.0.0.1:8000`

## Deploy

The included `render.yaml` is a starting point for Render:
1. Create a GitHub repository and upload these project files.
2. In Render, create a new Blueprint and connect the repository.
3. Set `LIBRETRANSLATE_URL` and (if required) `LIBRETRANSLATE_API_KEY` in the service environment.
4. Deploy and test with a small, non-sensitive PDF first.

Free hosting availability and limits change. Check the provider's current limits before relying on it for large documents. For public use, add authentication, per-user quotas, file retention/automatic deletion, malware scanning, rate limiting, and durable job storage. Do not upload confidential PDFs to an untrusted translation provider.
