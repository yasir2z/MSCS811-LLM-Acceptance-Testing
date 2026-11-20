# An Agile/XP Framework for LLM-Assisted Acceptance Test Generation from User Stories

**Author:** Yasir Alzahrani  


## Idea

This project proposes a way to use a large language model (Claude) inside an Agile/XP iteration to draft acceptance test cases from user stories, with a human review step before any case is accepted.

## Proposed Agile/XP framework

- **Roles:** the product owner writes the user stories and acceptance criteria. The tester reviews the generated cases. The developer implements against the approved tests. Claude is used as a drafting tool.
- **Placement:** test generation happens between iteration planning and test-first development, so approved acceptance tests are available before coding starts.
- **Review step:** the tester checks each generated case against a five-question checklist, decides to **Accept**, **Revise** or **Reject** it, and records the decision in a review log.
- **Feedback loop:** every assumption or gap that review surfaces goes back to the product owner.

## Repository contents

| Path | Description |
|---|---|
| [report/MSCS811_Report.pdf](report/MSCS811_Report.pdf) | Project report: framework, application, results, discussion, references |
| [evidence/MSCS811_Evidence.pdf](evidence/MSCS811_Evidence.pdf) | Evidence file: materials given to the model, the 42 generated test cases with their IDs, and case-by-case coverage scoring |
| [presentation/MSCS811_Presentation.pptx](presentation/MSCS811_Presentation.pptx) | Six-slide presentation (speaker notes are in Arabic) |

## Method (as executed)

- **Inputs:** 3 hypothetical e-commerce user stories (cash on delivery, discount coupon, stock validation) and 2 prompt packages:
  - **Package A (brief):** asks for test cases briefly.
  - **Package B (structured):** asks for Given-When-Then format, references to acceptance criteria, and positive, negative and boundary cases where they apply.
- **Generation:** Claude (model identifier `claude-fable-5-2`, as reported by the session) on 13 November 2026, in a single conversation. This produced 6 sets of 7 cases: 21 cases per package, **42 cases in total**. There were no repeated runs.
- **Evaluation metrics:**
  - coverage of required behaviour against an 18-condition reference checklist (6 per story)
  - the number of unsupported assumptions

The test cases are written in **natural language**. The application covered generating and evaluating them. No test was executed against a real store.

## Results

| Package | Story 1 | Story 2 | Story 3 | Coverage (of 18) | Unsupported assumptions |
|---|---|---|---|---|---|
| A, brief | 6 | 4 | 6 | 16 (89%) | 0 |
| B, structured | 6 | 6 | 6 | 18 (100%) | 0 |

Package A was not credited with two conditions, S2-C4 and S2-C5. Cases A-S2-5 and A-S2-6 test the expiry rule with correct expected results, but they do not state that no coupon is already applied, which the checklist input requires. This is a difference in documented coverage, not an incorrect test.

## Limitations

- The evaluation is a **preliminary, Claude-assisted assessment**, not an independent human evaluation.
- The reference checklist was available in the generation context, so the two packages and the checklist shared one conversation. The checklist was also drafted with the same model that generated the cases. Scores may overstate quality, and the observed difference cannot be attributed to the packages with confidence.
- One model, three synthetic stories in one domain, and one set per story and package, so run-to-run variation is unknown and the results do not extend to real backlogs.

## How to review this repository

1. Read the report: [report/MSCS811_Report.pdf](report/MSCS811_Report.pdf).
2. Trace the results in the evidence file, [evidence/MSCS811_Evidence.pdf](evidence/MSCS811_Evidence.pdf). Each score in the report links to case IDs (for example A-S2-5) and checklist conditions (for example S2-C4).
3. Review the presentation: [presentation/MSCS811_Presentation.pptx](presentation/MSCS811_Presentation.pptx).

## Use of AI tools

Claude was the object of study. It was also used to draft the study materials, generate and score the test cases, and draft the report. ChatGPT was used to review the study design. The author reviewed the materials and is responsible for the content.
