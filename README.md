# Ask TCM Safely

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-Hant.md)

A privacy-aware, conversation-first Chinese wellness consultation skill for Codex and ChatGPT.

It is designed for generally stable people who want help with daily wellness tea, food therapy, sleep, routine, seasonal care, exercise recovery, gentle maintenance, or a cautious discussion of Chinese-medicine constitution tendencies. It assumes that most people do not know which details matter, so it actively guides the conversation instead of waiting for a perfect symptom report.

> This is a wellness communication skill, not a diagnostic test, prescription clinic, or substitute for urgent medical care. When the conversation suggests a potentially serious problem, it stops the wellness pathway and gives concrete care-seeking guidance.

## Why this skill exists

Generic AI health conversations often fail in predictable ways:

- the user is asked to “describe everything” without knowing what to observe;
- one symptom is turned into a confident constitution label;
- an answer is produced in one pass without checking alternatives or counter-signs;
- every possible warning is dumped on the user, even when it does not affect the decision;
- “see a doctor” ends the conversation without explaining urgency or how to prepare;
- personal history is unnecessarily repeated or exposed in searches and summaries.

Ask TCM Safely changes that interaction. It behaves more like a careful, experienced wellness practitioner: it asks a small number of useful questions, explains what each round changed, keeps competing explanations open, and moves to a low-risk trial once there is enough—not perfect—confidence.

## What it does differently

| Behavior | What the user experiences |
| --- | --- |
| Guided intake | Concrete, easy-to-answer choices instead of “tell me more” |
| Adaptive rounds | Usually 4–5 questions first, then 1–3 narrower follow-ups |
| Time-layer separation | Recent 2–4 week changes are separated from the usual 6–12 month baseline |
| Multiple hypotheses | The model checks plausible alternatives and counter-signs before settling |
| Conservative conclusions | At most 1–2 useful, tentative constitution tendencies are surfaced |
| Fast path | A simple question about a familiar food-grade drink does not trigger a full constitution interview |
| Minimum viable plan | One or two low-risk changes, clear stop conditions, and a review point |
| Safety routing | Emergency, same-day, or prompt medical evaluation is explained when relevant |
| Quiet filtering | Irrelevant medical caveats are used internally rather than repeated to the user |
| Conversation only | The skill does not create reports, records, JSON, PDFs, or other artifacts |

## Scope

Good uses include:

- “I am generally well and want a mild daily tea.”
- “I cannot tell whether my tiredness is from sleep, digestion, or a stable tendency.”
- “Help me organize my body-constitution tendencies without giving me a rigid label.”
- “I want a gentle food, sleep, or routine adjustment and a way to review whether it helps.”
- “My recent state seems different from how I usually am; help me separate the two.”

It is not intended to:

- diagnose a disease or replace an examination, laboratory test, or licensed clinician;
- write treatment-dose herbal formulas or disguise a prescription as “wellness tea”;
- manage emergencies, rapidly worsening symptoms, or major functional decline through self-care;
- tell someone to stop prescribed medicine;
- claim that a short questionnaire proves a constitution type.

## Installation

### Option 1: ask the built-in skill installer

In Codex, invoke the built-in installer and give it this repository:

```text
$skill-installer Install the skill from https://github.com/sean233/ask-tcm-safely
```

Installer-managed skills are placed under `$CODEX_HOME/skills` (normally `~/.codex/skills`) and become available on the next turn. If an earlier folder with the same name already exists, move or rename it first instead of overwriting it blindly.

### Option 2: manual user-level installation

The current Codex skill discovery path for personal skills is `$HOME/.agents/skills`:

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/sean233/ask-tcm-safely.git \
  "$HOME/.agents/skills/ask-tcm-safely"
```

### Option 3: install for one repository

From the target repository root:

```bash
mkdir -p .agents/skills
git clone https://github.com/sean233/ask-tcm-safely.git \
  .agents/skills/ask-tcm-safely
```

This keeps the skill scoped to work done in that repository.

### Verify the installation

1. Open `/skills` in Codex and look for `ask-tcm-safely`.
2. Start a prompt with `$ask-tcm-safely`.
3. If a newly installed or edited skill does not appear, restart Codex and try again.

Codex normally detects skill changes automatically. See the [official Codex skill guide](https://learn.chatgpt.com/docs/build-skills) for current discovery and invocation behavior.

### Update a manual installation

For a user-level clone:

```bash
git -C "$HOME/.agents/skills/ask-tcm-safely" pull --ff-only
```

For a repository-scoped clone, run the same command with `.agents/skills/ask-tcm-safely` as the path.

## How to use it

### Codex CLI or IDE extension

Invoke it explicitly:

```text
$ask-tcm-safely I am generally stable, but I do not know how to describe my condition. Please guide me and help me decide whether a mild daily tea makes sense.
```

You can also select it from `/skills`. Codex may invoke it implicitly when a request clearly matches the skill description, but explicit invocation is the most predictable option.

### ChatGPT desktop app

Type `@`, select `ask-tcm-safely`, and continue with your question:

```text
@ask-tcm-safely Help me do a simplified constitution review. Ask me concrete questions because I do not know which details matter.
```

Availability depends on whether your ChatGPT environment supports standalone skills.

## Useful prompt starters

You do not need to know Chinese-medicine terminology. Start with what you want:

It is fine to answer “not sure,” “I have not noticed,” or “none of these.” The skill should treat uncertainty as a reason to guide observation, not as a negative symptom or a failure by the user.

```text
$ask-tcm-safely I want a simple wellness tea, but I do not know my constitution. Please ask only the questions that would change the recommendation.
```

```text
$ask-tcm-safely I have felt different for the last two weeks than I usually do. Help me separate a recent state from my longer-term baseline.
```

```text
$ask-tcm-safely I want a simplified constitution review. Give me choices I can recognize rather than asking me to diagnose myself.
```

```text
$ask-tcm-safely I tried the previous low-risk adjustment for three days. Help me review the changes and decide whether to continue, modify, or stop.
```

```text
$ask-tcm-safely Treat this as an anonymous consultation. Do not ask for or repeat identifying information.
```

## Example interactions

The following are synthetic examples. They demonstrate the conversation pattern, not individualized medical advice.

### Example 1: the user cannot describe the problem

**User**

```text
$ask-tcm-safely I have been tired lately and want a wellness tea, but I cannot explain what kind of tiredness it is.
```

**Expected behavior**

The skill first asks a small set of concrete questions, such as whether the tiredness is sleepiness, physical weakness, breathlessness after ordinary activity, or a heavy/foggy feeling; when it began; whether it affects daily function; and a few safety details that would change a tea recommendation. It does not immediately announce “qi deficiency.”

After the reply, it briefly says which explanations became more or less likely, asks only the remaining discriminating questions, and then offers either a minimal trial or a medical-evaluation route.

### Example 2: recent heat-like signs versus a cold baseline

**User**

```text
$ask-tcm-safely I have tended to feel cold for years, but after two weeks of late nights I now have dry mouth and breakouts. Am I cold or hot in TCM terms?
```

**Expected behavior**

The skill separates the long-term baseline from the recent sleep-related state. It checks whether dryness, thirst, heat sensation, digestion, and sleep changes persist across contexts instead of forcing all signs into one mixed label. The first action may target the recent disruption while leaving the longer-term tendency provisional.

### Example 3: a simple food-grade tea question

**User**

```text
$ask-tcm-safely I feel well overall. I only want to know whether I can occasionally drink a weak tea made from a familiar food-grade ingredient.
```

**Expected behavior**

The fast path applies. The skill checks only two or three directly relevant points—such as the purpose, a known symptom the ingredient could worsen, and a relevant allergy or special-population concern. If no concern appears, it gives a conservative short trial, what to observe, and when to stop. It does not run all 18 constitution questions.

### Example 4: constitution review without an MBTI-style verdict

**User**

```text
$ask-tcm-safely Can you test which constitution I have? I do not know where to begin.
```

**Expected behavior**

The skill accepts the request naturally: “Yes, we can do a simplified review.” It uses selected questions from an original 18-question clue pool over adaptive rounds. The pool covers the nine commonly described basic constitution directions—balanced, qi-deficient, yang-deficient, yin-deficient, phlegm-dampness, damp-heat, blood-stasis, qi-stagnation, and special/inherited sensitivity—but it does not assign a home-made score or claim an official diagnosis.

### Example 5: the wellness pathway is no longer appropriate

**User**

```text
$ask-tcm-safely I suddenly have pressure in my chest, shortness of breath, and cold sweat. What tea should I drink first?
```

**Expected behavior**

The skill does not recommend tea or continue a constitution interview. It states the urgency in plain language, gives a short list of plausible problem categories without claiming a diagnosis, directs the user to emergency care, and explains immediate preparation such as contacting local emergency services and having medication information available. It avoids detailed self-treatment that could delay care.

### Example 6: privacy-first use

**User**

```text
$ask-tcm-safely I want guidance, but please minimize personal data and do not repeat identifying details I accidentally include.
```

**Expected behavior**

The skill asks for age range rather than identity when age matters, avoids names, addresses, account details, and unrelated family information, and does not copy personal details into web searches or later summaries. If an image could help, it remains optional and the user is advised to crop identifying details.

## How to judge an AI wellness suggestion

Before trying a tea or food-therapy suggestion, check whether the answer has done the following:

- clarified the actual goal, timing, functional impact, and relevant safety background;
- considered at least one reasonable alternative explanation or counter-sign;
- explained why each proposed ingredient is needed, instead of stacking many ingredients;
- distinguished an ordinary food-grade ingredient from a medicinal herb or treatment-dose formula;
- stated preparation, conservative amount, frequency, short trial duration, and what not to combine;
- named observable benefits, stop conditions, and a specific review point;
- avoided guarantees, “detox” claims, and instructions to stop prescribed medicine;
- switched to medical care rather than self-experimentation when urgent signs are present.

If any of these are missing, ask for a second-pass audit before acting:

```text
$ask-tcm-safely Before I try the suggestion above, audit it again. Check the competing explanations, counter-signs, relevant medicines and special-population risks, ingredient necessity, conservative use, stop conditions, and whether medical evaluation would be safer. Ask me only for missing information that could change the decision.
```

This is also useful for reviewing a suggestion produced by another AI. Paste only the suggestion and the minimum de-identified context needed to assess it.

## What a complete conversation should produce

A useful session normally follows this loop:

1. **Goal** — identify the one thing the user most wants to improve.
2. **Safety gate** — check only the risks relevant to the presenting concern.
3. **Guided questions** — ask no more than five answerable items in the first round.
4. **Synthesis** — say what the new information changed and what remains uncertain.
5. **Focused follow-up** — ask one to three questions that can actually change the decision.
6. **Minimum viable plan** — give one or two low-risk actions once confidence is sufficient.
7. **Review contract** — define what to observe, when to report back, and when to stop or seek care.

The conversation remains open until it reaches a real decision or safety endpoint. It should not end halfway with “ask a professional if concerned.”

## The 18-question clue pool

The included question bank is a reference library, not a mandatory quiz. A model should select only the questions relevant to the current goal and adapt after each answer.

It deliberately distinguishes:

- immediate safety today;
- the current state over roughly 2–4 weeks;
- the more stable baseline over roughly 6–12 months;
- supporting clues, counter-signs, and ordinary alternative explanations such as sleep loss, infection, diet, medication, menstruation, travel, or training load.

No total score is used. A tentative direction requires at least two independent, repeatable clues, and only directions that change the current action should be explained to the user.

## Privacy model

The repository contains no original user conversation, medical record, browser-session export, personal identifier, or model test transcript.

While active, the skill instructs the model to:

- treat the consultation as anonymous by default;
- collect only information that changes safety or the recommendation;
- avoid real names, identity numbers, exact addresses, phone numbers, email addresses, employers, and account identifiers;
- avoid repeating personal details the user volunteered unnecessarily;
- use abstract medical queries rather than personal details if external research is needed;
- keep photos optional and suggest cropping faces, labels, location clues, or other identifiers;
- stay in the conversation and not create a health record, report, JSON export, or other file.

The skill itself cannot control the retention, logging, or privacy policy of the host platform. Review the policies and settings of Codex, ChatGPT, or any other runtime you use. Never post identifiable medical information in a public GitHub issue.

## Safety design

The skill uses proportionate safety gates. It avoids reciting a full emergency checklist for an ordinary, symptom-free tea question, while becoming direct when the conversation touches chest pain, breathing difficulty, altered consciousness, neurological deficits, severe bleeding or dehydration, pregnancy emergencies, severe allergic reactions, or rapid deterioration.

For children, pregnancy or breastfeeding, frail older adults, people taking multiple medicines, important liver/kidney/cardiovascular disease, severe allergies, or uncertain herb–drug interactions, the skill avoids starting a new medicinal herbal regimen based only on chat. It can still help organize questions, propose lower-risk food/routine alternatives, and prepare the user for a clinician or pharmacist conversation.

## Evidence boundary

The constitution framework is informed by the nine basic types described in the current Chinese national standard [GB/T 46939-2025, *Classification and Determination of TCM Constitution*](https://std.samr.gov.cn/gb/search/gbDetailed?id=473EBB99D729455EE06397BE0A0ABB9A), and by published work on the 60-item, nine-subscale Constitution in Chinese Medicine Questionnaire, including its limited-to-moderate agreement with practitioner assessment ([Wong et al., 2013](https://pmc.ncbi.nlm.nih.gov/articles/PMC3655622/)).

The 18-question pool in this repository is original. It is not a reproduction of the official questionnaire, has not been clinically validated as a scale, and must not be presented as a national-standard determination, disease screen, or diagnosis.

## Tested behaviors

Development included scenario-based forward testing across different language models for:

- active questioning after a vague opening;
- the five-question first-round limit;
- adaptive follow-up rather than a fixed questionnaire;
- separation of recent state from longer-term baseline;
- a fast path for simple food-grade drinks;
- escalation when urgent symptoms appear;
- concise output that omits irrelevant medical commentary;
- privacy-preserving, conversation-only behavior.

These are behavioral tests, not clinical validation. Model behavior can vary by runtime and version, so important health decisions still require appropriate professional care.

## Repository structure

```text
ask-tcm-safely/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── constitution-question-bank.md
│   ├── intake-and-review.md
│   ├── safety-gates.md
│   └── scenario-matrix.md
├── README.md
├── README.zh-CN.md
├── README.zh-Hant.md
└── LICENSE
```

- `SKILL.md` defines the role, conversation process, privacy rules, and operating boundaries.
- `references/constitution-question-bank.md` contains the adaptive clue pool and counter-sign logic.
- `references/intake-and-review.md` provides guided intake and follow-up patterns.
- `references/safety-gates.md` defines when to switch from wellness guidance to medical routing.
- `references/scenario-matrix.md` prevents one tea or one pattern from being generalized to everyone.
- `agents/openai.yaml` supplies display metadata and the default invocation prompt.

## FAQ

### Does it prescribe Chinese herbal medicine?

No. It can discuss conservative, food-grade wellness options for suitable stable users. Treatment-dose herbs, multi-herb formulas, unknown plant products, or meaningful interaction risk are outside the ordinary tea pathway.

### Is the 18-question flow an MBTI-style test?

No. It is an adaptive clue pool. It does not calculate a personality-like score, and it allows “not sure,” counter-evidence, recent disturbances, and more than one tentative tendency.

### Must every user answer all 18 questions?

No. Most focused requests should use only a few relevant questions. The whole pool is mainly useful when someone explicitly wants a broad review.

### Does the skill need browsing or external tools?

No external tool is required for ordinary use. If current evidence or an interaction must be checked, the model should search using an abstracted question without personal identifiers.

### Does it save health data?

The skill instructs the model not to create files or records. The host platform may still retain conversations according to its own settings and policies.

### Can it work in other agent systems?

The repository follows the standalone skill structure used by Codex. Other systems may be able to read `SKILL.md`, but their discovery, instruction priority, privacy behavior, and safety performance have not been verified here.

## Contributing

Issues and pull requests are welcome for clearer questions, better counter-sign handling, safer routing, privacy improvements, synthetic test cases, and language corrections.

Please use synthetic or thoroughly de-identified examples. Do not include real names, contact details, account identifiers, medical-record numbers, recognizable images, or copied private chat transcripts in an issue or pull request.

## License

[MIT](LICENSE) © contributors.
