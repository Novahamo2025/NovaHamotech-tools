# Browser support and remaining limitations

## Release qualification

The requested full acceptance standard is **not yet verified**. The app has real workspaces and exports, but browser QA, performance measurements and advanced feature gaps remain. Do not describe this build as 100% working or fully production-ready.

## Unavailable capability

- **PDF Password Protector:** no verified encryption engine is included. The page states it is unavailable and cannot export a misleading “protected” PDF.

## Reduced capabilities

- **Link Shortener:** URL cleanup and UTM building only; no globally hosted redirect.
- **Internet Speed Test:** browser connectivity and same-origin resource latency only; no bandwidth result.
- **Background removal:** manual transparent eraser, without automatic segmentation or subject recognition.
- **Watermark removal:** manual clone-source retouching, without automatic inpainting.
- **Image upscaling:** browser interpolation, without AI super-resolution.
- **Image resizing/cropping:** numeric controls with fit/cover; no draggable crop handles. Rotation is numeric; arbitrary angles may clip to the canvas. Metadata removal uses re-encoding, not exhaustive field auditing. Animated images flatten.
- **Image compositing:** shared top-left overlay positioning; collage uses a uniform grid. Text maker layers are line-based with shared typography/offset, not individually draggable layers.
- **Passport photos:** presets, numeric pixels/DPI, individual images and repeated A4 PDF output. Changing background fill does not automatically remove the existing photo background. No authority-compliance guarantee.
- **PDF → DOCX:** extracted text only, with no source layout or OCR.
- **DOCX → PDF:** paragraph text only; headers, tables, embedded images, styles and original pagination are not preserved.
- **PDF → XLSX:** extracted text lines in rows, not reconstructed tables.
- **XLSX → PDF:** values from the first worksheet as text. No legacy XLS/CSV input or formula recalculation.
- **PDF → PPTX:** page images, not editable slide objects.
- **PDF compression, grayscale and known-password unlock:** rasterized PDFs. Text search, forms, links and signatures are lost. Compression may increase size and reports that honestly. Rasterization is capped at 100 pages.
- **PDF editor:** text overlays only. Existing text cannot be changed, and arbitrary shape/image editing is not included. Signature tool accepts a visible image, not a digital certificate.
- **PDF crop/reorder/remove/extract:** numeric page ranges and coordinates, no drag-reordering UI. Preview shows up to 12 pages.
- **Text/HTML/DOCX/XLSX → PDF:** basic Latin-script typesetting; unsupported characters are replaced with “?” and the workspace explains this. HTML styles are not rendered.
- **PDF metadata removal:** common document information only, not all embedded metadata.
- **Video/audio:** single-thread FFmpeg runs only after user action. Codec availability depends on the bundled core. Merging requires compatible streams; unsupported inputs fail. Video rotation is 90° clockwise. Speed is limited to 0.5–2. GIF output uses a basic 10-fps conversion without palette optimization. Media browser outputs are not verified in this environment.
- **Resume/certificate:** two font styles with editable sections, local draft save and print-to-PDF. Certificates use typed signatory text, not uploaded signature artwork. PDF output depends on browser print settings.
- **ATS checker:** pasted resume text and optional job description, keyword/heading heuristics only. No claimed ATS pass score; no direct file upload in this workspace.
- **Captions/hashtags:** local English templates and keyword extraction, not AI/trend data.
- **Speech:** browser voice availability varies. Recognition may send audio to the browser vendor; the page requires explicit start/consent. Currently English (India).
- **Handwriting:** available device cursive font and print export, not genuine handwriting recognition.
- **Text reversal/counters:** Unicode code points, not grapheme-cluster segmentation; combined accents may count separately.
- **Regex:** dedicated worker terminated after 500 ms, max 200,000 input characters and 1,000 results.
- **SQL:** generic SQL dialect; no dialect chooser.
- **JWT:** decoding only, no signature verification.
- **Currency:** user-entered exchange rate only.
- **Salary:** India, FY 2026–27, manual tax/PF/deduction inputs. No tax slab engine.
- **Unit converter:** a selected set of length, mass and temperature units.
- **Notepad/drafts:** stored on the current device only; no sync.
- **QR customization:** minimum contrast and quiet zone enforced; local decode check gates downloads. Logo output is PNG only. Camera availability depends on permission and HTTPS.
- **Barcode:** selected symbologies only; generation exports SVG, scanning uses the shared camera/image decoder.

## Browser expectations (not a tested compatibility claim)

| Area | Requirements |
|---|---|
| Basic tools | Modern JS, localStorage, File/Blob, Canvas |
| Camera scanners | HTTPS/localhost, camera permission, getUserMedia |
| QR/image downloads | Canvas encoding support; WebP output varies |
| HEIC | Supported libheif decoder profile, sufficient memory |
| PDF preview | Modern PDF.js support, workers, sufficient memory |
| Media | WebAssembly, workers, DecompressionStream; ~32 MB core plus working memory |
| Audio notification | User interaction allowing AudioContext |
| Speech recognition | Browser SpeechRecognition implementation and microphone permission |
| Clipboard | Secure context and clipboard permission |
| Print export | Browser print dialog / Save as PDF |

## Outstanding validation and polish

- Execute Chromium, Firefox and WebKit acceptance tests on an environment with browser binaries.
- Manually test all file workflows with representative valid, malformed, encrypted, rotated and very large inputs.
- Verify media output playback and real QR scanning on physical devices.
- Measure Lighthouse and accessibility results; none are claimed.
- Add worker offloading for expensive image/PDF transformations. Some operations currently run on the main thread and can pause the interface.
- Add more exhaustive file-signature checks and per-tool file limits. Existing image/PDF decoders reject unsupported data, but upload validation is not exhaustive.
- Add more detailed per-tool instructions and FAQs; current workspace help is shared.
- Finish configurable social layouts, independent text layers, certificate signatures, and richer PDF overlays.
- Improve per-tool SEO text, route-specific social metadata and prerendering. Current app is a client-rendered SPA; sitemap/canonical output requires a configured real URL.
- Persisted data APIs can be restricted by private browsing/device policies. Graceful fallback is present for favorites/history but not every draft preference path.
