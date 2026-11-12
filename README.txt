Phil landing page (full scroll flow)
====================================

index.html is the whole site: one file, no build step.
Loads Sora from Google Fonts and Lenis (smooth scroll) from jsDelivr.
Upload it to any static host (Vercel, Netlify, GitHub Pages, Cloudflare Pages) as the root page.

Flow
  1. Preloader: dots gather into the Phil "P", then break apart into the page (~4s; click or Esc to skip).
  2. Hero: "Your texts, handled." + waitlist form + phone peek.
  3. Pinned story (scroll-driven): ask what you missed -> Phil replies as you (your phone + Ria's phone)
     -> Phil fills you in and adds it to your calendar.
  4. Closing CTA: "Keep the relationships. Let Phil fill you in." + second waitlist form.
  Reduced-motion users skip the preloader and smooth scroll.

Waitlist forms (needs one step)
  Both forms check the email but do not save it yet. In the main <script>:

      const WAITLIST_ENDPOINT="";

  Set it to the URL that collects signups. Each form sends a POST with a JSON body:
      { "email": "...", "source": "<hostname>", "ref": "<referrer>", "at": "<ISO time>" }
  Content-Type is text/plain (avoids CORS preflight, works with Google Apps Script).
  A 2xx response shows "You're on the list."; anything else shows an error and lets them retry.
  A hidden "company" field is a bot trap: if it's filled, the submit is ignored.
