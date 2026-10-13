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
- Times are Eastern (Taylor, Oct 12, 2026): every time in an artifact, page, reply or schedule for Taylor is Eastern Time (America/New_York, what his clock shows), labeled ET, never UTC. Convert stored UTC times before showing them.
- The app makes no calls to Turo (Taylor, Oct 13, 2026; released Oct 13). The Turo client, saved Turo login, Auto Pricer, nightly earnings pull, payout sync, login check, Turo ops scripts and the endpoint guide were removed; they live only in GitHub history (taylorsfleet, before commit 61d7864). Every TF_TURO_ Fly secret was unset. Never add a Turo call back, never guess or probe a Turo URL, and never add code comments saying the app doesn't call Turo. Trips and money come from Turo's emails, the earnings file the host uploads, and bookings typed in.
- Never pause or stop running work Taylor didn't ask to stop (Taylor, Oct 12, 2026): a question from him, a rejected tool call or a long answer is not a reason to pause sends, agents or releases, and never ask him to restart something he didn't stop. When he asks for something (a draft, a number), put it in the reply he reads first, before anything else.
- Agents produce results as they go (Taylor, Oct 12, 2026): every agent writes its output file after each item it finishes (each email, each review, each fix), never only at the end, so a stopped or restarted agent leaves everything it did behind.

## Outreach Emails (Taylor, Oct 11, 2026)

- Every outreach email follows OUTREACH_STANDARD.md in this repo. Read it before writing one.
- Research every recipient (name and facts, with source links); samples first for Taylor's approval; work in rounds with a tracker; a second reviewer checks each email; nothing reaches Taylor's mailbox until it passes; never send.
- No blanks, brackets, placeholders or markers. If only Taylor knows something, ask him before drafting.
- Subjects are Title Case. Never "Hi there,". Links are real links, never split.
- taylorsfleet.com mail (Oct 11, 2026): the @ MX record was "0 default.org." (dead) from Northwest's setup and was changed to "10 mailserver.businessidentity.llc." through Northwest's dashboard API (PUT client/domains/{id}/dns, records with changetype REPLACE; it replaces only that record set). Outbound from taylor@taylorsfleet.com passes SPF, DKIM and DMARC. Northwest's DNS page needs a live connection this cloud session can't make.
- No opt-out line of any kind (Taylor's call): one-off emails, no automated follow-ups; Taylor follows up personally only on a reply. Drafts go to taylor@taylorsfleet.com, not Gmail.
- The ask is to try the app (Taylor, Oct 12, 2026). Never a call or meeting; Taylor won't call every person. Partners who reach many hosts (co-host networks, coaches, communities, VA firms, vendors) may also be offered a partnership in the first email, ideally after the try-it ask (Taylor, Oct 12, 2026, later); see OUTREACH_STANDARD.md point 7.
- Referral terms (Taylor, Oct 12, 2026): a referrer gets 25% of the profit from every customer they bring, for that customer's lifetime. Profit here means what that customer pays, minus card fees and refunds; cloud costs are not subtracted (Taylor, Oct 12, 2026). Only fleets the referred account itself creates count, never invited crew. Partner links (taylorsfleet.com/r/code) and the Platform tab's partner totals were released Oct 12.
- Emails must sound like Taylor, not a template (Oct 12, 2026): see "Sound Like Taylor, Not a Template" in OUTREACH_STANDARD.md, including the side-by-side test.
- All outreach emails (Oct 12, 2026) live in the "Outreach Email Drafts" artifact, https://claude.ai/artifact/X9Jhq4yCWKdN2JUKSmBnNW, ranked by impact. Its page holds a JSON block `<script type="application/json" id="emails-data">` with rank, to, subject, text and html (signature included) for each email; read the artifact and load drafts from that block. Drafts go to taylor@taylorsfleet.com through the Gmail connector (IMAP is blocked from cloud sessions). Create drafts only, never send. Held and Not Written entries are not loaded unless Taylor releases them.
- Send approval (Taylor, Oct 12, 2026, just after midnight Eastern): send the drafted outreach emails ranked #1 to #177 on Oct 12, one every 1 to 2 minutes from 6:51 to about 11:05 AM Eastern (centered on 9 AM), by draft ID from this session. Do not send #26, #61 or #83 at all (addresses not published). Mark each sent email with a Sent checkbox on the artifact and give Taylor the updated artifact when done. Nothing else is sent without his say-so.
- Next outreach goal (Taylor, Oct 12, 2026): keep finding contacts like these and writing emails for them with the same research, tone and second review, until 3,000 are lined up (about 100 a day of sending). New emails go into the artifact (ranked) and into Gmail drafts as they pass review; never send them. **Stopped Oct 13, 2026, 1:16 AM ET at Taylor's request:** no more contact searching or email writing, now or later, unless Taylor asks again. 582 new emails were drafted (never sent) by then.
- Meta customer list (Taylor, Oct 13, 2026): every email found for hosts and rental companies (E1, E2, E9) goes into the Meta Customer List section of the Outreach Email Drafts artifact, in Meta's customer-list format (email, fn, ct, st, country), rebuilt with each page refresh; a second file adds detailers, VA firms and partners. Nothing is uploaded to Meta without Taylor's OK.
- Google Places for lead discovery (Taylor, Oct 12, 2026): never go past the free tier (Text Search Enterprise, 1,000 calls a month; the tool caps all agents at 900 a month, Pacific months). The key is never printed or committed; future sessions read it from the environment variable GOOGLE_PLACES_API_KEY.
- Mail is on Google Workspace (Taylor, Oct 12, 2026; Business Starter, monthly). DNS stays at Northwest and was set through its API: MX `1 smtp.google.com.`, SPF `v=spf1 include:_spf.google.com ~all`, DKIM at `google._domainkey`, DMARC `v=DMARC1; p=quarantine; adkim=r; aspf=r`, and Google's verification CNAME `flgtjidzc3kk`. The app's mg.taylorsfleet.com Mailgun records are separate and unchanged. Northwest's Email Service and Business Domain are free and left idle (cancelling could make Northwest rewrite the mail records). Keep the Registered Agent services for TayTech and Roadloom.

## Pricing (Taylor, Oct 13, 2026)

- Flat plans, never per car (the "Garage-to-Empire Ladder", review page https://claude.ai/artifact/CcooEUGm1oBKh15h3NZMMQ): Garage free (2 live cars, extra cars paused), Host $29 (5 cars), Fleet $49 (20), Pro $99 (50), Empire $179 (100) / $349 (250) / $649 (500); yearly is 10 times monthly. Every sign-up gets a 14-day Test Drive, no card. Taylor said ship it without waiting for approval (Oct 13, 7 PM ET). Stripe live Prices exist with lookup keys tf_<plan>_month / tf_<plan>_year. Deferred: the Founding 100 and the 30-day wait before a removed car comes back on Garage.
- Ads never state a price, dollar amount, plan name or car limit (Taylor, Oct 13, 2026), so prices can change without new ads. "Start free. Flat price, never per car." is fine.
- Meta (Oct 13, 2026, about 6:55 PM ET, Taylor's order): "Turo Hosts - Sign-Ups - Oct 2026" was paused, and a brand-new campaign, "Turo Hosts - Sign-Ups - Flat Plans - Oct 2026" ($40 a day, same audience and Lead goal), runs the new ads D, E and F.

## Ads (Taylor, Oct 12, 2026)

- Brand (Taylor, Oct 13, 2026): the company stays Taylor's Fleet Services. "Fleet Command" is only the internal name of the 3D city homepage concept and does not appear on the page (the name is used by NVIDIA Fleet Command and by rental and trucking fleet software). No rename without discussing it with Taylor first.
- Homepage Visits (released Oct 13, 2026; Platform > Homepage Visits): anonymous scroll, section, hover and click recording on the homepage and sign-up page. No Privacy Notice or FAQ update for it (Taylor, Oct 13, 2026, final). Taylor's own visits count like anyone's; no exclusion button. Ad visits are told apart by their source.

- Google Ads (TayTech Innovations LLC) is connected through the Camberstack connector. Read freely; change only through a proposal Taylor approves in chat, one proposal at a time. Every applied change can be undone.
- Oct 12, applied with Taylor's OK (proposal p_88bc0bc2): 30 negative keywords, paused the keyword "peer to peer car rental software", daily budget $85 to $20 on the Search campaign. Before that it had spent $164 since Oct 2 (about $15 a day, 33 clicks, 0 sign-ups). Judge it around Oct 26 on fleets created from Google (the app now records each account's source).
- Meta ads: guide at https://claude.ai/artifact/SNoExP5avsC2k49ndQSpvt, images at https://claude.ai/artifact/TfQDLXDgoEN4jjAusuS6i8. Meta Ads is connected (Oct 12; official connector, one ad account with a card on file, no business portfolio). Create, publish or activate anything only with Taylor's OK in chat. Its only Page is Turo Rentals Dayton; there is no Instagram account. Pixel 2098960450714876 gets PageView and Lead, no server events yet. taylorsfleet.com isn't verified with Meta yet (Taylor sends the code, I add the DNS record through Northwest).
- Meta campaign (Taylor's OK, Oct 12, 2026, about 6:50 PM ET): "Turo Hosts - Sign-Ups - Oct 2026", $40 a day, US, Advantage+ audience (21+), aimed at Lead (sign-up page visits) until real sign-ups exist, then switch to CompleteRegistration (fleet created). Page: Taylor's Fleet Services. Ads A (Cleaning), B (Profit), C (Team) link to taylorsfleet.com with utm_source=meta and utm_content=ad_a/ad_b/ad_c; images are served from taylorsfleet.com/static/img/ads/. Facebook only until an Instagram account is linked. Stop rule Taylor approved: after 7 days (about Oct 19) or about $280 with zero fleets created, pause it and report (Taylor approved a one-time check, scheduled for Mon Oct 19, 9:00 AM ET). The ads were approved and went live Oct 12, 7:07 PM ET. The three old Marketplace boosts were paused the same night at Taylor's request.

## Carry-Over Items

On the next artifact about final tasks, list these as Taylor's own tasks (his pick, Oct 10, 2026):

- Try the Subscribe flow and the header's Subscribe button end to end (billing was off on the review copy).
- Connect a real Google account and check the Gmail panel's green, yellow and red states.
- Test suite speed: CI passes, but a busy machine runs the suite in 16 to 18 seconds against the 15-second rule.
- With billing on, against real Stripe: Add to My Bill, Take Over This Bill, a payer leaving a fleet on their combined bill, and Pay With My Card (all tested only against a stand-in).

## Standing Decisions (Oct 11, 2026)

- Auto Pricer: removed entirely on Oct 13, 2026 at Taylor's request, with its tables (a backup from 9:19 PM ET Oct 12 holds them for 30 days).
- At the next legal change, and not before: remove PayPal and Venmo from the Privacy Notice, and add to terms section 6 that a removed car's unused days are credited on the next bill, never refunded.
- "Trip Money" extra feature: leave as built (see and enter trip money).
- Mechanic snooze (Oct 11): the "Snooze on Turo While At Mechanic" option and its code were removed at Taylor's request. It never ran on production. The app never snoozes or unlists a car.
- Earned by Car (Oct 11): every dollar per car, no Trips at the Range Edges row. Each car's Earned is on the headline's day-by-day basis (paid in the dates plus owed today). A deposit's part the app can't match to a trip payment goes to the cars whose trips were due just before it. Avg/Day replaces Avg/Trip, Trips counts trips with a rental day in the dates, and there are no Late + Overage, Discounts or Extras columns (email can't tell them reliably). The Expenses tab shows Earned as one box only, with no Earned by Car table (it is on Metrics).
- Oil changes (Oct 11): Oil Change Every (Miles) is set in Car Details on each car's page (default 5,000), not on the Mechanic tab; unknowns on the Mechanic tab are blank.
- Extra features (Oct 11): only the platform owner gives a person extras, in any fleet, on the Platform tab (People and Features). Not on each fleet's Team tab; a fleet's owner can't give extras.
- Money (Oct 11): Profit is the one big number; "Paid so far" is removed everywhere. The app does not estimate when Turo will pay (no Owed to You by Trip table, Next Payment, Arrives or Overdue); Owed to You is one figure.
- Turo API cut back (Oct 11): removed the daily posted-price snapshot (the Auto Pricer never used it), the hourly API listing refresh (listing news comes from Turo's emails only, as for every fleet), the relisted read-back, Market sourcing, and the automatic check-in photo poster (VAs post photos by hand; the trip photo zip download stays). Everything else that called Turo was removed Oct 13.
- Downtime Board (Oct 11): removed entirely (/admin/downtime, its routes and the Mechanic tab link). Shop visits start and end only from the car's page and the dashboard (Send to Mechanic, It's Back, Back in Service).
- Help (Oct 11): not a tab. A "?" icon the bell's size sits between the bell and Settings and opens /faq; the phone Menu lists Help.
- Schedule (Oct 11): remembers each person's List or Calendar and Day, Week or Month (stored with their appearance settings), silently; a Day view shows one day in three-hour columns; the bottom note ("A cleaning ends at its clean-by time...") is gone.
- A fleet with no owner yet can be closed by the co-host who created it, until it is claimed; after that, only the owner can close it.
- Also at the next legal change, and not before: add to the terms that a person who pays for more than one fleet can put them on one combined bill priced on the total car count, that a fleet taken off the bill or left keeps running to the end of the paid period with no refund, that a fleet moved to its owner's card or closed is credited for unused days, and that the money-back guarantee applies once, to the combined bill's first payment. Add to the Privacy Notice that Turo mail held for a person to file is kept whole until filed or removed, up to 180 days. Add to the Privacy Notice, and to the FAQ's cookies answer, that a first-party cookie (tf_src, 90 days) records which ad, campaign or partner link brought a visitor and is saved on the account they create (not recorded for ad sources when tracking is turned off; a partner code is still kept).

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
