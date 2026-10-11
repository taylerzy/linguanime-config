# Required Rules From Taylor

These are Taylor's standing rules. Follow them in every session.

## Calls and Contacting People

- Never tell Taylor to call, email or contact anyone unless you have already checked that you cannot get the answer yourself (web search, listing sites, county auditor and GIS, code libraries, the app's data, agents). Answers that are on the internet must be looked up, not handed to Taylor as a call.
- When a call is truly the only way, say what you already checked and why only a call can answer it.

## Working Style

- Don't tell Taylor to check things. Check them yourself.
- Don't ask for things you can easily get yourself.
- Do not wait for Taylor on deployments; release, but don't deploy broken things.
- Don't schedule check-ins or follow-ups without Taylor's approval.
- Short replies. Put decisions in one numbered list.
- Never print secrets. Ops output is aggregates only, with no guest names, emails or phones.
- Never refer to a fleet by its number (fleet 1, fleet 15). Use the fleet's name, such as Taylor's Rentals.

## Carry-Over Items

On the next artifact about final tasks, list these as Taylor's own tasks (his pick, Oct 10, 2026):

- Try the Subscribe flow and the header's Subscribe button end to end (billing was off on the review copy).
- Connect a real Google account and check the Gmail panel's green, yellow and red states.
- Test suite speed: CI passes, but a busy machine runs the suite in 16 to 18 seconds against the 15-second rule.
- With billing on, against real Stripe: Add to My Bill, Take Over This Bill, a payer leaving a fleet on their combined bill, and Pay With My Card (all tested only against a stand-in).

## Standing Decisions (Oct 11, 2026)

- Auto Pricer (Taylor, Oct 11, 2026): back to the engine as it was before the Oct 10 floor, entirely, with one tweak: a day priced under Turo's price moves a quarter of the way toward it (TOWARD_TURO_PCT = 25). Kept from Oct 10: hand-made listings skipped, Turo cars only, stop at Turo's first refused change. Kept from Taylor's Oct 11 ask: a car with no trips takes Turo's price, 5% under once listed a full day with nothing booked. Hold-or-raise is back at 60% booked. All existing days were reset to these prices on Oct 11 (fix_unfloor_fleet1.py).
- At the next legal change, and not before: remove PayPal and Venmo from the Privacy Notice, and add to terms section 6 that a removed car's unused days are credited on the next bill, never refunded.
- "Trip Money" extra feature: leave as built (see and enter trip money).
- Mechanic snooze (Oct 11): the "Snooze on Turo While At Mechanic" option and its code were removed at Taylor's request. It never ran on production. The app never snoozes or unlists a car.
- Earned by Car (Oct 11): every dollar per car, no Trips at the Range Edges row. Each car's Earned is on the headline's day-by-day basis (paid in the dates plus owed today). A deposit's part the app can't match to a trip payment goes to the cars whose trips were due just before it. Avg/Day replaces Avg/Trip, Trips counts trips with a rental day in the dates, and there are no Late + Overage, Discounts or Extras columns (email can't tell them reliably). The Expenses tab shows Earned as one box only, with no Earned by Car table (it is on Metrics).
- Oil changes (Oct 11): Oil Change Every (Miles) is set in Car Details on each car's page (default 5,000), not on the Mechanic tab; unknowns on the Mechanic tab are blank.
- A fleet with no owner yet can be closed by the co-host who created it, until it is claimed; after that, only the owner can close it.
- Also at the next legal change, and not before: add to the terms that a person who pays for more than one fleet can put them on one combined bill priced on the total car count, that a fleet taken off the bill or left keeps running to the end of the paid period with no refund, that a fleet moved to its owner's card or closed is credited for unused days, and that the money-back guarantee applies once, to the combined bill's first payment. Add to the Privacy Notice that Turo mail held for a person to file is kept whole until filed or removed, up to 180 days.

## Multi-Fleet Accounts (Taylor's decisions, Oct 11, 2026; released Oct 11)

- All accounts are the same kind. Only Taylor's own account keeps the platform owner's extras. An account's role comes from each fleet it belongs to: it can own fleets and be a co-host, VA or cleaner in others.
- Any account can create a fleet. Any account can be added to another fleet as a co-host, VA or cleaner.
- In one fleet only, a person sees just what their role there allows. In two or more fleets, they also get combined views: a My Home landing page with a section per fleet, an overall Cleaning tab, and an overall schedule of the cleanings they need to do. They can still pick one fleet at a time, which changes the tabs.
- An owner who also cleans for other fleets sees their own fleet's trips and cleanings in those combined views, plus the cleanings they do for the other fleets.
- One mailbox for a co-host's Turo mail, filed into the right fleet by car (VIN, listing, plate). Mail that can't be placed is held.
- One bill for everything a co-host pays for, priced on the combined car count. Any owner can still take over their own fleet's bill.
- Cleaner pay is recorded in each fleet, as that owner's expense and 1099. The cleaner sees one combined list.
- Taylor left these to my judgment (Oct 11; released Oct 11): keep "Remove From My Bill"; don't build account-level Gmail (forwarding to Your Turo Mail covers it) but refuse connecting one Gmail in several fleets and point to Your Turo Mail; add an All Fleets Alerts tab of the stored alerts from fleets where the person's role sees alerts.
- Follow-ups noted at release: when billing is on, My Home checks each fleet's bill, which will need batching for a person with hundreds of fleets; fleets someone already pays for separately are not merged into one bill automatically.

## Reminders Taylor Asked to Keep

Add these to the reminders at the end of every reply until Taylor says they are done:

- Drive: in Fleet Settings, Cleaning Photos, share the cleaning-photos folder with the app's Drive address as an Editor and paste the folder link, so the app can make each cleaning's folder.
