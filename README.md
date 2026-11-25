# Test Data

A developer toolbox for generating test data. It's a single self-contained HTML file with no build step, no dependencies to install, and no server-side code.

**Live:** https://unamailer.github.io/test-data/

## What's in it

- **Tax IDs:** checksum-valid IDs for 12 countries (AUS TFN, CAN SIN, CHN Resident ID, ESP DNI, GBR NINO, HKG HKID, IDN NPWP, MEX RFC, MYS MyKad, SGP NRIC, TWN National ID, USA SSN), with a Raw / Formatted switch.
- **Addresses:** a test address for each of those 12 countries, plus 229 more countries (address only). Click any field to copy it.
- **Test cards:** a Luhn-valid number generator for 7 brands (Visa, Mastercard, Amex, Discover, JCB, Maestro, UnionPay), with an expiry date and CVV, plus slots for your own gateway test cards (see below).
- **Nasty Strings:** 26 strings that break forms (SQL, XSS, Unicode, emoji, length, whitespace, odd but valid emails), each with notes on how to use it.
- **Utilities:**
  - World clock for all 12 countries
  - Timestamp converter (Unix s/ms, ISO, `mm/dd/yyyy`, SQL/CF, Rocket UniVerse / Pick internal date and time)
  - Encode / Decode (URL, Base64, HTML, JSON)
  - UUID generator, including ColdFusion `createUUID()` format
- **Recently Copied:** your last 10 copies.
- **Helpful Links:** a filterable list. Press `/` to search.
- Light and dark themes, works on a phone, and a few easter eggs.

## Running it

Open `index.html` in a browser, or drop it on any static host (GitHub Pages works). The only outside requests are Google Fonts and the `flag-icons` CSS from jsDelivr. Without a network connection the page still works, but it falls back to system fonts and shows no flags.

Settings (theme, collapsed panels, format, recent copies) stay in your browser's `localStorage` under the `devtools.` prefix.

## Add your own test cards

The card numbers are left out on purpose. Search `index.html` for these and put in your payment gateway's test numbers:

- `FIXED_CARDS`: the Auto-Approve and Auto-Decline cards
- `LIVE_TEST_CARD`: a card row that stays hidden until you type `live` anywhere on the page (not in a text box) or press and hold the **Test Cards** heading. It hides itself again after 30 seconds and is never saved to Recently Copied.

## Editing

Everything is in `index.html`:

- **CSS** sits in the `<style>` block at the top. Theme colors are custom properties on `:root`, with dark and light overrides.
- **Data** (countries, addresses, the `WORLD` list, test cards, `LINKS`, `NASTY` strings) is in plain arrays near the top of the `<script>`. Most changes only touch that data.
- **Helpful Links** puts links on hosts matched by `isInternal()` under an *Internal* heading and everything else under *External*. Change the hostname pattern in `isInternal()` to match your own domains.

If you put `</script>` inside a JavaScript string, write it as `<\/script>`. Otherwise it closes the script tag.

## UniVerse dates

UniVerse / Pick internal date = days since 12/31/1967 (day 0), so `1` = 01/01/1968 and `21513` = 11/24/2026. Internal time = seconds since midnight. The converter accepts `21513`, `21513*44387`, `21513 44387`, or `21513,44387`, and reads them in the browser's local time zone.
