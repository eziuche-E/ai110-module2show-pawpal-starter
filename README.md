# PawPal+ (Module 2 Project)

You are building **PawPal+**, a Streamlit app that helps a pet owner plan care tasks for their pet.

## Scenario

A busy pet owner needs help staying consistent with pet care. They want an assistant that can:

- Track pet care tasks (walks, feeding, meds, enrichment, grooming, etc.)
- Consider constraints (time available, priority, owner preferences)
- Produce a daily plan and explain why it chose that plan

Your job is to design the system first (UML), then implement the logic in Python, then connect it to the Streamlit UI.

## What you will build

Your final app should:

- Let a user enter basic owner + pet info
- Let a user add/edit tasks (duration + priority at minimum)
- Generate a daily schedule/plan based on constraints and priorities
- Display the plan clearly (and ideally explain the reasoning)
- Include tests for the most important scheduling behaviors

## Getting started

### Setup

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### Suggested workflow

1. Read the scenario carefully and identify requirements and edge cases.
2. Draft a UML diagram (classes, attributes, methods, relationships).
3. Convert UML into Python class stubs (no logic yet).
4. Implement scheduling logic in small increments.
5. Add tests to verify key behaviors.
6. Connect your logic to the Streamlit UI in `app.py`.
7. Refine UML so it matches what you actually built.

## 🖥️ Sample Output

This example shows the scheduling logic producing a daily plan for each pet while respecting the owner's time budget and task priorities.

```text
======================================================
   TODAY'S SCHEDULE  -  Sat  |  Owner: Jordan
======================================================

  Mochi's Schedule
  ------------------------------------------------
  08:00  [morning   ]  (daily)     walk                 30 min  (p4)
         > Selected walk for Mochi (priority 4, duration 30m, fixed time window, recurs daily, type weight 3).
  08:30  [morning   ]  (daily)     feeding              10 min  (p5)
         > Selected feeding for Mochi (priority 5, duration 10m, fixed time window, recurs daily, type weight 2).
  14:00  [afternoon ]  (daily)     grooming             10 min  (p2)
         > Selected grooming for Mochi (priority 2, duration 10m, fixed time window, recurs daily, type weight 0).

  Total: 50 min / 120 min

  Luna's Schedule
  ------------------------------------------------
  08:00  [morning   ]  (daily)     medication            5 min  (p5)
         > Selected medication for Luna (priority 5, duration 5m, fixed time window, recurs daily, type weight 10).
  08:30  [morning   ]  (daily)     feeding              10 min  (p5)
         > Selected feeding for Luna (priority 5, duration 10m, fixed time window, recurs daily, type weight 2).
  19:30  [anytime   ]  (daily)     litter               10 min  (p3)
         > Selected litter for Luna (priority 3, duration 10m, flexible timing, recurs daily, type weight 0).

  Total: 25 min / 120 min
```

## 🧪 Testing PawPal+

```bash
# Run the full test suite:
pytest

# Run with coverage:
pytest --cov
```

Sample test output:

```text
$ pytest -q
....

4 passed in 0.18s
```

## 📐 Smarter Scheduling

| Feature | Method(s) | Notes |
|---------|-----------|-------|
| Task sorting | `Scheduler.sort_by_time()`, `Scheduler.sort_by_priority_then_time()` | Orders tasks by time-of-day and by highest priority first when building a plan |
| Filtering | `PawPalSystem.filter_tasks()`, `get_tasks_for_pet()`, `get_tasks_for_window()` | Selects tasks by pet, status, or due window |
| Conflict handling | `Scheduler.detect_time_conflicts()`, `Scheduler.resolve_conflicts()` | Warns when overlapping times occur and keeps the highest-priority duplicate for the same pet/task type |
| Recurring tasks | `CareTask.is_due_today()`, `PawPalSystem.reset_for_new_day()` | Supports daily and weekly routines while resetting completed daily tasks for the next day |
| Explanations | `Scheduler.explain_decision()`, `get_last_explanations()` | Generates human-readable reasoning for why each task was chosen |

## 📸 Demo Walkthrough

1. Open the app and enter the owner name, daily time budget, and preferred time windows such as morning or afternoon.
2. Add a pet profile with a name and species, then create care tasks like walks, feeding, medication, or grooming with a duration and priority.
3. Review the task list; each item includes the due window, scheduled start time, and a priority badge.
4. Click Generate Schedule to let the scheduler rank tasks using priority, time preferences, and the owner’s daily limit.
5. Inspect any conflict warnings and the explanation text under each selected task to understand why the plan was built that way.

**Screenshot or video** *(optional)*: A screenshot can be taken from the Streamlit UI after generating a sample schedule for Mochi and Luna.
