𝐓𝐨𝐮𝐫𝐧𝐚𝐦𝐞𝐧𝐭 𝐀𝐩𝐩 𝐏𝐫𝐨𝐦𝐩𝐭:

Build a mobile-first, one-page native-style tournament app (Web or hybrid) for both players and admins. It should feel like a production-grade tournament platform (e.g. Mobile Legends, PUBG Tourneys), complete with payments, social referrals, user profiles, and a rich admin analytics dashboard—all optimized for smartphones.

Deliverable: Provide two files—user.html and admin.html.




---

🎨 1. Shared Visual & Technical Foundation

Framework: Single-page app (React Native Web or Ionic/Capacitor) or modern SPA.

Font: Russo One via Google Fonts for a gaming edge.

Color Palette (:root CSS variables):

:root {
  --bg-primary:   #F8FAFC;    /* soft white */
  --bg-secondary: #E2E8F0;    /* light gray */
  --text-dark:    #1E293B;    /* rich dark text */
  --accent-blue:  #2563EB;    /* brand blue */
  --accent-gold:  #FBBF24;    /* prize gold */
  --accent-red:   #DC2626;    /* alerts/danger */
  --border:       #CBD5E1;    /* soft outline */
}

Styling:

Card layouts, flat illustrations (SVG or Lottie), no heavy shadows.

Smooth hover/focus effects on buttons & inputs.

Fully responsive/flex-based grid.


Icons & Animations: Use lightweight SVG icons and optional Lottie for micro-animations (e.g. payment success, referral bonus pop-ups).



---

🏠 2. user.html (Public One-Page App)

A single scrollable/mobile-native view with these sections:

1. Home

Hero banner (“Free Fire Tournaments”)

“Play Now” CTA to live tournaments grid.



2. Tournaments (Live / Upcoming / Past tabs)

Card per tournament (title, time, map, prize, players joined / max)

“Join” button opens registration modal.



3. Refer & Earn

Unique referral code

“Share” buttons (WhatsApp, Telegram, Link copy)

Display earned credits from referrals.



4. Profile

Display user avatar, name, Free Fire UID, wallet balance.

“Top-up” button → Payment modal.

“My Registrations” list with join/cancel links.




🔧 Functional Scope

Registration modal: name, FF UID, hidden tournament ID → Confirm & deduct entry fee.

Payment feature: integrate Razorpay (or Stripe) SDK → single tap “Pay & Join”.

Referral tracking: store referrerId in user profile → credit on new sign-ups.

Wallet: show balance, “Top-up” via payment gateway, auto-deduction on join.



---

🛠️ 3. admin.html (One-Page Admin Panel)

Secure SPA with a drawer or bottom nav: Dashboard | Tournaments | Players | Analytics | Settings

1. Dashboard

Metrics widgets:

Total Tournaments

Total Players

Online Players (currently in matches)

Wallet Balance Held (entry fees)


Quick-action buttons: “Create Tournament”, “View Payments”, “Send Notification”.



2. Tournaments

Table or card list (search/filter by status)

Create/Edit modal: title, datetime, map, prize pool, entry fee, room ID/pass, max players

Bulk actions: enable/disable registrations, delete past events



3. Players

List of all registered players (search by name/UID/email)

View per-tournament registrations, referral source, wallet transactions



4. Analytics

Graphs for daily sign-ups, revenue (entry fees), referrals redeemed

Real-time active players gauge



5. Settings

Payment gateway config (Razorpay/Stripe keys)

Referral bonus rules

Admin users & roles




📜 JavaScript / Backend Placeholders

// Firebase / Firestore config placeholder
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

// Auth flow
firebase.auth().onAuthStateChanged(user => { … });

// User joins tournament:
async function joinTournament(tournId, userId) {
  await processPayment(entryFee);
  await db.collection('tournaments').doc(tournId)
          .collection('registrations').add({ userId, timestamp: Date.now() });
  await db.collection('users').doc(userId).update({ walletBalance: newBalance });
}

// Admin creates/edits:
await db.collection('tournaments').doc(tournId).set({ … }, { merge: true });


---

📂 Suggested Firebase/Firestore Structure
  {  "users": {    "userId123": {       "name": "Rohan", "uid": "987654321", "walletBalance": 500, "referrer": "userId456"    }  },  "tournaments": {    "tournId123": {      "title": "July Clash",      "matchTime": "2025-07-20T17:00",      "map": "Bermuda",      "prize": 1000,      "entryFee": 50,      "roomId": "12345",      "roomPass": "abcde",      "maxPlayers": 100,      "registrations": { /* subcollection */ }    }  },  "payments": { /* payment records */ },  "referrals": { /* referral tracking */ }}---✅ Deliverables Checklist⬜ Two files: user.html and admin.html⬜ Mobile-optimized, native-app UX (SPA framework)⬜ Payment gateway integration hooks⬜ Referral & wallet system placeholders⬜ Advanced admin analytics & metrics⬜ Well-commented, modular code structure⬜ Light Lottie/SVG micro-animations for flair> Pro Tip: Lazy-load heavy assets (SVGs/Lottie), and use real-time listeners only on active views to keep mobile performance snappy.
