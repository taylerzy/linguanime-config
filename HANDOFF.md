# Handoff: Continuing Taylor's Fleet Services Work (Oct 17, 2026)

Part A is Taylor's checklist of what to give a second Claude. Part B is the
text to paste into that Claude.

## Part A: Accesses to Give It

### Required

1. **GitHub.** The Claude GitHub App must have write access to two repos, and
   both must be added to its cloud environment:
   - `taylerzy/taylorsfleet`, the app. It needs push, pull requests, and
     Actions (start workflows and read their logs).
   - `taylerzy/linguanime-config`, Taylor's standing rules (`CLAUDE.md`,
     `OUTREACH_STANDARD.md`, this file).
2. **Network.** Its cloud environment must reach github.com, api.github.com,
   pypi.org, files.pythonhosted.org and taylorsfleet.com. Add
   tiles.openfreemap.org if it will screenshot the owner map.
3. **Rules.** Copy `linguanime-config/CLAUDE.md` into its own global
   instructions, or have it read that file at the start of every session.

### Not Needed

- **No Fly token** for releases, production reads or data fixes. All three run
  through GitHub Actions, which already holds `FLY_API_TOKEN` (the
  `production` environment) and `FLY_DB_TOKEN` as repo secrets.
- No Stripe, Mailgun or database keys. Those are Fly secrets on the app and
  are used only on the app machine.

### Optional, Only for the Work That Needs It

4. **Staging deploys.** Give it a staging-only Fly token:
   `fly tokens create deploy -a taylorsfleet-staging`. Put it in its cloud
   environment as `FLY_API_TOKEN`. Never give it a production or
   organization-wide Fly token.
5. **Connectors** (claude.ai, Settings, Connectors, in its own account). Each
   needs Taylor's sign-in:
   - Meta Ads
   - Camberstack (Google Ads)
   - Gmail (taylor@taylorsfleet.com, drafts only)
   - Google Drive
6. **Artifacts** belong to the account that made them. Share them with edit
   access if the new Claude must update them; otherwise it publishes new ones.
7. `GOOGLE_PLACES_API_KEY` as an environment variable. Only needed if lead
   searching resumes; it was stopped Oct 13.

## Part B: Instructions to Paste

You are continuing work for Taylor on Taylor's Fleet Services, a web app for
Turo hosts. The live site is https://taylorsfleet.com. It runs on the Fly app
`taylors-turo-fleet` with Postgres. The code is in `taylerzy/taylorsfleet`
(FastAPI, Python 3.12).

**Read first, every session:**

1. `linguanime-config/CLAUDE.md`: Taylor's standing rules. They override
   your defaults.
2. `taylorsfleet/CLAUDE.md`, `DEPLOY.md` and `docs/TESTING.md`: the
   source of truth for code, tests and releases. The rules file can lag
   behind the app; when they disagree about the code, the app repo wins.
   Flag the difference to Taylor.

**How Taylor wants answers:**

- Short replies, with decisions in one numbered list.
- Times in Eastern Time, labeled ET.
- Name fleets by name, never by number.
- Never print secrets. Production output is counts only: no people's names,
  emails or phones, and nothing about guests.
- Don't tell Taylor to check things; check them yourself.
- Don't schedule check-ins without his OK.
- Agents write their results to a file after each item they finish.

**Code:**

- `git fetch origin main` before every branch. One branch per feature; commit
  as you go.
- Pull before every push: others sometimes work on these repos. Fetch and pull
  the branch first (and `origin/main` before merging to it), check what's new,
  then merge or rebase. Never force-push over someone else's commits.
- Tests: **at most 50 tests, and the whole suite under 30 seconds** (the time
  pytest reports). `tests/conftest.py` enforces both. Don't add tests: edit
  the existing ones your change breaks, and if a test is truly needed, delete
  one.
- Before merging, run:
  1. `pip install -r requirements.txt`
  2. `python -m pytest -q`
  3. `python scripts/verify_launch_invariants.py`
- The pipeline is pinned by fingerprint. Never edit `.github/workflows/ci.yml`,
  add a workflow or schedule, or add a sleep without Taylor's written OK
  naming that change.
- Never add a call to Turo, guess a Turo URL, or write comments saying the app
  doesn't call Turo.
- GPS mileage is never used.
- Two-step sign-in is never mandatory.
- The sign-up username stays required.

**Releasing:**

1. Merge to `main`. A push to main only runs the tests; it does not deploy.
2. Release with
   `gh api -X POST repos/taylerzy/taylorsfleet/actions/workflows/ci.yml/dispatches -f ref=main`,
   or in GitHub: Actions, CI, Run workflow on `main`.
3. Watch the run:
   `gh api "repos/taylerzy/taylorsfleet/actions/workflows/ci.yml/runs?per_page=1"`.
4. Then `curl https://taylorsfleet.com/healthz` must answer
   `{"status":"ok","db":true,...}`.

Every release needs Taylor's approval. When he asks for a change, that is his
approval to release it: release as soon as it is done and tested, without
asking again. Don't release anything he didn't ask for, and never anything
broken. These always need his explicit OK for that exact change:

- any privacy notice change (never merge one to main unapproved, because
  main ships with the next release)
- pipeline changes
- Meta or Google Ads changes
- sending anything to people

**Rolling back without a Fly token:** revert the bad commit on main and
release again.

**Production data, read-only:**

1. Write `scripts/ops_queries/<name>.py`. Its docstring gives the date, says
   read-only, and says what it prints.
2. Push it to the branch `claude/oct12-owner-spark`.
3. Run:
   `gh api -X POST repos/taylerzy/taylorsfleet/actions/workflows/ops.yml/dispatches -f ref=claude/oct12-owner-spark -f "inputs[script]=readonly_query" -f "inputs[query]=scripts/ops_queries/<name>.py"`
4. Read the log. Get the latest run id from `.../actions/workflows/ops.yml/runs?per_page=1`, then its job id from `.../actions/runs/<id>/jobs`. `.../actions/jobs/<job_id>/logs` answers with a redirect; fetch the Location URL.

The script runs on the production machine against production's code, so that
branch being behind main is fine.

**Data fixes:** name the file `fix_<name>.py`. It changes nothing unless
`FIX_APPLY=1`. Run it once as `readonly_query` for a dry run, then as
`data_fix`, and only for a fix Taylor asked for.

**Staging:** https://taylorsfleet-staging.fly.dev, a separate app with made-up
fleets. Mail, Stripe and Drive are blocked there. Deploy to it by hand with
`flyctl deploy -a taylorsfleet-staging -c fly.staging.toml` (staging token
needed). It is never part of the pipeline.

**In flight on Oct 17, 2026:**

1. **Owner-only live fleet map.**
   - Branch `map/live-driving`: live GPS driving, plus a move to OpenFreeMap
     tiles in the homepage's night-city look so it works anywhere.
   - The old session's agent may still push commits to it. Finish it, test it,
     screenshot it, merge and release.
   - It stays owner-only (Taylor, Oct 17).
2. **Minor:** remove the never-shown CLAIMS line from the plan feature lists
   and `plan_gates.py` in the next release.
3. **Exotic 47-car Wheelbase prospect:** Taylor is assessing it. Do nothing
   until he asks.
4. **Bring up when the time is right:** the app tabs redesign in the
   night-city style. It is parked.
5. **No Test Drive (Taylor, Oct 17):** new fleets start on Garage, free with up to 2 live cars. Fleets from before Oct 14 kept 14 days.
6. **Meta:** two campaigns are active.
   - "Taylor's Fleet Services | New Creative Test | Oct 2026", $60 a day.
   - "Turo Hosts - Sign-Ups - Flat Plans - Oct 2026", $40 a day.
   - Taylor (Oct 17): working well, no change to ad spend or ads.
7. **Wm exotics Miami Beach** is Miguel's own fleet. Leave the account as it is.
8. **Not now (Taylor, Oct 17):** no setup-reminder emails, no password gate on staging.
