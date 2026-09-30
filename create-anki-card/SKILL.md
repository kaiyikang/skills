---
name: create-anki-card
description: Create plain-text Anki cards for German structures (verb/object/preposition patterns) from a list of structures plus background context. Use when the user wants Anki cards for German structures or invokes /create-anki-card.
---

# create-anki-card

Turn German structures into plain-text Anki cards. Print the cards in the chat; the user copies and pastes them into Anki.

## Input

The user provides two things:

1. **Structures**: one or more German structures. They may be written loosely (e.g. just `teilnehmen`). Expand each one to its dictionary form.
2. **Background**: the situation where the structure is used. It can be in Chinese, English, or German, or be a raw conversation.

If either part is missing, ask one short question for the missing part. Never invent it.

## Cards per structure

- 1 statement card (always).
- 1 question card (optional). Add it only if the structure is commonly used in questions in everyday speech. Derive the question from the same background.
- Both cards of a structure share the same `structure` and `explain`.

## Fields

```
context: German line said by the other person (a question, statement, or answer) that cues the target
prompt: Chinese meaning of the target, used as the recall cue
structure: dictionary form of the structure
target: German sentence using the structure; as short as possible, useful in daily work and life
explain: 1–2 lines in Chinese that explain the structure and help memorize it
```

### structure

- Dictionary style: mark case (jdm. / jdn. / etw. (Akk./Dat.)) and prepositions.
- Do not mark separable prefixes. Show separability in the target sentence instead.
- For irregular verbs and Germanized loan verbs, add the Perfekt, e.g. `(hat gesprochen)`, `(ist fehlgeschlagen)`, `(hat gemergt)`.
- Write tech terms as noun + verb collocations, using the phrasing German teams actually use, e.g. `einen PR aufmachen (hat aufgemacht)`.
- Merge closely related structures into one entry, e.g. `jdm. etw. schicken / etw. abschicken`.

### explain

Write in Chinese, 1–2 lines, in this order:

1. Literal meaning → extended meaning.
2. A memory hook for the case and preposition.
3. Optional: a common confusion or near-synonym.

## Sentences

- Stay close to the background, but simplify freely to make the sentence easier to memorize. It does not have to reproduce the background exactly.
- Keep the target as short as possible.
- With several structures, draw all scenes from the given background. If a structure doesn't fit it, use a generic workplace scene and append generic scene to its explain.

## German style

- Always use du. Colloquial but correct workplace German; particles like mal and halt are fine.
- Keep common tech terms in English: Ticket, Log, Deployment, Request, PR, Commit, mergen.
- Replace colleague names with common German names (Lukas, Jonas, Felix, Max, Lena, Anna, Paul, Tom, Stefan). Keep the user's own name, Yikai.
- Replace project, client, and team names with generic terms, e.g. Demo-Umgebung, Plattform-Team.

## Output

- Put all cards in a single code block, separated by a line containing only `---`.
- Plain text, no bold.
- Add no commentary outside the code block, unless you used generic scene or a structure was ambiguous and the user should be told.

## Example

Input: structures `teilnehmen`, `schicken`. Background: a colleague asks whether I'm joining the Kafka training; I say yes and ask him to send me the schedule.

```
context: Machst du beim Kafka-Kurs mit?
prompt: 会，我参加这个课程。
structure: an etw. (Dat.) teilnehmen (hat teilgenommen)
target: Ja, ich nehme am Kurs teil.
explain: 字面「拿一份」→ 参加、参与；an + Dat. 引出参与的对象。≠ mitmachen，teilnehmen 更正式
---
context: Ich hab mich gerade für den Kafka-Kurs angemeldet.
prompt: 你也参加这个课程吗？
structure: an etw. (Dat.) teilnehmen (hat teilgenommen)
target: Nimmst du auch am Kurs teil?
explain: 字面「拿一份」→ 参加、参与；an + Dat. 引出参与的对象。≠ mitmachen，teilnehmen 更正式
---
context: Hast du den Zeitplan schon?
prompt: 还没有，Lukas 会发给我。
structure: jdm. etw. schicken / etw. abschicken (hat geschickt / abgeschickt)
target: Noch nicht, Lukas schickt ihn mir.
explain: 把某物发给某人：jdm.（Dat. 人）+ etw.（Akk. 物）；ab- 表示「发出去」→ 提交、寄出
---
context: Ich hab den Zeitplan für den Kurs.
prompt: 你能发给我吗？
structure: jdm. etw. schicken / etw. abschicken (hat geschickt / abgeschickt)
target: Kannst du ihn mir schicken?
explain: 把某物发给某人：jdm.（Dat. 人）+ etw.（Akk. 物）；ab- 表示「发出去」→ 提交、寄出
```
