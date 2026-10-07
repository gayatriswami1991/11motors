# How leads reach you

Every form on the page (hero form, test-drive booking, new-arrivals band) does **three** things:

1. **Sends the lead to your inbox / Google Sheet** (needs the one-time setup below).
2. **Opens WhatsApp** with the customer's details pre-filled, addressed to `+254 116 101 111`.
3. **Retries automatically** on the visitor's next visit if the send failed.

Until step 1 is set up, leads only arrive when the customer actually sends the WhatsApp message.
Set up step 1 so you also get leads from people who close WhatsApp without sending.

## Option A: Google Sheet + email alert (free, 5 minutes, recommended)

1. Create a Google Sheet named **Eleven Motors Leads**. Row 1 headers:
   `submitted_at | source | name | phone | type | budget | payment | car | date | time | showroom | page | utm_source | utm_campaign | referrer`
2. In the Sheet: **Extensions → Apps Script**. Delete the sample code and paste:

```js
const EMAIL = "sales@elevenmotorske.com";   // where alerts go
function doPost(e) {
  const p = e.parameter, sh = SpreadsheetApp.getActiveSheet();
  const cols = ["submitted_at","source","name","phone","type","budget","payment","car","date","time","showroom","page","utm_source","utm_campaign","referrer"];
  sh.appendRow(cols.map(c => p[c] || ""));
  MailApp.sendEmail(EMAIL, "New lead: " + (p.name || p.phone) + " (" + p.source + ")",
    cols.filter(c => p[c]).map(c => c + ": " + p[c]).join("\n"));
  return ContentService.createTextOutput("ok");
}
```

3. **Deploy → New deployment → type: Web app**. Execute as: **Me**. Who has access: **Anyone**. Copy the Web app URL.
4. In `index.html`, set `leadEndpoint: "<that URL>"` inside `CONFIG`.
5. Submit a test lead on the live page. Check the Sheet and your inbox.

## Option B: Formspree / Web3Forms

Create a form, copy its endpoint URL into `leadEndpoint`. The page posts standard form fields, so both accept it.

## Tracking

Leads carry `utm_source`, `utm_campaign`, `gclid` and `fbclid` from the visit URL. Use links such as
`https://yourpage/?utm_source=google&utm_campaign=prado` in ads and Google Business Profile so you can see which source brings leads.
The page also pushes `lead`, `whatsapp_click` and `open_test_drive` events to `dataLayer` for Google Tag Manager / GA4.
