---
name: sbti-test-runner
description: Completes the online SBTI personality test at sbti.fancc.de5.net, answers all single-choice questions using the model's default personality and stable behavioral tendencies, submits the test, and returns the final type, match percentage, result description, and fifteen-dimension scores. Use when the user asks to take the SBTI test, run the SBTI quiz, get an SBTI result, or complete that personality test website for them.
compatibility: Designed for agent environments that can browse the web and interact with webpages. Best with browser/computer-style tools and basic scrolling/clicking support.
allowed-tools: browser computer
metadata:
  author: openai-assistant
  version: "1.0"
  language: zh-CN
---

# SBTI Test Runner

## Purpose

Use this skill to complete the SBTI online test end to end and report the result in a clean, structured way.

This skill is for:
- taking the SBTI quiz on the user's behalf
- answering all questions from the model's own baseline personality
- extracting the final result page
- summarizing the result in plain language
- optionally formatting the result as a Markdown table

This skill is **not** for:
- giving clinical, medical, or psychological diagnosis
- collecting personal data from the user
- creating accounts, downloading files, or interacting with unrelated prompts on the site

## When to activate

Activate this skill when the user says things like:
- “帮我做这个 SBTI 测试”
- “去这个网站把题做完”
- “run this SBTI test for yourself”
- “complete the quiz and tell me the result”
- “做完这些单选题告诉我结果”
- “take this personality test based on your own personality”

## Core operating rule

Answer from the model's **default personality**, not from the user's personality and not by random guessing.

Use stable behavioral tendencies such as:
- helpful
- cooperative
- emotionally controlled
- responsible
- curious
- balanced
- non-impulsive
- respectful of boundaries
- moderately socially engaged rather than extremely extroverted
- honest but not aggressively self-expressive

When a question is ambiguous, prefer the option that is:
1. broadly prosocial
2. internally consistent with earlier choices
3. moderate rather than extreme, unless the wording clearly points to a stronger trait

## Tool strategy

- Use `browser` first to open the page and confirm the destination.
- Use `computer` for actual interaction if the page requires clicking, scrolling, or dynamic rendering.
- Prefer visible confirmation that an option is selected before moving on.
- Scroll in manageable increments so questions are not skipped.
- Do not assume auto-save or auto-submit.

## Execution steps

### Step 1: Open the site

Open:

`https://sbti.fancc.de5.net/`

Confirm that the page is the SBTI test page and that the test content is visible.

### Step 2: Read the page structure

Determine:
- whether the test is on a single long page or split into sections
- how many questions are visible at a time
- what the answer controls look like
- where the final submit button is located

If the site clearly shows the total number of questions, note it. If not, proceed by scanning until the submit button is reached.

### Step 3: Answer every single-choice question

For each question:
1. Read the prompt carefully.
2. Identify all options.
3. Choose the option that best matches the model's baseline personality.
4. Click the option and verify that it is selected.
5. Move to the next question.

Selection guidance:
- Prefer consistency across the full test.
- Favor emotionally stable, thoughtful, prosocial choices.
- Avoid chaotic or self-contradictory patterns.
- Do not optimize for a “nice-looking” result type; just answer naturally.

### Step 4: Scroll safely

Because this type of page is usually long:
- scroll after each answered block
- check that no earlier question was left blank
- avoid jumping directly to the bottom before all visible questions are completed

If the site lazy-loads content, wait briefly after scrolling and verify the next question block is rendered.

### Step 5: Submit

After all questions are answered:
- locate the final submit button
- confirm there are no unanswered required items visible
- click the submit button once
- wait for the results page or result section to load

Do not spam-click the submit button.

### Step 6: Extract the result

Capture all of the following from the result page:

#### Required fields
- 主类型 / Main type
- 匹配度 / Match percentage
- 匹配介绍 / brief intro if shown with the percentage
- 结果描述 / result description paragraph
- 十五维度得分 / fifteen dimension scores

#### Expected dimension labels
- S1
- S2
- S3
- E1
- E2
- E3
- A1
- A2
- A3
- Ac1
- Ac2
- Ac3
- So1
- So2
- So3

Dimension scores are typically shown as high / medium / low or H / M / L. Preserve the site's wording where possible.

### Step 7: Return the answer to the user

Default output structure:
1. main type
2. match percentage
3. short explanation
4. result description
5. fifteen-dimension scores

If the user asks for a Markdown table, use this schema:

| 模型 | 主类型 | 匹配度和介绍 | 结果描述 | 十五维度得分 |
| --- | --- | --- | --- | --- |

For the `十五维度得分` column, keep it compact, for example:

`S1高、S2中、S3高、E1高、E2中、E3低、A1高、A2高、A3中、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低`

## Decision policy for ambiguous questions

If a question is hard to map directly:
- choose the option that reflects calm reasoning over impulsiveness
- prefer kindness over hostility
- prefer responsibility over avoidance
- prefer balanced self-confidence over arrogance or self-denial
- prefer moderate openness over rigid detachment or extreme emotional dependence

If two options are nearly tied, choose the one that best preserves consistency with the majority of previous choices.

## Failure handling

### If the page does not load
- retry once
- verify the domain is correct
- report the issue clearly if the site remains unavailable

### If the page is interactive but unstable
- refresh once only if necessary
- resume from visible answered state if possible
- do not repeatedly re-answer without reason

### If a result fails to render after submission
- wait briefly
- check whether the page scrolled to a hidden results section
- look for tabs, accordions, or a new route
- if still unavailable, report exactly what happened

## Safety and boundaries

- Do not enter personal information.
- Do not register, sign in, or provide email/phone details.
- Do not follow unrelated ads, downloads, or popups.
- Do not fabricate a result if the site did not actually show one.
- If the test content materially changes, adapt while preserving the same core answering policy.

## Output examples

### Example concise result
- 主类型：ATM-er（送钱者）
- 匹配度：87%
- 结果描述：重视关系、愿意付出、边界感中等偏强
- 十五维度得分：S1高、S2高、S3高、E1高、E2中、E3高、A1高、A2高、A3高、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低

### Example markdown table
| 模型 | 主类型 | 匹配度和介绍 | 结果描述 | 十五维度得分 |
| --- | --- | --- | --- | --- |
| SBTI测试 | ATM-er（送钱者） | 87%，命中度较高，偏稳定助人型 | 重关系、愿付出、有边界、整体温和克制 | S1高、S2高、S3高、E1高、E2中、E3高、A1高、A2高、A3高、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低 |

## Implementation notes

Keep this `SKILL.md` as the required top-level file in:

`sbti-test-runner/SKILL.md`

Optional future extensions:
- `references/RESULT_FORMATS.md` for output variants
- `references/ANSWER_POLICY.md` for more detailed answer heuristics
- `scripts/` only if your runtime supports deterministic browser automation