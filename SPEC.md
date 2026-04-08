# Die With Zero — Card Game

Build a complete single-player browser card game as a single `index.html` file 
with embedded CSS and JS. No frameworks, no build tools, no npm. Just one file 
that opens in a browser.

## Start here
1. Create `index.html` with the full game
2. Open it and verify it renders correctly
3. Test all three screens: splash, game, end screen
4. Fix any bugs found during testing

## Core mechanics to implement

### Hidden death
Generate a secret death turn at game start (Normal: 12–20, Hard: 8–16, Brutal: 
6–14). Never show the exact number. Show a vitality bar that decreases but hides 
the endpoint. Near death, show random warning messages — some must be false 
positives.

### Life windows
Split life into 3 phases based on % of hidden lifespan:
- Young (0–35%): XP ×1.5, all adventure cards available
- Active (35–65%): XP ×1.1–1.3, most cards available  
- Late (65–100%): adventure cards LOCKED with overlay, XP ×0.5–0.7

Show animated banner when entering new window. Cards show colored top stripe 
by window (gold/green/blue). Locked cards show 🔒 overlay.

### Dormant money penalty
If player ends turn with money > threshold and played no experience that turn:
- Increment dormant streak
- Next turn start: apply XP penalty = base × streak
- Normal: threshold $9k, penalty 12 XP/streak
- Show orange warning banner when active
- Playing any experience resets streak to 0

## Card types
- Experience (gold): cost money, give XP, window-restricted
- Job (green): give salary each turn, passive effects
- Fate (purple): auto-attack player each turn, not playable by player
- Legacy (blue): powerful, end-game effects
- Challenge (red): high risk/reward

## DwZ Score
score = (money_spent_ratio × 50) + (xp_ratio × 50) − dormant_penalty_score
Grades: S≥90, A≥75, B≥60, C≥45, D<45

## UI specs
- Mobile-first, max-width 500px
- Base font-size: 16px (everything in rem from here)
- Cards: 96×138px minimum
- Action buttons: minimum 44px height
- Fonts: Cinzel (headers), EB Garamond (body), DM Mono (stats) from Google Fonts
- Dark palette: background #0b0906, gold #c9a84c/#e8c97a

## Animations required
- Floating particles on splash screen
- Cards slide in when drawn (staggered)
- XP floater animates upward when gained
- Money floater (green/red) on balance changes  
- Vitality bar color shifts green→orange→red
- Death screen: dramatic full-screen takeover
- Window transition: centered overlay banner

## Screens
1. Splash — title, difficulty picker, start button
2. Setup — name, archetype (4 options), difficulty confirmation
3. Game — HUD, vitality bar, fate zone, card table, hand, action bar
4. Death overlay — dramatic death moment before results
5. End screen — DwZ score, grade, window breakdown, objectives, top memories

## After building
- Run `open index.html` to verify in browser
- Check mobile viewport renders correctly
- Verify all 5 card types work
- Verify death triggers correctly
- Verify window transitions fire
