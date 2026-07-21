# 🔐 Password Strength Analyzer

A lightweight, client‑side tool that evaluates password strength in real time, estimates entropy and crack time, warns about weak patterns, and generates secure alternatives—**without ever sending your data anywhere**.

![Screenshot of the generator and vault features](https://github.com/user-attachments/assets/08681463-6a2b-429a-8138-563e9632171f)
![Screenshot of the Password Strength Analyzer in action](https://github.com/user-attachments/assets/ccf72c90-b0e1-4aa5-a67c-41bdd2fa8931)

---

## ✨ Features

- **Real‑time analysis** – See strength, entropy, and crack time update as you type.
- **Detailed checklist** – Pass/fail for length, character variety, common passwords, keyboard sequences, and repeated chars.
- **Visual dial** – A color‑coded gauge that instantly shows how strong your password is.
- **“Remember” vault** – Stores only SHA‑256 hashes locally. Alerts you if you reuse a password you've previously stored.
- **Secure generators** – Creates cryptographically strong random passwords (16 chars) and memorable passphrases (5 words) using `crypto.getRandomValues()`.
- **100% offline** – No external requests, no tracking, no server‑side processing. Everything runs in your browser.

---

## 🚀 How to Use

1. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari).
2. Type a password into the input field.
3. Instantly see:
   - Entropy (bits)
   - Estimated crack time (at 10 billion guesses/sec)
   - A strength category (Very Weak → Very Strong)
   - A checklist of what's good and what isn't.
4. Click **“Remember this password”** to store its hash locally. The tool will warn you if you ever type that same password again.
5. Expand the **“Stronger alternatives”** section to generate a new random password or passphrase with one click.

---

## ⚙️ How It Works

### Entropy & Crack Time

The tool estimates entropy as:

entropy = length × log₂(character_pool_size)


Then applies penalties for:

- **Common passwords** – if the password is in a built‑in list of ~100 common ones, entropy is capped at 8 bits.
- **Keyboard sequences** – e.g., `qwerty`, `1234`, `abcd` → subtracts 8 bits.
- **Repeated characters** – three or more in a row (e.g., `aaa`) → subtracts 6 bits.

Crack time is calculated assuming an offline attacker can try **10 billion guesses per second**—a realistic figure for a leaked, poorly‑hashed database.

### The Local Vault

- When you click **“Remember this password”**, the tool computes the SHA‑256 hash and stores it in `localStorage`.
- The plaintext password is **never saved**.
- On every new input, the tool hashes the password and checks it against the vault. If there's a match, it shows a reuse warning.

### Password Generation

- **Random password** – 16 characters with at least one uppercase, one lowercase, one digit, and one symbol. Ambiguous characters (like `O` and `l`) are excluded.
- **Passphrase** – 5 words from a 200‑word list, with a random digit and symbol inserted, and the first word capitalised (e.g., `Anchor‑ember‑glacier3#`). High entropy and easier to remember.

All randomness comes from the Web Crypto API (`crypto.getRandomValues()`).

---

## 🛡️ Privacy & Security

- **Zero data leaves your device** – no analytics, no telemetry, no external network calls.
- **Plaintext never stored** – the vault contains only irreversible SHA‑256 hashes.
- **Cryptographically secure randomness** – all generated passwords use `crypto.getRandomValues()`.
- **Fully transparent** – the entire application is a single, self‑contained HTML file. Feel free to inspect the source.

---

## 📁 Tech Stack

- Vanilla JavaScript (ES6)
- Web Crypto API (`crypto.subtle`, `crypto.getRandomValues`)
- `localStorage` (with fallback to in‑memory storage)
- Google Fonts (loaded on first visit; no tracking)

No frameworks, no build tools, no dependencies.

---


## 📄 License

This project is open source. Feel free to use, modify, and distribute it. (You can add your preferred license, e.g., MIT.)

---

## 🤝 Contributing

Contributions are welcome! If you find a bug, have a suggestion, or want to expand the wordlist / common‑password list, please open an issue or submit a pull request.
