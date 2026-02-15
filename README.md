# Host architecture

Host is a federated events and invitations platform within the [Geisha](https://geisha.app) suite. It gives people full sovereignty over their event data through open calendar standards, end-to-end encryption, and federated sync — combining scheduling, invitations, and event management in a single privacy-first experience.

## What is Host?

Host replaces the fragmented landscape of event tools (Evite for invitations, Doodle for scheduling, Eventbrite for ticketing, Google Calendar for time management) with a unified platform where event data stays under the host's control. Every event, guest list, and RSVP is encrypted and syncs through standards-based protocols — no vendor lock-in, no data harvesting.

### Ecosystem context

Host operates within the Geisha ecosystem and the broader Omnifi infrastructure:

- **[Naamio Link Space](https://naamio.cloud)** provides the federation protocol for cross-instance event discovery, RSVP, and content sharing
- **[Sinetti](https://sinetti.dev)** handles identity and authentication via `auth.geisha.app`, supporting OAuth 2.1, OpenID Connect, WebAuthn, and Biscuit tokens
- **[Guide](https://geisha.app/guide)** provides venue and place discovery integration
- **[Grocer](https://geisha.app/grocer)** enables shared meal planning and expense tracking for gatherings
- **[Chef](https://geisha.app/chef)** offers recipe curation for hosted meals and potlucks
- **[Minttu](https://minttu.dev)** provides the foundational design system and CSS framework

### Standards compliance

Host builds on established open standards rather than inventing proprietary formats:

| Standard | Purpose |
|----------|---------|
| iCalendar (RFC 5545) | Event representation and interchange |
| CalDAV (RFC 4791) | Calendar sync with any compliant server |
| jCal (RFC 7265) | JSON representation of calendar data |
| vCard 4.0 (RFC 6350) | Contact and guest information |
| FEP-8a8e | ActivityPub event federation |
| Schema.org Event | Structured event metadata for discovery |
| h-event microformat | IndieWeb event publishing |
| WebDAV (RFC 4918) | Attachment and media storage |
| W3C Web Annotation | Event notes and collaborative annotation |

### Differentiators

1. **Privacy-preserving guest lists**: guests do not see each other by default — the host controls visibility
2. **Selective location disclosure**: full venue address revealed only to confirmed guests; invitees see approximate area only
3. **End-to-end encrypted event data**: server never sees plaintext event details, guest lists, or location data
4. **Local-first with conflict-free replication**: CRDT-based sync (Yjs) across devices, works offline
5. **Combined scheduling and invitations**: availability polling, invitation delivery, and RSVP management in one flow — no separate scheduling tool needed
6. **Federation-first**: events discoverable across Host and Naamio Link instances via ActivityPub
7. **CalDAV interoperability**: bidirectional sync with Nextcloud, iCloud, Google Calendar, and any compliant server
8. **Wasm plugin extensibility**: custom event workflows, approval chains, and integrations via WebAssembly components

## What this repository is for

This repository holds architectural governance artefacts for Host — the decisions and discussions that shape how Host is built.

| Folder | Contains | Purpose |
|--------|----------|---------|
| `decisions/` | Accepted architectural decisions | Record of choices made and their rationale |
| `comments/` | Discussion and review threads | Community input on proposed decisions |

This follows the [Omnifi governance process](https://handbook.omnifi.foundation/engineering/architecture/governance.md), which replaces traditional ADRs and RFCs with a simpler two-folder model.

### How the process works

1. **Propose** — open an issue using the `decision` template describing the architectural choice
2. **Discuss** — community and maintainers discuss in the issue; longer-form analysis goes in `comments/`
3. **Decide** — maintainers accept or reject; accepted decisions are recorded in `decisions/`
4. **Implement** — the relevant project repositories implement the decision
5. **Revisit** — decisions can be superseded by new decisions as understanding evolves

## Projects in scope

Host spans several concerns, each progressing through the milestone roadmap:

### Event data model and calendar integration

The foundation. iCalendar and jCal compliance for event representation. Schema.org Event and h-event microformat support. CalDAV bidirectional sync with Nextcloud, iCloud, Google Calendar, and any compliant server. Recurring event patterns (RRULE) with exception handling. Availability detection and free/busy queries. Time zone handling across distributed guests. Calendar views with smooth transitions.

### Invitation and RSVP system

Customisable invitation templates and theming. RSVP management with configurable response options. Privacy-controlled guest lists. Email and link-based delivery. QR code invitations for in-person sharing. vCard 4.0 contact integration. Guest dietary preferences, accessibility needs, and custom fields. Scheduling polls with anonymous preference collection.

### Event creation and management

Rich event pages with descriptions, agendas, and schedules. Multi-session and multi-track support. Event branding. Host dashboard with real-time tracking. Co-host and organiser roles with delegated permissions. Templates for recurring gatherings. Cancellation and rescheduling with automatic notification. Accessibility information and accommodation management.

### Location and venue management

Selective address disclosure based on RSVP status. Venue profiles with capacity, amenities, and accessibility features. Open map data integration. Virtual and hybrid event configuration. Guide companion integration for venue discovery. Weather context for outdoor events.

### Check-in, attendance, and ticketing

QR code and NFC-based check-in. Self-service kiosk mode. Ticketing for paid events with pluggable payment processing. Ticket tiers with capacity limits. Waitlist management. Digital ticket wallet with Apple Wallet and Google Wallet passes. Badge generation for professional events.

### Content sharing and collaboration

Privacy-preserving photo and media galleries. Document and agenda distribution. Post-event summaries. Gift registry for milestone events. Shared expense tracking (Grocer companion integration). Event feedback collection. Exportable event memories.

### Sync and data sovereignty

CalDAV and WebDAV sync. CRDT-based conflict resolution across devices. Zero-knowledge end-to-end encryption. Per-event encryption with guest-specific key distribution. Git-based event archive. Privacy dashboard. Offline access via Service Workers. Export to iCalendar, jCal, and CSV.

### Web application

Progressive web application at `host.geisha.app` built with Deno Fresh 2 and Islands Architecture. Declarative shadow DOM custom components. Real-time updates via Server-Sent Events. Minttu styling with Geisha Host style extensions. Offline-first with background sync. Push notifications. Full PWA installation on mobile and desktop.

### Federation and community

Naamio Link Space and ActivityPub federation (FEP-8a8e). Cross-instance event discovery and RSVP. Community event boards. Recurring groups with membership management. Event series and seasonal programmes.

### Intelligence and native applications

On-device event recommendations. Wasm plugin interface for custom workflows. Native iOS application (Swift and SwiftUI). Enterprise event management with approval workflows and compliance.

## Governance

Host is governed by the [Omnifi Foundation](https://omnifi.foundation). Development follows the foundation's engineering handbook and architectural governance process.

- [Engineering handbook](https://handbook.omnifi.foundation/engineering/)
- [Architecture governance](https://handbook.omnifi.foundation/engineering/architecture/governance.md)
- [Contribution guidelines](CONTRIBUTING.md)

## Repository structure

```
.
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── decisions/
│   └── .gitkeep
├── comments/
│   └── .gitkeep
├── templates/
│   ├── decision.md
│   └── comment.md
├── .gitlab/
│   └── issue_templates/
│       ├── decision.md
│       └── comment.md
└── .github/
    └── ISSUE_TEMPLATE/
        ├── decision.md
        └── comment.md
```

## Licence

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International](LICENSE).
