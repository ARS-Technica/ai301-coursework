# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check                               | Evidence                                                                                                                                                                             | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Weight    |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |

| 'Scope-Bounded' | Issue description, Issue body and all entries in the Comments section | Target: The issue requests a single, cohesive change deliverable in one pull request.  

The issue asks for one bounded change with a single contribution outcome. A body that lists several parts, files, sub-headings, or named causes still passes as long as they all serve that one outcome and one PR could plausibly cover them (e.g., one new documentation page plus updating existing pages pointing to it; a bug resolved identically across an enumerated list of call sites; or a maintainer exploring multiple candidate causes for a single bug). A maintainer or collaborator proposing multiple theories or approaches to scope an investigation is not an unsettled debate and does not fail this check. Missing reproduction steps, a terse description, or a bare checklist of acceptance criteria do not fail it either: evaluate the volume of work required, not the polish of the writeup.

Fail strictly on:

1. Umbrella / Tracking Issues: A body that explicitly indicates sub-items will be divided into separate, independently tracked issues or PRs.

2. Unsettled Design Debates: The thread demonstrates ongoing, unresolved disagreement where two or more contributors (excluding a solo maintainer exploring ideas) propose competing designs with no maintainer consensus or decision reached.

3. Ambiguous Intent: A maintainer explicitly questions whether the work should be performed at all, or leaves critical input/design decisions open or TBD.

4. Engine Internals: A maintainer notes that the fix requires modifying core architecture or internals (such as parsers, renderers, or compilers).

5. Support Inquiries: The issue is an end-user usage or support question rather than a code or documentation change. | required |


| 'Maintainer-Alive' | Repo facts: author names and commit titles in "last 5 default-branch commits", and the days-to-first-response figures in "maintainer first-response sample". Comments section: author_association on each comment | Passes on either signal: a default-branch commit within 60 days of capture that represents human work (including bot merge commits merging a contributor's PR, but excluding automated dependency bumps or generated docs); or a maintainer first response of 60 days or less in the sample; or an OWNER, MEMBER, or COLLABORATOR comment in this issue's thread. Fail or grade unclear when no source establishes recent human maintainer activity within 60 days.	| required |


| 'Maintainer-in-Thread' | Issue header: original submitter's author association line; Comments section: author_association metadata tags attached to each comment | 
The thread demonstrates direct engagement or stewardship from project leadership.

Passes if: At least one comment in the conversation thread, or the initial issue creation itself, originates from a GitHub user whose author_association is explicitly tagged as OWNER, MEMBER, or COLLABORATOR.

Fails if: The issue and all subsequent comments come entirely from non-maintainer community members (such as CONTRIBUTOR, FIRST_TIME_CONTRIBUTOR, NONE), or if there are no comments and the creator is not an owner/member. | preferred |

 
| 'AI-Policy-Permits' | Repo facts: the "contribution policy" line, including any quoted policy guidelines, contributing files, or template excerpts | The project does not explicitly prohibit AI-assisted contributions.

Passes if:
* Silence: The policy does not mention AI, or no contribution policy line is present.    * Conditional Use: Policies requiring AI disclosure, human verification/testing, full comprehension of submitted code, or bans on fully automated/unreviewed generation that still permit AI assistance as a tool.    
Fails strictly on: An unambiguous, explicit ban on AI-assisted contributions (e.g., stating "AI-assisted pull requests will be closed" or "we do not accept AI-generated or AI-assisted code"). | required | 


| 'Repo-in-Use' | Repo facts: "archived:" status line, dates under "last 5 default-branch commits", and "last push to any branch" timestamp | The repository is active and maintained.

Passes if: The repository is not marked as archived, and at least one activity indicator (either the most recent default-branch commit or the most recent push across any branch) occurred within 90 days of the capture date.

Fails if: The repository status is explicitly marked as archived, or if both the newest commit on the default branch and the last branch push are older than 90 days from capture. |

required |


| 'Unclaimed' | Issue header: state. Repo facts: "this issue: assignees", "linked PRs" and their states. Comments section: pull requests referenced and intent-to-claim comments | Passes if: The issue is currently open, has no assignees listed, carries no open linked or thread-mentioned pull requests at capture, and contains no active claim comment (e.g., "I'll take this", "can I work on this", "/assign", "working on this") posted within 60 days of capture that remains unretracted.
Exceptions that DO NOT fail this check:

1. Closed/Unmerged PRs: A previously closed, unmerged pull request represents an abandoned attempt rather than an active reservation.
    
2. Stale Claims: Any claim comment older than 60 days that has no accompanying open pull request.    
(Note: If running in live mode, any specific claim rules defined in scope.md apply). |    required |


| 'Attempt-History' | Repo facts: issue creation date ("opened") and "linked PRs" with their respective states. Comments section: discussion history regarding claims, unassignments, or abandoned work | The issue does not show a pattern of multiple failed, abandoned pull requests indicating hidden complexity.

Fails strictly when BOTH conditions occur simultaneously:

1. The issue has been open for more than 365 days from the date of capture.    

2. The issue has 2 or more closed, unmerged pull requests explicitly linked in repo facts or referenced in the thread.    

Passes in all other circumstances:
* Issue age alone (even $>365$ days) passes.    
* A single closed, unmerged pull request passes regardless of issue age.    
* Stale bot notifications, inactive claim comments lacking an associated PR, or maintainer prompts re-opening the floor to new contributors all pass without penalty. | required |    
 

| 'Fix-Located' | The issue description/body, and any maintainer comments in the Comments section | The issue or an accompanying maintainer comment provides concrete pointers identifying where the implementation change should occur.

Passes if: The body or any maintainer comment explicitly references a specific file path, function name, class, method, or line number to be modified, or provides a code snippet or illustrative diff demonstrating the proposed correction.

Fails if: The write-up describes the desired behavior, error symptom, or high-level request purely conceptually without directing the contributor to specific source files or code identifiers. | preferred | 


## Verdict rule

- **Verdict Determination:**
  - An issue receives an **`accept`** verdict if and only if **all 6 required checks pass**.
  - If any required check evaluates to **`fail`** or **`unclear`**, the verdict is deterministically **`reject`**.
  - **`preferred`** checks do not affect the binary pass/fail gate; they are used strictly to score and rank candidates that pass all required checks.
- **Ranking / Scoring:**
  - Candidates with an `accept` verdict are ranked by the number of passing preferred checks (0/2, 1/2, or 2/2).


<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
