# Password-Strength-Analyzer

A browser‑based tool that evaluates password strength in real time, estimates entropy and crack time, flags weak patterns, and generates secure alternatives—all without sending any data to a server.

Features
Real‑time analysis – Instantly inspect any password as you type.

Entropy & crack time – Calculates character‑pool entropy and estimates how long an offline attacker would need to guess it (at 10 billion guesses per second).

Detailed checklist – Shows passes/fails for length, character diversity, common passwords, keyboard sequences, and repeated characters.

Visual dial – A clear, colour‑coded gauge that reacts to password strength.

“Remember” vault – Stores SHA‑256 hashes of passwords you choose to keep on your device. The tool warns you if you reuse a previously stored password (without ever seeing the original).

Random password generator – Produces cryptographically strong random passwords (16 characters) and passphrases (5 words) using the browser’s native crypto.getRandomValues().

Local only – No network requests, no tracking, no external dependencies. Everything runs in your browser.

How It Works
Strength Calculation
Entropy is estimated as:
entropy = length × log₂(character_pool_size)

The following penalties are applied:

Common passwords – If the password appears in a built‑in list of 100 common passwords, entropy is capped at 8 bits.

Keyboard sequences – Detects runs like 1234, qwerty, abcd, etc., and subtracts 8 bits.

Repeated characters – Three or more identical characters in a row (e.g., aaa) subtracts 6 bits.

The final entropy determines the strength category:

< 28 bits → Very weak

28 – 39 → Weak

40 – 59 → Fair

60 – 79 → Strong

≥ 80 → Very strong

Crack time assumes an attacker can try 10 billion guesses per second, a typical rate for offline hashing attacks.

The “Vault”
When you click “Remember this password”, the tool computes the SHA‑256 hash of the current password and stores it in your browser’s localStorage (or an in‑memory fallback if localStorage is unavailable). The plaintext password is never saved.

Later, when you type a password, the tool hashes it and checks whether that hash exists in the vault. If it does, you’ll see a reuse warning, helping you avoid password recycling.

Password Generation
Two generation modes are available:

Random password – 16 characters, including at least one uppercase, one lowercase, one digit, and one symbol. The character set excludes ambiguous characters like O (zero‑risk) and 1 (looks like l).

Passphrase – 5 words from a 200‑word list, with a random digit and symbol inserted, and the first word capitalised (e.g., Anchor‑ember‑glacier3#). This results in high entropy and better memorability.

All randomness comes from the Web Crypto API (crypto.getRandomValues), which is cryptographically secure.

Usage
Open the HTML file in any modern browser (Chrome, Firefox, Edge, Safari, etc.). No internet connection is required after the initial load.

Type a password into the input field.

Watch the dial, verdict, and checklist update.

Expand the “Stronger alternatives” section to generate a new password/passphrase.

Click “Remember this password” to add its hash to the vault for reuse detection.

Click “Clear vault” to erase all stored hashes.

Privacy & Security
Zero data leaves your device – No analytics, no telemetry, no external requests.

Plaintext never stored – The vault only contains irreversible SHA‑256 hashes.

Cryptographically secure randomness – All generated passwords use the browser’s built‑in random source.

Transparent code – The entire application is a single, self‑contained HTML file. You are encouraged to inspect the code.

Dependencies
None. The tool uses only standard browser APIs:

crypto.subtle.digest (SHA‑256)

crypto.getRandomValues

localStorage (optional, fallback to memory)

License
This tool is provided as open source. You may use, modify, and distribute it freely. (No explicit license is included; you are welcome to add your own.)

Contributing
Feel free to open issues or pull requests on the repository hosting this file. Contributions that improve the entropy estimation, expand the wordlist, or add more attack models are especially welcome.
