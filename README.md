# West-Coast HR Mail Desk

Outlook ke candidate emails padh kar dashboard banata hai. **Koi API key, secret, AI ya server nahi.**
HR apne Microsoft account se sign in karta hai (Recruitment Mailer jaisa), sab kaam browser me hota hai.

## Kya karta hai
- Inbox ke naye mails padhta hai, job application aur doosre mails alag karta hai
- CV (PDF / Word .docx) aur mail body se nikalta hai: naam, mobile, email, post, qualification,
  experience, city, current company, CTC, expected CTC, notice period, skills, LinkedIn, source
- Scanned CV ke liye "Read scanned CV" button (browser me hi OCR, koi key nahi)
- Dashboard: aaj ke / hafte ke applications, 14 din ka chart, top posts, qualification, need-a-look list
- Candidates: search, filter (post, qualification, stage, date), stage change, bulk actions
- **Har candidate aapki Google Sheet (HRDHO_CANDIDATE_DETAILS) me apne aap add hota hai** — purane columns
  wahi rehte hain, naye columns (qualification, stage, status…) end me jud jaate hain. Same email dobara
  aaye ya HR stage badle to wahi row update hoti hai, duplicate nahi banti.
- CV Google Drive ke folder "HR Mail Desk - Candidate CVs" me save hoti hai, link Sheet me
- Excel export: poori details, ya **bio-data list format** (Recruitment Mailer me seedha upload ho sake)

## Files
| File | Kaam |
|---|---|
| `index.html` | poora app |
| `redirect.html` | Microsoft sign-in ke liye (zaroori) |
| `logo.png` | **aap daaloge** — West-Coast logo (Recruitment Mailer wala hi) |

## Setup (10 minute)
1. Is folder ki teeno files (`index.html`, `redirect.html`, `logo.png`) ek nayi GitHub repo me upload karo
   → Vercel me import karo (Framework: **Other**) → Deploy. Koi environment variable nahi chahiye.
2. **entra.microsoft.com → App registrations → West-Coast Recruitment Mailer** (wahi purani app):
   - **Authentication → Single-page application → Add URI**:
     `https://AAPKI-NAYI-SITE.vercel.app/redirect.html` → Save
   - **API permissions → Add → Microsoft Graph → Delegated → Mail.Read** → Add
     (shared HR mailbox padhna ho to **Mail.Read.Shared** bhi)
3. Nayi site kholo → **Settings** → Client ID + Tenant ID daalo (Recruitment Mailer wale hi) → Save
4. **Google Sheet (5 minute, ek baar):**
   - console.cloud.google.com → New Project → **APIs & Services → Library** → **Google Sheets API** Enable,
     **Google Drive API** Enable
   - **OAuth consent screen** → (company Google Workspace ho to *Internal*, warna *External* + jis Google
     account se login karoge use **Test users** me add karo)
   - **Credentials → Create credentials → OAuth client ID → Web application**
     → **Authorized JavaScript origins**: `https://AAPKI-NAYI-SITE.vercel.app` (koi redirect URI nahi)
     → Create → **Client ID** copy karo (Client secret ki zaroorat nahi)
   - Site → Settings → **Google Sheet** card → Client ID paste → **Save and connect** → Google login →
     dono permission (Sheets, Drive) tick → Allow
   - Jis Google account se login karo uske paas Sheet ka **Editor** access hona chahiye
5. Left side **Connect Outlook** → HR account se sign in → Accept
6. App pichhle 30 din ke mails padh lega. Uske baad har 10 minute me apne aap check karta hai
   (jab tak page khula hai).

## Dhyan rakhne wali baatein
- Data **isi computer ke browser** me save hota hai. Doosre computer par bhi chahiye to
  Settings → Download backup → doosre computer par Restore backup.
- Google sign-in 1 ghante chalta hai. Uske baad naye rows "waiting" me rehte hain — sidebar me
  **Sign in to Google again** dabao, sab ek saath Sheet me chale jaayenge (kuch miss nahi hota).
- Page band hoga to auto-check bhi band. Kholte hi naye mails padh lega, kuch miss nahi hota.
- Rules se details nikalti hain (AI nahi), isliye kabhi-kabhi koi field khaali reh sakti hai —
  wo candidate **Needs a look** me dikhega, khol kar theek karo aur Save.
- Purane .doc (Word 97-2003) CV padhe nahi jaate; "Open CV" se khol kar details bhar do.
- Demo dekhna ho: `https://AAPKI-SITE.vercel.app/?demo` (sample data, kuch save nahi hota)
