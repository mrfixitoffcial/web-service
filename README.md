# MrFixit — Service Directory Prototype

## What is included
- Responsive customer homepage with service categories, searchable worker cards and profile details.
- Direct call / WhatsApp links for real worker profiles with provided phone numbers.
- Admin interface to create, edit, pause, activate and delete profiles, with a footer-only demo password prompt.
- Listing expiry filter and ₹499/month subscription overview display.
- Six clearly identified *fictional sample* profiles, with no contact numbers.

## Try it locally
Open `index.html` in a browser. For more reliable local storage, run `python3 -m http.server 8000` from the folder and open `http://localhost:8000`.

## IMPORTANT: Not a deployable paid marketplace backend
This is an interactive visual prototype, **not** a secure production admin system. Admin can be opened only via the footer password prompt (`0812`), but this is client-side only and **not secure authentication**. The password is visible to anyone inspecting the site code. Demo data is stored in that browser's `localStorage`. It is not shared across browsers, and its 'Active' and expiry inputs are manual demos—not payment proof. Never collect real ₹499 subscriptions through this prototype.

## Build the production site in Wix
1. Create a Wix site named **MrFixit**, and install **CMS**, **Members Area**, and **Pricing Plans**.
2. Add a CMS collection `Workers` with fields: `name` (text), `category` (text), `area` (text), `city` (text), `description` (text), `experience` (number), `phone` (text), `photo` (image), `price` (text), `verified` (boolean), `approved` (boolean), `memberId` (text), `planOrderId` (text), `subscriptionActive` (boolean), `paidThrough` (date). Set write/update/delete permissions to Admin only. Do **not** expose sensitive admin-only fields in a public dataset.
3. Create a **₹499 / month provider listing** recurring plan in Wix Pricing Plans. Set up a payment provider supporting actual recurring collection in your region. Wix pricing plan feature and payment gateway capabilities vary: verify recurring support, mandate requirements, settlement fees and taxes before launch.
4. Set up a Wix native admin CMS workflow, or a role-restricted admin page for staff. Collect worker documents privately for verification, and keep confidential documents separate from publicly readable profile data.
5. Implement subscription linkage **server-side**. Map each paid plan order to the correct member profile; use Wix subscription order changes / official events and periodic reconciliation to set whether a worker has an active, paid entitlement. A cancellation at period-end should keep a listing live only through the paid period; failed renewals, refunds, immediate cancellations and expirations should be handled per billing status. Client-supplied paid status must never be trusted.
6. On the public directory, query **approved AND subscriptionActive** workers only through a safe backend endpoint. Return only public-safe profile fields.
7. Build pages matching this prototype using Wix Studio sections, repeater/grid elements, searchable controls, dynamic provider pages and Velo backend calls. Connect the site to a domain and test payments, renewals, cancellation, and public visibility before launch.

### Notes
- Wix's editor does not directly import these static HTML/CSS/JS files as editable Wix Studio elements. Recreate sections in the editor; individual design components may be embedded as HTML, but the backend must be implemented with native Wix capabilities.
- Workers pay ₹499/month for directory presence; customer-provider hire/payment is not processed by this prototype.
- Do not claim providers are vetted unless they are actually vetted; the demo deliberately avoids verified badges.
- Consent, worker privacy, safety checks, refund/cancellation policy, GST/tax and consumer protection compliance require review.

Official docs: https://dev.wix.com/docs/velo/apis/wix-data-v2/collections/introduction and https://dev.wix.com/docs/velo/apis/wix-pricing-plans-backend/orders/introduction
