# Onyx Captions website

Static landing page for the Onyx Captions DaVinci Resolve extension, hosted on GitHub Pages and used as the store website for Polar, the payment provider and Merchant of Record.

No build step — plain HTML, CSS and a little JavaScript.

```
index.html      Landing page (headline, demo video, features, price, FAQ, support, refund line)
terms.html      Terms of Service
privacy.html    Privacy Policy
refund.html     Refund Policy
assets/
  style.css     All styles
  main.js       Demo-video fallback animation + footer year
  favicon.svg   Logo / favicon
  demo.mp4      Demo recording (web version)
downloads/
  Install-Onyx-Captions.lua   ← the free trial installer (add before launch)
```

## Before launch 

- **Free trial installer:** build it in the extension's repository with `npm run installer` and copy `release/Install Onyx Captions.lua` to `downloads/Install-Onyx-Captions.lua` (no spaces in the web address; browsers still save it as *Install Onyx Captions.lua*). Every *Download free trial* link points there. Keep the file name the same for each release so the links never change.
- **Polar product:** a one-time $20 product with two benefits: *License Keys* with an activation limit of **2** (the site promises two computers), customers allowed to deactivate activations themselves (the FAQ says they can), and no expiry; and *File Downloads* with the same installer.
- **Checkout link:** the *Get Lifetime License* button in `index.html` uses the product's Polar checkout link (Products › Checkout Links). Create a new link and update it there if you ever change the product.
- Check that the feature bullets, the compatibility table and the FAQ still match the extension after each release, and that `privacy.html` section 4 matches what the extension sends over the network.

### Demo video

`assets/demo.mp4` is the web version of the demo recording (H.264 MP4, 1080p, about 10 MB). Keep it well under 100 MB — GitHub rejects larger files. To make a web version from a full-size recording:

```bash
ffmpeg -i recording.mp4 -map 0:v:0 -map 0:a:0? -vf "scale=1920:-2" -c:v libx264 -preset slow -crf 24 -pix_fmt yuv420p -c:a aac -b:a 128k -movflags +faststart assets/demo.mp4
```

Until `assets/demo.mp4` exists, the page shows an animated caption preview instead.

To use YouTube or Vimeo instead, replace the `<video>` element in `index.html` with the `<iframe>` shown in the comment above it.

## Preview locally

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Publish on GitHub Pages

1. Create a GitHub repository and push this folder to its `main` branch.
2. In the repository: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main`, folder `/ (root)`.
3. After a minute the site is live at `https://<username>.github.io/<repo>/`.
4. Optional custom domain: add it under **Settings → Pages → Custom domain** and enable **Enforce HTTPS**.

Use the resulting URL as your website in Polar's account review.
