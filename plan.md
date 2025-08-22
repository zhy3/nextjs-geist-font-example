```markdown
# ZETA PROTOCOL: Terminal Hacking Simulation Game – Implementation Plan

This plan details the required changes and new files for integrating the "ZETA PROTOCOL" game into the existing Next.js project. The game will simulate a terminal interface with a cyberpunk aesthetic, incorporating multiple puzzle levels, animations (typewriter effects, fake loading screens), and backend integration via mock functions.

---

## 1. Game Entry Point – `/src/app/zeta-protocol/page.tsx`

**Purpose:**  
Serve as the web‐based game’s entry point.

**Steps:**
- Create a new folder: `/src/app/zeta-protocol/`
- Create `page.tsx` inside the new folder.
- Import React, the `Terminal` component (from `/src/components/Terminal.tsx`), and backend methods from `/src/lib/backend.ts`.
- Use React’s `useEffect` to call `backend.initialize()` when the page loads.
- Retrieve saved game state with `backend.getGameState()` and pass it to the game engine.
- Render the `Terminal` component.

---

## 2. Terminal UI Component – `/src/components/Terminal.tsx`

**Purpose:**  
Display a terminal interface mimicking a cyberpunk hacking environment.

**Steps:**
- Create a new file `Terminal.tsx` in `/src/components/`.
- Render a container `<div>` styled with:
  - Black background
  - Green text (e.g., color: `#00FF00`)
  - Monospace font (e.g., using `font-family: monospace`)
- Include a scrollable output area to show game prompts and animations.
- Add a text input field styled as a terminal command prompt. On user input submission, pass the command to the game engine.
- Implement a typewriter effect with React state and `useEffect` for rendering text gradually.
- Integrate fake loading screens and "security breach" animations using CSS animations.
- Ensure error messages are clearly displayed when a command is invalid.

---

## 3. Game Logic – `/src/lib/game.ts`

**Purpose:**  
Implement the core game engine, managing levels, puzzles, and scoring.

**Steps:**
- Create a `game.ts` file in `/src/lib/`.
- Define a game engine object or class that includes:
  - An array of level objects representing puzzles.
  - Functions: `loadLevel(level: number)`, `checkSolution(input: string)`, and `advanceLevel()`.
  - Manage the game score and level progression.
- Use proper TypeScript typing and error handling (e.g., try-catch blocks) in asynchronous functions.

---

## 4. Puzzle Definitions – `/src/lib/puzzles.ts`

**Purpose:**  
Store and define puzzles for each level.

**Steps:**
- Create a file `puzzles.ts` in `/src/lib/`.
- Define an array (or object) of at least 5 puzzle levels:
  - **Level 1:** Caesar cipher decryption
  - **Level 2:** Pattern recognition (e.g., prime number sequence)
  - **Level 3:** Password cracking (simulate brute-force puzzle)
  - **Level 4:** Binary-to-text conversion
  - **Level 5:** Final logic puzzle (firewall breach challenge)
- For each puzzle, include:
  - Puzzle description and instructions
  - Expected solution or a solution checking function
  - Optional hints or feedback messages

---

## 5. Backend Integration – `/src/lib/backend.ts`

**Purpose:**  
Simulate backend calls to initialize, get/save game state, and log game events.

**Steps:**
- Create a file `backend.ts` in `/src/lib/`.
- Export asynchronous functions:
  - `initialize()`: Simulate backend initialization; log to console and return a resolved promise.
  - `getGameState()`: Return a mock game state (e.g., current level, score) as a promise.
  - `logEvent(event: string)`: Simulate logging of an event for gameplay analytics; wrap in try-catch and output errors to console.
- Ensure all functions include error handling to avoid breaking the UI.

---

## 6. Terminal Styling – Update `/src/app/globals.css` (or create new CSS)

**Purpose:**  
Define the cyberpunk terminal aesthetics.

**Steps:**
- Append CSS classes in `/src/app/globals.css` or create a new file (e.g., `/src/app/terminal.css`) and import it.
- Add styles for:
  - `.terminal-container`: Set background to black, color to `#00FF00`, padding, and full-screen dimensions.
  - `.terminal-output`: Scrollable area with fixed height, custom scrollbar styling.
  - `.terminal-input`: Input field styling matching terminal interface (borderless, blinking cursor effect).
- Include CSS keyframe animations for a typewriter effect and fake loading screen transitions.

---

## 7. Windows Build Script – Packaging the Game

**Purpose:**  
Package the production build into a zip file for Windows distribution.

**Steps:**
- Create a file `build_game.bat` (for Windows) in the project root.
- The script should:
  - Run `npm run build` (using Next.js build process).
  - Check the build output for errors.
  - On success, package the build folder into a zip file (using a zip CLI tool available on Windows).
- Provide error handling in the script to ensure the build completes before zipping.

---

## 8. Documentation and Testing Protocol

**Purpose:**  
Provide comprehensive user and developer documentation.

**Steps:**
- Update `README.md` with a new section "ZETA PROTOCOL Game Instructions" explaining game controls (keyboard input), puzzle types, and backend integration.
- Create a new markdown file at `/docs/level-design.md` that describes each level’s puzzle, design rationale, and expected user interactions.
- Add a testing section in `README.md` detailing:
  - How to run the game locally.
  - How to execute the build script.
  - Sample commands to simulate backend calls (using curl if needed for endpoints).
- Ensure that all documentation is clear and concise for both players and developers.

---

## 9. (Optional) AI-Enhanced Hint Feature

**Purpose:**  
Enhance gameplay by allowing players to request hints via an LLM-based API.

**Steps:**
- In `/src/components/Terminal.tsx`, add a “Request Hint” button.
- Create a function (e.g., `fetchHint()`) that:
  - Calls an LLM provider’s API endpoint (e.g., `https://openrouter.ai/api/v1/chat/completions`).
  - Uses model `anthropic/claude-sonnet-4` by default.
  - Sends the current puzzle context and receives a hint.
- Display the hint in the terminal interface with proper error handling if the API call fails.
- Clearly note that this feature is optional and may require an API key from the user.

---

## Summary

- Created a new Next.js route `/src/app/zeta-protocol/page.tsx` as the game entry point.
- Developed a styled terminal component in `/src/components/Terminal.tsx` with animations and input handling.
- Implemented core game logic in `/src/lib/game.ts` and organized puzzles in `/src/lib/puzzles.ts`.
- Simulated backend integration using `/src/lib/backend.ts` with initialization and logging functions.
- Updated global styles in `/src/app/globals.css` to reflect cyberpunk aesthetics.
- Added a Windows build script (`build_game.bat`) for packaging the project as a zip file.
- Enhanced documentation with game instructions and level design details.
- Optionally integrated an AI-based hint feature using an LLM API for enriched gameplay.
