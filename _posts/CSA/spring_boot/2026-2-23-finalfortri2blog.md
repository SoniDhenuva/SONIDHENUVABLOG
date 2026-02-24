---
title: Reflection Blog for Trimeter 2 CSA 
layout: post
type: hacks
comments: true
courses: {csa: {week: 20}}
type: ccc
---



# Incorporate AI NPC History Professor with Dialogue System, Typewriter, Voice, and Full-Stack Gemini Integration

## Analytics
<img width="927" height="575" alt="Image" src="https://github.com/user-attachments/assets/02d4b8e8-9356-4817-82fd-9c8567cb4d9d" />

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

## MCQ

<img width="1272" height="82" alt="Image" src="https://github.com/user-attachments/assets/b407eb76-d34a-4fe6-ad29-8e680aa995a8" />

<img width="1580" height="700" alt="Image" src="https://github.com/user-attachments/assets/72f65c6a-05b0-44be-b76a-dd2d50f9eb85" />

## What I Did Well

* **Object-Oriented Logic:** My high scores in Units 1 and 3 show I understand how classes are structured, how to instantiate objects, and how to call methods.
* **Syntax:** I’m not making basic Java writing mistakes — my errors are mostly in **code tracing**.
* **Pacing:** I’m moving through MCQs at a good speed.


<img width="1043" height="727" alt="Image" src="https://github.com/user-attachments/assets/96a05562-e2ee-42ac-9205-de9b7768e68d" />

### ArrayList Methods

**Error:** I chose `[2, 3, 2, 1]` instead of `[2, 0, 2, 1]`.

**Key Idea:**

* `set(index, value)` → replaces
* `add(index, value)` → shifts

I forgot that `set(0, 2)` **replaces** the value rather than moving it.

<img width="1577" height="639" alt="Image" src="https://github.com/user-attachments/assets/f5d10cf1-c410-47be-bf57-c3992b818b48" />

<img width="1058" height="520" alt="Image" src="https://github.com/user-attachments/assets/97ed55ca-6d01-4441-8b36-c14259b1bdbf" />

<img width="1028" height="615" alt="Image" src="https://github.com/user-attachments/assets/e4488fae-076c-41e7-961e-58bb78c64825" />

<img width="1002" height="600" alt="Image" src="https://github.com/user-attachments/assets/48761837-2cba-4c9c-8723-7ed5c6ce034d" />

### Loop Logic

**Error:** I confused `i < m*n` with nested loop behavior.

**Key Idea:**
The inner loop ran **n − 1 times**, so total executions =
[
m(n - 1) = mn - m
]

I also missed an **infinite loop** case: if `i++` is inside an `if` that doesn’t run, `i` never changes and the loop runs forever.

<img width="1554" height="433" alt="Image" src="https://github.com/user-attachments/assets/85217a0d-b390-4ceb-adef-08f7dc7e82a6" />

<img width="494" height="487" alt="Image" src="https://github.com/user-attachments/assets/51e1654f-c06f-48ad-9e51-d9795af852b8" />

<img width="1087" height="489" alt="Image" src="https://github.com/user-attachments/assets/075e94e6-eb98-4168-8ae3-9bfd1a5a3c7a" />



### Indexing & Tracing

**Error:** I chose the first item instead of the second.

**Key Idea:**
Java uses **zero-based indexing**:

* `get(0)` = first item
* `get(1)` = second item

I forgot that `cList.get(1)` refers to the **second** element.

# FRQ 
- [2024 FRQ 2](https://github.com/SoniDhenuva/soni_2025/issues/30)
- [2016 FRQ 3](https://github.com/SoniDhenuva/SONIDHENUVABLOG/issues/12)
- [2019 FRQ 4](https://github.com/Frogpants/gamers/issues/45)
- [2025 FRQ 1](https://github.com/SoniDhenuva/SONIDHENUVABLOG/issues/13)






