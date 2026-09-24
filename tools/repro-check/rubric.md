# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| complex-prose | log, comment body | 12th grade reading level or less. Easy English that a high school student can understand. Industry standard technical jargon is acceptable. Avoide corporate buzzwords. | Required |

| punctuation-check | log, comment body | Free of standard AI formatting tropes: No inline emojis. No em-dashes (`—`). No decorative arrows (`->`). No superficial opening/closing pleasantries such as "Thanks for raising this!". No frequent use of acronyms. No ASCII art. | Required |

| symptom-alignment | output excerpt read against the issue's description | The actual output or error trace produced in the report matches the specific bug reported in the original issue ticket, rather than an unrelated build or syntax error. | Required |

| syllable-check | comment body | The number of syllables in any one word in the comment.  There should be no more that 5 syllables in any one word. The comment should be concise. | Preferred |

| tone-check | comment body | Communicates professionally and directly. No begging.  No threatening.  No demanding. | Preferred | 

| tools-record | repro report's environment record | The Environment is reproducible.  The report names the libraries and tools used.  The report lists of the version of the libraries and tools.  The report lists the OS used. | Required |

| traceable-proof | log, comment body | Reproduction steps are provided. Could someone unfamiliar with this project re-run the steps accurately.  Detailed information is given about libraries, tools, and specs. | Required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

**Verdict Determination:** 
  - An issue receives an **`accept`** verdict if and only if **all required checks pass**.
  - If any required check evaluates to **`fail`** or **`unclear`**, the verdict is deterministically **`reject`**.
  - **`preferred`** checks do not affect the binary pass/fail gate; they are used strictly to score and rank candidates that pass all required checks.  -->
 **Ranking / Scoring:**
  - Candidates with an `accept` verdict are ranked by the number of passing preferred checks. 

