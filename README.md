[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/QtC5AQlU)
# Week 9 Homework: The Case of the Missing Festival Lanterns

## Student Info

Name: Raj Ghimire 

Student number: 2412076

GitHub username: rajgh1020

---

## Summary

`analyze_lanterns` solves the problem of figuring out what went wrong at a festival by checking lantern records against what was expected. It takes in a set of expected lantern names, a log of where each lantern actually showed up, and a dictionary of where each lantern was supposed to be. It then builds a report that covers things like which lanterns were missing, which ones showed up that weren't supposed to, which ones appeared more than once, and which ones were in the wrong section. The report is returned as a dictionary so the data can be used by other parts of the program.

---

## Approach

- First, I created empty collections to track everything I needed: a set for seen lanterns, a set to help detect duplicates, a set for duplicates themselves, a dictionary for section counts, and a dictionary for wrong-section lanterns.
- During the loop, I went through each record in `lantern_log` and added the lantern name to `seen_lanterns`. I used a `seen_once` set to check if I had already encountered a lantern — if yes, it went into `duplicate_lanterns`.
- Also during the loop, I counted how many records appeared in each section using `count_by_section`, and checked if an expected lantern was in the wrong section, only recording the first wrong section if it appeared multiple times.
- After the loop, I used set subtraction to get `missing_lanterns` (expected but not seen) and `unexpected_lanterns` (seen but not expected).
- Finally, I returned a dictionary with all six required keys.

---

## How I Used Dictionaries and Sets

1. Sets were used for `seen_lanterns`, `seen_once`, `duplicate_lanterns`, `missing_lanterns`, and `unexpected_lanterns`. Set operations like `-` made it really easy to find missing and unexpected lanterns in one line.
2. Dictionaries were used for `count_by_section` (section name → count) and `wrong_section_lanterns` (lantern name → expected/actual sections).
3. Dictionaries and sets were better than lists here because checking membership with `in` is O(1) for sets and dicts, while it would be O(n) for lists. Also, sets automatically handle uniqueness, so I didn't have to write extra code to avoid adding duplicates.

```text
Sets: seen_lanterns, seen_once, duplicate_lanterns, missing_lanterns, unexpected_lanterns
Dicts: count_by_section, wrong_section_lanterns
Better than lists because membership checks are O(1) and sets handle uniqueness automatically.
```

---

## Complexity

```text
Time complexity: O(n)
Space complexity: O(n)
Explanation: The code loops through lantern_log exactly once, so time grows linearly with the number of log entries. There are no nested loops. The extra space used scales with the number of unique lanterns and sections in the log, which is at most O(n).
```

---

## Edge-Case Checklist

- [x] empty `lantern_log`
- [x] empty `expected_lanterns`
- [x] no missing lanterns
- [x] no unexpected lanterns
- [x] duplicate lanterns
- [x] wrong-section lanterns
- [x] unexpected lanterns ignored for wrong-section checking

Add one more edge case you thought about:

```text
A lantern that appears three or more times should still only appear once in duplicate_lanterns, not multiple times.
```

---

## Tests I Added

```text
tests/test_challenges.py
```

Describe the test you added:

```text
Test name: test_analyze_lanterns_all_present_correct_sections
What it checks: That when every expected lantern shows up exactly once in the right section, all the problem fields (missing, unexpected, duplicates, wrong section) come back empty.
Why it matters: It confirms the happy path works and that the function doesn't accidentally flag correct data as an error.

Test name: test_analyze_lanterns_empty_log_with_expected
What it checks: That when the log is empty but expected_lanterns has entries, all expected lanterns show up as missing and nothing else breaks.
Why it matters: It checks a realistic edge case where the festival data wasn't recorded at all.
```

---

## How to Run the Tests

```bash
pytest -q
```

```text
7 passed in 0.03s
```

---

## Assistance and Sources

```text
AI used? Y: Used Claude to help explain the approach and check my logic.
What it helped with: Explaining set operations, reviewing edge cases, and helping write the README.
Other sources used: Course slides on dictionaries and sets.
```

---

## Submission Self-Check

- [x] I completed `analyze_lanterns` in `src/challenges.py`.
- [x] I added at least one meaningful test of my own.
- [x] `pytest -q` passes.
- [x] I completed this README.
- [x] I pushed my latest work to GitHub.