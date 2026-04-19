# 🧂 salt-text

A secure, offline-first text editor that encrypts your files entirely in the browser. No server. No account. No tracking. Just download the file and use it.

---

## Deploy in one step

Download [`salt-text.html`](https://raw.githubusercontent.com/AbhijithBaby/Salt-Text/main/salt-text.html) and open it in a browser.

OR 

use terminal 
```bash
curl -L -O https://raw.githubusercontent.com/AbhijithBaby/Salt-Text/main/salt-text.html
```
```bash
wget https://raw.githubusercontent.com/AbhijithBaby/Salt-Text/main/salt-text.html
```

That's it. There is no install, no server, no dependencies, and no network requests. The app uses your device's system font and works fully offline from the first open.

---

## How it works

Everything happens locally in your browser using the [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API).

- **Encryption:** AES-256-GCM
- **Key derivation:** PBKDF2 with SHA-256, 250,000 iterations, random 16-byte salt
- **IV:** Random 12-byte nonce generated fresh on every save
- **Output format:** JSON file containing `{ v, salt, iv, iterations, ciphertext }` — all base64-encoded

Your password never leaves the browser. The encrypted file never touches a server. I (or whoever hosts this) sees nothing — there is nothing to see.

---

## Features

- Encrypt and decrypt `.enc.json` files with a password of your choice
- Save as plain `.txt` when encryption is not needed
- Inline Find & Replace with match highlighting, Prev/Next navigation, Replace, Replace All 
- Draft auto-save to `localStorage` (opt-in, plaintext — you are warned)
- Draft stores your file name across sessions
- File name remembered after open, editable inline
- Insert current date and time at cursor
- Dark / Light / System theme
- Fully responsive — works on desktop, tablet, and mobile
- No analytics, no ads, no network requests after initial load

---

## Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl / ⌘ + O` | Open file |
| `Ctrl / ⌘ + N` | New file |
| `Ctrl / ⌘ + S` | Save encrypted |
| `Ctrl / ⌘ + Shift + S` | Save plain text |
| `Ctrl / ⌘ + F` | Toggle Find bar |
| `Ctrl / ⌘ + P` | Set / change password |
| `Ctrl / ⌘ + D` | Insert date & time |
| `F3` / `Shift + F3` | Next / Previous match |
| `Ctrl / ⌘ + G` / `+ Shift` | Next / Previous match |
| `Enter` | Next match (when focused in Find input) |
| `Escape` | Close Find bar or close modal |

---

## File format

Encrypted files are saved as `.enc.json` with this structure:

```json
{
  "v": 1,
  "salt": "<base64>",
  "iv": "<base64>",
  "iterations": 250000,
  "ciphertext": "<base64>"
}
```

The format is open and documented. You can decrypt these files with any tool that supports AES-256-GCM + PBKDF2, independent of salt-text.

---

## Security notes

- **Your password is everything.** AES-256-GCM is effective with current technology.
- **The draft feature stores plaintext** in `localStorage`. It is off by default. Enable it only on a device you trust and are the sole user of. Nothing is sent to any server.
- **Encryption is client-side only.** No key, no password, and no plaintext ever leaves your browser i don't collect or store any data. 
- **If you lose your password, your data is gone.**  i repeat **If you lose your password, your data is gone.**
- **Threat model:** salt-text protects your files at rest against anyone who gets hold of the `.enc.json` file but does not know your password. It does not protect against malware on your device, a compromised browser, or someone watching your screen.

---

## Browser support

Any browser that supports the Web Crypto API and `AES-GCM`:

i think least you want is :
Google Chrome: Full support since version 37 (2014).
 Firefox: Full support since version 34 (2014).

recommend:
- Chrome / Edge 37+
- Firefox 34+
- Safari 11+
- All modern mobile browsers

---

## Self-hosting (optional)

If you want to serve it from a web server instead of opening it as a local file:

```bash
# Python
python3 -m http.server 8080

# Node (npx)
npx serve .

# Caddy
caddy file-server --browse
#or any file Server tech 
```

Then open `http://localhost:8080/salt-text.html`.



## License

Do whatever you want with it. 
