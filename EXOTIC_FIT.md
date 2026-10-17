<!-- Markdown copy of the Exotic Fleet Fit Review artifact (https://claude.ai/artifact/37WtvVuFwkk2BVdjwhZqYt), updated Oct 17, 2026, 4:15 PM ET. The artifact is the original; regenerate this file when it changes. -->

Prospect Fit Review

# Exotic Fleet Fit Review

47 cars, mostly exotic · Came from our ads · Books through Wheelbase (and Turo) · Prepared Sat Oct 17, 2026 · Updated 4:15 PM ET · Demo lead: Miguel

The prospect asked for six things. This checks each one against what the app actually does today, read from the code, then sizes what it would take to close each gap and whether to build it into the product or charge for it as custom work.

## The Email

As received through our ads, word for word. Requirement numbers below match theirs.

From the prospect · 47 mostly-exotic cars · Wheelbase and Turo

Hello Taylor,

We are looking for a fleet management tool. We saw your ad and was wondering if this will fit our purpose. Can you please let us know if we can have a demo to understand what you are offering and the scope of work involved. Pls see our below requirements:

1. **Calendar / booking visibility:** Pull or sync daily pickups and dropoffs from Wheelbase (and ideally Turo) into one operational calendar, with a visual day/week view showing which vehicles are moving and when.
2. **Driver task management:** Create and assign tasks to specific drivers for vehicle pickup and dropoff. Each task should be tied to a specific vehicle, location, time window, and customer or booking reference. Drivers should be able to mark tasks complete with photo or checklist proof (vehicle condition, mileage, fuel level, etc). We need support for both single stop handoffs (most common for us) and multi stop runs, where a driver relocates multiple vehicles in one trip.
3. **Accountability:** Timestamped, GPS verified task completion, visibility into who did what and when, and any issues flagged during pickup or dropoff, along with a historical record or reporting per driver.
4. **Team communication:** Group chat with separate channels, not just comments on a single record, for example by task, by driver, by location, or by issue type, with the ability to share directions, notes, or updates tied to a specific task.
5. **Maintenance tracking:** Track service schedules, mileage based maintenance alerts, and repair history per vehicle, ideally tied into the same vehicle records used for daily task assignment.
6. **Route management:** This would be a nice to have if a driver is handling multiple pickups or dropoffs in one trip, but it is not a primary need since most of our tasks are single location handoffs.

**0** Fully met today

**3** Partly met: calendar, accountability, maintenance

**3** Not met: driver handoff tasks, team chat, routes

### Bottom Line

- Today we are a strong cleaning and money tool with a partial operations layer. For a delivery-heavy exotic fleet, the core gap is **driver handoff tasks**: the only live driver flow is runs to and from the mechanic.
- Most of what they want sits on parts we already run (the email ask engine, no-login phone pages, GPS checks, the service log). Closing requirements 1, 2, 3 and 5, plus the useful part of 6, is about **21 to 31 working days** of effort, shippable in **three releases over about three weeks**.
- Recommendation: **build those into the product, no custom fee**. Every one of them is something a Turo host doing airport and hotel deliveries also wants. Do not build Slack-style channel chat or route optimization; offer task threads and link-outs instead, and quote chat as custom only if they insist.
- At 47 cars they land on **Pro: $99 a month or $990 a year**. Comparable single-purpose tools cost them far more (see Pricing Context), which is the case for building rather than charging extra.

## Current State

What has changed, or matters, since this review was first written earlier today. Nothing below changes the six ratings.

**Built so far:** Nothing for this prospect yet. The six areas in the code are unchanged since the review: main's latest commit is Oct 17, 10:56 AM ET, about alerts and Turo mail. The mechanic changes from this morning ("Mark At Mechanic" in one press, and Request Pickup needing a shop on file) were already counted.

**Trying it alone:** There is no 14-day Test Drive any more (released Oct 14, Taylor confirmed Oct 17). A new fleet starts free on Garage with 2 live cars and every other car paused until it pays. Alone, a 47-car fleet would see 2 live cars. For them to evaluate the whole fleet, either give free days from the Platform tab (Comp, with a number of days) or show them the demo.

**Their plan:** Pro ($99 a month or $990 a year) covers up to 50 cars, so 47 fits. Pricing is flat and never per car. Yearly includes done-for-you setup.

**Demo accounts:** Miguel's own fleet, Wm exotics Miami Beach, has 29 cars and 1,333 past trips. It is on Garage, so 2 cars are live and 27 are paused (Taylor: leave that account as it is). Staging (taylorsfleet-staging.fly.dev) has three made-up fleets of 2, 8 and 20 cars, and sends no mail.

**Fleet map:** A live 3D map of the fleet exists, but only for Taylor's own fleet, and it stays owner-only (Taylor, Oct 17). Live driving and a worldwide night-city map are on the branch `map/live-driving`, not released. Route management (requirement 6) stays None for customers.

**Who builds it:** Taylor reviews this page, then tells the second Claude what to build. Its access and rules are in `HANDOFF.md` in `taylerzy/linguanime-config`. This page is shared by link, and the same content is in `EXOTIC_FIT.md` in that repo, so the second Claude can read it either way.

**Privacy notice:** Two parts bring in data the notice doesn't name yet. The Wheelbase feed brings renters' booking details (names, contact and pickup addresses, if the Zap sends them), and proof of handoff records a driver's phone location. The notice must change before that code ships, and the repo rule is absolute: Taylor approves the exact text first. Draft it on a branch alongside the code.

## Requirement by Requirement

Rated against what the client asked for, not what exists nearby. Partial means their own words are met part of the way.

### 01. Calendar and Booking Visibility

*[Partial]*

Pull Wheelbase (and ideally Turo) pickups and dropoffs into one calendar with a day and week view of which vehicles move when.

#### Have Today

- Schedule tab with a List view and a Calendar view, Day, Week or Month, remembered per person. One row per car with trip, cleaning, planned cleaning, shop and late bars. Day view uses three-hour columns.
- Trip starts and ends, late returns and clean-by times for the next 21 days, refreshed every 30 seconds.
- Bookings from forwarded Turo emails, the Turo earnings file, and bookings typed in.

#### Missing

- No Wheelbase feed, and no booking API, webhook, iCal or CSV import of any kind.
- Trips have no pickup or dropoff location, so the calendar can't say where a car goes.
- Crew work (who moves which car) isn't on the calendar.
- Turo stays on forwarded emails, by design. That already works and covers "ideally Turo".

### 02. Driver Task Management

*[None for Handoffs]*

Assign pickup and dropoff tasks to drivers, tied to a car, location, time window and booking; completion with photo or checklist proof (condition, mileage, fuel); single-stop and multi-stop runs.

#### Have Today (Reusable Parts)

- Mechanic runs: a runner is emailed, accepts or declines, and marks dropped off or returned on a phone page with no login. Arrival can be confirmed by Bouncie GPS. Runners are paid on arrival.
- A Tasks panel with three types (deliver to mechanic, fix tires, other), assigned to a person with one date and a note. The assignee can't mark it done.
- Cleaning photos in Google Drive, odometer read from photos by AI, and a trip photo zip.

#### Missing

- Customer delivery and collection tasks tied to a booking. Nothing creates them today.
- Location, time window and booking reference on a task.
- Checklist, condition, fuel level and mileage capture at a handoff. Photo upload on the driver's phone page.
- Multi-stop relocation runs.
- A driver role in the live flows.

### 03. Accountability

*[Partial]*

Timestamped, GPS-verified completion; who did what and when; issues flagged at pickup or dropoff; history and reporting per driver.

#### Have Today

- Timestamps on every ask, reply, completion, shop arrival and car state change, with a Cleaning History per car.
- GPS verification of three things, from Bouncie: a car arriving at the mechanic, a mechanic task auto-completing, and a trip return at a return location.
- Per-person pay records (newest 200) and per-person 1099 exports.

#### Missing

- GPS checks use the car's Bouncie only. Exotics may have no Bouncie, and nothing checks the driver's phone location.
- No way for crew to flag an issue (damage, fuel, late customer). Replies are read as yes, no or done.
- No per-driver report (tasks done, on-time rate, issues). No screen to read the audit log.

### 04. Team Communication

*[None]*

Group chat with separate channels (by task, driver, location or issue type), sharing directions, notes and updates tied to a task.

#### Have Today

- One-way emails to crew, with replies read back in, plus an alert bell and push alerts for the owner's team.
- Free-text notes on a car's status, a task and a shop visit. A shareable cleaning guide.

#### Missing

- No chat, channels, threads or comments anywhere.
- No notes on a trip, and no in-app messages or push to crew.

### 05. Maintenance Tracking

*[Partial]*

Service schedules, mileage-based maintenance alerts and repair history per vehicle, on the same vehicle records used for tasks.

#### Have Today

- A service log per car: oil, tires, brakes, repair, inspection and other, with date, vendor, cost and odometer.
- Oil change by mileage per car (default every 5,000 miles), shown as overdue, due soon or OK. Oil changes are also picked up from mechanic invoices.
- Shop visits, shop invoices read and filed to the right car, check-engine codes from Bouncie, and registration and document expiry reminders.

#### Missing

- Oil due is on screen only: no email or alert.
- No mileage or time intervals for anything but oil (tires, brakes, inspections).
- No alert when a check-engine light comes on.
- No single repair timeline per car joining the log, invoices and shop visits.

### 06. Route Management

*[None]*

Nice to have for multi-stop trips; not a primary need.

#### Have Today

- A map pin on each car's page and "Open in Google Maps" pin links. Address lookup.

#### Missing

- No multi-stop planning, directions links, distance or ETA, and no fleet map.

### Do Not Demo or Promise These

The database has tables for several of the things they asked for, but no working code behind them. They can look finished in a quick look at the app; they aren't.

- Deliveries, checklists, damage photos and maintenance thresholds: tables only.
- The "crew" task layer with photo and GPS proof: built but switched off, with no screens. It is a good starting point for driver tasks, not a feature.
- Damage claims: no claims feature exists. Say "trip photo zip for damage claims", which is real.

## What It Takes

Effort is working days for one builder, sized against the parts we already run. The work splits into three releases.

| Feature Add | Covers | Builds On | Effort | Build As |
| --- | --- | --- | --- | --- |
| **Wheelbase booking feed.** Their Zapier "New or Updated Reservation" trigger posts each booking to a new secured address on our side. Bookings become trips like every other source, with pickup and dropoff locations shown on the calendar. Cancellations and changes update the trip. | 1 | Trip records, schedule, calendar | 2 to 3 days | *[Product]* |
| **Driver handoff tasks.** Delivery and collection tasks tied to a booking: car, address, time window, booking reference. Assigned to a driver, asked by email with backups like cleaners, and created automatically from bookings marked as deliveries. A no-login phone page with a checklist (condition, mileage, fuel), photos and notes. Shown on the calendar as "who moves which car when". | 2 | The ask engine (escalation, reply reading, pay on completion), the runner phone page, the switched-off crew layer's camera capture | 8 to 12 days | *[Product]* |
| **Multi-stop runs.** Several handoffs or relocations grouped into one run with an order, and one Google Maps link with every stop. | 2, 6 | Driver handoff tasks | 2 to 3 days | *[Product]* |
| **Proof and accountability.** The driver's phone location stamped at each step and checked against the task address (plus the car's GPS when it has Bouncie or Qarhami). An Issue button at handoff with photos that alerts the owner. A per-driver page: tasks, on-time rate, issues, pay. | 3 | Timestamps and GPS checks already in place, pay records | 3 to 5 days | *[Product]* |
| **Task threads.** A message thread on every task and car, seen by the owner's team and the assigned driver, emailed to the driver, replies by email or on the phone page. Share an address or directions link in one tap. | 4 (most of it) | Email replies already read back in | 3 to 4 days | *[Product]* |
| **Maintenance alerts and schedules.** Emails and alerts for oil due, mileage and time intervals for tires, brakes and inspections, a check-engine alert, and one repair timeline per car. | 5 | Service log, oil status, invoices, check-engine events | 3 to 4 days | *[Product]* |
| **Channel chat** (Slack-style channels by driver, location or issue, live updates, push to crew phones, moderation). | 4 (the rest) | Nothing; new real-time system | 15 to 25 days, then upkeep | *[Custom Only]* |
| **Route optimization** (best stop order, traffic, ETAs). Needs a paid maps service per use. | 6 (the rest) | Multi-stop runs | 8 to 12 days, plus usage fees | *[Skip]* |

Recommended set (the six Product rows): about 21 to 31 working days. The Wheelbase feed needs one sample reservation from their Zapier before building, because Wheelbase's own API is Enterprise-only and its field names aren't published. Zapier's free plan stops at 100 runs a month, so at 47 cars they would need a paid Zapier plan.

### Three Releases

*Release 1, about Fri Oct 23*

### See Everything

- Wheelbase booking feed with pickup and dropoff locations on the calendar
- Maintenance alerts and schedules
- Task threads on tasks and cars

*Release 2, about Fri Oct 30*

### Dispatch Drivers

- Driver handoff tasks from bookings
- Phone page with checklist, photos, mileage and fuel
- Phone location stamped at each step

*Release 3, about Fri Nov 6*

### Prove It

- Multi-stop runs with one Maps link
- Issue flags with photos at handoff
- Per-driver history and on-time report

Dates assume work starts Mon Oct 19, 2026 and keep the current pace of releases. The Wheelbase part of Release 1 waits on their sample reservation.

## Build Into the Product, or Charge Custom?

One test: would a Turo host doing airport and hotel deliveries want it too? If yes, it belongs in the product. Custom code for one client becomes a second app to maintain.

*[Product]*

**Booking feed, driver handoffs, proof, task threads, maintenance alerts, multi-stop runs.** Delivery is common on Turo, Getaround and private rentals, so every one of these widens what the app sells to the whole market, and most reuse code we already run. No custom fee. The plan they're on already covers it.

*[Custom Only]*

**Channel chat, and a direct Wheelbase API connection** instead of Zapier. Chat is a second product (live updates, push, moderation) that most hosts get free from WhatsApp or Slack. A direct API needs Wheelbase's Enterprise plan. Quote either one separately only if they insist.

*[Skip]*

**Route optimization.** They said most handoffs are single-stop. An ordered multi-stop Maps link covers the rest without per-use map fees.

### Pricing Context

What this fleet would pay to stitch the same needs together from single-purpose tools, against one flat Pro plan.

| Need | Typical Tool | Their Cost at 47 Cars |
| --- | --- | --- |
| Driver dispatch with photo proof | Onfleet | $619+ a month |
| Handoff inspections and photos | Record360 | about $100 to $295 a month |
| Maintenance tracking | Fleetio ($4 to $10 per vehicle) | about $188 to $470 a month |
| All of the above, plus cleaning and profit | Taylor's Fleet Services Pro | $99 a month or $990 a year |

The gap is why building beats a custom fee: the value lands in Pro, which a 47-car fleet already needs. Whether driver handoffs belong in Pro and up, or in every paid plan, is one of the decisions below. Prices on the ladder don't need to change for this.

### Economics of This Account

- Pro yearly: $990 up front; monthly: $99.
- Miguel: $30 when they pay, plus 20% of profit after that.
- Card fees about $3 a month at $99. Cloud cost for 47 cars is small next to the price.
- Done-for-you setup comes with yearly. That includes importing their 47 cars and setting up the Wheelbase Zap with them.

### For Miguel's Demo

**Show today:** the Schedule calendar (Day and Week), the runner phone page, cleaners asked automatically with backups, the Mechanic tab with oil status, GPS returns, profit per car.

**Say is coming, with dates:** the three releases above.

**Ask them for:**

1. A test run of Zapier's "New or Updated Reservation" trigger (one sample booking).
2. Whether their cars have Bouncie or Qarhami trackers.
3. How drivers are paid today (per handoff, hourly).
4. Their usual pickup and dropoff spots (lot, airport, hotels).

## For the Builder

Where each part starts in `taylerzy/taylorsfleet`, and the rules every release follows.

| Feature Add | Start From | Done When |
| --- | --- | --- |
| **Wheelbase booking feed** | `app/models/trip.py`, `app/routes/schedule_routes.py`, the Turo mail path in `app/services/inbound_email_service.py` (as the model for a booking source), a new secured route for the Zap | A sample reservation from their Zap becomes a trip with pickup and dropoff places on the Day and Week calendar; a change or cancel updates it; a replay doesn't duplicate it |
| **Driver handoff tasks** | `app/services/cleaner_request_service.py` (asks, backups, reply reading, pay), `app/routes/runner_routes.py` (no-login phone page), the switched-off crew layer in `app/models/effector.py` and `app/routes/effector_routes.py`, unused tables in `app/models/delivery.py` and `app/models/checklist.py` | A delivery booking creates a task with car, address, window and booking reference; a driver accepts by email; the phone page takes the checklist (condition, mileage, fuel), photos and notes; the calendar shows who moves which car |
| **Multi-stop runs** | Driver handoff tasks | Several tasks grouped in order, with one Google Maps link with every stop |
| **Proof and accountability** | `app/services/bouncie_service.py`, `app/services/car_location_service.py`, the GPS checks already used for shop arrivals and returns | Each step stamped with time and phone location, checked against the task address; an Issue button with photos alerts the owner; a per-driver page shows tasks, on-time rate, issues and pay |
| **Task threads** | `app/routes/task_routes.py`, `app/services/task_service.py`, `app/models/task.py`, email replies already read back in | A thread on each task and car, emailed to the driver, answered by email or on the phone page |
| **Maintenance alerts** | `app/services/maintenance_service.py`, `app/routes/maintenance_routes.py`, `app/services/mechanic_invoice_service.py`, check-engine events from Bouncie | Oil due, tire, brake and inspection intervals by miles or time raise alerts; a check-engine light alerts; one repair timeline per car |

### Rules for Every Release

- Read the repo's `CLAUDE.md`, `DEPLOY.md` and `docs/TESTING.md` first.
- At most 50 tests and the whole suite under 30 seconds. Don't add tests; edit the ones a change breaks.
- Pull before every push. Others sometimes work on this repo.
- The Zap's address is a normal app route. No new GitHub workflow, and no change to the pinned pipeline.
- No calls to Turo. Turo bookings keep coming from forwarded email.
- Which plans get driver tasks follows Taylor's decision below (`app/services/plans.py`, `plan_gates.py`).
- Release when Taylor asks for it and it is done and tested. Privacy notice text waits for his explicit OK.

### Decisions for Taylor

1. Build the six Product rows into the product with no custom fee?
2. Driver handoff tasks on Pro and up, or on every paid plan?
3. Task threads now, with channel chat quoted as custom only if they insist?
4. Start the Wheelbase feed now, or wait for their sample reservation from Miguel's demo?
5. For their trial: free days from the Platform tab, or demo only?

## Sources

[Zapier: Wheelbase triggers, including New or Updated Reservation](https://zapier.com/apps/wheelbase/integrations)
[Wheelbase help: What is Zapier](https://help.wheelbasepro.com/hc/en-us/articles/12559543147419-What-is-Zapier)
[Wheelbase pricing (full API on Enterprise)](https://www.wheelbasepro.com/pricing)
[Wheelbase developer docs](https://docs.wheelbasepro.com)
[Onfleet pricing](https://www.upperinc.com/blog/onfleet-pricing/)
[Record360 on Capterra](https://www.capterra.com/p/148961/Record360/)
[Fleetio pricing](https://www.costbench.com/software/fleet-management/fleetio/)
App findings come from reading the Taylor's Fleet Services code on Oct 17, 2026.

Taylor's Fleet Services · Prepared Sat Oct 17, 2026 · Updated 4:15 PM ET
