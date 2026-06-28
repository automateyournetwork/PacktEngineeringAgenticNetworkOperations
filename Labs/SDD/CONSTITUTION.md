# Project constitution — network educational game

## Purpose
Build a web-based educational game that teaches networking concepts through interactive gameplay. The game must be both accurate and engaging. It functions as a teacher: it never guesses, never invents answers, and never allows a player to progress on incorrect knowledge.

## The non-negotiable rule
**The game must never present incorrect information, even under time pressure or to be "more fun."** If a mechanic requires an answer, that answer must be deterministically correct or deterministically incorrect — no fuzzy grading, no partial-credit ambiguity that could reinforce misconceptions. When in doubt, the game waits, not guesses.

## Learning design principles
1. **Correctness over completion** — a player who hasn't learned the concept cannot advance. This is a feature, not a bug.
2. **Immediate, specific feedback** — wrong answers always explain *why* they are wrong, not just that they are wrong.
3. **Layered complexity** — concepts build on each other. A player cannot encounter BGP before they understand IP routing.
4. **Recall over recognition where possible** — prefer typed answers or drag-to-build mechanics over pure multiple choice. Recognition inflates confidence; recall builds retention.
5. **Real-world grounding** — every mechanic should map to something a network engineer actually does or encounters. Fictional constructs are allowed only as metaphor, clearly labeled.

## Gameplay principles
- Progress is earned, not gifted. No "try again and we'll lower the bar."
- Mistakes are learning moments, not punishments. Tone is calm and explanatory, never scolding.
- Speed bonuses are acceptable only for mechanics where speed is genuinely relevant (e.g. recognizing a packet header format). Speed bonuses must never be the *only* way to earn points.
- Every level must be completable with zero prior knowledge if the player reads all available hints. The game teaches; it does not assume.

## Code quality standards
- All question/answer data lives in a separate, editable data file (JSON or JS module). No hardcoded Q&A inside game logic.
- Every factual claim in the game data must include a `source` field (RFC number, textbook chapter, or authoritative URL) even if not shown to the player. This makes the data auditable.
- Difficulty is data-driven. Adding a new level means editing data, not code.
- No external quiz APIs, AI-generated answers, or runtime-fetched content for question correctness — the ground truth is local and audited.

## UX standards
- Works on desktop browsers without install.
- Keyboard navigable for all core interactions.
- Feedback copy is written in plain English, not jargon — unless teaching the jargon is the point of the question.
- Loading states, error states, and empty states all have explicit designs.

## What this game is not
- Not a trivia app that happens to have networking questions.
- Not a flashcard deck with a progress bar.
- Not a simulation that rewards clicking without understanding.

The game should feel like the best professor you ever had — patient, precise, and genuinely delighted when you get it right.