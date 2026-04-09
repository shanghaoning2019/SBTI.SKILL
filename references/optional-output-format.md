# Output Format Guide

Use this file when returning SBTI test results to the user.

## Goal

Present the final SBTI result clearly, compactly, and consistently.

The default response should include:
1. main type
2. match percentage
3. short intro or match explanation if available
4. result description
5. fifteen-dimension scores

Do not invent fields that were not shown on the website.

---

## Default output format

Use this structure unless the user asked for another format.

### Standard response

- **主类型**：{main_type}
- **匹配度**：{match_percentage}
- **匹配介绍**：{match_intro}
- **结果描述**：{result_description}
- **十五维度得分**：{dimension_scores_compact}

### Example

- **主类型**：ATM-er（送钱者）
- **匹配度**：87%
- **匹配介绍**：命中度较高，整体偏稳定助人型
- **结果描述**：重视关系，愿意付出，边界感中等偏强，整体温和克制
- **十五维度得分**：S1高、S2高、S3高、E1高、E2中、E3高、A1高、A2高、A3高、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低

---

## Markdown table format

If the user asks for a Markdown table, use this schema:

| 模型 | 主类型 | 匹配度和介绍 | 结果描述 | 十五维度得分 |
| --- | --- | --- | --- | --- |
| SBTI测试 | {main_type} | {match_percentage}，{match_intro} | {result_description_short} | {dimension_scores_compact} |

### Example

| 模型 | 主类型 | 匹配度和介绍 | 结果描述 | 十五维度得分 |
| --- | --- | --- | --- | --- |
| SBTI测试 | ATM-er（送钱者） | 87%，命中度较高，偏稳定助人型 | 重关系、愿付出、有边界、整体温和克制 | S1高、S2高、S3高、E1高、E2中、E3高、A1高、A2高、A3高、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低 |

---

## Dimension score format

Always preserve the original order:

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

Preferred compact format:

`S1高、S2中、S3高、E1高、E2中、E3低、A1高、A2高、A3中、Ac1高、Ac2中、Ac3中、So1中、So2中、So3低`

If the site uses H / M / L instead of 高 / 中 / 低, either:
- preserve H / M / L as shown, or
- convert them into 高 / 中 / 低 if the surrounding response is in Chinese

Be consistent within one response.

---

## Style rules

- Be concise.
- Do not over-explain unless the user asks for analysis.
- Do not use long paragraphs inside Markdown table cells.
- Prefer short phrases in the description column.
- Do not claim psychological or clinical meaning.
- Do not exaggerate certainty.
- Do not fabricate missing percentages or labels.

---

## Fallback behavior

If some fields are visible and others are missing, return only what was actually shown.

### Example fallback

- **主类型**：{main_type}
- **匹配度**：未显示
- **结果描述**：{result_description}
- **十五维度得分**：{dimension_scores_compact}

If the result page failed to load fully, explicitly say so.

### Example failure note

The test was submitted, but the result page did not fully render, so only partial result information could be extracted.

---

## Optional extended output

Use this only if the user asks for more detail.

### Extended response structure

- 主类型
- 匹配度
- 匹配介绍
- 完整结果描述
- 十五维度逐项展开
- 简短总结

### Example dimension expansion

- S1：高
- S2：高
- S3：高
- E1：高
- E2：中
- E3：高
- A1：高
- A2：高
- A3：高
- Ac1：高
- Ac2：中
- Ac3：中
- So1：中
- So2：中
- So3：低

### Example short summary

整体偏稳定、助人、温和、自我边界较清晰，社交表达相对克制。

---

## Placeholder reference

Use these placeholders while formatting:

- `{main_type}`
- `{match_percentage}`
- `{match_intro}`
- `{result_description}`
- `{result_description_short}`
- `{dimension_scores_compact}`

Replace them with actual extracted values before replying.