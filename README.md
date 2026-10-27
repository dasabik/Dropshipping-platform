# Seller Drop Shipping AI — Unified Seller Workspace
**Your Business. Our Automation.**

## Included workspace features
- Entry flow: Welcome screen → seller registration or sign-in → dashboard. Sign-in accepts the registered mobile number and password. Authentication is backed by PostgreSQL, bcrypt password hashing, and signed bearer tokens.
- Original responsive seller dashboard, store connections, supplier hub, orders/logistics, COD/RTO tools, inventory, operations, profit calculator, growth/support and store profile.
- 1-minute promotional video studio with upload, canvas-based scene rendering and WebM export (browser capabilities vary).
- High-resolution product graphic studio: product photo upload, square/portrait/story/landscape layouts, theme selection, product name/offer/price and PNG export.
- Social post workspace: caption helper, platform selection, local draft calendar, edit/delete and text export.
- Unified channel hub for Flipkart, Amazon, Meesho, Shopify, Delhivery and Shiprocket connection-state review.
- Seller-scoped PostgreSQL order/product APIs; no fabricated API orders or fake AWB/tracking success from the backend.

## Run locally
1. Install Node.js 20+ and PostgreSQL.
2. Create database `seller_dropshipping_db`.
3. Copy `.env.example` to `.env`; set `DATABASE_URL` and a unique random `JWT_SECRET` of at least 32 characters. The example defaults to development for local setup; use `NODE_ENV=production` only after setting all production secrets.
4. Run `npm install` then `npm start`. The web server now remains available if PostgreSQL is temporarily down and retries database initialization every 15 seconds; sign-in/registration will show a clear database-not-ready error until it succeeds.
5. Open `http://localhost:5000` (do not double-click `frontend/index.html` for real authentication). Choose Create a New Account to register, or Continue to Login and use the email or mobile number registered in this PostgreSQL database. Accounts created in older standalone/local previews are not server accounts and must be registered again here.
6. Check `http://localhost:5000/api/health`; `database: "connected"` means the schema is ready. If not, check PostgreSQL is running and the `.env` database credentials are correct. The Welcome page also has a clearly labelled offline preview option, which does not authenticate or connect live services.

## Important: what is and is not live
The creative tools included here can render template-based graphics and a browser-rendered promotional video. This is not the same as generative AI image/video inference. AI-generated imagery, AI-generated video, voiceover generation, social publishing, marketplace catalog/listing pushes, live marketplace order sync, carrier booking and live tracking require provider-approved API access, provider-specific adapters, OAuth/webhooks where required, and end-to-end verification. The UI must not claim success for actions until the server confirms a real provider response.

The connection hub shows whether credential variables are present, not whether an account has been fully authorized or an API has passed live tests. Never put API secrets in frontend code. Use only official provider documentation and authorized seller accounts.

## Deployment checklist
- HTTPS and `NODE_ENV=production`; trusted exact origins in `FRONTEND_ORIGINS`.
- Managed PostgreSQL, least-privilege credentials, backups and monitoring.
- Add email verification, password reset, rate limiting, audit logging and account recovery before public launch.
- Implement and test the provider adapters against current official APIs.


## Welcome Screen Refresh (2026-10-26)
- Premium high-contrast welcome screen with animated gradient headline, glow effects, glass-style command-center visual, and feature cards.
- Login accepts registered mobile number or email address.
- Authentication is backend-only: standalone HTML and unavailable backend states do not create or accept local/demo accounts.
- The supplier catalog starts empty until verified provider listings are returned; no sample products, seller identity, orders, AWBs or tracking results are seeded.


## Google Gemini AI Assistant and Image Lab

The dashboard includes a live multilingual AI chat and generative image workspace backed by Google Gemini. The same server-side service can create product headlines, a 30-second voiceover script, selling points, and an image prompt. The marketing endpoint is POST /api/ai/generate-marketing; dashboard chat and image endpoints are POST /api/ai/chat and POST /api/ai/image. All AI actions require a signed-in seller.

1. Copy .env.example to .env in the project root (same folder as package.json).
2. Set GEMINI_API_KEY to a private Google AI Studio key. Never put the key in frontend HTML, GitHub, screenshots or public chats. If a real key was exposed, revoke it and create a replacement.
3. Check that GEMINI_MODEL and GEMINI_IMAGE_MODEL are available to your Google AI Studio project and region. Model IDs can change and access varies by account.
4. Configure PostgreSQL and a unique JWT_SECRET of at least 32 characters, run npm install, then npm start. Register/sign in through the backend before using AI.
5. Visit /api/ai/status to see whether credentials are present, then actually send a chat and generate an image. Status only confirms that settings are present; it does not prove a live provider call works.

Image generation may be paid, rate-limited or unavailable to some projects. Generated image resolution depends on the selected model; the UI's size selector chooses an aspect ratio and does not guarantee exact pixel dimensions or 4K. The marketing tool generates a video script, not a finished video file. Live video generation requires a separate video model/API and is not included in this integration.

## Validation and testing
- Run `npm test` to execute the included static regression checks (JavaScript syntax, required UI/API routes, unique HTML IDs, inline click-handler references, AI authentication and no seeded fake supplier/seller data).
- Run `node --check backend/server.js` for a backend syntax check.
- These checks do not replace end-to-end testing against PostgreSQL, an AI provider, marketplace OAuth/API, or courier APIs. Those tests require network access, database credentials, provider credentials and approved account access.
- Frontend styling and icons load from Tailwind CSS and Lucide CDN, so an internet connection is required for those assets.


## Standalone browser preview and startup flow (2026-10-27)
- The standalone HTML begins with a clean white splash screen showing “SELLER DROP SHIPPING AI”, then transitions to the existing premium Welcome Page after about 1.75 seconds. “Continue now” skips the splash.
- In a downloaded `file://` HTML preview, the login form opens a clearly-labelled local preview workspace after a valid email/mobile and non-empty password. This is **not production authentication** and does not verify the password against a server. Local accounts created using Register are stored in that browser only and their password is checked locally.
- Real account authentication, persistent server-side accounts, live AI, marketplace APIs and courier APIs require the Node.js backend, PostgreSQL, and the appropriate provider credentials.


## Google Gemini AI Assistant and Image Lab

This build includes a server-side Google Gemini adapter for live multilingual chat, product marketing copy, a 30-second video voiceover script, and generative product-image creation. The existing welcome → login/register → dashboard flow and visual design are preserved. The marketing endpoint is POST /api/ai/generate-marketing; the dashboard chat and image tools use POST /api/ai/chat and POST /api/ai/image. All three require a signed-in seller.

1. Copy .env.example to .env in the project root (same folder as package.json).
2. Put your private Google AI Studio key in GEMINI_API_KEY. Do not put the key in HTML, screenshots, GitHub or this chat. If a real key was exposed, revoke it and create a replacement.
3. Check that GEMINI_MODEL and GEMINI_IMAGE_MODEL are available to your Google AI Studio project and region. Defaults in this sample are configurable and are not a guarantee of account access.
4. Set PostgreSQL and JWT_SECRET, run npm install, then npm start. Register/sign in through the backend before using AI.
5. Visit /api/ai/status to see whether credentials are present, then actually send a chat and generate an image. The status endpoint checks configuration only; it does not prove a live provider call works.

Image generation may be paid, rate-limited or unavailable to some projects. Model names, regional access and prices change. The generated product image is not guaranteed to be 4K; this endpoint requests a model-supported aspect ratio and returns the actual image supplied by the provider. The marketing tool produces a video script, not a finished video file.


## Finding the AI Chat and Image Studio

On the welcome screen, select **Open AI Chat & Image Studio** to jump straight to the AI interface preview. This offline preview only demonstrates the UI; it cannot call AI services. For live replies and generated images, start the backend, configure PostgreSQL and a private `GEMINI_API_KEY` in the backend `.env`, create/sign into a real seller account, then open the site through the server URL (not by opening `index.html` directly).
