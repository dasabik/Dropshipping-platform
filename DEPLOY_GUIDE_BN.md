# Seller Drop Shipping AI — আপলোড ও চালুর বাংলা নির্দেশিকা

## গুরুত্বপূর্ণ কথা
এই প্যাকেজে ফ্রন্টএন্ড, Node.js/Express ব্যাকএন্ড, PostgreSQL সংযোগ, লগইন/রেজিস্ট্রেশন এবং AI API রুট একসঙ্গে আছে। `npm test`-এর ১২টি স্ট্যাটিক পরীক্ষা পাস করেছে (API_BASE সংক্রান্ত একটি অতিরিক্ত পরীক্ষা-সহ)। তবে এটি লাইভ সার্ভার, PostgreSQL, Gemini API বা marketplace account-এ end-to-end পরীক্ষা করা হয়নি। তাই সবকিছু ভুলহীন বা লাইভ বলে নিশ্চয়তা দেওয়া যাবে না।

## GitHub Pages-এর সীমাবদ্ধতা
GitHub Pages শুধু static HTML/CSS/JavaScript পরিবেশন করে; Node.js ব্যাকএন্ড চালায় না। তাই শুধু এই ফাইল GitHub Pages-এ আপলোড করলে আসল login/database/AI কাজ করবে না। এই প্রজেক্টে `backend/server.js` ফ্রন্টএন্ডও পরিবেশন করে—ফ্রন্টএন্ড ও ব্যাকএন্ড একই Node.js ওয়েব সার্ভিসে চালানোই সহজতম পথ। ফ্রন্টএন্ডে `API_BASE` একই সার্ভিসের জন্য খালি রাখা হয়েছে; আলাদা GitHub Pages সাইটে রেখে শুধু ব্যাকএন্ড চালালে CORS ও API URL আলাদাভাবে সেট করতে হবে।

## ধাপ ১ — GitHub-এ কোড রাখুন
1. ZIP ফাইলটি extract/unzip করুন।
2. ZIP-এর ভেতরের `frontend`, `backend`, `tests`, `package.json`, `.env.example`, `README.md` ইত্যাদি ফাইল ও ফোল্ডারগুলো repository-র root-এ রাখুন। পুরো ZIP ফাইলটিকে শুধু ওয়েবসাইট হিসেবে আপলোড করবেন না।
3. `.env` বা কোনো আসল API key/password GitHub-এ আপলোড করবেন না। `.env.example` শুধু উদাহরণ।

## ধাপ ২ — Node.js সার্ভিস হোস্ট করুন
1. আপনার GitHub repository-কে Node.js web service host (যেমন Render)-এর সঙ্গে connect করুন।
2. Root directory-তে `package.json` থাকতে হবে।
3. Build command: `npm install`
4. Start command: `npm start`
5. Node.js 20 বা তার নতুন সংস্করণ ব্যবহার করুন।

## ধাপ ৩ — PostgreSQL ও environment variables
হোস্টে PostgreSQL database তৈরি করে তার connection string গোপন environment variable `DATABASE_URL`-এ দিন। নিচের ভ্যারিয়েবলগুলোও সেট করুন:
- `NODE_ENV=production`
- `JWT_SECRET` = কমপক্ষে ৩২ অক্ষরের অনন্য, random secret
- `DATABASE_URL` = আপনার PostgreSQL connection string
- `GEMINI_API_KEY` = AI Studio ব্যবহার করতে চাইলে, provider থেকে নেওয়া key

AI key কখনো HTML/JavaScript ফাইলে বা public GitHub repository-তে রাখবেন না। `JWT_SECRET` এবং database password-ও চ্যাটে পাঠাবেন না।

## ধাপ ৪ — পরীক্ষা
1. হোস্টিং থেকে পাওয়া HTTPS service URL খুলুন।
2. `/api/health` যোগ করে খুলুন। `database` connected না দেখালে login/register করার আগে database settings ঠিক করুন।
3. সাইটের Register থেকে নতুন account তৈরি করে তারপর login করুন। আগের offline preview-তে তৈরি account PostgreSQL account নয়; নতুন করে register করতে হবে।
4. AI Studio ব্যবহার করতে হলে `GEMINI_API_KEY` সঠিকভাবে সেট করে সার্ভিস restart/redeploy করুন।

## বর্তমান সীমাবদ্ধতা
- Marketplace ও courier integration-এ আসল provider authorization, API adapter এবং অনুমোদন লাগবে। বাটন থাকা মানেই live sync/booking চালু নয়।
- AI image/text generation-এর জন্য সঠিক API key, সমর্থিত model এবং provider-side access প্রয়োজন।
- এই প্যাকেজে স্বয়ংক্রিয় স্ট্যাটিক টেস্ট পাস করেছে; live database, account login, AI generation, mobile browser এবং third-party integrations এখানে চালিয়ে যাচাই করা হয়নি।
