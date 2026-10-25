# Campus Lost & Found

A shared lost-and-found board for your college. Students sign in with Google, post lost or found items with a photo, and owners claim items by answering a private question. Everyone sees the same live board.

## Setup (about 15 minutes, free)

1. **Create a Firebase project** at https://console.firebase.google.com (Add project; Analytics is optional).
2. **Add a web app**: Project overview > the `</>` icon. Copy the `firebaseConfig` values.
3. **Paste the config** into `index.html`, in the `firebaseConfig` block near the bottom. Optionally set `COLLEGE` to your college name.
4. **Turn on login**: Build > Authentication > Get started > Sign-in method > Google > Enable.
5. **Create the database**: Build > Firestore Database > Create database > production mode, pick a region close to you.
6. **Publish the security rules**: Firestore > Rules tab > replace everything with the contents of `firestore.rules` > Publish.
7. **Make yourself admin** (optional): sign in once on the site, then in Authentication > Users copy your **User UID**. In Firestore > Start collection `admins` > Document ID = your UID > add any field (for example `role` = `admin`).
8. **Test locally**: browsers block Firebase login from `file://`. Run `npx serve` (or VS Code "Live Server") in this folder and open the `localhost` address.
9. **Deploy**: push to GitHub and enable GitHub Pages, or drag the folder to Netlify. Then add your site's domain in Authentication > Settings > Authorized domains.

## How permissions work

| Action | Who can do it |
|---|---|
| Read posts | Anyone |
| Post an item | Signed-in users |
| Mark returned, reopen, delete | The poster, or an admin |
| Send a claim | Signed-in users, but not the poster |
| Read claims and the private answer | The poster, or an admin (and each claimant sees their own claim) |
| Approve or reject a claim | The poster, or an admin |

These rules live in `firestore.rules` and are enforced by Firebase, so hiding buttons is not the only protection.

## Notes

- **Photos** are shrunk in the browser (max 800 px) and stored inside the post, so you don't need Firebase Storage. Storage may need a paid plan; check current Firebase pricing if you want to switch.
- **Contact details are public** on each post. Tell students to use an email or a number they're happy to share.
- **Free-tier limits** change over time. Check Firebase's current Spark plan limits before a big launch.
- Videos are not supported yet. Add them later with Storage, a size limit, and a report button.

## Next ideas

Auto-match found and lost posts, a WhatsApp contact button, a QR poster for notice boards, and a desk handover code.
