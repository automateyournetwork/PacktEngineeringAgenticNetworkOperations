# Plan — Packet Quest technical implementation

## Tech stack
- Vanilla HTML, CSS, and JavaScript only — no frameworks, no build tools, no bundler
- However use THREE.JS for the framework of the game engine (SVG rendering, animation, and routing logic)
- Single HTML file entry point (index.html) with linked CSS and JS modules
- All game data in /data/levels.json — structured, auditable, no logic inside
- Local storage for save state (no backend, no auth)
- SVG for network topology diagrams (generated from level data, not hand-drawn)
- No canvas API — DOM-based rendering for accessibility

## Architecture

### File structure
/
├── index.html
├── style.css
├── main.js              # bootstraps game, routes views
├── /engine
│   ├── router.js        # routing table logic (pure functions, fully testable)
│   ├── topology.js      # SVG topology renderer from JSON
│   ├── feedback.js      # feedback copy generator
│   └── state.js         # game state management
├── /views
│   ├── briefing.js      # pre-level concept introduction
│   ├── gameplay.js      # main routing decision UI
│   └── summary.js       # post-level debrief
└── /data
    └── levels.json      # all levels, questions, routes, sources

### levels.json schema (one level)
{
  "id": "level-03",
  "concept": "longest prefix match",
  "briefing": { "title": "...", "explanation": "...", "example": "..." },
  "topology": { "routers": [...], "links": [...] },
  "packet": { "src": "10.1.1.5", "dst": "192.168.40.10" },
  "routing_table": [ { "prefix": "0.0.0.0/0", "next_hop": "R2", "source": "static" }, ... ],
  "correct_path": ["R1", "R3", "R4", "DST"],
  "wrong_choices": {
    "R2": { "why_wrong": "The default route matches, but R3 has a more specific /24 prefix. Longest prefix match wins.", "concept_reinforced": "longest prefix match" }
  },
  "source": "RFC 1812 §4.3.2.4"
}

### Routing engine (router.js)
- Pure function: getNextHop(routingTable, destinationIP) → { nextHop, matchedPrefix, rule }
- Implements longest prefix match in JavaScript
- Fully unit-testable with no DOM dependency
- This is the single source of truth — UI never makes routing decisions

### Topology renderer (topology.js)
- Takes level topology JSON → generates SVG
- Highlights current router, animates packet movement between hops
- Interfaces labeled with IP/mask
- No external SVG libraries

## What I am deliberately not building in v1
- User accounts or leaderboards
- Mobile touch optimization (desktop-first)
- Audio
- A level editor UI (edit levels.json directly)

## Definition of done for each level
- Routing logic validated against manually verified correct/incorrect paths
- Briefing reviewed for accuracy against cited RFC or textbook
- All wrong-choice explanations written and reviewed
- Level playable start to finish with keyboard only