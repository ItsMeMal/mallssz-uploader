# mallssz-uploader

Guest-first image uploader with a responsive UI, drag-and-drop, animated previews, real upload progress, direct links, Markdown/HTML snippets, and local upload history.

## Stack

- Static HTML, CSS, and vanilla JavaScript — no build step or framework.
- Designed to deploy directly on Vercel.
- Cloudinary unsigned image upload for storage.
- No account, login, or registration for visitors.

## Enable uploads (one-time setup)

The UI works without configuration, but real uploads stay disabled until a storage provider is configured. This repository uses Cloudinary unsigned uploads so no API secret needs to be exposed in the browser.

1. Create or open a Cloudinary account and copy the **Cloud name**.
2. In Cloudinary, create a new upload preset and set **Signing Mode** to **Unsigned**.
3. Restrict the preset to the image formats you want to accept (JPG, PNG, WEBP, GIF, AVIF), set a maximum upload size of **10 MB**, disable overwriting, and choose a dedicated folder if available. Unsigned upload presets are public, so configure strict limits.
4. Edit `config.js`:

   ```js
   window.UPLOADER_CONFIG = {
     cloudName: "your-cloud-name",
     uploadPreset: "your-unsigned-preset"
   };
   ```

5. Commit and push to GitHub. Vercel will redeploy automatically if the repository is connected.

Do **not** put a Cloudinary API secret in `config.js` or any browser code.

## Features

- Guest upload, multi-file selection, drag-and-drop, and previews.
- Accepts JPG/JPEG, PNG, WEBP, GIF, AVIF; maximum 10 MB per file and 20 files per batch.
- Real progress from the upload request, per-file success/error feedback, and retry failed files.
- Copies direct URL, Markdown, and HTML snippets.
- Stores the last 12 successful uploads in the current browser's local storage. It is not a cross-device account history.
- Removing an entry only removes it from local history; it does **not** delete the remote image.
- Subtle motion with support for `prefers-reduced-motion`.

## Deploy to Vercel

Import `ItsMeMal/mallssz-uploader` in Vercel and deploy from the `main` branch. The site is static; no build command or output directory is required. Set a custom domain in Vercel if desired.

## Important notes

- Upload functionality requires valid Cloudinary configuration. The repository intentionally ships with empty public config values.
- A public unsigned preset can be abused. Apply upload restrictions in Cloudinary and watch your storage/quota usage.
- This frontend does not provide remote deletion or a database-backed global upload gallery.
