# lab-grader-preview

A student-facing skill that estimates a lab grade and explains how to improve the work before submitting. It uses the grading standards of [lab-grader](https://github.com/vanderbilt-ai-studies/lab-grader), without the submission-processing or LMS workflow.

The preview includes rubric scores, a reason for each deduction, specific revision advice, and short tutorials when the work reveals a conceptual misunderstanding. When course notes are available, it points to the relevant day and section. The estimate is not an official grade.

## What you need

Give the assistant the **filename or path of your lab writeup**, plus:

1. Assignment instructions.
2. Grading rubric, with point totals and scoring levels.

Include instructor guidance or clarifications if you have them. The skill asks whether guidance is available, but **guidance is not required**: it can estimate a grade from the assignment and rubric alone. It notes when guidance was unavailable and can revise the estimate if you supply it later. Missing guidance does not cost you points.

Your instructor provides the assignment and rubric. The skill will ask for either missing required document rather than invent grading rules. Course notes are optional but enable specific study references. Screenshots and other evidence that belong to your writeup should also be accessible.

A simple folder arrangement is:

```text
my-lab/
├── my-lab-writeup.pdf
└── grading-documents/
    ├── assignment.md
    ├── rubric.md
    ├── instructor-guidance.md  # optional
    ├── calibration.md          # if supplied/referenced by the instructor
    └── notes/                 # optional course notes
```

These filenames and formats are examples. The documents may be PDFs, Markdown, or other formats your assistant can read. They may be in another directory if you give its location. A single document containing clearly identified assignment and rubric sections, with guidance if available, is also fine.

## Use it

Clone this repository or download its source ZIP:

```sh
git clone https://github.com/vanderbilt-ai-studies/lab-grader-preview.git
```

Install the folder containing `SKILL.md` using your assistant's skill installer. If your assistant can read local files but does not install skills, tell it to read and follow that `SKILL.md` explicitly. Give the assistant access to your lab directory, then ask:

> Use $lab-grader-preview to preview `my-lab-writeup.pdf`.

If the documents are elsewhere:

> Use the lab-grader-preview skill to preview `/path/to/my-lab/writeup.pdf`. The assignment and rubric are in `/path/to/course/lab-02/grading-documents/`. I do not have additional instructor guidance.

The preview appears in the conversation. The skill does not modify your writeup, create grading files, download submissions, anonymize files, export packets, or post to Brightspace. If it cannot inspect a screenshot or linked evidence, it identifies the uncertainty instead of treating that evidence as missing work.

## How it matches lab-grader

[SKILL.md](SKILL.md) preserves the core grading rules:

- Apply the supplied rubric and explicit instructor clarifications.
- Check each deduction against the requirement, evidence, point level, and possible double counting.
- Credit valid alternatives and reasoned choices without inventing extra tests or mandatory vocabulary.
- Honor confirmed interface limitations and distinguish missing work from inaccessible evidence.
- Give concrete feedback and concept help with verified course-note references.

For the closest model match, use Sol at medium reasoning or Sonnet with medium thinking where supported. A supported agent environment can use a fresh grading worker followed by a coordinator check. Otherwise, the skill provides a direct preview and discloses its review basis. It does not promise the same score as the instructor: document versions, accessible evidence, model behavior, and instructor judgment can differ.

The initial grading rules were adapted from lab-grader revision [`d06076d`](https://github.com/vanderbilt-ai-studies/lab-grader/commit/d06076d00111565ceacb5de5a1162ce165943499). This skill is self-contained; installing lab-grader is not required. When updating it, compare the grading and feedback rules with the upstream skill. Keep assignment-specific decisions in instructor guidance. Cohort calibration pilots, private identity processing, batch operations, and official grade publication belong to the instructor workflow.

## Edit and suggest improvements

Edit `SKILL.md` to change the preview's behavior. `agents/openai.yaml` supplies the display name and suggested starting prompt for compatible hosts.

Students and TAs are welcome to suggest wording improvements through issues or pull requests. Explain what would make a preview clearer, fairer, or more useful; use synthetic examples. Keep real writeups, grades, names, and individual grading disputes out of this public repository and its issues. Store your own work in a separate lab directory.
