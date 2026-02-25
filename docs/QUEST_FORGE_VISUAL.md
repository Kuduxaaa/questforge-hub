<p align="center">
  <img src="https://img.shields.io/badge/QuestForge-Visual%20Identity-c9a84c?style=for-the-badge" alt="Visual Identity"/>
  <img src="https://img.shields.io/badge/Version-1.0-2E4057?style=for-the-badge" alt="Version"/>
</p>

<h1 align="center">⚔️ QuestForge — Visual Identity & Design Language</h1>
<p align="center"><em>This is not a website. This is a game client.</em></p>

---

## The Golden Rule

> **QuestForge must never look like a web application, an admin panel, or a SaaS dashboard.**
> 
> It must look, feel, and behave like a **game client** — the kind of experience you get when you launch League of Legends, Dota 2, Valorant, or World of Warcraft. When a player opens QuestForge, they should feel like they just entered a fantasy world, not like they opened a browser tab.

Every design decision flows from this principle. If something looks like it belongs in a CRUD app, it doesn't belong in QuestForge.

---

## 1. Visual Philosophy

### 1.1 What We Are

QuestForge is a **game client for tabletop RPGs**. Think about what happens when you launch League of Legends:

- You see your champion, your rank, your friends
- The entire interface is themed, atmospheric, alive
- Background art shifts and breathes with ambient animations
- Music plays, particles float, the UI feels like part of a living world
- Navigation isn't tabs and sidebars — it's integrated into the experience
- Everything screams "you are about to play a game"

That is what QuestForge must be. Not a character sheet viewer with a chat sidebar. A **portal into your D&D life**.

### 1.2 What We Are NOT

| ❌ We are NOT | ✅ We ARE |
|---|---|
| A web application | A game client that runs in a browser |
| An admin panel with fantasy colors | An immersive fantasy experience |
| A CRUD interface for character stats | A living character that breathes on screen |
| A form-based session scheduler | A war room where parties assemble |
| A chatbox with dice buttons | A battlefield command center |
| D&D Beyond with a dark theme | Something that has never existed before |

### 1.3 The Feeling

When a player opens QuestForge, the emotional response should be:

- **"This is cool."** — Not "this is useful." Cool first, useful always.
- **"I want to show this to my friends."** — The UI itself is a selling point.
- **"I feel like I'm in the game."** — Immersion is not optional, it's the core.
- **"This was made by people who play D&D."** — It has soul, not just features.

---

## 2. Art Direction

### 2.1 Theme: Dark Fantasy Parchment

The visual language blends **medieval fantasy** with **modern game UI design**. Imagine a magical grimoire that somehow has a touchscreen.

**Primary Atmosphere:**
- Dark, rich backgrounds — deep blacks and warm browns, like a tavern at night
- Parchment and gold accents — aged paper textures, gilded borders, wax seals
- Warm candlelight glow — not flat UI lighting, but atmospheric light that feels organic
- Subtle fog, particle dust, and ambient movement in backgrounds
- Typography that feels hand-lettered but remains perfectly readable

**Not This:**
- Not "dark mode with brown" — that's just a color swap
- Not "medieval clipart" — no tacky goblet icons or Comic Sans in a scroll frame
- Not "realistic parchment texture overlaid on Bootstrap" — that's a costume, not an identity
- Not grimdark or horror — this is high fantasy, adventurous, warm, inviting

### 2.2 Visual References

**Study These:**
- **League of Legends Client** — Layout structure, social features, lobby system, how it handles champion select
- **Dota 2 Dashboard** — Atmospheric backgrounds, hero showcase, match history presentation
- **Valorant Agent Select** — Full-screen character presentation, dramatic transitions
- **Baldur's Gate 3 UI** — Fantasy aesthetic done right in a modern context, inventory and character sheet UX
- **World of Warcraft Character Screen** — How a character is presented with weight and importance
- **Hearthstone** — How a card game made every interaction feel tactile and magical
- **Divinity: Original Sin 2** — Inventory, character sheet, journal UX in a fantasy context

**What to take from each:**
- LoL/Valorant → Client architecture, social UX, lobby flow, matchmaking feel
- Dota 2 → Atmospheric depth, background art as storytelling, stat presentation
- BG3/DOS2 → Fantasy UI patterns that work, how game information is displayed
- Hearthstone → Tactile feel, sound design philosophy, how simple actions feel rewarding

### 2.3 Color System

```
┌─────────────────────────────────────────────────────────┐
│  QUESTFORGE COLOR PALETTE                                │
├──────────────────┬──────────────────────────────────────┤
│                  │                                      │
│  BACKGROUNDS     │  Primary:     #0D0B08  (void black)  │
│                  │  Secondary:   #1A1410  (dark leather) │
│                  │  Surface:     #241E17  (aged wood)    │
│                  │  Elevated:    #2E2519  (warm shadow)  │
│                  │                                      │
│  GOLD SYSTEM     │  Bright:      #E2C97E  (pure gold)   │
│  (Primary)       │  Standard:    #C9A84C  (aged gold)   │
│                  │  Muted:       #8A7235  (dim gold)    │
│                  │  Faint:       #5A4D3A  (gold shadow) │
│                  │                                      │
│  PARCHMENT       │  Light:       #E8DCC4  (fresh paper) │
│  (Text)          │  Standard:    #D4C5A0  (aged paper)  │
│                  │  Dim:         #B8A882  (old paper)   │
│                  │  Muted:       #9A8B6E  (faded ink)   │
│                  │                                      │
│  ACCENTS         │  Blood Red:   #8B2E2E  (combat)      │
│                  │  Arcane Blue:  #2E4A6B  (magic)      │
│                  │  Forest Green: #3A6B3A  (nature/heal) │
│                  │  Shadow Purple:#4A2E5A  (mystery)     │
│                  │  Fire Orange:  #B8652E  (warning)     │
│                  │                                      │
│  FUNCTIONAL      │  Success:     #5A9A5A  (heal/buff)   │
│                  │  Danger:      #B44040  (damage/alert) │
│                  │  Info:        #4A7AB0  (arcane/info)  │
│                  │  Warning:     #D4A040  (caution)      │
│                  │                                      │
└──────────────────┴──────────────────────────────────────┘
```

**Usage Rules:**
- Backgrounds are always dark — never white, never gray, never "light mode"
- Gold is the primary accent — used for important elements, active states, and highlights
- Parchment tones are for text — never use pure white (#FFFFFF) for text
- Accent colors map to game concepts — red for combat/damage, blue for magic/arcane, green for nature/healing
- Every color should feel like it exists in a fantasy world — no sterile UI blues or corporate greens

### 2.4 Typography

**Display / Headlines:**
- Primary: A serif font with character — something like **Cinzel**, **Cormorant Garamond**, or **Playfair Display**
- Used for: page titles, character names, session names, dramatic moments
- Must feel: hand-crafted, important, like carved stone or printed in a grimoire

**Body / Interface:**
- Primary: A clean but warm serif — **Crimson Text**, **Lora**, or **Source Serif Pro**
- Used for: descriptions, chat messages, lore text, session logs
- Must feel: readable at any size, warm, not sterile

**UI / Labels:**
- Primary: A refined sans-serif — **Jost**, **Outfit**, or **DM Sans**
- Used for: buttons, labels, navigation, stats, numbers
- Must feel: modern but not clinical, clear hierarchy with the serif fonts

**Monospace / Dice:**
- Primary: **JetBrains Mono** or **Fira Code**
- Used for: dice results, roll formulas, technical displays
- Must feel: precise, satisfying to read when dice are rolled

**Rules:**
- NEVER use Inter, Roboto, Arial, or system fonts — these scream "web app"
- Headings should feel like they were etched, not typed
- Numbers (stats, dice, HP) should be prominent and satisfying to read
- Font sizes should be generous — this is a game, not a spreadsheet

### 2.5 Iconography

**Do:**
- Custom icon set that matches the fantasy aesthetic
- Icons that feel hand-drawn or engraved, not flat Material Design
- Use emoji as placeholders only — replace with custom icons in production
- Consider using a fantasy icon set like **Game Icons (game-icons.net)** as a base

**Don't:**
- Material Design icons, Feather icons, or any "web app" icon set
- Flat, geometric icons that look like they belong in a settings panel
- Inconsistent styles — every icon should feel like it's from the same world

### 2.6 Textures & Effects

**Background Textures:**
- Subtle parchment grain across surfaces — not a flat image overlay, but a living texture
- Dark leather or stone patterns for deep background layers
- Vignette effect on edges to draw focus inward
- Noise overlay (very subtle, 2-4% opacity) for depth

**Border & Frame Treatments:**
- Borders should feel like carved frames, not CSS `border: 1px solid`
- Corner ornaments on important containers (character cards, session panels)
- Gold trim on primary interactive elements
- Beveled edges on buttons to give them physicality

**Glow & Light Effects:**
- Gold ambient glow on active/hovered elements
- Candlelight flicker effect on key focal points (very subtle, CSS animation)
- Magical glow around spell-related elements (blue/purple)
- Combat elements pulse with a warm red glow during active sessions

**Particle Systems:**
- Floating dust motes in the background (subtle, slow-moving)
- Ember particles near combat elements
- Magical sparkles around spell and arcane elements
- All particles should be CSS/Canvas-based for performance

---

## 3. Layout & Navigation Philosophy

### 3.1 Not a Website — A Game Client

The layout should mirror how game clients work, not how web apps work:

**Traditional Web App (what we DON'T want):**
```
┌─────────────────────────────────┐
│  Logo    Nav    Nav    Nav  🔔  │  ← Top navbar
├────────┬────────────────────────┤
│ Sidebar│  Content Area          │  ← Sidebar + content
│ Link 1 │  Card Card Card        │
│ Link 2 │  Card Card Card        │
│ Link 3 │  Table Table Table     │
│        │                        │
└────────┴────────────────────────┘
```

**Game Client (what we WANT):**
```
┌─────────────────────────────────────────┐
│                                         │
│    ╔═══╗   QUESTFORGE              🔔 👤│  ← Minimal top bar, integrated
│    ║ ⚔ ║   Level 7 Barbarian           │     into the background art
│    ╚═══╝                                │
│                                         │
│   ┌─────────┐  ┌────────────────────┐   │
│   │Character│  │ Upcoming Session   │   │  ← Floating panels on a rich
│   │ Panel   │  │ The Sunken Temple  │   │     atmospheric background
│   │         │  │ Tonight, 21:00     │   │
│   └─────────┘  └────────────────────┘   │
│                                         │
│   🏠  🧙  ⚔️  🎪  🏰  💬             │  ← Bottom nav bar (game-style)
└─────────────────────────────────────────┘
```

### 3.2 Navigation Model

**Primary Navigation: Bottom Bar (Mobile & Desktop)**
- Positioned at the bottom, like mobile game UIs
- 5-6 main sections with themed icons
- Active state has a gold glow, not just a color change
- Slight haptic feedback on mobile tap

```
┌──────────────────────────────────────────────┐
│   🏠        🧙        ⚔️        🎪       🏰  │
│  Home    Heroes    Battle    Lobby    Guild  │
│   ══                                         │
└──────────────────────────────────────────────┘
     ↑ Active indicator (gold line + glow)
```

**Secondary Navigation: Contextual**
- Within each section, use tabs or contextual menus
- No breadcrumbs — this isn't a content management system
- Transitions between sections are animated, not page loads

### 3.3 Screen Architecture

Every screen in QuestForge follows one of these templates:

**1. Showcase Screen** (Home, Character View)
- Full-bleed atmospheric background
- Content floats as panels over the background
- Hero element (character art, session banner) takes visual priority
- Information is layered: primary → secondary → tertiary depth

**2. Command Screen** (Lobby, Guild)
- Split layout with a primary action area and supporting information
- Clear visual hierarchy — what you need to do is obvious
- Interactive elements are large and satisfying to use

**3. Battle Screen** (Live Session)
- Maximum information density, but organized into clear zones
- Real-time updates with smooth animations
- Combat tracker dominates, with supporting panels for dice, chat, and character

**4. Social Screen** (Friends, Chat, Guild Members)
- List-based with rich presence information
- Easy one-tap actions (invite, message, view profile)
- Status indicators that feel alive (pulsing online dots, activity badges)

---

## 4. Component Design Language

### 4.1 Cards & Panels

Cards in QuestForge are not flat rectangles with `border-radius: 8px`. They are **parchment sheets**, **wooden plaques**, or **magical frames**.

**Character Card:**
```
╔══════════════════════════════════╗
║  ┌──────┐                        ║
║  │ CHAR │  Thorn Ironveil        ║
║  │ ART  │  Half-Orc Barbarian    ║
║  │      │  Level 7               ║
║  └──────┘                        ║
║  ═══════════════════════════════  ║
║  STR 18  DEX 14  CON 16         ║
║  INT 8   WIS 12  CHA 10         ║
║  ─────────────────────────────── ║
║  HP ████████████░░░  85/92       ║
╚══════════════════════════════════╝
  ↑ Ornate border, slight inner glow
```

**Properties:**
- Background: dark surface with subtle parchment texture
- Border: ornate frame (not plain CSS border), gold accents on hover
- Shadow: deep, warm shadow (not generic `box-shadow`)
- Corner ornaments on important cards
- Content padding is generous — nothing feels cramped

### 4.2 Buttons

**Primary Button (Gold):**
- Background: gold gradient with metallic sheen
- Border: slightly beveled, gold frame
- Text: dark, bold, uppercase with slight letter-spacing
- Hover: golden glow expands, slight scale-up (1.02)
- Active: pressed-in effect, glow intensifies
- Sound: subtle "click" (like placing a chess piece)

**Secondary Button (Parchment):**
- Background: transparent with parchment-colored border
- Hover: fills with warm parchment tone
- More understated than primary

**Danger Button (Blood):**
- Background: deep red gradient
- Used sparingly — end session, delete character
- Pulsing glow when hovered

**Icon Buttons:**
- Circular or rounded square
- Hover reveals a tooltip with gold accent
- Active state has a subtle ring animation

### 4.3 Dice Roller

The dice roller is one of the most-used components and must feel **incredible**.

**Design:**
- Dice are not flat icons — they should feel 3D, tactile
- Each die type has a distinct shape rendered in the UI (d4 pyramid, d20 icosahedron, etc.)
- Rolling animation is physics-based — the die tumbles, bounces, settles
- Natural 20 triggers a golden explosion effect with the word "CRITICAL!" in dramatic serif font
- Natural 1 triggers a dramatic red flash
- Roll sound effects are essential
- Roll history shows in a scroll-like panel

### 4.4 HP & Resource Bars

Not standard progress bars. These should feel **alive**:

**HP Bar:**
- Full: deep green with a subtle pulse
- Damaged: transitions through green → yellow → orange → red
- Low HP (<25%): bar flickers/pulses urgently
- Healing: brief green flash animation
- Damage: red flash + slight shake

**XP Bar:**
- Gold gradient that fills like liquid
- Level-up triggers a dramatic golden burst

**Spell Slots:**
- Not checkboxes — they are glowing arcane orbs
- Filled: blue/purple glow
- Used: dim, cracked appearance
- Recovering (during rest): gentle restoration animation

### 4.5 Chat & Session Feed

**Chat bubbles** should feel like parchment notes:
- Player messages: warm parchment background
- AI DM messages: darker, with a magical border glow and distinct styling
- System messages (dice rolls, combat): styled with relevant accent colors
- Dice roll results are formatted prominently with the die icon and result

### 4.6 Initiative Tracker

During combat, the initiative tracker is the **centerpiece**:
- Vertical or circular layout showing turn order
- Active combatant is dramatically highlighted (gold frame, larger, glowing)
- Enemies have red-tinted frames, allies have gold/green
- Smooth animations when initiative order changes
- "Your Turn" notification is a dramatic, full-screen flash that quickly recedes

---

## 5. Animation & Motion

### 5.1 Principles

- **Purposeful**: Every animation serves a function — feedback, transition, or atmosphere
- **Fantasy-appropriate**: Movements feel organic and magical, not mechanical
- **Performant**: All animations target `transform` and `opacity` for 60fps
- **Respectful**: Animations don't block interaction or waste time

### 5.2 Transition Catalog

| Transition | Style | Duration |
|---|---|---|
| Page change | Fade + subtle directional slide | 300ms |
| Card appear | Fade up from below, staggered | 400ms, 50ms stagger |
| Hover state | Gold glow expansion | 200ms ease |
| Button press | Scale down + glow | 150ms |
| Dice roll | Physics-based tumble | 500-800ms |
| Damage taken | Red flash + shake | 300ms |
| Critical hit | Golden explosion + screen flash | 600ms |
| Level up | Dramatic golden burst + confetti | 1200ms |
| Session start | Cinematic fade-in with ambient reveal | 1500ms |
| Notification | Slide in from right with fade | 400ms |
| Turn change | Spotlight shift in initiative tracker | 500ms |

### 5.3 Ambient Motion

The UI should never feel completely still:
- Background: very slow parallax or subtle movement (drifting clouds, flickering torchlight)
- Particle dust: random, slow-moving particles across the background (CSS or lightweight Canvas)
- Character idle: subtle breathing animation on character portraits
- Gold elements: very slow shimmer/pulse
- Online status dots: gentle pulse for online friends

### 5.4 Sound Design (Future Enhancement)

Sound is critical for game feel. Plan for:
- UI sounds: button clicks, page transitions, notification chimes
- Dice sounds: rolling, bouncing, landing (different for each die type)
- Combat sounds: attack hits, spell casts, damage taken
- Ambient: background tavern atmosphere, dungeon ambience during sessions
- Music: optional ambient soundtrack that changes based on context (lobby vs. combat vs. exploration)

---

## 6. Responsive & Mobile Design

### 6.1 Mobile-First Game Client

QuestForge must feel native on mobile. Not "responsive web" — native game app.

**Key principles:**
- Touch targets are large and satisfying (minimum 44x44px, preferably larger)
- Swipe gestures for navigation (swipe between sections)
- Pull-to-refresh with a themed animation (sword being drawn, dice being rolled)
- Bottom navigation is always accessible with thumb
- Haptic feedback on interactions (dice roll, button press, damage taken)
- Full-screen immersion — no browser UI visible in PWA/native mode

### 6.2 Mobile Layout Adaptations

**Home Screen (Mobile):**
```
┌──────────────────────┐
│  ⚔️ QuestForge  🔔 👤│
│                      │
│  ┌──────────────────┐│
│  │  SESSION TONIGHT │├── Banner notification
│  │  Sunken Temple   ││
│  │  21:00 • Join →  ││
│  └──────────────────┘│
│                      │
│  ┌──────────────────┐│
│  │  🪓 Thorn        ││
│  │  Lvl 7 Barbarian │├── Character showcase
│  │  HP █████░ 85/92 ││    (swipeable)
│  └──────────────────┘│
│                      │
│  Quick Actions       │
│  [🧙 New] [⚔ Lobby] │
│  [🎲 Roll] [🏰 Guild]│
│                      │
│ ═════════════════════│
│ 🏠  🧙  ⚔️  🎪  🏰  │ ← Bottom nav
└──────────────────────┘
```

**Live Session (Mobile):**
```
┌──────────────────────┐
│  ● LIVE  Round 1     │
│  The Sunken Temple   │
├──────────────────────┤
│                      │
│  [Initiative] [Chat] │ ← Swipeable tabs
│                      │
│  ⚔ Thorn ← YOUR TURN│
│  👹 Goblin Chief     │
│  🔮 Elara            │
│  👺 Goblin x2        │
│  🗡 Bran             │
│                      │
│  HP ████████░░ 72/92 │
│                      │
│  ┌──┬──┬──┬──┬──┬──┐ │
│  │d4│d6│d8│10│12│20│ │ ← Always-visible dice
│  └──┴──┴──┴──┴──┴──┘ │
│                      │
│  [⚔ Attack] [🛡 Defend] [📜 Spell]  │
│ ═════════════════════│
│ 🏠  🧙  ⚔️  🎪  🏰  │
└──────────────────────┘
```

### 6.3 Tablet Layout

Tablet gets the richest experience — enough screen space for atmospheric backgrounds with floating panels, similar to an iPad game. Use the extra space for:
- Side-by-side initiative tracker + session feed
- Full character sheet visible during live session
- Expanded dice roller with roll history

---

## 7. Key Screen Specifications

### 7.1 Home — "The Hearth"

The player's home base. What they see when they open QuestForge.

**Hero Element:** Active character showcase with atmospheric background art relevant to their current campaign. Character stands in a dramatic pose (future: animated idle).

**Primary Panels:**
- Upcoming session banner (if scheduled) — urgent, prominent, gold-bordered
- Active character quick-view with HP, key stats
- Quick action buttons (New Character, Create Lobby, Quick Roll, Browse Guilds)

**Secondary Panels:**
- Recent activity feed (scrollable)
- Friends list with online status
- Session history

**Atmosphere:**
- Background: dark tavern interior with warm candlelight, subtle particle dust
- Ambient sound: (future) tavern background noise — muffled conversations, crackling fire

### 7.2 Character — "The Grimoire"

Full character sheet that feels like a magical book, not a spreadsheet.

**Design:**
- The character sheet should feel like opening an ancient tome
- Pages/sections transition with a page-turn animation
- Ability scores are displayed as carved runes or medallions, not text fields
- The character portrait is prominent and framed ornately
- Stats are organized spatially, not in a data table

### 7.3 Lobby — "The War Room"

Where parties assemble before heading into adventure.

**Design:**
- Dark stone chamber aesthetic
- Player slots arranged in a circle or around a table (like a virtual round table)
- Empty slots glow dimly, inviting players to join
- DM slot is elevated/special (throne-like)
- When all players are ready, a dramatic "Begin Adventure" button appears
- Countdown timer to scheduled session with theatrical presentation

### 7.4 Live Session — "The Battlefield"

Maximum information density meets maximum immersion.

**Design:**
- Background adapts to the scene (dungeon, forest, tavern) based on AI DM context
- Initiative tracker is the vertical spine of the layout
- Dice roller is always accessible (bottom sheet on mobile, side panel on desktop)
- AI DM messages appear with distinct magical styling — slightly glowing text, different background
- Combat animations for attacks, spells, damage
- "Your Turn" notification is cinematic — brief spotlight effect

### 7.5 Guild — "The Hall"

Community hub for finding players and organizing.

**Design:**
- Grand hall aesthetic — banners, long tables, gathering spaces
- Guild banner/crest prominently displayed
- Member list with presence indicators
- Event board styled as a physical notice board with pinned notices
- LFG posts styled as quest postings on a board

---

## 8. Design Anti-Patterns

Things that must NEVER appear in QuestForge:

| ❌ Anti-Pattern | Why It Kills the Vibe |
|---|---|
| White backgrounds | Destroys fantasy atmosphere instantly |
| Gray UI chrome | Looks like Chrome DevTools, not a game |
| Standard form inputs | HTML defaults feel like a government form |
| Data tables | This is a game, not Excel |
| Breadcrumb navigation | Screams "enterprise software" |
| Toast notifications (generic) | Boring. Use themed, animated alerts |
| Hamburger menu | Lazy. Design proper navigation |
| Loading spinners (generic) | Use themed loading (rotating dice, opening scroll) |
| Pagination controls | Infinite scroll or "load more" with animation |
| Standard dropdown selects | Custom-styled selectors that match the world |
| Blue hyperlinks | No web aesthetics in a game client |
| "Dashboard" terminology | Call it "The Hearth", "Home", or "Camp" |

---

## 9. Implementation Notes

### 9.1 Technology Approach

- All UI built with **Vue 3 + TypeScript** with component-based architecture
- Styling via **scoped CSS** with CSS variables for the design token system
- Animations primarily CSS with **GSAP** for complex sequences (dice physics, cinematic transitions)
- Particle effects via lightweight **Canvas** or CSS-only where possible
- Sound via **Howler.js** or **Tone.js** for audio management
- Mobile-first CSS with desktop enhancements, not the reverse

### 9.2 Performance Targets

- First Contentful Paint: < 1.5s
- Time to Interactive: < 3s
- Animation frame rate: 60fps minimum
- Background effects must not impact battery life significantly on mobile
- All particles and ambient effects respect `prefers-reduced-motion`

### 9.3 Asset Pipeline

- Character portraits: AI-generated during character creation (future feature)
- Background art: curated set of atmospheric scenes for different contexts
- Icons: custom SVG icon set in the QuestForge style
- Textures: lightweight CSS patterns + SVG filters for parchment/leather effects
- Sound effects: curated library of fantasy UI sounds

---

## 10. Summary

QuestForge's visual identity is its competitive advantage. Any developer can build a character sheet app. Any team can connect a chat to a database. But creating an experience that makes players **feel like they've entered a fantasy world** — that's what makes QuestForge special.

Every pixel, every animation, every transition, every sound should answer one question:

> **"Does this feel like a game, or does this feel like a website?"**

If the answer is "website," redesign it.

---

<p align="center">
  <strong>⚔️ QuestForge</strong> — Not a website. A game client. A portal to adventure.
</p>
