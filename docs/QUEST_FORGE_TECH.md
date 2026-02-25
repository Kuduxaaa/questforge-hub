<p align="center">
  <img src="https://img.shields.io/badge/Backend-FastAPI%20%2B%20Socket.IO-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/Frontend-Vue%203%20%2B%20TypeScript-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white" alt="Vue 3"/>
  <img src="https://img.shields.io/badge/Database-MariaDB%20%2B%20SQLAlchemy-003545?style=for-the-badge&logo=mariadb&logoColor=white" alt="MariaDB"/>
  <img src="https://img.shields.io/badge/Cache-Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis"/>
</p>

<h1 align="center">⚔️ QuestForge — Technical Documentation</h1>
<p align="center"><em>Complete technical specification for developers</em></p>

---

## Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Tech Stack Details](#2-tech-stack-details)
3. [Project Structure](#3-project-structure)
4. [Database Schema](#4-database-schema)
5. [API Architecture](#5-api-architecture)
6. [WebSocket Events](#6-websocket-events)
7. [Authentication & Authorization](#7-authentication--authorization)
8. [AI Integration](#8-ai-integration)
9. [D&D 5e Rules Engine](#9-dd-5e-rules-engine)
10. [Development Roadmap](#10-development-roadmap)
11. [Infrastructure & Deployment](#11-infrastructure--deployment)
12. [Testing Strategy](#12-testing-strategy)

---

## 1. Architecture Overview

### 1.1 High-Level Architecture

```
┌────────────────────────────────────────────────────────────┐
│                        CLIENTS                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │  Web (Vue 3) │  │  iOS (PWA/   │  │  Android     │     │
│  │  SPA + TS    │  │  Capacitor)  │  │  (PWA/Cap.)  │     │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘     │
│         │                 │                  │              │
│         └─────────────────┼──────────────────┘              │
│                           │                                 │
│                    HTTPS / WSS                              │
│                           │                                 │
├───────────────────────────┼─────────────────────────────────┤
│                      API GATEWAY                            │
│                     (Nginx/Caddy)                           │
│                           │                                 │
├──────────┬────────────────┼────────────────┬────────────────┤
│          │                │                │                │
│  ┌───────▼───────┐ ┌─────▼──────┐ ┌───────▼──────┐       │
│  │   FastAPI     │ │ Socket.IO  │ │  Celery      │       │
│  │   REST API    │ │ Server     │ │  Workers     │       │
│  │   (HTTP)      │ │ (WSS)      │ │  (Async)     │       │
│  └───────┬───────┘ └─────┬──────┘ └───────┬──────┘       │
│          │               │                 │               │
│          └───────────────┼─────────────────┘               │
│                          │                                  │
│              ┌───────────┼───────────┐                     │
│              │           │           │                     │
│       ┌──────▼───┐ ┌────▼────┐ ┌────▼──────┐            │
│       │ MariaDB  │ │  Redis  │ │ AI Service │            │
│       │ (Primary)│ │ (Cache/ │ │ (Claude    │            │
│       │          │ │  Pub/   │ │  API)      │            │
│       │          │ │  Sub)   │ │            │            │
│       └──────────┘ └─────────┘ └────────────┘            │
│                                                           │
│                    INFRASTRUCTURE                          │
└───────────────────────────────────────────────────────────┘
```

### 1.2 Request Flow

```
Client Action → Nginx → FastAPI/Socket.IO → Service Layer → Repository → MariaDB
                                                   │
                                                   ├── Redis (cache/sessions/pubsub)
                                                   └── Claude API (AI features)
```

### 1.3 Key Architectural Decisions

| Decision | Choice | Reasoning |
|---|---|---|
| API Framework | FastAPI | Async-first, auto-docs, type validation with Pydantic, excellent performance |
| Real-time | Socket.IO (python-socketio) | Room-based communication perfect for lobbies/sessions, fallback transport |
| ORM | SQLAlchemy 2.0 (async) | Mature, flexible, excellent MariaDB support, async session support |
| Cache/PubSub | Redis | Session state caching, Socket.IO adapter for multi-process, pub/sub for events |
| Task Queue | Celery + Redis | Background tasks: notifications, AI processing, session recaps |
| Frontend | Vue 3 + TypeScript + Vite | Reactive, composable, excellent TS support, fast HMR |
| Mobile | PWA + Capacitor | Single codebase, native-like mobile with push notifications |
| AI | Anthropic Claude API | Superior narrative generation, function calling for rules engine |

---

## 2. Tech Stack Details

### 2.1 Backend

```
Python 3.12+
├── FastAPI 0.110+              # REST API framework
├── python-socketio 5.x         # WebSocket server (Socket.IO protocol)
├── SQLAlchemy 2.0 (async)      # ORM with async support
├── Alembic                     # Database migrations
├── Pydantic 2.x                # Data validation & serialization
├── Celery 5.x                  # Distributed task queue
├── Redis (via redis-py)        # Caching, pub/sub, session store
├── Passlib + python-jose       # Password hashing + JWT
├── httpx                       # Async HTTP client (for AI API calls)
├── uvicorn                     # ASGI server
└── pytest + pytest-asyncio     # Testing
```

### 2.2 Frontend

```
Node 20+ / Vue 3 + TypeScript
├── Vue 3.4+ (Composition API)  # UI framework
├── Vue Router 4                # Client-side routing
├── Pinia                       # State management
├── TypeScript 5.x              # Type safety
├── Vite 5                      # Build tool & dev server
├── socket.io-client            # WebSocket client
├── GSAP                        # Advanced animations
├── Howler.js                   # Audio management
├── VueUse                      # Composition utilities
├── Capacitor                   # Native mobile wrapper
└── Vitest + Vue Test Utils     # Testing
```

### 2.3 Infrastructure

```
├── MariaDB 11.x                # Primary database
├── Redis 7.x                   # Cache, pub/sub, task broker
├── Nginx / Caddy               # Reverse proxy, SSL, static files
├── Docker + Docker Compose     # Containerization
├── GitHub Actions              # CI/CD pipeline
└── Linux (Ubuntu 24.04)        # Server OS
```

---

## 3. Project Structure

### 3.1 Backend (`/server`)

```
server/
├── alembic/                    # Database migrations
│   ├── versions/
│   └── env.py
├── app/
│   ├── __init__.py
│   ├── main.py                 # FastAPI + Socket.IO app factory
│   ├── config.py               # Settings (env-based)
│   ├── database.py             # SQLAlchemy engine, session factory
│   │
│   ├── models/                 # SQLAlchemy models
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── character.py
│   │   ├── campaign.py
│   │   ├── session.py
│   │   ├── lobby.py
│   │   ├── guild.py
│   │   ├── chat.py
│   │   └── friendship.py
│   │
│   ├── schemas/                # Pydantic schemas (request/response)
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── character.py
│   │   ├── session.py
│   │   ├── lobby.py
│   │   └── guild.py
│   │
│   ├── api/                    # REST API routes
│   │   ├── __init__.py
│   │   ├── deps.py             # Shared dependencies (auth, db session)
│   │   ├── auth.py             # POST /auth/register, /auth/login, /auth/refresh
│   │   ├── users.py            # GET/PATCH /users/{id}
│   │   ├── characters.py       # CRUD /characters
│   │   ├── lobbies.py          # CRUD /lobbies
│   │   ├── sessions.py         # /sessions (game sessions)
│   │   ├── guilds.py           # CRUD /guilds
│   │   ├── friends.py          # /friends
│   │   └── chat.py             # /chat/history
│   │
│   ├── sockets/                # Socket.IO event handlers
│   │   ├── __init__.py
│   │   ├── manager.py          # Socket.IO server setup
│   │   ├── lobby_events.py     # Lobby room events
│   │   ├── session_events.py   # Live session events (dice, combat, turns)
│   │   ├── chat_events.py      # Real-time chat
│   │   └── presence_events.py  # Online status
│   │
│   ├── services/               # Business logic
│   │   ├── __init__.py
│   │   ├── auth_service.py
│   │   ├── character_service.py
│   │   ├── combat_service.py   # D&D 5e combat engine
│   │   ├── dice_service.py     # Dice rolling with modifiers
│   │   ├── spell_service.py    # Spell management & validation
│   │   ├── lobby_service.py
│   │   ├── session_service.py
│   │   ├── ai_service.py       # AI DM integration
│   │   ├── notification_service.py
│   │   └── guild_service.py
│   │
│   ├── engine/                 # D&D 5e rules engine
│   │   ├── __init__.py
│   │   ├── abilities.py        # Ability score calculations
│   │   ├── skills.py           # Skill checks, proficiency
│   │   ├── combat.py           # Attack rolls, damage, AC
│   │   ├── spells.py           # Spell slot management, casting rules
│   │   ├── conditions.py       # Status conditions & effects
│   │   ├── initiative.py       # Initiative order management
│   │   ├── rest.py             # Short/long rest recovery
│   │   ├── leveling.py         # XP, level-up logic
│   │   └── srd/                # SRD data files
│   │       ├── races.json
│   │       ├── classes.json
│   │       ├── spells.json
│   │       ├── items.json
│   │       ├── monsters.json
│   │       └── backgrounds.json
│   │
│   ├── tasks/                  # Celery background tasks
│   │   ├── __init__.py
│   │   ├── notifications.py    # Push notification delivery
│   │   ├── ai_tasks.py         # AI response generation
│   │   └── recaps.py           # Session recap generation
│   │
│   └── utils/
│       ├── __init__.py
│       ├── security.py         # JWT, password hashing
│       ├── redis_client.py     # Redis connection
│       └── exceptions.py       # Custom exception classes
│
├── tests/
│   ├── conftest.py
│   ├── test_auth.py
│   ├── test_characters.py
│   ├── test_combat.py
│   ├── test_dice.py
│   └── test_sessions.py
│
├── alembic.ini
├── requirements.txt
├── Dockerfile
└── pyproject.toml
```

### 3.2 Frontend (`/client`)

```
client/
├── public/
│   ├── icons/                  # PWA icons
│   └── sounds/                 # UI sound effects
├── src/
│   ├── main.ts                 # App entry point
│   ├── App.vue                 # Root component
│   ├── router/
│   │   └── index.ts            # Vue Router configuration
│   │
│   ├── stores/                 # Pinia stores
│   │   ├── auth.ts             # Authentication state
│   │   ├── character.ts        # Character data & mutations
│   │   ├── lobby.ts            # Lobby state
│   │   ├── session.ts          # Live session state
│   │   ├── social.ts           # Friends, chat, presence
│   │   └── ui.ts               # UI state (theme, notifications)
│   │
│   ├── composables/            # Vue composables
│   │   ├── useSocket.ts        # Socket.IO connection
│   │   ├── useDice.ts          # Dice rolling logic + animations
│   │   ├── useAudio.ts         # Sound effect management
│   │   ├── useNotifications.ts # Push notification handling
│   │   └── useCharacter.ts     # Character helpers
│   │
│   ├── services/               # API client layer
│   │   ├── api.ts              # Axios/fetch instance with auth
│   │   ├── auth.api.ts
│   │   ├── character.api.ts
│   │   ├── lobby.api.ts
│   │   ├── session.api.ts
│   │   └── guild.api.ts
│   │
│   ├── views/                  # Page-level components
│   │   ├── HomeView.vue        # "The Hearth" — dashboard
│   │   ├── CharacterView.vue   # "The Grimoire" — character sheet
│   │   ├── CharacterCreateView.vue  # Character creation wizard
│   │   ├── LobbyView.vue      # "The War Room" — lobby
│   │   ├── SessionView.vue     # "The Battlefield" — live session
│   │   ├── GuildView.vue       # "The Hall" — guild page
│   │   ├── FriendsView.vue     # Friends & social
│   │   ├── LoginView.vue       # Authentication
│   │   └── RegisterView.vue    # Registration
│   │
│   ├── components/
│   │   ├── common/             # Shared components
│   │   │   ├── QfButton.vue
│   │   │   ├── QfCard.vue
│   │   │   ├── QfModal.vue
│   │   │   ├── QfInput.vue
│   │   │   ├── QfToast.vue
│   │   │   ├── QfHpBar.vue
│   │   │   ├── QfLoadingDice.vue  # Themed loading spinner
│   │   │   └── QfParticles.vue    # Background particle effect
│   │   │
│   │   ├── character/
│   │   │   ├── AbilityScores.vue
│   │   │   ├── SkillList.vue
│   │   │   ├── SpellBook.vue
│   │   │   ├── Inventory.vue
│   │   │   ├── CharacterCard.vue
│   │   │   └── CreationWizard/
│   │   │       ├── StepRace.vue
│   │   │       ├── StepClass.vue
│   │   │       ├── StepAbilities.vue
│   │   │       ├── StepBackground.vue
│   │   │       └── StepEquipment.vue
│   │   │
│   │   ├── session/
│   │   │   ├── DiceRoller.vue
│   │   │   ├── InitiativeTracker.vue
│   │   │   ├── CombatManager.vue
│   │   │   ├── SessionFeed.vue
│   │   │   ├── TurnNotification.vue
│   │   │   └── AiDmPanel.vue
│   │   │
│   │   ├── social/
│   │   │   ├── FriendsList.vue
│   │   │   ├── ChatPanel.vue
│   │   │   ├── LobbyCard.vue
│   │   │   └── OnlineStatus.vue
│   │   │
│   │   └── layout/
│   │       ├── AppShell.vue    # Main layout wrapper
│   │       ├── BottomNav.vue   # Game-style bottom navigation
│   │       ├── TopBar.vue      # Minimal top bar
│   │       └── Background.vue  # Atmospheric background
│   │
│   ├── assets/
│   │   ├── styles/
│   │   │   ├── variables.css   # Design tokens (colors, fonts, spacing)
│   │   │   ├── base.css        # Reset + global styles
│   │   │   ├── typography.css  # Font declarations + scale
│   │   │   ├── animations.css  # Global animation keyframes
│   │   │   └── transitions.css # Vue transition classes
│   │   ├── fonts/
│   │   ├── images/
│   │   │   ├── backgrounds/    # Atmospheric scene backgrounds
│   │   │   └── textures/       # Parchment, leather, stone SVGs
│   │   └── icons/              # Custom fantasy icon SVGs
│   │
│   └── types/                  # TypeScript type definitions
│       ├── character.ts
│       ├── session.ts
│       ├── socket-events.ts    # Socket.IO event type map
│       └── api.ts              # API response types
│
├── capacitor.config.ts         # Mobile native config
├── index.html
├── vite.config.ts
├── tsconfig.json
├── package.json
└── Dockerfile
```

---

## 4. Database Schema

### 4.1 Entity Relationship Overview

```
Users ──< Characters
Users ──< Friendships >── Users
Users ──< GuildMembers >── Guilds
Users ──< LobbyPlayers >── Lobbies
Lobbies ──< GameSessions
GameSessions ──< SessionLogs
GameSessions ──< SessionParticipants >── Characters
Characters ──< CharacterSpells >── SrdSpells
Characters ──< InventoryItems >── SrdItems
Guilds ──< GuildEvents
Guilds ──< GuildPosts
Users ──< ChatMessages >── ChatRooms
```

### 4.2 Full Schema (SQLAlchemy Models)

#### Users

```python
class User(Base):
    __tablename__ = "users"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    email           = Column(String(255), unique=True, nullable=False, index=True)
    username        = Column(String(50), unique=True, nullable=False, index=True)
    password_hash   = Column(String(255), nullable=False)
    display_name    = Column(String(100), nullable=False)
    avatar_url      = Column(String(500), nullable=True)
    bio             = Column(Text, nullable=True)
    timezone        = Column(String(50), default="UTC")
    location        = Column(String(200), nullable=True)
    play_preference = Column(Enum("player", "dm", "both"), default="both")
    is_active       = Column(Boolean, default=True)
    is_verified     = Column(Boolean, default=False)
    last_online_at  = Column(DateTime, nullable=True)
    created_at      = Column(DateTime, default=func.now())
    updated_at      = Column(DateTime, default=func.now(), onupdate=func.now())

    # OAuth
    oauth_provider  = Column(String(20), nullable=True)  # "google", "discord"
    oauth_id        = Column(String(255), nullable=True)

    # Stats
    sessions_played = Column(Integer, default=0)
    total_rolls     = Column(Integer, default=0)

    # Relationships
    characters      = relationship("Character", back_populates="owner")
    guild_memberships = relationship("GuildMember", back_populates="user")
```

#### Characters

```python
class Character(Base):
    __tablename__ = "characters"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    owner_id        = Column(BigInteger, ForeignKey("users.id"), nullable=False, index=True)
    name            = Column(String(100), nullable=False)
    race            = Column(String(50), nullable=False)      # "half-orc", "high-elf", etc.
    class_name      = Column(String(50), nullable=False)      # "barbarian", "wizard", etc.
    subclass        = Column(String(50), nullable=True)
    level           = Column(Integer, default=1)
    experience_points = Column(Integer, default=0)
    background      = Column(String(50), nullable=True)
    alignment       = Column(String(30), nullable=True)
    portrait_url    = Column(String(500), nullable=True)

    # Ability Scores
    strength        = Column(Integer, nullable=False)
    dexterity       = Column(Integer, nullable=False)
    constitution    = Column(Integer, nullable=False)
    intelligence    = Column(Integer, nullable=False)
    wisdom          = Column(Integer, nullable=False)
    charisma        = Column(Integer, nullable=False)

    # Combat Stats
    max_hit_points  = Column(Integer, nullable=False)
    current_hit_points = Column(Integer, nullable=False)
    temp_hit_points = Column(Integer, default=0)
    armor_class     = Column(Integer, nullable=False)
    speed           = Column(Integer, default=30)
    initiative_bonus = Column(Integer, default=0)

    # Hit Dice
    hit_dice_total  = Column(Integer, default=1)
    hit_dice_remaining = Column(Integer, default=1)
    hit_die_type    = Column(Integer, default=8)  # d6, d8, d10, d12

    # Proficiencies (stored as JSON arrays)
    skill_proficiencies = Column(JSON, default=list)   # ["athletics", "intimidation"]
    skill_expertise     = Column(JSON, default=list)   # ["stealth"]
    saving_throw_profs  = Column(JSON, default=list)   # ["strength", "constitution"]
    tool_proficiencies  = Column(JSON, default=list)
    language_profs      = Column(JSON, default=list)
    armor_profs         = Column(JSON, default=list)
    weapon_profs        = Column(JSON, default=list)

    # Spellcasting (nullable for non-casters)
    spellcasting_ability = Column(String(20), nullable=True)  # "intelligence", "wisdom", etc.
    spell_slots     = Column(JSON, nullable=True)  # {"1": {"total": 4, "used": 1}, "2": {...}}

    # Features & Traits (JSON)
    features        = Column(JSON, default=list)   # [{"name": "Rage", "uses": 3, "used": 1, ...}]
    traits          = Column(JSON, default=list)    # Racial traits
    proficiency_bonus = Column(Integer, default=2)

    # Currency
    copper          = Column(Integer, default=0)
    silver          = Column(Integer, default=0)
    gold            = Column(Integer, default=10)
    platinum        = Column(Integer, default=0)

    # Conditions (active conditions during session)
    active_conditions = Column(JSON, default=list)  # ["poisoned", "frightened"]

    # Death Saves
    death_save_successes = Column(Integer, default=0)
    death_save_failures  = Column(Integer, default=0)

    # Notes
    personality_traits = Column(Text, nullable=True)
    ideals          = Column(Text, nullable=True)
    bonds           = Column(Text, nullable=True)
    flaws           = Column(Text, nullable=True)
    backstory       = Column(Text, nullable=True)
    notes           = Column(Text, nullable=True)

    # Meta
    is_active       = Column(Boolean, default=True)  # False = archived
    created_at      = Column(DateTime, default=func.now())
    updated_at      = Column(DateTime, default=func.now(), onupdate=func.now())

    # Relationships
    owner           = relationship("User", back_populates="characters")
    inventory       = relationship("InventoryItem", back_populates="character")
    known_spells    = relationship("CharacterSpell", back_populates="character")
```

#### Character Spells & Inventory

```python
class CharacterSpell(Base):
    __tablename__ = "character_spells"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    character_id    = Column(BigInteger, ForeignKey("characters.id"), nullable=False, index=True)
    spell_slug      = Column(String(100), nullable=False)  # References SRD spell data
    is_prepared     = Column(Boolean, default=False)
    is_always_prepared = Column(Boolean, default=False)    # Class/subclass grants
    source          = Column(String(50), default="class")  # "class", "race", "feat"

    character       = relationship("Character", back_populates="known_spells")


class InventoryItem(Base):
    __tablename__ = "inventory_items"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    character_id    = Column(BigInteger, ForeignKey("characters.id"), nullable=False, index=True)
    item_slug       = Column(String(100), nullable=True)   # References SRD item (null for custom)
    custom_name     = Column(String(200), nullable=True)   # For non-SRD items
    quantity        = Column(Integer, default=1)
    weight          = Column(Float, default=0)
    is_equipped     = Column(Boolean, default=False)
    is_attuned      = Column(Boolean, default=False)
    notes           = Column(Text, nullable=True)

    character       = relationship("Character", back_populates="inventory")
```

#### Friendships

```python
class Friendship(Base):
    __tablename__ = "friendships"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    requester_id    = Column(BigInteger, ForeignKey("users.id"), nullable=False, index=True)
    addressee_id    = Column(BigInteger, ForeignKey("users.id"), nullable=False, index=True)
    status          = Column(Enum("pending", "accepted", "blocked"), default="pending")
    created_at      = Column(DateTime, default=func.now())
    updated_at      = Column(DateTime, default=func.now(), onupdate=func.now())

    __table_args__ = (UniqueConstraint("requester_id", "addressee_id"),)
```

#### Lobbies & Game Sessions

```python
class Lobby(Base):
    __tablename__ = "lobbies"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    creator_id      = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    name            = Column(String(200), nullable=False)
    description     = Column(Text, nullable=True)
    scheduled_at    = Column(DateTime, nullable=True)
    location        = Column(String(300), nullable=True)
    max_players     = Column(Integer, default=6)
    dm_mode         = Column(Enum("human", "ai", "ai_assist"), default="human")
    dm_user_id      = Column(BigInteger, ForeignKey("users.id"), nullable=True)  # Human DM
    campaign_id     = Column(BigInteger, ForeignKey("campaigns.id"), nullable=True)
    status          = Column(Enum("open", "full", "in_session", "closed"), default="open")
    invite_code     = Column(String(20), unique=True, nullable=True)
    is_recurring    = Column(Boolean, default=False)
    recurrence_rule = Column(String(100), nullable=True)  # iCal RRULE format
    created_at      = Column(DateTime, default=func.now())

    players         = relationship("LobbyPlayer", back_populates="lobby")
    sessions        = relationship("GameSession", back_populates="lobby")


class LobbyPlayer(Base):
    __tablename__ = "lobby_players"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    lobby_id        = Column(BigInteger, ForeignKey("lobbies.id"), nullable=False, index=True)
    user_id         = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    character_id    = Column(BigInteger, ForeignKey("characters.id"), nullable=True)
    role            = Column(Enum("player", "dm", "spectator"), default="player")
    is_ready        = Column(Boolean, default=False)
    joined_at       = Column(DateTime, default=func.now())

    lobby           = relationship("Lobby", back_populates="players")

    __table_args__ = (UniqueConstraint("lobby_id", "user_id"),)


class GameSession(Base):
    __tablename__ = "game_sessions"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    lobby_id        = Column(BigInteger, ForeignKey("lobbies.id"), nullable=False)
    campaign_id     = Column(BigInteger, ForeignKey("campaigns.id"), nullable=True)
    dm_mode         = Column(Enum("human", "ai", "ai_assist"), nullable=False)
    status          = Column(Enum("active", "paused", "completed"), default="active")
    started_at      = Column(DateTime, default=func.now())
    ended_at        = Column(DateTime, nullable=True)

    # Session state (stored in Redis during active session, persisted on end)
    current_round   = Column(Integer, default=0)
    is_in_combat    = Column(Boolean, default=False)
    initiative_order = Column(JSON, nullable=True)

    # AI context
    ai_context      = Column(JSON, nullable=True)  # Scene state, NPC states, story progress
    ai_scenario     = Column(String(100), nullable=True)  # Scenario template used

    # Recap
    recap_text      = Column(Text, nullable=True)
    xp_awarded      = Column(Integer, default=0)

    lobby           = relationship("Lobby", back_populates="sessions")
    participants    = relationship("SessionParticipant", back_populates="session")
    logs            = relationship("SessionLog", back_populates="session")


class SessionParticipant(Base):
    __tablename__ = "session_participants"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    session_id      = Column(BigInteger, ForeignKey("game_sessions.id"), nullable=False, index=True)
    user_id         = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    character_id    = Column(BigInteger, ForeignKey("characters.id"), nullable=True)
    role            = Column(Enum("player", "dm"), default="player")

    # Snapshot of character stats at session start (for history)
    character_snapshot = Column(JSON, nullable=True)


class SessionLog(Base):
    __tablename__ = "session_logs"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    session_id      = Column(BigInteger, ForeignKey("game_sessions.id"), nullable=False, index=True)
    timestamp       = Column(DateTime, default=func.now())
    event_type      = Column(Enum(
        "narrative", "dice_roll", "attack", "damage", "heal",
        "spell_cast", "condition_applied", "condition_removed",
        "initiative_roll", "turn_start", "turn_end", "combat_start",
        "combat_end", "rest", "level_up", "loot", "player_action",
        "dm_action", "npc_dialogue", "system"
    ), nullable=False)
    actor_user_id   = Column(BigInteger, ForeignKey("users.id"), nullable=True)
    actor_name      = Column(String(100), nullable=True)  # Character or NPC name
    data            = Column(JSON, nullable=False)  # Event-specific data
    is_public       = Column(Boolean, default=True)  # False = DM-only

    session         = relationship("GameSession", back_populates="logs")
```

#### Campaigns

```python
class Campaign(Base):
    __tablename__ = "campaigns"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    creator_id      = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    name            = Column(String(200), nullable=False)
    description     = Column(Text, nullable=True)
    world_state     = Column(JSON, nullable=True)  # Persistent world state for AI
    session_count   = Column(Integer, default=0)
    is_active       = Column(Boolean, default=True)
    created_at      = Column(DateTime, default=func.now())
```

#### Guilds

```python
class Guild(Base):
    __tablename__ = "guilds"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    creator_id      = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    name            = Column(String(100), nullable=False)
    description     = Column(Text, nullable=True)
    banner_url      = Column(String(500), nullable=True)
    location        = Column(String(200), nullable=True)
    latitude        = Column(Float, nullable=True)
    longitude       = Column(Float, nullable=True)
    join_policy     = Column(Enum("open", "invite", "application"), default="open")
    member_count    = Column(Integer, default=0)
    is_active       = Column(Boolean, default=True)
    created_at      = Column(DateTime, default=func.now())

    members         = relationship("GuildMember", back_populates="guild")
    posts           = relationship("GuildPost", back_populates="guild")
    events          = relationship("GuildEvent", back_populates="guild")


class GuildMember(Base):
    __tablename__ = "guild_members"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    guild_id        = Column(BigInteger, ForeignKey("guilds.id"), nullable=False, index=True)
    user_id         = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    role            = Column(Enum("owner", "officer", "member"), default="member")
    joined_at       = Column(DateTime, default=func.now())

    guild           = relationship("Guild", back_populates="members")
    user            = relationship("User", back_populates="guild_memberships")

    __table_args__ = (UniqueConstraint("guild_id", "user_id"),)


class GuildPost(Base):
    __tablename__ = "guild_posts"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    guild_id        = Column(BigInteger, ForeignKey("guilds.id"), nullable=False, index=True)
    author_id       = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    post_type       = Column(Enum("announcement", "lfp", "discussion"), default="discussion")
    title           = Column(String(200), nullable=False)
    content         = Column(Text, nullable=False)
    is_pinned       = Column(Boolean, default=False)
    created_at      = Column(DateTime, default=func.now())

    guild           = relationship("Guild", back_populates="posts")


class GuildEvent(Base):
    __tablename__ = "guild_events"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    guild_id        = Column(BigInteger, ForeignKey("guilds.id"), nullable=False, index=True)
    creator_id      = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    name            = Column(String(200), nullable=False)
    description     = Column(Text, nullable=True)
    scheduled_at    = Column(DateTime, nullable=False)
    location        = Column(String(300), nullable=True)
    max_attendees   = Column(Integer, nullable=True)
    created_at      = Column(DateTime, default=func.now())

    guild           = relationship("Guild", back_populates="events")
```

#### Chat

```python
class ChatRoom(Base):
    __tablename__ = "chat_rooms"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    uuid            = Column(String(36), unique=True, nullable=False, default=uuid4)
    room_type       = Column(Enum("direct", "group", "lobby", "guild"), nullable=False)
    name            = Column(String(100), nullable=True)  # For group/guild chats
    lobby_id        = Column(BigInteger, ForeignKey("lobbies.id"), nullable=True)
    guild_id        = Column(BigInteger, ForeignKey("guilds.id"), nullable=True)
    created_at      = Column(DateTime, default=func.now())

    members         = relationship("ChatRoomMember", back_populates="room")
    messages        = relationship("ChatMessage", back_populates="room")


class ChatRoomMember(Base):
    __tablename__ = "chat_room_members"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    room_id         = Column(BigInteger, ForeignKey("chat_rooms.id"), nullable=False, index=True)
    user_id         = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    joined_at       = Column(DateTime, default=func.now())

    room            = relationship("ChatRoom", back_populates="members")

    __table_args__ = (UniqueConstraint("room_id", "user_id"),)


class ChatMessage(Base):
    __tablename__ = "chat_messages"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    room_id         = Column(BigInteger, ForeignKey("chat_rooms.id"), nullable=False, index=True)
    sender_id       = Column(BigInteger, ForeignKey("users.id"), nullable=False)
    content         = Column(Text, nullable=False)
    message_type    = Column(Enum("text", "dice_roll", "session_invite", "system"), default="text")
    metadata        = Column(JSON, nullable=True)  # Dice results, invite data, etc.
    created_at      = Column(DateTime, default=func.now(), index=True)

    room            = relationship("ChatRoom", back_populates="messages")
```

#### Notifications

```python
class Notification(Base):
    __tablename__ = "notifications"

    id              = Column(BigInteger, primary_key=True, autoincrement=True)
    user_id         = Column(BigInteger, ForeignKey("users.id"), nullable=False, index=True)
    type            = Column(String(50), nullable=False)  # "session_reminder", "friend_request", etc.
    title           = Column(String(200), nullable=False)
    body            = Column(Text, nullable=True)
    data            = Column(JSON, nullable=True)  # Action payload
    is_read         = Column(Boolean, default=False)
    created_at      = Column(DateTime, default=func.now(), index=True)
```

### 4.3 Indexes

```sql
-- Performance-critical indexes
CREATE INDEX idx_characters_owner ON characters(owner_id, is_active);
CREATE INDEX idx_lobby_players_lobby ON lobby_players(lobby_id);
CREATE INDEX idx_session_logs_session ON session_logs(session_id, timestamp);
CREATE INDEX idx_chat_messages_room ON chat_messages(room_id, created_at DESC);
CREATE INDEX idx_notifications_user ON notifications(user_id, is_read, created_at DESC);
CREATE INDEX idx_friendships_users ON friendships(requester_id, addressee_id, status);
CREATE INDEX idx_guild_members_guild ON guild_members(guild_id, role);
CREATE INDEX idx_guilds_location ON guilds(latitude, longitude);  -- For nearby guild search
```

---

## 5. API Architecture

### 5.1 REST Endpoints

#### Auth
```
POST   /api/v1/auth/register          # Create account
POST   /api/v1/auth/login             # Login → JWT pair
POST   /api/v1/auth/refresh           # Refresh access token
POST   /api/v1/auth/logout            # Invalidate refresh token
POST   /api/v1/auth/verify-email      # Email verification
POST   /api/v1/auth/oauth/{provider}  # OAuth login (google, discord)
```

#### Users
```
GET    /api/v1/users/me               # Current user profile
PATCH  /api/v1/users/me               # Update profile
GET    /api/v1/users/{uuid}           # Public profile
GET    /api/v1/users/search?q=        # Search users
```

#### Characters
```
GET    /api/v1/characters             # List my characters
POST   /api/v1/characters             # Create character
GET    /api/v1/characters/{uuid}      # Get character
PATCH  /api/v1/characters/{uuid}      # Update character
DELETE /api/v1/characters/{uuid}      # Archive character
POST   /api/v1/characters/{uuid}/level-up  # Level up
POST   /api/v1/characters/{uuid}/rest      # Short/long rest
```

#### Lobbies
```
GET    /api/v1/lobbies                # List my lobbies
POST   /api/v1/lobbies               # Create lobby
GET    /api/v1/lobbies/{uuid}         # Get lobby
PATCH  /api/v1/lobbies/{uuid}         # Update lobby
POST   /api/v1/lobbies/{uuid}/join    # Join lobby
POST   /api/v1/lobbies/{uuid}/leave   # Leave lobby
POST   /api/v1/lobbies/{uuid}/start   # Start session
GET    /api/v1/lobbies/invite/{code}  # Join via invite code
```

#### Sessions
```
GET    /api/v1/sessions               # List my sessions
GET    /api/v1/sessions/{uuid}        # Get session details
GET    /api/v1/sessions/{uuid}/log    # Get session log
POST   /api/v1/sessions/{uuid}/end    # End session
```

#### Friends
```
GET    /api/v1/friends                # List friends
POST   /api/v1/friends/request        # Send friend request
POST   /api/v1/friends/{id}/accept    # Accept request
POST   /api/v1/friends/{id}/reject    # Reject request
DELETE /api/v1/friends/{id}           # Remove friend
```

#### Guilds
```
GET    /api/v1/guilds                 # List guilds (with location filter)
POST   /api/v1/guilds                 # Create guild
GET    /api/v1/guilds/{uuid}          # Get guild
PATCH  /api/v1/guilds/{uuid}          # Update guild
POST   /api/v1/guilds/{uuid}/join     # Join guild
POST   /api/v1/guilds/{uuid}/leave    # Leave guild
GET    /api/v1/guilds/{uuid}/posts    # Get guild posts
POST   /api/v1/guilds/{uuid}/posts    # Create post
GET    /api/v1/guilds/{uuid}/events   # Get guild events
POST   /api/v1/guilds/{uuid}/events   # Create event
GET    /api/v1/guilds/nearby?lat=&lng= # Find nearby guilds
```

#### SRD Data
```
GET    /api/v1/srd/races              # All races
GET    /api/v1/srd/classes            # All classes
GET    /api/v1/srd/spells             # All spells (filterable)
GET    /api/v1/srd/items              # All items
GET    /api/v1/srd/monsters           # All monsters
GET    /api/v1/srd/backgrounds        # All backgrounds
```

#### Notifications
```
GET    /api/v1/notifications          # List notifications
PATCH  /api/v1/notifications/{id}/read  # Mark as read
POST   /api/v1/notifications/read-all   # Mark all as read
```

### 5.2 Response Format

```json
{
  "success": true,
  "data": { ... },
  "meta": {
    "page": 1,
    "per_page": 20,
    "total": 42
  }
}
```

Error format:
```json
{
  "success": false,
  "error": {
    "code": "CHARACTER_NOT_FOUND",
    "message": "Character with uuid xyz not found",
    "details": null
  }
}
```

---

## 6. WebSocket Events

### 6.1 Connection

```typescript
// Client connects with JWT
const socket = io("wss://api.questforge.app", {
  auth: { token: "eyJhbG..." }
});
```

### 6.2 Presence Events

```typescript
// Server → Client
"presence:online"        { userId, username }
"presence:offline"       { userId }
"presence:status_update" { userId, status: "Playing D&D" }

// Client → Server
"presence:set_status"    { status: string }
```

### 6.3 Lobby Events

```typescript
// Client → Server
"lobby:join"             { lobbyUuid }
"lobby:leave"            { lobbyUuid }
"lobby:select_character" { lobbyUuid, characterUuid }
"lobby:ready"            { lobbyUuid, isReady: boolean }
"lobby:kick"             { lobbyUuid, userId }  // DM only

// Server → Client (room: lobby:{uuid})
"lobby:player_joined"    { user, character }
"lobby:player_left"      { userId }
"lobby:player_ready"     { userId, isReady }
"lobby:character_selected" { userId, character }
"lobby:session_starting" { sessionUuid, countdown: 5 }
```

### 6.4 Live Session Events

```typescript
// Client → Server
"session:roll_dice"      { sessionUuid, dice: "1d20+5", purpose: "attack" }
"session:declare_action" { sessionUuid, action: string, targetId?: string }
"session:end_turn"       { sessionUuid }
"session:apply_damage"   { sessionUuid, targetCharId, amount, type }
"session:apply_heal"     { sessionUuid, targetCharId, amount }
"session:cast_spell"     { sessionUuid, spellSlug, level, targets }
"session:use_ability"    { sessionUuid, abilityName }
"session:short_rest"     { sessionUuid }
"session:long_rest"      { sessionUuid }
"session:talk_to_npc"    { sessionUuid, npcId, message }

// Server → Client (room: session:{uuid})
"session:dice_result"    { userId, characterName, dice, result, modifier, total, purpose, isCritical }
"session:narrative"      { text, speaker: "dm" | "npc", npcName? }
"session:combat_start"   { initiativeOrder: [...] }
"session:combat_end"     { }
"session:turn_change"    { currentTurnUserId, characterName, round }
"session:your_turn"      { round, combatState }
"session:damage_applied" { targetName, amount, type, remainingHp }
"session:heal_applied"   { targetName, amount, currentHp }
"session:spell_cast"     { casterName, spellName, level, effect }
"session:condition_change" { targetName, condition, action: "applied" | "removed" }
"session:hp_update"      { characterId, currentHp, maxHp, tempHp }
"session:xp_awarded"     { amount, reason }
"session:loot_found"     { items: [...] }
"session:session_ended"  { recap, xpTotal }
```

### 6.5 Chat Events

```typescript
// Client → Server
"chat:send"              { roomUuid, content, messageType }
"chat:typing"            { roomUuid }

// Server → Client
"chat:message"           { roomUuid, message: {...} }
"chat:typing"            { roomUuid, userId, username }
```

---

## 7. Authentication & Authorization

### 7.1 JWT Token Strategy

```
Access Token:  15 min expiry, stored in memory (not localStorage)
Refresh Token: 7 day expiry, stored in httpOnly cookie
```

### 7.2 Token Payload

```json
{
  "sub": "user-uuid-here",
  "uid": 12345,
  "username": "thorn_player",
  "exp": 1709913600,
  "iat": 1709912700
}
```

### 7.3 Authorization Levels

```
Public          → SRD data, guild discovery
Authenticated   → Character management, friends, chat
Lobby Owner     → Kick players, start session, modify lobby
DM (in session) → Control combat, override rules, manage NPCs
Guild Owner     → Guild settings, member management
Guild Officer   → Pin posts, create events, moderate
```

---

## 8. AI Integration

### 8.1 Architecture

```
Player Action → Socket.IO → AI Service → Claude API → Response → Socket.IO → Players
                                │
                                ├── System Prompt (D&D 5e rules, campaign context)
                                ├── Session State (characters, HP, conditions, location)
                                ├── Conversation History (recent 50 exchanges)
                                └── World State (campaign persistent data)
```

### 8.2 AI DM System Prompt Structure

```python
SYSTEM_PROMPT = """
You are the Dungeon Master for a D&D 5th Edition game.

RULES:
- Follow D&D 5e rules strictly (SRD)
- Never fudge dice rolls or ignore game mechanics
- Always specify when a player needs to roll and what modifiers apply

CURRENT STATE:
{session_state_json}  # Characters, HP, conditions, initiative, location

CAMPAIGN CONTEXT:
{campaign_context}    # Ongoing story, NPC relationships, world state

PARTY:
{party_details}       # Each character's name, class, level, notable abilities

TONE: {tone_setting}  # "serious", "humorous", "horror", "heroic"

RESPONSE FORMAT:
- Narrate in second person ("You see...", "The goblin attacks...")
- When combat actions occur, specify exact rolls needed
- Return structured data for mechanical effects (damage, conditions, etc.)
- Keep responses concise but atmospheric
"""
```

### 8.3 AI Response Format

The AI returns structured JSON alongside narrative text:

```json
{
  "narrative": "The goblin chief swings his rusty blade at Thorn...",
  "mechanical_effects": [
    {
      "type": "attack_roll",
      "attacker": "Goblin Chief",
      "target": "Thorn",
      "roll": 15,
      "modifier": 4,
      "total": 19,
      "hits": true
    },
    {
      "type": "damage",
      "target": "Thorn",
      "amount": 8,
      "damage_type": "slashing"
    }
  ],
  "requires_player_action": false,
  "next_turn": "player:elara"
}
```

### 8.4 AI Modes Implementation

| Mode | System Prompt Additions | Player Interaction |
|---|---|---|
| Full DM | Full narrative control, NPC management, encounter creation | AI drives story, players respond |
| DM Assistant | Suggestion mode, rule lookups, NPC dialogue generation | Human DM sees AI suggestions privately |
| NPC Dialogue | Character personality context, knowledge boundaries | Players chat directly with NPC |
| Encounter Gen | Party level, composition, difficulty target, terrain type | Returns encounter data, not narrative |
| Rule Enforcer | Action validation, modifier checking, rule references | Flags invalid actions with explanations |

---

## 9. D&D 5e Rules Engine

### 9.1 Core Calculations

```python
# app/engine/abilities.py

def ability_modifier(score: int) -> int:
    return (score - 10) // 2

def proficiency_bonus(level: int) -> int:
    return (level - 1) // 4 + 2

def skill_bonus(ability_score: int, level: int, is_proficient: bool, has_expertise: bool) -> int:
    mod = ability_modifier(ability_score)
    prof = proficiency_bonus(level)
    if has_expertise:
        return mod + (prof * 2)
    if is_proficient:
        return mod + prof
    return mod

def spell_save_dc(ability_score: int, level: int) -> int:
    return 8 + ability_modifier(ability_score) + proficiency_bonus(level)

def spell_attack_bonus(ability_score: int, level: int) -> int:
    return ability_modifier(ability_score) + proficiency_bonus(level)
```

### 9.2 Dice Engine

```python
# app/engine/dice.py

import random
from dataclasses import dataclass

@dataclass
class DiceResult:
    expression: str       # "2d6+3"
    individual_rolls: list[int]  # [4, 2]
    modifier: int         # 3
    total: int            # 9
    is_critical: bool     # True if natural 20 on d20
    is_fumble: bool       # True if natural 1 on d20

def roll(expression: str, advantage: bool = False, disadvantage: bool = False) -> DiceResult:
    """Parse and roll dice expression like '2d6+3', '1d20', 'd8'"""
    # Parse expression: NdS+M format
    # If advantage/disadvantage on d20: roll twice, take highest/lowest
    ...
```

### 9.3 Combat Engine

```python
# app/engine/combat.py

class CombatState:
    round: int
    turn_index: int
    initiative_order: list[CombatantState]  # Sorted by initiative
    is_active: bool

class CombatantState:
    id: str
    name: str
    initiative: int
    is_player: bool
    character_id: int | None
    hp: int
    max_hp: int
    temp_hp: int
    armor_class: int
    conditions: list[str]
    concentration_spell: str | None

def roll_initiative(combatants: list[CombatantState]) -> list[CombatantState]:
    """Roll initiative for all combatants, sort descending"""
    ...

def resolve_attack(attacker: CombatantState, target: CombatantState,
                   attack_roll: DiceResult, weapon_damage: str) -> AttackResult:
    """Check if attack hits AC, calculate damage, apply to target"""
    ...

def apply_condition(target: CombatantState, condition: str) -> list[str]:
    """Apply condition, return list of active mechanical effects"""
    # e.g., "poisoned" → ["Disadvantage on attack rolls", "Disadvantage on ability checks"]
    ...
```

---

## 10. Development Roadmap

### Phase 1: Foundation (Weeks 1-6)

**Goal:** Users can register, create characters, and manage them.

```
Week 1-2: Project Setup
├── Initialize monorepo (server/ + client/)
├── FastAPI boilerplate with async SQLAlchemy
├── MariaDB + Alembic migrations setup
├── Vue 3 + TypeScript + Vite setup
├── Docker Compose (MariaDB, Redis, API, Client)
├── CI/CD pipeline (GitHub Actions)
└── Basic project documentation

Week 3-4: Authentication
├── User model + migration
├── POST /auth/register (email/password)
├── POST /auth/login → JWT pair
├── POST /auth/refresh → new access token
├── Email verification flow
├── OAuth (Google) integration
├── Vue auth pages (Login, Register)
├── Auth store (Pinia) + route guards
└── Token refresh interceptor

Week 5-6: Character System
├── Character model + related models + migrations
├── SRD data import (races, classes, spells, items as JSON)
├── Character CRUD API endpoints
├── D&D 5e rules engine (abilities, skills, proficiency)
├── Character creation wizard (Vue multi-step form)
├── Character sheet view
├── Character edit functionality
├── Level-up flow
└── Rest mechanics (short/long)
```

**Phase 1 Deliverable:** A user can sign up, create a D&D 5e character through a guided wizard, view and edit their character sheet, and level up.

### Phase 2: Social & Real-Time (Weeks 7-12)

**Goal:** Users can add friends, chat, create lobbies, schedule sessions, and play with live session tools.

```
Week 7-8: Social Layer
├── Friendship model + API
├── Friend request/accept/reject flow
├── Socket.IO server setup
├── Presence system (online/offline/status)
├── Chat room model + API
├── Real-time chat (Socket.IO)
├── Vue friends list + chat panels
└── Push notification infrastructure (Celery + FCM/APNs via Capacitor)

Week 9-10: Lobby System
├── Lobby model + API
├── Create lobby (name, time, location, DM mode)
├── Invite system (friends invite + invite code)
├── Lobby Socket.IO room (real-time player join/leave/ready)
├── Session scheduling + timezone handling
├── Notification system (session reminders)
├── Vue lobby views (create, join, waiting room)
└── Recurring session support

Week 11-12: Live Session Engine
├── GameSession model + SessionLog
├── Session state management (Redis)
├── Dice roller (engine + Socket.IO events + Vue component)
├── Initiative tracker (roll, sort, turn management)
├── Combat manager (HP tracking, damage, healing, conditions)
├── Spell slot tracker
├── Session feed (real-time log of events)
├── Turn notifications ("Your turn!")
├── Short/long rest during session
├── Session end + recap generation
└── Vue live session view (responsive, mobile-optimized)
```

**Phase 2 Deliverable:** A group can add each other as friends, chat, create a lobby, schedule a session, and play a live D&D session with dice rolling, initiative tracking, combat management, and a real-time session feed.

### Phase 3: AI & Community (Weeks 13-20)

**Goal:** AI Dungeon Master in all modes, guild system, community features.

```
Week 13-15: AI Dungeon Master
├── AI service (Claude API integration via httpx)
├── System prompt engineering for D&D 5e DM
├── Session context builder (characters, state, history)
├── Full DM mode (narrative, NPCs, encounters, combat)
├── DM Assistant mode (suggestions, rule lookups)
├── NPC Dialogue mode (conversational NPC interaction)
├── Encounter Generator (balanced encounter creation)
├── Rule Enforcer (action validation)
├── AI response parser (narrative + mechanical effects)
├── Campaign world state persistence
├── Vue AI DM interface (session feed integration)
└── AI settings (tone, difficulty, content filters)

Week 16-18: Guilds & Community
├── Guild model + members + posts + events
├── Guild CRUD API
├── Guild discovery (location-based with lat/lng)
├── Guild boards (announcements, LFP, discussions)
├── Guild events with scheduling
├── Guild chat rooms
├── Vue guild views (browse, detail, manage)
└── LFP (Looking for Players) system

Week 19-20: Polish & Mobile
├── PWA configuration (manifest, service worker, offline basics)
├── Capacitor setup for iOS/Android
├── Push notifications (native)
├── Mobile-specific optimizations
├── Animation system (GSAP integration)
├── Sound effects (Howler.js)
├── Performance optimization
├── Comprehensive testing
└── Beta launch preparation
```

**Phase 3 Deliverable:** Full AI DM capabilities, community features, and a polished mobile experience ready for beta testing.

---

## 11. Infrastructure & Deployment

### 11.1 Docker Compose (Development)

```yaml
version: "3.8"
services:
  db:
    image: mariadb:11
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
      MYSQL_DATABASE: questforge
      MYSQL_USER: questforge
      MYSQL_PASSWORD: ${DB_PASSWORD}
    volumes:
      - db_data:/var/lib/mysql
    ports:
      - "3306:3306"

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

  api:
    build: ./server
    command: uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
    environment:
      DATABASE_URL: mysql+aiomysql://questforge:${DB_PASSWORD}@db:3306/questforge
      REDIS_URL: redis://redis:6379/0
      JWT_SECRET: ${JWT_SECRET}
      ANTHROPIC_API_KEY: ${ANTHROPIC_API_KEY}
    volumes:
      - ./server:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis

  celery:
    build: ./server
    command: celery -A app.tasks worker --loglevel=info
    environment:
      DATABASE_URL: mysql+aiomysql://questforge:${DB_PASSWORD}@db:3306/questforge
      REDIS_URL: redis://redis:6379/0
      ANTHROPIC_API_KEY: ${ANTHROPIC_API_KEY}
    volumes:
      - ./server:/app
    depends_on:
      - db
      - redis

  client:
    build: ./client
    command: npm run dev -- --host 0.0.0.0
    volumes:
      - ./client:/app
      - /app/node_modules
    ports:
      - "5173:5173"

volumes:
  db_data:
```

### 11.2 Production Architecture

```
                    ┌─────────────┐
                    │  Cloudflare  │  ← CDN + DDoS protection
                    │     CDN      │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   Nginx     │  ← SSL termination, static files, proxy
                    │   Reverse   │
                    │   Proxy     │
                    └──┬──────┬──┘
                       │      │
              ┌────────▼┐  ┌──▼────────┐
              │ FastAPI  │  │ Socket.IO │
              │ (HTTP)   │  │ (WSS)     │
              │ x2 inst  │  │ x2 inst   │
              └────┬─────┘  └────┬──────┘
                   │             │
          ┌────────┼─────────────┼────────┐
          │        │             │        │
     ┌────▼───┐ ┌──▼──┐ ┌───────▼──┐ ┌───▼────┐
     │MariaDB │ │Redis │ │ Celery   │ │ Claude │
     │Primary │ │      │ │ Workers  │ │ API    │
     │+ Repli │ │      │ │          │ │        │
     └────────┘ └──────┘ └──────────┘ └────────┘
```

### 11.3 Environment Variables

```env
# Database
DATABASE_URL=mysql+aiomysql://user:pass@host:3306/questforge

# Redis
REDIS_URL=redis://host:6379/0

# JWT
JWT_SECRET=<random-256-bit-key>
JWT_ACCESS_EXPIRE_MINUTES=15
JWT_REFRESH_EXPIRE_DAYS=7

# AI
ANTHROPIC_API_KEY=sk-ant-...
AI_MODEL=claude-sonnet-4-5-20250929
AI_MAX_TOKENS=2048

# OAuth
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...

# Push Notifications
FCM_SERVER_KEY=...

# App
APP_URL=https://questforge.app
API_URL=https://api.questforge.app
ENVIRONMENT=production
```

---

## 12. Testing Strategy

### 12.1 Backend Tests

```
tests/
├── unit/
│   ├── test_dice_engine.py       # Dice parsing and rolling
│   ├── test_combat_engine.py     # Attack resolution, damage, conditions
│   ├── test_ability_calc.py      # Modifier, proficiency, skill bonus
│   ├── test_spell_engine.py      # Slot management, concentration
│   └── test_rest_engine.py       # Short/long rest recovery
│
├── integration/
│   ├── test_auth_flow.py         # Register → verify → login → refresh
│   ├── test_character_crud.py    # Create → read → update → level up
│   ├── test_lobby_flow.py        # Create → join → ready → start
│   ├── test_session_flow.py      # Start → roll → combat → end
│   └── test_friendship_flow.py   # Request → accept → list
│
└── e2e/
    └── test_full_session.py      # Complete session from lobby to recap
```

### 12.2 Frontend Tests

```
tests/
├── components/
│   ├── DiceRoller.spec.ts
│   ├── AbilityScores.spec.ts
│   ├── InitiativeTracker.spec.ts
│   └── HpBar.spec.ts
│
├── stores/
│   ├── auth.spec.ts
│   ├── character.spec.ts
│   └── session.spec.ts
│
└── e2e/
    ├── auth.spec.ts
    ├── character-creation.spec.ts
    └── live-session.spec.ts
```

### 12.3 D&D Rules Engine Tests

Critical — the rules engine must be correct:

```python
# test_dice_engine.py
def test_d20_range():
    for _ in range(1000):
        result = roll("1d20")
        assert 1 <= result.total <= 20

def test_modifier_applied():
    result = roll("1d20+5")
    assert result.modifier == 5
    assert result.total == result.individual_rolls[0] + 5

# test_ability_calc.py
def test_ability_modifiers():
    assert ability_modifier(1) == -5
    assert ability_modifier(10) == 0
    assert ability_modifier(11) == 0
    assert ability_modifier(18) == 4
    assert ability_modifier(20) == 5
    assert ability_modifier(30) == 10

def test_proficiency_bonus_by_level():
    assert proficiency_bonus(1) == 2
    assert proficiency_bonus(4) == 2
    assert proficiency_bonus(5) == 3
    assert proficiency_bonus(9) == 4
    assert proficiency_bonus(13) == 5
    assert proficiency_bonus(17) == 6

# test_combat_engine.py
def test_attack_hits_when_roll_meets_ac():
    # Attack total of 15 vs AC 15 should hit
    ...

def test_natural_20_always_hits():
    # Natural 20 hits regardless of AC
    ...

def test_natural_1_always_misses():
    # Natural 1 misses regardless of modifiers
    ...
```

---

<p align="center">
  <strong>⚔️ QuestForge</strong> — Technical Documentation v1.0
</p>
