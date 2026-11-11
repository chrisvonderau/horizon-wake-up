# Horizon: Wake Up — test report

Run in headless Chromium (Playwright 1.49, Chromium 131) against the built page, over HTTP and over `file://`. The page was the real game, with `?test=1` only so the harness could reach later levels and read state. No Mac Safari, iPad, physical pad, speaker, or human playthrough was available here.

A case-insensitive search of `HorizonWakeUp.html` and `index.html` (they are byte-identical) found no email addresses, no personal names, and no local filesystem paths. The letters "matrix" occur only as Three.js transform fields such as `this.matrix` and `mat4 matrix` in the inlined library. They are not a title, and no character names or quoted lines from a famous 1999 film are present.

Boot logged no console errors and no page errors. Chromium did print a Three.js warning that WebGL 1 is deprecated in this library version. That warning was not treated as a test failure.

| Check | Result | Notes |
| --- | --- | --- |
| Boot, no console errors | PASS | Title reached, harness ready, no console errors or page errors. |
| No network requests besides the document | PASS | HTTP load requested only the HTML document. |
| Start a run | PASS | Clicked through Press A to start, then Play. Level 1 entered. |
| Movement | PASS | Holding W moved Horizon forward relative to the camera. |
| Strikes and combos | PASS | Three light strikes on a monitor. Combo reached 3. Health fell from 86 to 1. |
| Focus slowing time | PASS | Full Focus pressure set time scale to 0.13 and drained the meter. Releasing it restored time scale to 1. |
| Dodge | PASS | Dodge unlocked on level 2. A roll started and a point-blank enemy shot did not reduce health. |
| Code Sight | PASS | Level 3 opened in wireframe. Toggled off, then back on. Wireframe followed the toggle. |
| Stop dropping bullets | PASS | A live shot became held, then fell. One landing chime was counted. |
| Return damaging enemies | PASS | A returned shot hit a monitor. Health fell and the return-hit counter increased. |
| Unlock of each power per level | PASS | Focus, Dodge, Code Sight, Stop, and Return each started locked on their level and were set by that level's unlock beat. |
| Completing each level | PASS | Levels 1 through 5 reached the clear screen after their encounters were defeated through the combat damage path. |
| Principal boss phases and win | PASS | Phase 1, then phase 2 with a 20-shot volley, then phase 3, then the win screen. Damage used the real hit function so the phase changes could be reached in the harness. |
| Health and death/checkpoint | PASS | After walking forward, a lethal hit rewound Horizon to the checkpoint with health restored. Death count increased. |
| All difficulties | PASS | The same 25-point hit removed 13.75 health on Easy, 25 on Normal, and 36.25 on Hard. |
| Save/load surviving a reload | PASS | Blood off, Hard, and Low graphics were still set after reload. Clearing level 1 left level 2 unlocked after another reload. |
| Blood toggle | PASS | A hit with blood on counted a red burst. With blood off, the same hit counted only a green glyph burst. |
| Simulated standard gamepad with analog RT | PASS | Injected `navigator.getGamepads` standard pad. Light RT pressure time scale about 0.45. Hard RT pressure about 0.15. |
| Rumble call | PASS | `vibrationActuator.playEffect('dual-rumble')` was invoked for an incoming shot. |
| Missing or throwing actuators | PASS | A pad with no actuator, one whose `playEffect` throws, and one that returns a rejected promise did not cause a page error. |
| Simulated second gamepad for co-op | PASS | Second pad took Vesper. Vesper moved on stick input. Pixel and Lumen stayed AI. |
| Touch controls | PASS | On-screen stick moved Horizon. The light button started a swing. |
| speechSynthesis present | PASS | A line was spoken. Pixel's pitch was about 1.45 and the rate about 1.24. The same line was on screen. |
| speechSynthesis absent | PASS | With `speechSynthesis` forced missing, the game still showed a subtitle and did not throw. |
| file:// boot | PASS | Opened the HTML by file URL. One document request, canvas had WebGL, no errors. |
| Resizing | PASS | Viewport 1100×640 and then 390×844. The renderer followed both. |
| Pause on hide | PASS | After `visibilitychange` with `document.hidden` true, Horizon stopped moving while a move key was held. |
| Real Mac Safari | NOT TESTED | No Mac Safari in this environment. |
| Real iPad | NOT TESTED | No iPad in this environment. |
| Physical Xbox 360 pad | NOT TESTED | No physical controller. The pad tests used an injected standard gamepad. |
| Rumble motor | NOT TESTED | The rumble API was called. No motor hardware was attached. |
| Human listening to audio and voices | NOT TESTED | Music, hits, and speech were not listened to by a person. |
| Human 30-minute playthrough | NOT TESTED | No person played a full run. Normal is tuned so a learning run is about half an hour. |
| Case-insensitive grep for personal names, emails, and local paths | PASS | No emails, no personal names, and no local filesystem paths in the shipped HTML. See the note above about Three.js `matrix` fields. |
