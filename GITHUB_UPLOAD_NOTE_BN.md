# GitHub আপলোড নোট — Seller Drop Shipping AI

এই প্রজেক্টে `vite.config.js` প্রয়োজন নেই: বর্তমান আপডেটেড সংস্করণটি Vite দিয়ে নয়, Express/Node.js সার্ভার দিয়ে চালানোর জন্য সাজানো।

## ফোল্ডার কাঠামো অক্ষত রাখুন
- `frontend/index.html` — ওয়েব UI
- `backend/server.js` — Express API/server
- `backend/services/aiStudioService.js` — সার্ভার-সাইড Gemini/AI Studio সংযোগ
- `tests/static.test.js` — static checks
- `package.json` — scripts ও dependencies
- `.env.example` — নমুনা environment settings; আসল secret নয়
- `README.md`, `DEPLOY_GUIDE_BN.md`, `AI_SETUP.md`, `TEST_REPORT.md` — নির্দেশিকা ও টেস্ট রিপোর্ট

## আপলোডের আগে
1. ZIP extract করুন।
2. GitHub repository-র root-এ `package.json`-সহ এই ZIP-এর ভেতরের ফাইল ও ফোল্ডারগুলো আপলোড করুন।
3. `frontend`, `backend`, `backend/services`, `tests` ফোল্ডারের নাম/অবস্থান পরিবর্তন করবেন না।
4. `.env` বা আসল API key/password GitHub-এ আপলোড করবেন না।
5. `vite.config.js` নিজে থেকে বানাবেন না; এই সংস্করণে সেটি ব্যবহৃত হয় না।
