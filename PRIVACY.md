# MAJ Privacy Policy

Last updated: November 11, 2026

This policy covers the **MAJ browser extension** (Chrome Web Store) and the **MAJ Desktop** app
(downloaded from https://github.com/LeandroDettmer/maj-releases). MAJ is a bug recorder: it records
what happens on a page while you reproduce a bug, so you can hand the recording to a developer.

**In short:** MAJ captures only while a recording or Instant Replay is active. What it captures stays
on your computer. MAJ has no analytics, no ads, and does not sell or share your data. Nothing leaves
your computer unless you choose to share a recording with a server you set up yourself.

## 1. When the extension captures anything

The extension captures nothing while it is idle. Its capture code is added to a tab only when a
session starts, and stops capturing when the session stops. A session starts only in one of these
ways:

- You click **Record this tab** or **Instant Replay** in the extension popup. Only that tab is
  captured.
- You start a screen recording in MAJ Desktop. The extension then captures the browser tab that is
  active, and switches to whichever tab you make active, until the desktop recording stops.

The capture code runs only in the tab's top-level page, not inside embedded frames. The toolbar
badge shows
**REC** or **IR** whenever a session is active.

While idle, the extension keeps a local connection open to MAJ Desktop (if it is installed) so the
app can see that the extension is present and ask it to start. Over that idle connection the
extension sends only its own ID, the browser name and the time. No page data is sent.

## 2. What is captured during a session

From the captured tab:

- **Console:** messages the page logs (`console.log`, `warn`, `error`, …), uncaught errors,
  unhandled promise rejections, and their stack traces. Long values are shortened.
- **Network requests made by the page** with `fetch`, `XMLHttpRequest`, `sendBeacon` and
  WebSocket (connection open/close only, not messages): URL, method, status, request and response
  headers, timing, and request/response bodies. Bodies are kept only for JSON, text and
  form-encoded content, up to 256 KB each (longer bodies are cut and marked as truncated). Other
  bodies (images, files, binary data) are not kept.
- **Other network resources (optional, off by default):** if you turn on "Capture all network
  resources" in the popup (Chrome asks you for the extra `webRequest` permission), MAJ also records
  the URL, method, status, response headers and timing of images, stylesheets, scripts, fonts and
  documents loaded by that tab. No bodies.
- **Navigation:** the page URL, page title and URL changes.
- **Your actions on the page:** clicks (which element, plus up to 80 characters of its visible
  label), that a form field changed (never what you typed), the Enter, Escape and Tab keys, form
  submissions, and the scroll position.
- **Device details:** operating system, browser name and version, window size and language.
- **Page structure (Instant Replay only):** the page's structure and visible text, recorded with the
  open-source rrweb library so the moment can be replayed. All form field values are masked, and
  canvas content is not recorded. Instant Replay keeps only the last two minutes in memory and
  discards everything else; nothing is saved unless you click **Save last 2 minutes**.
- **Tab video and audio (only without MAJ Desktop):** when MAJ Desktop is not connected, a
  recording you start from the popup also records the video and sound of that tab.

The extension does not read cookies, passwords you type, other tabs, your browsing history, or
pages you visit while no session is active.

## 3. Automatic redaction

Before any captured event leaves the page's tab (and, for the optional network resources, before it
is stored), the extension masks values that look secret and replaces them with `[REDACTED]`:

- headers `Authorization`, `Cookie`, `Set-Cookie`, `Proxy-Authorization`, `X-API-Key`,
  `X-CSRF-Token`, and any header whose name looks sensitive;
- fields named like `password`, `secret`, `token`, `api_key`, `client_secret`, `auth`, `sid`,
  `signature`, `otp`, `card`, `cvv`, `ssn`, `cpf`, `cnpj` (and similar) in JSON bodies, form bodies,
  URL query strings and `key=value` text;
- values that look like JWTs, `Bearer` tokens, some well-known API key formats, e-mail addresses,
  payment card numbers, Brazilian CPF/CNPJ numbers and phone numbers, and user names/passwords
  inside URLs.

Redaction is automatic and pattern-based, so it can miss data that does not match these patterns.
It does not apply to video, audio or camera recordings (they show whatever is on screen), and
Instant Replay page snapshots mask form fields but keep the page's visible text. Review a recording
before you share it. Parts of a page can be excluded by its developer with the `maj-block` class or
the `data-maj-mask` attribute.

## 4. Where the data goes

- **With MAJ Desktop installed:** the extension sends the session to the MAJ Desktop app on the
  same computer through Chrome's native messaging (a local channel, not the internet). The app saves
  it as files in its own folder on your computer.
- **Without MAJ Desktop:** the extension keeps the session in memory and, when you stop, offers a
  `.maj` file that you download to your computer.

The extension itself sends nothing to the internet: it has no servers, no analytics, and does not
load remote code. The extension stores only two small things in the browser: the state of the
current session (ID, tab, start time and page title) so a session survives the extension's
background worker restarting, and your "Capture all network resources" setting.

## 5. MAJ Desktop

MAJ Desktop records your screen and system audio, and your microphone and camera only if you turn
them on, while a recording is running. Recordings are saved as files on your computer.

MAJ Desktop connects to the internet only to:

- **check for updates** when it starts, by downloading a version file from GitHub
  (`github.com/LeandroDettmer/maj-releases`), and download an update if you choose to install it.
  GitHub receives a normal web request (including your IP address) under GitHub's own privacy
  policy;
- **share a recording**, only if you set up a MAJ server address yourself, sign in to it, and click
  to share a specific recording. That recording is then uploaded to that server, which is operated
  by you or your organization, not by the MAJ project. MAJ has no server of its own that receives
  your recordings.

The optional local MCP server (`maj-mcp`) lets an AI coding tool on your computer read your
recordings from disk. It uploads nothing itself; what the AI tool does with the data is governed by
that tool's own policy.

## 6. What MAJ does not do

- No analytics, telemetry, tracking or advertising.
- No sale, rental or transfer of your data to anyone.
- No use of your data for anything other than making the recordings you ask for.
- No use or transfer of your data to determine creditworthiness or for lending purposes.

## 7. Keeping and deleting data

Recordings live only on your computer (in MAJ Desktop's data folder, or wherever you saved a `.maj`
file) until you delete them. Deleting a recording in MAJ Desktop, or deleting the `.maj` file,
removes it. A recording you shared to your own server stays there until it is deleted on that
server. Uninstalling the extension removes the small amount of data it keeps in the browser.

## 8. Children

MAJ is a developer tool and is not directed at children under 13.

## 9. Changes

If this policy changes, the new version will be published at this address with a new date above.

## 10. Contact

Questions or requests: open an issue at https://github.com/LeandroDettmer/maj-releases/issues
