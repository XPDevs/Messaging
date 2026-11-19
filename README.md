# ntfy Chat

ntfy Chat is a complete messaging app built on ntfy topics. It runs as a single page app from index.html and uses one HTML file for the chat interface, one file for the call screen and a small service worker for offline use. There is no build step and no framework. The app includes direct chats, groups, communities, status updates, real time voice and video calls, rich media, privacy controls, storage tools, backup and restore, business tools and a full settings area.

The default transport is the public ntfy.sh server. The server can be changed in Settings, Advanced, URL. The app checks the ntfy health endpoint before saving a new address and then resubscribes every conversation on the new server.

The app opens a WebSocket connection first. If a network blocks that, it falls back to server sent events, then to HTTP polling. This keeps messages arriving on restrictive networks and avoids the cross origin error browsers show when an event stream is blocked. Messages and links that point to a local file URL are ignored, so old device paths cannot break the page.

## Run the app

Open the folder with any static web server. For example, run npx serve . in the project folder and open the address it prints. Do not open index.html as a file URL, because encryption and the service worker need a secure context. HTTPS is required for camera, microphone, notifications and encryption in most browsers. Localhost is treated as secure.

The first run asks for a display name. The app creates an eleven digit number. That number is the ntfy topic for your own channel. Share the number or the invite link with another person, or scan the QR code. A one to one chat uses the other person number as its topic.

## Messaging

Direct messages support reply, edit, forward, pin, star, copy, multi select, bulk delete, mark unread, scheduled sending, reminders, drafts, link previews, text formatting, spoilers, in chat search and message information. Formatting uses asterisks for bold, underscores for italic, tildes for strikethrough, backticks for monospace and double pipes for spoilers. Long messages and large files are split into parts and rebuilt on the other side. Media includes photos, video, files, voice notes and location. Each message shows sent, delivered and read state when the other side permits receipts.

Drafts are saved as you type and restored when you reopen a chat. Scheduled messages send while the app is open. A message reminder creates a local notification at the chosen time. Link previews fetch a title and image for the first link in a message and can be disabled in Settings, Advanced.

## Privacy and security

One to one chats derive an AES GCM key from an ECDH key pair on each device. The key exchange happens automatically when both devices are online. Text, photos, voice notes, locations and call signalling are sealed before they reach the server. A safety number can be compared in Settings, Privacy. Groups use the shared topic and rely on topic secrecy, while Vault Lock can protect an individual message or attachment with a passcode.

Privacy controls include disappearing messages, view once media, chat lock, hidden chats, block and report, last seen, online status, read receipts, typing indicator, profile photo visibility, about visibility and status visibility. Security alerts record account and privacy changes. Active sessions can be reviewed and other session records can be logged out. The session list is stored on this device, because ntfy has no account server.

Disappearing messages remove content from this app after the timer. Copies already delivered to the server or another device are outside the control of this app. View once media is removed from the app after it is opened.

## Groups

Groups support a name, description, profile photo, admin roles, admin permission management, member permissions, invite links, QR invitations, join requests, join approval, member removal, ownership transfer, announcement mode, mentions, message pinning, polls, events, mute controls and member search. A group invite link can be shared from the group information page. The person who opens the link sends a join request, and an admin can approve or deny it. Only admins can post when announcement mode is enabled. Poll votes and event replies are delivered as control messages on the same topic.

## Status

Status updates support text, photo, video, GIF and voice, with captions, reactions, replies, viewers, view counts, privacy, audience exclusions, muting, resharing, drafts and automatic expiry after twenty four hours. Status metadata is sent to each direct chat and to group chats. Media is stored locally and the other side receives the caption and type, because a full media broadcast would exceed the ntfy message size limit. Status reactions and viewer receipts return over the same topic.

## Communities

A community can contain several groups, an announcement group, a description, a photo, administrators, an invite link, membership tools, community wide announcements and notification settings. Creating a community also creates an announcement group. The announcement composer sends the message to every group in the community.

## Chat organisation

Chats can be pinned, archived, restored, sorted, filtered by folder, marked as favourites and marked unread. The sidebar has filters for all chats, unread chats, favourites, groups and archived chats, plus any custom folders. Starred messages have their own page. Saved messages can use your own channel. Every chat can have its own wallpaper, colour, mute state, notification mode, tone and disappearing timer. Desktop shortcuts include Control or Command and K for search, Control or Command and comma for settings, Control or Command and N for a new chat, Control or Command and F for in chat search, Alt and the arrow keys for chat navigation and Escape to close a panel.

## Contacts

Contacts are stored on this device. A contact can have a name, number, label, favourite flag and block state. The contact page shows a profile, QR code, message button, call buttons, sharing and removal. Contacts can be exported and imported as JSON. The sync from chats action adds unknown chat participants to the contact list. Blocked contacts are listed in Contacts and in Privacy.

## Notifications

Notifications support per chat settings, per chat tones, timed mute, quiet hours, Do Not Disturb, mention only mode, preview privacy and notification history. Browser notifications work while the app is running. Notification grouping uses one tag per chat. Sound patterns are generated with the Web Audio API and do not need extra files.

## Storage and backups

The storage page shows total use, use per conversation and media size. Media can be managed per chat, cleared from the cache, downloaded on demand or limited by size. Automatic media download, a download limit and a low data mode are available. Standard JSON backup and restore use the original app format. Encrypted backups use AES GCM with a passcode. A single conversation can be exported as text. A device snapshot can be sent to your own channel to move history to another device. Diagnostics export contains settings and counts but no message text.

## Calls

Calls use WebRTC with the ntfy topic as the signalling channel. One to one voice and video calls, group voice calls and group video calls are supported. A call has mute, camera control, screen sharing, participant management, quality indicators, reconnect handling, permission checks and privacy controls. Video quality can be set to low, automatic or high. Call history appears in the Calls page and in the conversation. The call screen uses public STUN servers. A TURN server is not included, so a very restrictive network may prevent a direct media path.

## Stickers and GIF

Sticker packs, custom sticker upload, animated GIF search, sticker favourites, sticker search and pack sharing are included. Custom stickers and avatars are stored on this device. GIF search uses a public GIF service and needs a network connection. Emoji stickers are sent as messages with a sticker marker, so the other side renders them at sticker size.

## Platform and usability

The app includes a web app manifest, installable PWA icons, an offline app shell, an offline banner, retry of failed text messages, keyboard shortcuts, screen reader labels, font scaling, language selection for the main interface, connection indicators, update notices, a help centre and a feedback action. Multi device history can be moved with a backup file or a snapshot sent to your own channel. Language support covers English, Spanish, French and German labels for the main areas. Font scaling ranges from small to larger.

## Business tools

Business mode adds a business name, description, opening times, open days, a verified mark, a product catalogue, product sharing, automated greeting and away messages, quick replies, customer labels and local statistics. Greetings and away replies are limited to one per contact in twelve hours. Quick replies can be inserted from the composer.

## Settings and advanced server

The settings area is a full page with sections for Profile, Privacy, Chats, Notifications, Storage and data, Calls and video, Stickers and GIF, Business, Advanced and About. The Advanced section contains the ntfy server address.

To change the server, open Settings, Advanced, enter an address such as https://ntfy.example.com, then press Test and save. The app requests the ntfy health endpoint at /v1/health. A valid ntfy server answers with a healthy flag. After a successful test the address is stored, every conversation is resubscribed and new messages use the new server. The Reset to ntfy.sh button returns to the public server. The server address must use HTTPS when the app is served over HTTPS.

The Advanced section also has link preview control, transport state, encryption state, diagnostics export, keyboard shortcut notes, a new number action and a reset action.

## Files

index.html contains the whole chat app, the settings page, the status page, communities, contacts, calls and the enhancement layer. call.html is the standalone call page from the original project. manifest.json describes the installable app. sw.js provides the offline shell. favicon.ico and the PNG icons provide app artwork. ringtone.mp3 is the ring sound. The QR helper library is included in its own folder.

## Privacy limits

The ntfy server sees topic names, message timing, message sizes and encrypted payloads. It does not see the plaintext of a one to one chat once keys are exchanged. Group topics are shared secrets and should only be given to trusted people. Status media is stored on the device that created it. Session management and business statistics are local records, not server side account features. Call media travels directly between browsers when a path is available, and the ntfy server only carries signalling.

## Licence and origin

The project started from XPDevs Messaging and keeps the same single file approach. The app contains no AI features and sends no analytics.
