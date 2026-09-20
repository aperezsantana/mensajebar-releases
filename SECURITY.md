# Security

## What the app does on purpose

MensajeBar reads the Messages database on the Mac it runs on and emails matching messages to the
addresses configured in it. That is the product, not a vulnerability:

- Anyone sitting at the **unlocked Mac** can open the rules window and add a recipient. The
  app deliberately has no password of its own — it lives behind the macOS login.
- The forwarding **history holds message text** (including one-time codes) until it is cleared.
  It is a plain file in the user's Application Support folder, readable by that user.
- Email is sent through **Mail.app**, so it inherits that account's transport and its security.

## What is a bug

- Forwarding a message that **no enabled rule matches**.
- Sending to an address that is not in the matching rule's recipient list.
- Ignoring the maximum-age limit.
- Installing an update whose DMG does not match the `sha256:` in the release notes.
- Anything that lets code outside the app read the data it holds.

## Reporting

Please use GitHub's **private vulnerability reporting** on this repository
(Security → Report a vulnerability). It does not expose an email address for anyone.
