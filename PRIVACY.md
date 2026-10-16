# Privacy & data

**Short version: everything stays on your device. Nothing is uploaded, ever.**

GDT Assistant is a single, static HTML page with no backend. The live site makes exactly one network request at runtime: an anonymous visit count (see "Visit counting" below). A downloaded copy makes none at all.
A `Content-Security-Policy` (`connect-src 'none'`, images only from GoatCounter) blocks every other
request, so the page cannot send what you enter anywhere.

## What is stored, where, and why
- **Where:** your browser's `localStorage`, on **this device only**.
- **What:** the settings and inputs *you* choose — enabled topics & platforms, the Targeted-Audiences
  and Multi-genre toggles, primary/secondary genres, game length, in-game year/month, and your
  **game log** (the genre/topic/platform/audience/score of games you record). Plus a single flag
  remembering your "save my progress" choice.
- **Why:** so the tool remembers your playthrough and you can continue where you left off.
- **What is NOT collected:** no name, email, account, IP logging, advertising, fingerprinting,
  cookies, or third-party scripts of any kind.

## Visit counting
The live site (gdt-assistant.com) sends one anonymous request per visit to
[GoatCounter](https://www.goatcounter.com), a privacy-friendly, open-source counter, so I can see
how many people use the tool. What it receives: page path, query string, referrer, and the request's
User-Agent/IP — the latter two are used transiently server-side to de-duplicate unique visits and
are never stored (per GoatCounter's privacy policy). No cookies, no fingerprinting, no cross-site
tracking, and Do Not Track is honored. If you download index.html and run it locally, no request
is made at all.

## Your control
- **Export / Import** (☰ menu) save or restore your data as a JSON file. The file only leaves your
  device if *you* share it.
- **Reset to defaults** (☰ menu) and **Clear my saved data** (Privacy panel) erase everything stored.
- You can also clear the site's storage in your browser at any time.
- On first visit you may choose **Save my progress** or **Use without saving**. If you decline, nothing
  is written to storage and the tool runs in memory for that session.

## Legal basis (EU ePrivacy / GDPR)
Storing only your own settings/data locally, with no transfer of your data to anyone, is
**"strictly necessary" functional storage** for the service you explicitly requested, and is **exempt
from the cookie-consent requirement** under the ePrivacy Directive Art. 5(3) (cf. EDPB *Guidelines
2/2023 on the Technical Scope of Art. 5(3)*). We use **no cookies** and still show a notice with a
decline option as a courtesy. Because the data never leaves your device and you control it directly
(view/export/delete), your GDPR data-subject rights over it are satisfied locally.

*This is a plain-language summary, not formal legal advice. *

## About this tool
GDT Assistant is an **unofficial, fan-made tool** — **not affiliated with, endorsed by, or sponsored by
Greenheart Games**. *Game Dev Tycoon* and all related names, logos and trademarks are the property of
Greenheart Games. Game data is partly derived from the
[Game Dev Tycoon Fandom wiki](https://gamedevtycoon.fandom.com/), whose text is licensed
[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) — see **[CREDITS.md](CREDITS.md)** for full
attribution. Please support the developers by buying the game:
[Steam](https://store.steampowered.com/app/239820/Game_Dev_Tycoon/) ·
[greenheartgames.com](https://www.greenheartgames.com/app/game-dev-tycoon/).

## Contact
Questions? Open an issue on the project's repository.
