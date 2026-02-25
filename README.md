<p align="center">
  <img src="https://img.shields.io/badge/D%26D-5th%20Edition-7B2D26?style=for-the-badge&logo=dungeonsanddragons&logoColor=white" alt="D&D 5e"/>
  <img src="https://img.shields.io/badge/Status-Concept-C19A6B?style=for-the-badge" alt="Status: Concept"/>
  <img src="https://img.shields.io/badge/Platform-Web%20%2B%20Mobile-2E4057?style=for-the-badge" alt="Platform"/>
  <img src="https://img.shields.io/badge/License-TBD-444444?style=for-the-badge" alt="License"/>
</p>

<h1 align="center">⚔️ QuestForge</h1>
<h3 align="center">Your Table. Your Rules. Enhanced.</h3>
<p align="center"><em>A D&D 5e digital companion platform for physical tabletop sessions</em></p>

---

## 🎯 What is QuestForge?

QuestForge is a **digital companion platform** for Dungeons & Dragons 5th Edition. It is not a video game or a virtual tabletop — it's an intelligent layer on top of the real-world D&D experience.

Think of it like the **League of Legends client**, but for D&D: a persistent hub where you manage your character, coordinate with friends, form guilds, and launch into live game sessions — all while sitting at the same table with your party.

**The problem:** D&D requires tracking complex character sheets, rules, spell slots, and session logistics on paper. This creates friction, errors, and overhead that pulls you out of the game.

**The solution:** An app that digitizes everything — character management, rule enforcement, session coordination, and optionally an AI Dungeon Master — so you can focus on what matters: the adventure.

---

## ✨ Core Features

### 🧙 Character Management
Full D&D 5e character creation and lifecycle management.

- Step-by-step creation wizard: **Race → Class → Abilities → Background → Equipment**
- All SRD races, classes, spells, and items
- Ability scores (standard array, point buy, 4d6 drop lowest) with auto-calculated modifiers
- Spellbook with slot tracking, prepared spells, and concentration management
- Inventory with weight/encumbrance tracking and currency management
- Level progression with guided feature and spell selection
- Active conditions with automatic rule reminders
- Multiple characters per account with import/export

### 👥 Social & Lobby System
A social hub inspired by competitive gaming clients.

- **Friends:** Add friends, see online status, quick-invite to lobbies
- **Chat:** Real-time messaging (DMs, group chats, in-lobby chat) with rich content (dice results, character links, session invites)
- **Lobbies:** Create sessions with name, date/time, location, max players. Share invite links. Recurring scheduling support
- **Notifications:** Push alerts for session reminders, turn notifications, friend requests, guild activity
  ```
  📍 Session planned: 24 Feb, 23:00 — Georgia, Tbilisi | Table Games Club Guild
  ```

### ⚔️ Live Session Engine
When a session starts, the app transforms into a real-time game companion.

| Feature | Description |
|---------|-------------|
| **Dice Roller** | Any dice (d4–d100), auto-applies modifiers, advantage/disadvantage, roll history |
| **Initiative Tracker** | Auto-roll initiative, visual turn order, "Your turn!" notifications |
| **Combat Manager** | HP tracking, damage/healing, death saves, temp HP, conditions |
| **Spell Tracker** | Slot usage per level, concentration indicator, auto-deduct on cast |
| **Shared View** | DM shares info to all or specific players, secret rolls, DM-only data |
| **Session Log** | Auto-generated recap: rolls, combat events, story beats. Exportable |
| **Rest System** | Short rest (hit dice, ability recharge) and long rest (full recovery) |

### 🤖 AI Dungeon Master
QuestForge's signature feature. The group decides how AI participates.

| Mode | Description | Best For |
|------|-------------|----------|
| 🤖 **Full DM** | AI runs everything: narration, NPCs, encounters, combat, story | Groups without a DM, spontaneous sessions, learning D&D |
| 🤝 **DM Assistant** | AI supports the human DM with rule lookups, encounter balancing, NPC generation | Experienced DMs who want to reduce prep time |
| 🗣️ **NPC Dialogue** | Players have natural-language conversations with AI-driven NPCs | Deep roleplay, investigation-heavy sessions |
| 🎲 **Encounter Generator** | AI creates balanced encounters based on party level and story context | DM prep, random encounters, one-shots |
| ⚖️ **Rule Enforcer** | AI validates actions against D&D 5e rules, flags errors, calculates outcomes | Learning groups, rules-heavy combat |

### 🏰 Guilds & Community
Connect beyond your friend group.

- Create guilds with custom rules, banners, and join policies (open / invite-only / application)
- Guild boards: announcements, LFP posts, campaign ads, discussions
- Shared campaigns where multiple parties play in the same world
- Location-based guild discovery (find D&D groups in your area)
- Guild events, tournaments, and one-shots with sign-up

---

## 📋 D&D 5e Rules Engine

QuestForge implements D&D 5e rules **strictly** using the System Reference Document (SRD).

| System | Implementation |
|--------|---------------|
| Ability Checks | d20 + modifier + proficiency, advantage/disadvantage, passive checks |
| Attack Rolls | d20 + mod + proficiency vs AC, critical hits, auto damage calculation |
| Saving Throws | d20 + mod + proficiency vs DC, auto-applied effects |
| Spellcasting | Attack rolls, save DCs, components, concentration, upcasting |
| Combat | Full action economy (action, bonus, reaction, movement), opportunity attacks, cover |
| Conditions | All 15 conditions with automated mechanical effects, duration tracking |
| Resting | Short rest (hit dice) and long rest (full recovery), exhaustion management |

> **Note:** SRD content is available under Creative Commons. Paid sourcebook content may be added via content packs in future updates.

---

## 🗺️ Development Roadmap

### Phase 1: Foundation `Auth + Character System`
- [ ] User registration / login (email + OAuth)
- [ ] User profiles with avatar and preferences
- [ ] Full D&D 5e character creation wizard
- [ ] Character sheet view and editing
- [ ] SRD data integration (races, classes, spells, items)
- [ ] Responsive web app foundation

### Phase 2: Social Layer `Lobby + Friends + Chat + Live Session`
- [ ] Friends system with online status
- [ ] Real-time chat (WebSocket)
- [ ] Lobby creation, invites, scheduling
- [ ] Push notifications
- [ ] Dice roller and initiative tracker
- [ ] Combat manager (HP, conditions, turns)
- [ ] Session logging and recaps

### Phase 3: Intelligence `AI Master + Guilds + Community`
- [ ] AI Full DM mode (narrative, combat, NPCs)
- [ ] AI DM Assistant mode
- [ ] AI NPC dialogue system
- [ ] Encounter generator
- [ ] Rule enforcement engine
- [ ] Guild system with boards and events
- [ ] Local guild discovery and community features

---

## 🏆 Competitive Landscape

| Feature | QuestForge | D&D Beyond | Roll20 | Foundry VTT |
|---------|-----------|------------|--------|-------------|
| **Focus** | Physical table companion | Digital reference | Virtual tabletop | Virtual tabletop |
| **AI DM** | ✅ Full + Assistant | ❌ | ❌ | ❌ |
| **Social Hub** | ✅ Friends + Guilds | ⚠️ Basic | ⚠️ LFG only | ❌ |
| **Offline Play** | ✅ Primary mode | ⚠️ Reference only | ❌ Online only | ❌ Online only |
| **NPC Dialogue** | ✅ AI-powered | ❌ | ❌ | ❌ |
| **Mobile App** | ✅ Web + Mobile | ✅ | ⚠️ Limited | ❌ Self-hosted |

**Key differentiator:** QuestForge is built for the table, not the screen. It's the only platform designed specifically to enhance in-person D&D with AI capabilities.

---

## 🛠️ Tech Stack

> **TBD** — Technology decisions are pending. Candidates under consideration:
> - **Backend:** NestJS / Laravel
> - **Frontend:** Vue 3
> - **Database:** PostgreSQL / MariaDB with Prisma ORM
> - **Real-time:** WebSocket (Socket.io / Pusher)
> - **AI:** LLM API (Claude / GPT / open-source) with D&D 5e fine-tuning
> - **Mobile:** PWA or native (React Native / Flutter)

---

## 🤔 Open Questions

- **Licensing:** SRD content is CC-licensed. Paid sourcebook integration requires WotC partnership or user-provided content
- **AI Model:** Evaluate LLM providers for DM capabilities — fine-tuning vs prompt engineering
- **Monetization:** Freemium (free basic, premium AI + content) vs subscription vs one-time purchase
- **Mobile Strategy:** PWA for quick cross-platform vs native apps for better UX
- **Offline Support:** Character viewing and dice rolling should work offline with sync on reconnect
- **Data Architecture:** Cloud-first with local cache vs local-first with cloud sync

---

## 📄 Documentation

You can see project's documentation in the [docs folder](./docs/README.md). It contains detailed design docs on the overall vision, visual identity, and technical architecture of **QuestForge**.

---

## 🤝 Contributing

This project is currently in the **concept phase**. Contributions, ideas, and feedback are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-idea`)
3. Commit your changes (`git commit -m 'Add amazing idea'`)
4. Push to the branch (`git push origin feature/amazing-idea`)
5. Open a Pull Request

---

## 📬 Contact

Have ideas or want to join the project? Open an issue or reach out!

---

<p align="center">
  <strong>⚔️ QuestForge</strong> — Your Table. Your Rules. Enhanced.
</p>
