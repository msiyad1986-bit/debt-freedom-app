# Debt Freedom App – മലയാളം സജ്ജീകരണ നിർദ്ദേശങ്ങൾ

ഈ പുതിയ പതിപ്പ് Firebase project `debt-freedom-app-383d8`-നായി ക്രമീകരിച്ചിരിക്കുന്നു. Email/Password + Google Login, Cloud Firestore, Firebase Storage എന്നിവ ഉപയോഗിക്കുന്നു.

## ഉൾപ്പെടുത്തിയ സൗകര്യങ്ങൾ
- Email/Password Signup & Login, Google Login
- Finance Dashboard: മാസ വരുമാനം, ചെലവ്, EMI, ശേഷിപ്പ്, ആകെ കടബാക്കി
- Income / Expense tracking
- Loans & EMI: ബാക്കി, EMI, വാർഷിക പലിശ, കുറിപ്പുകൾ
- Debt priority: Snowball (ചെറിയ ബാക്കി ആദ്യം), Avalanche (ഉയർന്ന പലിശ ആദ്യം)
- Personal Document Locker: CSWIP, Passport, Visa, Aadhaar, PAN, bank statements, property/solar രേഖകൾ എന്നിവയുടെ metadata + PDF/JPG/PNG upload
- Expiry reminders: expiry-ന് 3 മാസം മുമ്പ് മുതൽ; expiry കഴിഞ്ഞാൽ ആഴ്ചതോറും reminder
- Finance Locker: ബാങ്ക്/ലോൺ പേര്, account type, അവസാന 4 അക്കങ്ങൾ, customer care/branch, സുരക്ഷിതമായ ചെറിയ reference
- ഓരോ user-ന്റെയും ഡാറ്റ സ്വന്തം Firebase UID-ൽ മാത്രം വായിക്കാനും മാറ്റാനും കഴിയുന്ന Firestore/Storage rules

## Firebase-ൽ ഒരിക്കൽ ചെയ്യേണ്ട ക്രമീകരണം
1. Firebase Console → Authentication → Sign-in method: **Email/Password**യും **Google**യും Enable ചെയ്യുക.
2. Authentication → Settings → Authorized domains-ൽ GitHub Pages domain ചേർക്കുക (ഉദാ. `username.github.io`).
3. Firestore Database ഇതിനകം `asia-south1`-ൽ സൃഷ്ടിച്ചിട്ടുണ്ട്. Rules ഭാഗത്ത് `firestore.rules` ഉള്ളടക്കം paste ചെയ്ത് Publish ചെയ്യുക.
4. യഥാർത്ഥ ഫയലുകൾ upload ചെയ്യാൻ Firebase Console → Storage → Get started വഴി Storage enable ചെയ്യുക. ശേഷം `storage.rules` paste ചെയ്ത് Publish ചെയ്യുക. Storage enable ചെയ്തില്ലെങ്കിൽ മറ്റ് app features പ്രവർത്തിക്കും; file upload മാത്രം പ്രവർത്തിക്കില്ല.
5. `index.html`-ൽ Firebase config ഇതിനകം project `debt-freedom-app-383d8`-നായി ചേർത്തിട്ടുണ്ട്. വേറെ project ഉപയോഗിക്കുമ്പോൾ മാത്രം മാറ്റുക.

## GitHub Pages-ൽ പ്രസിദ്ധീകരിക്കൽ
1. ZIP extract ചെയ്യുക.
2. ഇതിലെ `index.html`, `firestore.rules`, `storage.rules`, `README_ML.md` എന്നിവ repository root-ലേക്ക് upload ചെയ്യുക.
3. GitHub → Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.
4. പ്രസിദ്ധീകരിച്ച domain Firebase Authentication → Authorized domains-ൽ ചേർക്കുക.

## Reminder എങ്ങനെ പ്രവർത്തിക്കുന്നു?
- expiry date-ന് 90 ദിവസം മുമ്പ് മുതൽ dashboard-ൽ മുന്നറിയിപ്പ് കാണിക്കും.
- expiry കഴിഞ്ഞാൽ ഓരോ 7 ദിവസ ഇടവേളയിലും ആപ്പ് തുറന്ന് ലോഗിൻ ചെയ്യുമ്പോൾ reminder പുതുക്കും.
- browser notification അനുവദിച്ചാൽ notification ലഭിക്കും. Browser അടച്ചിരിക്കുമ്പോഴും ഫോൺ offline ആയിരിക്കുമ്പോഴും സ്വയം background notification അയക്കാൻ ഈ static web app-ന് കഴിയില്ല; app തുറക്കുമ്പോഴാണ് തീയതി പരിശോധിക്കുന്നത്.

## സുരക്ഷാ നിർദ്ദേശങ്ങൾ
- **ഒരിക്കലും** ബാങ്ക് പാസ്‌വേഡ്, ATM/UPI PIN, OTP, CVV, പൂർണ്ണ കാർഡ് നമ്പർ എന്നിവ സൂക്ഷിക്കരുത്.
- Finance Locker-ൽ അക്കൗണ്ടിന്റെ അവസാന 4 അക്കങ്ങൾ മാത്രം നൽകുക.
- Firestore/Storage rules publish ചെയ്തശേഷം മാത്രമേ യഥാർത്ഥ രേഖകൾ upload ചെയ്യാവൂ.
- Firebase web config-ലെ API key browser app-ൽ കാണപ്പെടുന്നത് സാധാരണമാണ്; ഡാറ്റാ സുരക്ഷ Authentication + Rules മുഖേനയാണ്.
- Spark plan-ൽ Storage ഉപയോഗത്തിനുള്ള billing/availability നിബന്ധനകൾ Firebase Console-ൽ പരിശോധിക്കുക. Storage enable ചെയ്യാൻ billing ആവശ്യപ്പെട്ടാൽ ഫയൽ upload സജ്ജമാക്കുന്നതിന് മുമ്പ് ആ സ്ക്രീനിൽ നിർത്തുക; Firestore metadata/features തുടരും.
- എല്ലാ തുകയും ഒരേ കറൻസിയിൽ നൽകുക. INR, QAR ഒരേ കണക്കിൽ കലർത്തരുത്.
- ഇത് വ്യക്തിഗത പ്ലാനിങ് ഉപകരണമാണ്; ബാങ്ക്/ഫിനാൻഷ്യൽ ഉപദേശം അല്ല. കൃത്യമായ loan payoff date ഈ പതിപ്പ് ഉറപ്പുനൽകുന്നില്ല.
