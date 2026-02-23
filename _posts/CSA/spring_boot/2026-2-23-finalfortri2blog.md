---
title: Reflection Blog for Trimeter 2 CSA 
layout: post
type: hacks
comments: true
courses: {csa: {week: 20}}
type: ccc
---

## Improved the Dialogue System + AI NPCs

# Incorporate AI NPC History Professor with Dialogue System, Typewriter, Voice, and Full-Stack Gemini Integration

## Summary

This issue documents the integration of a fully functional AI NPC, specialized as a History Professor, into the game. The implementation spans both frontend and backend, and includes:

1. **Dialogue System Integration**
2. **Typewriter Text Effect**
3. **Voice / Speech Synthesis**
4. **Full-Stack Backend Integration with Gemini API for AI Responses**

---

## Work Completed

### Frontend Enhancements

- Integrated `DialogueSystem` for NPC interactions.
- Added typewriter effect for AI response text.
  

**Commits (Frontend):**

- [Dialogue system and typewriter integration](https://github.com/Frogpants/gamers/commit/4a6be3377c0f13e3f4b2673a492dd3d6685f074c)
- [Voice synthesis for NPC responses](https://github.com/Frogpants/gamers/commit/821b6598f36b8fe7c727854e273754fc3627265d)
- [Enhanced dialogue interaction and UI improvements](https://github.com/Frogpants/gamers/commit/dfbf68928f93c18769c2ff8c5978683921e33656)
- [Current commit](https://github.com/Frogpants/gamers/commit/5ca7bfd3aeb72c48fc60abf21c19f650603d98d8)

### AI NPC History Professor

- Implemented an AI NPC system + an example sprite who is a History Professor.
- Supports user prompts, chat history, and example knowledge topics.


**Commits:**

- [Frontend](https://github.com/Frogpants/gamers/commit/60cc74f55aea97ecf2512aaad1f666f4b57867c3)
- [Backend](https://github.com/SoniDhenuva/gamers_flask/commit/02cc85a01d5a2a4663549d497c9dda075ea689a0)
- [Fallback Backend](https://github.com/SoniDhenuva/gamers_flask/commit/18d116292f13ccbd3d6651ab4e638519917f5fdd)

**Notes:**

- The backend uses **Flask** to handle AI requests securely with environment-stored Gemini API keys.
- This is a **full-stack implementation**, unlike previous local or mock AI NPC interactions.
- A pull request was created for the backend to merge these changes.

---

## Planning

- [Flowchart](https://github.com/Frogpants/gamers/issues/13)
- [Burn Down List / Testing](https://github.com/Frogpants/gamers/issues/42)

## Feedback

- [Crossover Reviews — Team](https://github.com/Frogpants/gamers/issues/28)
- [Crossover Reviews — Individual](https://github.com/SoniDhenuva/SONIDHENUVABLOG/issues/9)

---

## Video Demo

<video src="https://github.com/user-attachments/assets/0b9d0bab-dd85-4b78-94f4-c1f2e44cecb0" controls></video>

## Analytics
<img width="280" height="204" alt="Image" src="https://github.com/user-attachments/assets/103b4b14-1689-4f9d-ba7b-b5b4a3474741" />