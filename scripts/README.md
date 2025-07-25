# MTG Data Scraping Scripts

This directory contains scripts to scrape comprehensive Magic: The Gathering data from reliable sources and generate JSON files for use in the frontend application.

## Overview

The scrapers collect data from:
- **MTG Wiki (mtg.fandom.com)** - For game formats, mechanics descriptions, and detailed rules content
- **Scryfall API** - For comprehensive mechanics lists and fresh data

## Scripts

### 🎮 Game Overview Scraper (`scrapers/gameOverview.js`)
Scrapes comprehensive MTG introduction and learning guide.

**Output:** `data/gameOverview.json`

### 🎨 Colours Scraper (`scrapers/colours.js`)
Scrapes the six MTG colours (including colourless) with their philosophies, strengths, and associated mechanics.

**Output:** `data/colours.json`

### 🃏 Card Types Scraper (`scrapers/cardTypes.js`)
Scrapes card type information including descriptions, rules, usage, and timing.

**Output:** `data/cardTypes.json`

### 🕒 Turn Phases Scraper (`scrapers/turnPhases.js`)
Scrapes official MTG turn structure with detailed phase and step breakdowns.

**Output:** `data/turnPhases.json`

### 📋 Card Anatomy Scraper (`scrapers/cardAnatomy.js`)
Scrapes detailed information about card parts, layout, and reading tips.

**Output:** `data/cardAnatomy.json`

### 🏆 Win Conditions Scraper (`scrapers/winConditions.js`)
Scrapes all ways to win MTG games, including primary and alternative conditions.

**Output:** `data/winConditions.json`

### 🏗️ Deck Building Scraper (`scrapers/deckBuilding.js`)
Scrapes deck construction rules, strategies, and best practices.

**Output:** `data/deckBuilding.json`

### ⚔️ Combat Basics Scraper (`scrapers/combatBasics.js`)
Scrapes combat system mechanics, steps, and strategic considerations.

**Output:** `data/combatBasics.json`

### ⚡ Enhanced Mechanics Scraper (`scrapers/mechanics.js`)
- Fetches comprehensive mechanics list from Scryfall API (keyword abilities + ability words)
- Scrapes detailed descriptions for 50+ priority mechanics from MTG Wiki
- Provides simple descriptions, rules text, reminder text, and complexity ratings
- Categorises mechanics by type (evergreen, beginner-friendly, etc.)
- Includes first appearance information and example cards

**Output:** `data/mechanics.json`

### 🎮 Game Modes Scraper (`scrapers/gameModes.js`)
- Scrapes comprehensive format information from MTG Wiki
- Covers rotating, eternal, limited, multiplayer, and custom formats
- Includes detailed descriptions, rules, and popularity ratings
- Organises formats into logical categories for easy browsing

**Output:** `data/gameModes.json`

## Usage

### Install Dependencies
```bash
npm install
```

### Run Individual Scrapers
```bash
# Scrape game overview only
npm run scrape:overview

# Scrape colors only
npm run scrape:colors

# Scrape card types only
npm run scrape:card-types

# Scrape turn phases only
npm run scrape:turn-phases

# Scrape card anatomy only
npm run scrape:anatomy

# Scrape win conditions only
npm run scrape:win-conditions

# Scrape deck building only
npm run scrape:deck-building

# Scrape combat basics only
npm run scrape:combat

# Scrape mechanics only
npm run scrape:mechanics

# Scrape game modes only
npm run scrape:game-modes
```

### Run Multiple Scrapers
```bash
# Run all fundamental scrapers (excludes mechanics for speed)
npm run scrape:fundamentals

# Run all scrapers sequentially
npm run scrape:all
```

### Copy Data to Frontend
```bash
# Copy JSON files to frontend/data directory
npm run copy
```

### Full Pipeline
```bash
# Scrape all data and copy to frontend
npm run build
```

## Rate Limiting

The scrapers include built-in rate limiting to be respectful to the MTG Wiki:
- 500ms delay between priority mechanic requests
- 1-2 second delays between major scraper runs
- Graceful fallbacks if scraping fails

## Data Structure

### Game Overview (`gameOverview.json`)
```json
{
  "introduction": {
    "title": "What is Magic: The Gathering?",
    "description": "Magic: The Gathering (MTG) is a collectible card game...",
    "tagline": "The world's first and most popular trading card game"
  },
  "basics": { "players": "...", "gameLength": "...", "ageRange": "..." },
  "coreGameplay": { "overview": "...", "gameFlow": "...", "strategy": "..." },
  "learningPath": [{ "step": 1, "title": "...", "description": "..." }]
}
```

### Colours (`colours.json`)
```json
{
  "white": {
    "name": "White",
    "description": "White represents order, peace...",
    "philosophy": "White believes in creating...",
    "strengths": ["Life gain", "Protection", ...],
    "mechanics": ["First strike", "Vigilance", ...],
    "emoji": "⚪",
    "symbol": "W"
  }
}
```

### Card Types (`cardTypes.json`)
```json
{
  "creature": {
    "name": "Creature",
    "description": "Creatures represent beings...",
    "rules": "Creatures enter with summoning sickness...",
    "usage": "Your primary way to deal damage...",
    "timing": "Main phase only (sorcery speed)",
    "examples": ["Combat creatures", ...],
    "icon": "👹"
  }
}
```

### Turn Phases (`turnPhases.json`)
```json
{
  "phases": {
    "beginning": {
      "name": "Beginning Phase",
      "order": 1,
      "description": "The start of your turn where you untap...",
      "steps": {
        "untap": { "name": "Untap Step", "rules": [...] },
        "upkeep": { "name": "Upkeep Step", "commonTriggers": [...] },
        "draw": { "name": "Draw Step", "strategicNotes": [...] }
      }
    }
  },
  "timingRules": { "priority": {...}, "spellSpeeds": {...} }
}
```

### Card Anatomy (`cardAnatomy.json`)
```json
{
  "cardParts": {
    "manaCost": {
      "name": "Mana Cost",
      "location": "Top right corner",
      "description": "Shows the mana required to cast the spell...",
      "components": ["Colourless mana", "Coloured mana", ...]
    }
  },
  "readingTips": ["Always read the card name first", ...]
}
```

### Win Conditions (`winConditions.json`)
```json
{
  "primaryWinConditions": {
    "lifeTotal": {
      "name": "Life Total Victory",
      "emoji": "❤️",
      "description": "The most common way to win...",
      "tips": ["Creatures are your main source of damage", ...]
    }
  },
  "alternativeWinConditions": { ... }
}
```

### Deck Building (`deckBuilding.json`)
```json
{
  "fundamentalRules": {
    "minimumDeckSize": {
      "rule": "60 cards minimum for Constructed formats",
      "explanation": "Most competitive formats require...",
      "formatVariations": { "Standard/Modern/Pioneer": "60 cards minimum" }
    }
  },
  "deckBuildingSteps": [{ "step": 1, "title": "...", "description": "..." }]
}
```

### Combat Basics (`combatBasics.json`)
```json
{
  "combatSteps": {
    "declareAttackers": {
      "name": "Declare Attackers Step",
      "order": 2,
      "description": "The active player chooses which creatures attack...",
      "whatHappens": ["Active player declares attacking creatures", ...]
    }
  },
  "combatKeywords": { "attackingKeywords": { ... }, "blockingKeywords": { ... } }
}
```

### Enhanced Mechanics (`mechanics.json`)
```json
{
  "lastUpdated": "2025-07-18T09:58:44.616Z",
  "source": "Scryfall API + MTG Wiki + Manual curation",
  "stats": {
    "totalCount": 273,
    "keywordAbilitiesCount": 210,
    "abilityWordsCount": 63,
    "evergreenCount": 16,
    "beginnerFriendlyCount": 11
  },
  "mechanics": {
    "flying": {
      "name": "Flying",
      "description": "Flying is an evergreen evasion ability...",
      "simpleDescription": "Can only be blocked by creatures with flying or reach.",
      "rulesText": "...",
      "reminderText": "...",
      "category": "evasion",
      "type": "keyword_ability",
      "isEvergreen": true,
      "isBeginnerFriendly": true,
      "complexity": "simple",
      "firstAppeared": "Alpha",
      "wikiUrl": "https://mtg.fandom.com/wiki/Flying",
      "exampleCards": [...]
    }
  },
  "categories": {
    "evergreen": [...],
    "beginnerFriendly": [...],
    "keywordAbilities": [...],
    "abilityWords": [...],
    "byComplexity": {
      "simple": [...],
      "medium": [...],
      "complex": [...]
    }
  }
}
```

### Game Modes (`gameModes.json`)
```json
{
  "lastUpdated": "2025-07-18T09:50:36.957Z",
  "source": "MTG Wiki + Manual curation",
  "categories": {
    "rotating": {
      "title": "🔁 Rotating",
      "description": "These formats have card pools that change over time",
      "formats": [
        {
          "name": "Standard",
          "description": "Standard is a rotating constructed play format...",
          "rules": "Standard decks must contain a minimum of sixty cards...",
          "isDigitalOnly": false,
          "isCompetitive": true,
          "isRotating": true,
          "popularity": "very-high",
          "wikiUrl": "https://mtg.fandom.com/wiki/Standard"
        }
      ]
    }
  },
  "allFormats": [...]
}
```

## Integration with Frontend

After running the scrapers, the data is automatically copied to `frontend/data/` where it can be imported:

```javascript
// Import the data
import gameOverview from "../data/gameOverview.json";
import colours from "../data/colours.json";
import cardTypes from "../data/cardTypes.json";
import turnPhases from "../data/turnPhases.json";
import cardAnatomy from "../data/cardAnatomy.json";
import winConditions from "../data/winConditions.json";
import deckBuilding from "../data/deckBuilding.json";
import combatBasics from "../data/combatBasics.json";
import { mechanicsDetails, getMechanicDetails } from "../data/mechanics.js";
import gameModes from "../data/gameModes.json";

// Use in components
const introduction = gameOverview.introduction;
const whiteColor = colors.white;
const creatureType = cardTypes.creature;
const beginningPhase = turnPhases.phases.beginning;
const manaCostInfo = cardAnatomy.cardParts.manaCost;
const lifeTotalWin = winConditions.primaryWinConditions.lifeTotal;
const deckRules = deckBuilding.fundamentalRules;
const combatSteps = combatBasics.combatSteps;
const flyingMechanic = getMechanicDetails("Flying");
const standardFormat = gameModes.categories.rotating.formats.find(f => f.name === "Standard");
```

## Troubleshooting

### Common Issues

1. **Network errors**: The scrapers include retry logic, but if wiki pages are down, fallback data is used
2. **Rate limiting**: If you get 429 errors, increase delays in the scraper files
3. **Missing data**: Some mechanics may not have detailed descriptions - this is expected for advanced mechanics

### Debugging

Run individual scrapers to isolate issues:
```bash
# Test specific scraper
npm run scrape:overview
npm run scrape:colours
npm run scrape:turn-phases
npm run scrape:win-conditions

# Check output
cat data/gameOverview.json | jq
cat data/turnPhases.json | jq
cat data/colours.json | jq
```

## Contributing

When adding new scrapers:
1. Follow the existing pattern in `scrapers/`
2. Include fallback data for reliability
3. Add rate limiting for external requests
4. Update the main index file to include your scraper
5. Add appropriate npm scripts

## Data Sources

- **MTG Wiki**: https://mtg.fandom.com/ (Community-maintained, comprehensive)
- **Scryfall API**: https://api.scryfall.com/ (Official card database API)

Both sources are used under fair use for educational/community purposes.