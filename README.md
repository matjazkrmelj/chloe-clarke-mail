# Email form app

A single static page (`index.html`) where fans send Chloe Clarke an email: their email address, subject, message, a "favourite Drag Queen" YES/NO check (only YES sends), and a Send button. Built mobile-first and served by GitHub Pages at https://matjazkrmelj.github.io/chloe-clarke-mail/.

## How sending works
All settings live in the `CONFIG` block near the bottom of `index.html`.

- **EmailJS (custom email template)** is used as soon as `publicKey`, `serviceId` and `templateId` are filled in.
- **FormSubmit** is the fallback while any of those are empty. It sends to `RECIPIENT` using FormSubmit's own layout. The first message triggers a one-time activation email to that address.

## Set up EmailJS (free, 200 emails/month)
1. Create an account at https://www.emailjs.com.
2. **Email Services → Add New Service → Gmail.** Connect the Gmail account that should send the emails, then copy the **Service ID**.
3. **Email Templates → Create New Template**, and fill it in like this:
   - **Subject:** `{{subject}}`
   - **To Email:** your friend's email address
   - **Reply To:** `{{from_email}}`
   - **Content:**
     ```
     From: {{from_email}}

     {{message}}
     ```
   Save it and copy the **Template ID**.
4. **Account → General**: copy the **Public Key**.
5. Optional but recommended: in **Account → Security**, add `https://matjazkrmelj.github.io` as an allowed origin so only this page can use your keys.
6. Put the three values in the `EMAILJS` block in `index.html` and push.

The template variables the page sends are `{{from_email}}`, `{{subject}}` and `{{message}}`. Replying to a received email goes straight back to the sender.
