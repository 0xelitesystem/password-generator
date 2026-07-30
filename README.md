# Password Generator

Generate strong passwords and passphrases in your browser using the cryptographic random source (`crypto.getRandomValues`, never `Math.random`). See an entropy estimate in bits, a strength label, and copy any result with one click. No server, no tracking, no external dependencies.

## Live demo

https://0xelitesystem.github.io/password-generator/

## Features

- Password mode with a length slider (6 to 64) and toggles for uppercase, lowercase, digits, and symbols
- Exclude ambiguous characters (`0 O l 1 I`)
- Passphrase mode: N words (3 to 12) from an embedded list of a few hundred common words, joined by a separator of your choice, with optional capitalization and an appended digit
- Entropy estimate in bits, computed from the real pool or word-list size, plus a strength label and bar
- Generate multiple at once (1 to 20)
- Copy a single result or copy all
- Dark-mode toggle, keyboard usable

## How it works

Every random choice comes from `crypto.getRandomValues`. To pick an item from a list of size N without bias, the tool uses rejection sampling: it draws a random byte and discards any value in the small leftover range that would skew the distribution, so each item is equally likely. `Math.random` is never used.

Entropy is the base-2 logarithm of the number of equally likely outcomes:

- Password: `length x log2(poolSize)`, where `poolSize` is the number of distinct characters actually available after your toggles.
- Passphrase: `words x log2(listSize)`, plus `log2(10)` if you append a digit, where `listSize` is the exact length of the embedded word list.

Because the words are chosen uniformly and independently, the per-word entropy is honest at `log2(listSize)` bits. A larger word list would give more bits per word, this one is deliberately compact so it can be embedded inline.

## Privacy

Everything runs in your browser. Generated values never leave your machine. You can confirm this by viewing the page source or watching the network tab in DevTools, no requests are made. The tool works offline with no external dependencies. For real accounts, store passwords in a password manager, never reuse them, and turn on two-factor authentication.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
