# Career Quest Map

An AI-guided pathway discovery game for Singapore youth. Career Quest Map turns career exploration into a short, story-driven game. Instead of dumping course lists on you, it starts with self-discovery, narrows down your interests, and then gives realistic next steps you can actually do.

## Demo Preview

- Part 1 in the House: quick self-discovery questions
- Part 2 with the Wise Man: deeper narrowing questions
- Analysis: strengths, work style, feedback
- Gates: ranked pathways you can explore
- Dragon quests: actionable 1-week and 1-month tasks
- Quest booth: review your analysis and quests

## Why We Built This

Many students are pushed to choose early. Grades tell performance. They do not tell fit. This project is designed to help users:

- Understand strengths and work style
- Explore options based on fit and growth
- Leave with an action plan, not just a recommendation

## Key Features

### 1) Adaptive Question Flow (LLM-powered)

Profile step collects:

- Name
- Education status (Secondary School, JC, Poly)
- Poly course of study (only if Poly)

The LLM generates questions based on the user context. Outputs are constrained using strict JSON schemas and validation.

### 2) Part 1: House Questions (5 questions)

Goal: broad self-discovery, then tighten slightly.

Question types are enforced:

- 2 MCQ
- 1 slider (0 to 10 with labels)
- 1 rating (1 to 5)
- 1 text

Topic focus:

- Secondary School / JC: interests, personality, curiosity, preferred activities
- Poly: course challenges, frustrations, motivation, preferred learning style, other interests

### 3) Part 2: Wise Man Questions (12 questions + Poly extra)

Goal: narrow across 3 inferred fields.

The LLM:

- Infers exactly 3 fields from Part 1 answers
- Generates 12 sequential narrowing questions

Question types are enforced:

- 4 MCQ
- 3 slider
- 3 rating
- 2 text

Poly-only extra question:

- Work
- Go to uni

### 4) Analysis (Schema C)

After Part 2, the system generates:

- 3 strength tags
- 2 to 4 work style tags
- 2 to 5 feedback lines (fantasy-lite, short)
- Exactly 3 ranked suggested options
  - Poly Work: careers/roles
  - Else: courses

### 5) Gates and Gate Scenes (Schema D)

The user enters a gate scene with 3 gates, ranked 1, 2, 3 based on Part 2 answers.

Inside each gate, the Wise Man explains:

- What to study or skills to build
- Employment outlook (safe wording)
- Impact on people
- If work-path: also salary outlook and work style (safe wording)

Then user chooses:

- **Yes**: unlocks Dragon quests
- **No**: return and explore other gates

### 6) Dragon Quests and Resources

If the user says Yes:

- 1-week micro quest (short sessions, tangible output)
- 1-month mini project (Plan, Build, Review)
- Resources list (free and accessible)

### 7) Quest Log and Guidance

Quest reminders like:

- Go to house
- Go to wise man
- Go to gates

Helps users stay oriented and reduces confusion during exploration.

### 8) Game Feel

- Top-down exploration maps
- Walking animation
- Collision physics so you cannot walk through objects
- Scene-to-scene progression feels like a journey

### 9) Reliability and Safety Controls

- Strict JSON schemas and validation for LLM outputs
- Fallback content if LLM fails, so the game still runs
- Curated dataset for pathways so recommendations stay realistic

## Tech Stack

- Python 3
- Pygame
- Azure OpenAI (LLM generation)
- JSON schemas + validators
- Curated pathways dataset (`options_catalog.json`)

## Project Flow

1. Start screen
2. Profile input (name, education status, optional poly course)
3. Part 1 generated and played in House
4. Part 2 generated and played with Wise Man
5. Analysis shown (strengths, work style, feedback, 3 ranked options)
6. Gates scene (3 ranked gates)
7. Gate scene (Yes/No)
8. Dragon quest scene (if Yes)
9. Quest booth review
10. Final completion scene

## How to Run

### 1) Install Dependencies

```bash
pip install -r requirements.txt
```

### 2) Set Environment Variables (Azure OpenAI)

Set these in your terminal or `.env` file:

```
AZURE_OPENAI_ENDPOINT
AZURE_OPENAI_API_KEY
AZURE_OPENAI_API_VERSION
AZURE_OPENAI_DEPLOYMENT
```

### 3) Run the Game

From `src`:

```bash
python -m app.main
```

### Controls

| Action | Keys |
|---|---|
| Movement | Arrow keys or WASD |
| Interact / Advance dialog | Enter |
| Back / Exit screen | Esc |
| Gate decision | Y or N |
| House questions | Type answer then Enter, or click Next |

## Assets

Place game assets in:

```
src/ui/assets/
```

Example filenames used by screens:

```
background.png
warrior_up.png
warrior_down.png
warrior_left.png
warrior_right.png
house.png
wise_man.png
gate_background.png
wise_man_gate.png
dragon_warrior.png
```

> If an asset is missing, the game will fall back to simple shapes.

## Known Limitations

- LLM calls introduce latency between scenes, even with loading text.
- More logic (animations, collision blocks) can affect smoothness on low-end devices.
- LLM outputs may still vary, so we rely on validation and fallbacks to keep flow stable.

## Future Improvements

- Cache LLM results per user session to reduce repeated waiting
- Add a clearer minimap or waypoint arrow for quests
- Expand the curated dataset for more pathways
- Improve the final review booth with export to PDF or shareable plan

## Credits

Built for **CCDS Tech for Good Hackathon 2026**.

**Team:** Zin Hmue Paing, Thiha Htoo Zin, Bhone Min Thant
