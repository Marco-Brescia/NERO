# Project context
Software for a robot built on ROS 2 Jazzy (Ubuntu 24.04), C++17 and Python 3.12.
The repo is a colcon workspace: ROS packages live in `src/`, project documentation (written by the maintainer) lives in `docs/`.

# Scope: where you may read and write
- `docs/` is your **instruction manual**. Read it, never modify it.
- `src/` is the **only place you may modify**. Code, launch files, params and tests (`src/<pkg>/test/`) all live here.
- Everything else in the repository (`.github/`, deploy scripts, CI, hardware or machine configuration, secrets,
  anything outside `docs/` and `src/`) is **out of scope**: do not open it, do not quote it, do not edit it.
  If a task seems to require touching it, stop and ask in the issue or PR comments.
- Never modify anything under a `safety/` directory in `src/`, even though it is inside `src/`.

# How to work
1. Start by listing `docs/` and read the documents relevant to the task (begin with an index or README if there is one).
2. Follow the conventions, testing and safety rules written there. If code and docs disagree, or the docs are silent
   on something that matters, report it in the issue or PR; do not guess.
3. Keep changes small and inside the packages named in the task.

# Build and test (run before opening or updating a PR)
```bash
rosdep install --from-paths src --ignore-src -y
colcon build --event-handlers console_cohesion+
colcon test && colcon test-result --verbose
```

# Safety (non-negotiable)
- Never weaken speed, acceleration or joint limits, timeouts, or emergency-stop behaviour.
- Every behaviour change needs a test (unit, integration or simulation).
- If a requirement is ambiguous or involves real hardware, leave a comment and do not guess.

# Pull requests
- Description: what changed, why, how it was tested.
- One PR = one goal. Open separate issues for unrelated problems you notice.
