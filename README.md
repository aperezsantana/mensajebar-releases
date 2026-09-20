# MensajeBar for macOS

**Forward incoming iMessage and SMS to email, automatically, the moment they arrive.** A menu-bar
app that watches the Messages database on your Mac and mails whatever matches your rules — by
sender, by keyword, or both — to whichever addresses you choose. No server, no cloud account, no
telemetry.

**[⬇︎ Download the latest build](https://github.com/aperezsantana/mensajebar-releases/releases/tag/latest)**
· universal (Apple Silicon + Intel) · macOS 13 or newer

This repository holds the **downloads**. The source is private.

---

## What it's for

- **Get one-time codes where you actually are.** Bank, delivery, Google, fuel-app codes arriving as
  SMS on a Mac you're not sitting at — forwarded to the inbox you do read.
- **Archive what a carrier deletes.** Verification and notification texts land in your mail
  archive, searchable, with the history kept in the app too.
- **Route different senders to different people.** One rule per sender or keyword, each with its
  own recipients and its own sending account.
- **Push it to another device or person over iMessage**, instead of — or as well as — email.

## Works with

| | |
|---|---|
| **Messages** | iMessage and SMS/MMS, including SMS relayed from an iPhone via Text Message Forwarding |
| **Mail.app** | sends from any account already configured there — iCloud, Gmail, Exchange, IMAP/SMTP |
| **macOS** | 13 Ventura or newer, Apple Silicon and Intel |

It reads the local Messages database, so **anything your Mac receives in Messages can be
forwarded** — you do not need an iPhone, a carrier feature, or an SMS gateway. It does not touch
WhatsApp, Telegram or Signal, which keep no readable local database.

## Rules

| Field | Meaning |
|---|---|
| Sender contains | substring of the handle **or of the contact's name**, case-insensitive. Empty = any sender |
| Keywords | comma-separated; any one of them is enough. Empty = any text |
| Send from | one of your Mail.app accounts |
| Forward to | comma-separated email recipients, per rule |
| Forward over Messages | iMessage recipients — send it on to another contact, or to your own number |
| Max age | global, in minutes — older messages are not forwarded |

Sender and keywords combine with AND. A rule with neither is refused: it would forward every
message that arrives on the Mac.

**Try before you save.** «Probar en seco» runs the rule against the last 300 real messages and
shows exactly what it would have caught, without sending anything.

**The max age matters.** If the Mac has been off for days, the app would otherwise find everything
that matched in the meantime and mail it in one burst — a pile of already-expired codes. Anything
older than the limit is skipped and counted in the log.

## No polling

macOS keeps messages in a SQLite database. The app watches its write-ahead log with `kqueue`, so
the kernel wakes it the instant Messages commits a row: forwarding happens in milliseconds, not on
a timer.

## Permissions it asks for, and why

- **Full Disk Access** — the only way to read `~/Library/Messages/chat.db`. Without it the app
  shows a warning icon and forwards nothing.
- **Automation → Mail** — to hand the message to Mail.app for sending.
- **Automation → Messages** — only if a rule forwards over iMessage.
- **Contacts** — optional: lets rules be written with a person's name, and puts that name in the
  subject instead of a phone number. Refuse it and everything still works on raw handles.

Nothing else. The app makes no network connection of its own except checking this page for updates.

## Privacy

Your messages go from your Mac to the addresses **you** configured, through **your own** mail
account. Nothing is sent anywhere else. The forwarding history lives on your Mac, holds the last
500 messages, and can be cleared from the app at any time.

## Install

1. Download and open the DMG, drag **MensajeBar** to Applications.
2. First launch: System Settings → Privacy & Security → **Open Anyway** (the app is not notarized).
3. Grant **Full Disk Access** to MensajeBar.
4. In the menu-bar icon, turn on **«Arrancar al iniciar sesión»** so it starts with your session.

The app updates itself from this repository. Each release body carries the `commit:` and `sha256:`
of its build, and nothing is installed unless the downloaded DMG matches that hash.

## Spanish or English

Pick the interface language in the rules window — *Automático* follows your Mac's. It is a personal
tool, published in case it is useful to someone else.

## No warranty

This software is provided as is, with no warranty of any kind — see [LICENSE](LICENSE). It reads
your messages and sends them by email: set your rules carefully, and check the history after
changing them. A rule wider than you intended will forward more than you meant.

The app is MIT-licensed. The source repository is private, so today the licence covers this build
and its documentation.

## Related

- [PorteroBar](https://github.com/aperezsantana/porterobar-releases) — Fermax DUOXME video
  intercom in the menu bar
- [AirzoneBar](https://github.com/aperezsantana/airzone-bar-releases) — Airzone HVAC over the local
  API, no cloud account
- [Imprenta](https://github.com/aperezsantana/imprenta-releases) — share any printer over AirPrint
