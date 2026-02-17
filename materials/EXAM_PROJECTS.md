# 🎯 Exam: 20 Projects to Choose From

> **Vibe Coding 2025** | ITMO | Master's Program
>
> **Time**: 3 hours | **Tool**: Claude | **Result**: GitHub repository

---

## Grading Criteria

| Criterion | Points | How to get the max |
|-----------|:------:|-------------------|
| **Working MVP** | 2-5 | It launches and solves the stated problem |
| **Evolution (commits)** | 2-5 | 10+ meaningful commits showing clear progression |
| **Tests** | 2-5 | pytest-bdd with .feature files, tests BEFORE code |
| **Documentation** | 2-5 | README + CLAUDE.md + launch instructions |
| **Vibe Coding approach** | 2-5 | BDD as specification, AI as co-author |

### ✅ Checklist for 25/25

- [ ] Repository on GitHub
- [ ] README with description and launch instructions
- [ ] CLAUDE.md describing how you worked with AI
- [ ] BDD .feature files (pytest-bdd)
- [ ] Tests run and pass
- [ ] 10+ commits with clear messages
- [ ] MVP works and solves the client's problem

---

## 🎪 Projects

---

### 1. 😤 MEETING ROOMS (or how I spent 2 hours of my life in a hallway)

> So look, I work in an office with 8 meeting rooms. EIGHT! You'd think — just grab any one. Yeah, right.
>
> Monday, 10:55. Call with the client in 5 minutes. I head to "Mars" — occupied, even though Outlook says it's free. I knock — some dudes in there eating borscht out of containers. BORSCHT! IN A MEETING ROOM!
>
> I sprint to "Venus" — locked from inside, I can hear someone screaming into a phone.
>
> "Jupiter" — three people watching YouTube on the projector.
>
> "Saturn" — under renovation.
>
> "Neptune" — booked by Ivanov from 9:00 to 18:00 every day for a year in advance (he quit ages ago).
>
> End result: I take my client call sitting on a windowsill in the hallway. Professional? Extremely.
>
> The Outlook calendar is a FICTION. Nobody marks when they leave early. Nobody cancels the booking when a meeting falls through. And HR keeps sending emails "colleagues, please vacate meeting rooms on time 🙏". Uh huh, works great.
>
> **Build a Telegram bot:**
> - I type "any free?" — shows which rooms are ACTUALLY free right now
> - "Book Mars 15:00-16:00" — books it
> - "Freed up Mars" — releases the booking early
> - "Who's in Venus?" — shows who booked it and until when
>
> No Outlook integrations needed (that's impossible anyway), just its own honest database. Where people actually mark things themselves.

**Stack**: `Python` `aiogram` `SQLite`

---

### 2. 🍕 HOW MUCH DO I OWE VASYA (or the Friday night drama)

> Friday. 6:00 PM. Six of us are still at the office — deadline.
>
> Vasya (a saint): "Ordering pizza, wanna chip in?"
> Everyone: "Yeeeees!"
>
> Pizza arrives. 4,200 rubles.
>
> Vasya: "Okay, that's 700 per person"
> Petya: "I only had two slices!"
> Masha: "I literally only had one pepperoni!"
> Kolya: "But you, Petya, drank all the Coke!"
> Petya: "Not all of it! Half a liter!"
> Olya: "I'm on a diet, I only had the salad"
> Everyone: "WHAT SALAD OLYA, WE ORDERED PIZZA"
>
> Vasya: *quietly weeping*
>
> A week later:
> "Who still owes me for last week's pizza?"
> "I already paid!"
> "When?"
> "Last week!"
> "That was two weeks ago, you didn't pay last week"
> "I DID!!!"
>
> I started tracking it in Excel. Forgot to update it. Vasya started a notebook. Lost it. Masha created a chat called "Food Debts." 500 messages and total chaos.
>
> **Build a bot:**
> - Vasya types: "pizza 4200 @Petya @Masha @Kolya @Olya @Dima"
> - Bot: "Got it! 700 each. Total owed to Vasya: 3,500"
> - Petya: "paid Vasya 700"
> - Bot: "Noted! Petya is all clear. Remaining: Masha, Kolya, Olya, Dima"
> - Anyone: "debts"
> - Bot: "Masha owes Vasya 700 (2 weeks). Kolya owes Vasya 1,400 (overdue!)..."
>
> PEACE. FRIENDSHIP. PIZZA.

**Stack**: `Python` `aiogram` `SQLite`

---

### 3. 📚 WHERE'S MY BOOK (a detective story spanning 3 years)

> 2022. My buddy Seryoga: "Oh, Pelevin! Can I borrow it?" — "Sure, go ahead"
>
> 2023. Me: "I wanna re-read Generation P... where is it? Screw it, I'll buy a new one"
>
> 2024. Seryoga is at my place. On his shelf sits MY Pelevin. With MY dog-eared page.
> "Seryoga... that's my book"
> "Nah man, I bought it"
> "Seryoga, I spilled coffee on page 47"
> "..."
> "..."
> "Well... maybe you gave it to me as a gift?"
>
> I'm missing:
> - "The Master and Margarita" (suspects: 4 people)
> - "1984" by Orwell (I have zero memory of who I lent it to)
> - "Harry Potter and the Philosopher's Stone" (mom says she has it, mom is lying)
> - A collection of Chekhov short stories (maybe I lost it during the move?)
>
> I have ~200 books at home. I occasionally lend them out. I never write it down. I SUFFER.
>
> **Build a CLI or bot:**
> - `book add "The Master and Margarita" "Bulgakov"` — added to the catalog
> - `book lend "The Master and Margarita" "Seryoga" 01.15.2025` — recorded who I gave it to
> - `book list --lent` — "Who has my books: Seryoga (Bulgakov, 2 months!), Mom (Harry Potter, 1 YEAR!!!)"
> - `book remind` — "Time to nudge: Mom has had the book for a YEAR"
> - `book return "The Master and Margarita"` — returned, hooray!
>
> Bonus: option to add a photo of the cover so you know exactly which edition.

**Stack**: `Python` `click` or `aiogram`

---

### 4. ⏰ WHEN TO WAKE UP (math at 3 AM)

> 2:47 AM. Flight to Dubai at 7:20. Not sleeping — watching a show. Suddenly remember the plane.
>
> Okay so... I need to be at the airport 2 hours before... that's 5:20. Sheremetyevo. No traffic at night, but an hour's drive for sure... so leave at 4:20. Nice. Call a taxi 15 minutes before... 4:05. Getting ready takes... 40 minutes? No, quick, 30 minutes. So wake up at 3:35.
>
> That's in 48 minutes.
>
> Maybe just don't sleep?..
>
> *falls asleep*
>
> *wakes up at 6:15*
>
> *misses the flight*
>
> And when you're flying somewhere with a layover across time zones — your brain just melts.
>
> "Departure from Moscow 19:00, arrive Istanbul 22:00 local, 3-hour layover, depart at 01:00, arrive Bali 18:00 local... SO WHAT TIME DO I NEED TO WAKE UP IN MOSCOW?!"
>
> **Build a CLI:**
> - `flight plan --depart "Moscow" 07:20 --to "Dubai"`
> - Output:
>   ```
>   🛫 Flight plan: Moscow → Dubai
>
>   You need to:
>   03:50 — Wake up
>   04:30 — Leave (call taxi at 04:15)
>   05:20 — Be at the airport
>   07:20 — Departure
>   11:20 — Arrival (Dubai local time)
>
>   💤 You have 4.5 hours left to sleep. Sweet dreams!
>   ```
> - Settings: how long to get ready, travel time to airport, buffer

**Stack**: `Python` `click` `datetime/pytz`

---

### 5. 🏃 RUNNING LOG (or how I'm training for a marathon in random notes)

> Decided to run a marathon. 42 km. Serious business.
>
> Started training and keeping notes:
>
> *Phone notes, January:*
> - "ran 5km fine"
> - "ran. tired. 4 something km"
> - "today was amazing!!! ran fast"
> - "didn't run knee hurts"
> - "5.3km 27min or 28 can't remember"
>
> *February:*
> - "long run 10km"
> - "ran 6km good pace"
> - "ran"
>
> Coach: "What's your monthly mileage?"
> Me: "Well... a lot... somewhere around... *scrolling notes* ...I dunno"
> Coach: "And your 5K progress over the last 2 months?"
> Me: "Um... got faster... probably..."
> Coach: *looks at me with pity*
>
> **Build a CLI:**
> - `run add 5.2km 27:30` — logged a run
> - `run add 10km 58:45 --note "dying for the last 2km"` — with a comment
> - `run week` — "This week: 3 runs, 21.4km, avg pace 5:32/km"
> - `run month` — monthly stats
> - `run best 5km` — "5K PR: 24:15 (set on Feb 15, 2025)"
> - `run progress` — weekly chart
> - `run compare --weeks 4` — compare last 4 weeks

**Stack**: `Python` `click` `SQLite`

---

### 6. 🎬 WHAT TO WATCH (the Friday night quest)

> Friday, 10:00 PM. Kids are asleep. Wife and I on the couch. Two hours of free time ahead. A rare occurrence. A celebration!
>
> "What are we watching?"
> "I dunno, you pick"
> "No, you pick"
> "I don't care"
> "Me neither"
> *open Netflix*
> "Seen it"
> "Don't want that"
> "That's 3 hours, we won't make it"
> "That one has subtitles, too lazy to read"
> "Oh, this looks interesting! Actually no, it's about a serial killer, not before bed"
> *scroll*
> *scroll*
> *30 minutes later*
> "Maybe a series?"
> *open series*
> *20 more minutes*
> "Fine, let's just rewatch something old"
> "Sure... what?"
> *15 more minutes*
> "You know what, it's late, let's just go to sleep"
>
> EVERY. SINGLE. FRIDAY.
>
> **Build a bot:**
> - During the week, I add movies: "wanna watch Oppenheimer"
> - Wife adds hers: "wanna watch Barbie"
> - On Friday: "what are we watching?"
> - Bot: picks a random movie from the overlap (stuff we both want), or if no overlap — from the combined list
> - "Watched Oppenheimer, 8/10" — goes to archive with a rating
> - "History" — what we've watched over the past year

**Stack**: `Python` `aiogram` `SQLite`

---

### 7. 💊 MOM'S PILLS (or how I went grey at 30)

> Mom's 68. Blood pressure. Diabetes. Thyroid. Heart. The whole works.
>
> Pills:
> - Enalapril — morning, on an empty stomach
> - Metformin — after breakfast
> - L-thyroxine — at lunch
> - Cardiomagnil — evening
> - Plus some vitamins
>
> Me: "Mom, did you take your pills?"
> Mom: "Yes yes, I took them"
> Me: "Which ones?"
> Mom: "Well... those... the little white ones"
> Me: "Which white ones? There are three kinds of white ones!"
> Mom: "The morning ones"
> Me: "And the evening ones?"
> Mom: "Oh, I forgot!"
>
> Or the other way around:
> Mom: "I'm not feeling well..."
> Me: "Did you take your pills?"
> Mom: "Yes, all of them"
> Me: "The morning ones too?"
> Mom: "Yes... or no? I don't remember. I'll take them again just in case"
> Me: "MOM NO YOU CAN'T TAKE THEM TWICE"
>
> I'm at work. I can't call every 4 hours!
>
> **Build a bot for mom:**
> - 8:00 AM — "Good morning! ☀️ Time to take enalapril (small white one)"
> - Mom taps "Took it ✅" or responds with anything
> - If no response within an hour — I get a message: "⚠️ Mom hasn't confirmed enalapril!"
> - I can check: "mom's stats" — how many times she missed this week
> - Evening message to mom: "All pills for today taken! 💪 Good night!"

**Stack**: `Python` `aiogram` `APScheduler`

---

### 8. 🧾 WHERE DID THE MONEY GO (a financial mystery)

> 1st of the month. Paycheck: 150K. I'm rich. I'm handsome. Life is beautiful.
>
> 15th. 40K left on the card. Strange.
>
> 25th. 8K left. Panic.
>
> 28th. Borrowing money until payday. Shameful.
>
> "Where did 150 thousand go in one month?!"
>
> I try to recall:
> - Morning coffee... 300 × 22 days = 6,600
> - Lunches... 500 × 22 = 11,000
> - Taxis on days I overslept... about 8 times... × 600 = 4,800
> - Subscriptions... Spotify, Netflix, YouTube Premium, iCloud, something else... 3,000?
> - Bars on Fridays... 5K a night... 4 Fridays... 20,000
> - Oh, and some courses I paid for... 15,000
> - And sneakers... 12,000
> - And mom's birthday gift... 8,000
>
> Total: 80,400. BUT WHERE'S THE OTHER 70 THOUSAND?!
>
> I download a budget app. Track expenses for two days. On day three I forget. Delete the app.
>
> **Build the simplest possible bot:**
> - I type: "coffee 300" — logged under "Food"
> - "taxi 600" — category "Transport" (auto-detects from the keyword)
> - "bar 5000" — "Entertainment"
> - "gym 4000" — "Health"
> - End of month: "expenses" — a nice breakdown by category
> - "coffee this month" — "You spent 7,200 on coffee 😱"
> - "top expenses" — "1. Entertainment: 25K, 2. Food: 18K..."

**Stack**: `Python` `aiogram` or `click`

---

### 9. 🎂 BIRTHDAYS (the story of one epic fail)

> March 15, 2024. An ordinary day. Sitting at work.
>
> Phone call from wife:
> "Did you call my mom?"
> "Which mom? Why?"
> "It's her birthday today"
> "..."
> "..."
> "I'll call back"
>
> I call my mother-in-law:
> "Irina Pavlovna! Happy birthday! All the best!"
> "Thank you, Dima. How nice that you remembered... at 6 PM"
> "I... work... so much going on..."
> "Of course. You're a busy man. I understand."
>
> To this day, every time we meet: "Oh it's fine, I understand, you're a BUSY MAN" *icy stare*
>
> I have 300+ contacts. They all have birthdays. Some are critical (wife, mom, mother-in-law, boss). Some would just be nice to acknowledge. I CANNOT remember 300 dates!
>
> **Build a bot:**
> - "Add: Mother-in-law Irina Pavlovna 03.15" — priority "critical"
> - "Add: Colleague Vasya 07.22" — priority "normal"
> - 3 days before: "⚠️ Birthday in 3 days: Mother-in-law Irina Pavlovna! ORDER FLOWERS!"
> - On the day: "🎂 TODAY IS: Mother-in-law's birthday! Call RIGHT NOW!"
> - "Upcoming" — who's celebrating this month
> - "Today" — who to congratulate today

**Stack**: `Python` `aiogram` `APScheduler`

---

### 10. 📝 RECIPES (the hunt for the perfect apple cake)

> Mom on WhatsApp: "Honey, here's grandma's apple cake recipe" + photo + 4-minute voice message + another photo + "oops, wrong one" + the correct photo.
>
> Wife in our chat: link to an Instagram reel with a pasta recipe.
>
> Friend on Telegram: "Bro, made this yesterday, absolute banger" + link to a 40-minute YouTube video.
>
> Me on Pinterest: saved 150 recipes to a board called "To Cook," opened it 0 times.
>
> A month later:
>
> Wife: "Make that pasta"
> Me: "Which one?"
> Wife: "The one I sent you"
> Me: "When?"
> Wife: "A month ago"
> *scrolling the chat for 20 minutes*
> *can't find it*
> "Can't find it, send it again"
> Wife: "Find it yourself" 😤
>
> **Build a bot:**
> - I send text/photo/link — it saves it
> - Add tags: #dessert #moms #quick #pasta
> - "find apple cake" — found
> - "random #dinner" — random recipe tagged dinner
> - "all #moms" — all of mom's recipes
> - "quick chicken" — filtered results

**Stack**: `Python` `aiogram` `SQLite`

---

### 11. 🚗 CAR (maintaining the chaos)

> Call from the service center: "You have a scheduled maintenance appointment"
> "I do? When?"
> "Today at 10:00"
> "Today?! I'm at work!"
> "You made the appointment 3 months ago..."
> "Oh... yeah... right..."
>
> I keep car maintenance notes on scraps of paper. The scraps live in the glove compartment. The glove compartment is a graveyard of paper scraps, receipts, napkins, and one ancient candy.
>
> What I'm supposed to remember:
> - Oil change every 10,000 km (last changed in October at 85K, right now... gotta go check)
> - Brake pads — every 30,000 km (when did I last change them? no idea)
> - Timing belt — every 90,000 km (CRITICAL — if it snaps, the engine is toast)
> - Tires: winter ↔ summer (usually a month late on the swap)
> - Insurance — every year
> - Vehicle inspection — every year
>
> **Build a CLI or bot:**
> - `car add "Oil change" 10.15.2024 85000km --next +10000km`
> - `car add "Insurance" 03.01.2025 --remind 30d`
> - `car mileage 93500` — updated the odometer
> - `car status`:
>   ```
>   ⚠️ Oil change: in 1,500 km!
>   ✅ Insurance: 45 days left
>   ⚠️ Tires: time to switch to summer (already +5°C outside)
>   ```

**Stack**: `Python` `click` or `aiogram`

---

### 12. 🏠 CLEANING (the war for hygiene)

> Apartment. Four adults. One toilet.
>
> Monday evening:
> "Who cleaned the bathroom last?"
> "I did it last week!"
> "No, I did it last week!"
> "You did it TWO weeks ago!"
> "And you didn't even clean it, you just wiped the sink!"
> "THE SINK IS PART OF THE BATHROOM!"
> "NO IT'S NOT!"
>
> Wednesday:
> "Whose dishes are in the sink?"
> "Not mine"
> "Not mine"
> "Not mine"
> "THERE ARE FOUR PLATES, THERE ARE FOUR OF US"
>
> Friday:
> "Who's taking out the trash?"
> *silence*
> *everyone pretends they didn't hear*
> *trash overflowing*
> *war*
>
> **Build a bot for the group chat:**
> - "Cleaned the bathroom" — bot: "Noted! Vasya, bathroom, Jan 15, 7:30 PM"
> - "Took out the trash" — noted
> - "Stats" — who did what this month:
>   ```
>   Vasya: bathroom (2), kitchen (1), trash (4)
>   Masha: bathroom (3), kitchen (3), trash (0) ← 🤔
>   ```
> - "Whose turn for trash" — "Masha, you haven't taken out the trash in 3 weeks. Your turn."

**Stack**: `Python` `aiogram` `SQLite`

---

### 13. 💪 GYM (the diary of suffering)

> Trainer: "What's your working weight on bench?"
> Me: "Well... 70... or 80... somewhere around there"
> Trainer: "And your max?"
> Me: "Did 90 once... or 85... can't remember when"
> Trainer: *sighs*
>
> I had a training log. Three logs, actually. All lost.
>
> The entries looked like this:
> - "bench 70×8, 75×6, 80×4" (okay, that's fine)
> - "squat lots" (???)
> - "arms tired" (which exercises?!)
> - *illegible scribble* (my handwriting)
>
> **Build a CLI:**
> - `gym add "bench press" 80kg 8reps 3sets`
> - `gym add "squat" 100kg 5x4 --note "knee was aching"`
> - `gym today` — what I did today
> - `gym max "bench press"` — my max: 95kg (set Dec 15, 2024)
> - `gym progress "squat"` — chart over 3 months
> - `gym last "deadlift"` — when I last did it

**Stack**: `Python` `click` `SQLite`

---

### 14. 🎵 MUSIC (the lost track)

> Bar. Friday. 11:00 PM. Third drink in.
>
> The PERFECT song is playing. The beat slaps. The voice is angelic. The lyrics hit right in the soul.
>
> I pull out Shazam. Can't identify it (too loud, echo, people shouting).
> I go up to the bartender: "What's playing?"
> "It's the owner's playlist, I don't know"
>
> I try to remember the lyrics: "something about... love? and fire? and dancing in the... something?"
>
> I type in my notes: "bar on pyatnitskaya friday electronic female voice something about love and fire incredible!!!"
>
> Two months later:
> "There was this song... in some bar... it was great... female voice... about something..."
> *check notes*
> *40 similar entries*
> *no idea which one was THE one*
>
> **Build a bot:**
> - I log: location "Mayak bar," time "Fri 11PM," genre "electronic," voice "female," lyrics "love, fire, dancing," mood "groovy but sad"
> - Tags: #bar #friday #electronic
> - Later: "find Mayak bar January" — all entries from there
> - "sad electronic" — filter by mood and genre
> - Maybe someday I'll find it from these notes...

**Stack**: `Python` `aiogram` `SQLite`

---

### 15. 📦 PACKAGES (where's my cable)

> Wife: "Another AliExpress delivery"
> Me: "What arrived?"
> "No idea, it's for you"
> *I open it*
> "Oh, a cable!"
> "What cable?"
> "USB-C to... something. I ordered it!"
> "When?"
> "Two... or three months ago?"
> "Why do you need a cable?"
> "Can't remember anymore"
>
> Right now I have incoming:
> - Something from Ozon (no clue what)
> - Headphones from Wildberries (or was it a pillow?)
> - Three packages from AliExpress (absolutely no idea)
> - A book from Labirint (I think)
>
> Tracking numbers? In my email. In five different messages. Half of them in Chinese.
>
> **Build a CLI or bot:**
> - `parcel add "Sony headphones" wildberries` — even without tracking
> - `parcel add "USB cable" ali --track LP123456789CN`
> - `parcel list`:
>   ```
>   📦 In transit:
>   • Sony headphones (WB) — added Jan 12
>   • USB cable (Ali) — added Dec 15 (A MONTH!)
>   • Book "Thinking Fast and Slow" (Labirint)
>   ```
> - `parcel received "headphones"` — got it, archived
> - `parcel lost` — what's been in transit for over a month (time to investigate)

**Stack**: `Python` `click` or `aiogram`

---

### 16. 🐱 CAT (Barsik's medical record)

> Vet: "When did you last give him a dewormer?"
> Me: "Umm... fall? Or summer?"
> "And the vaccination?"
> "Last year for sure... or the year before?"
> "Which vaccine?"
> "Well... you know... the one in the little bottle..."
> *vet stares disapprovingly*
>
> Barsik the cat. 5 years old. My friend and companion.
> His medical history lives in my head (and it's not really there).
>
> What I need to remember:
> - Vaccination — once a year
> - Dewormer — every quarter (must be 10 days before vaccination!)
> - Weight — the vet always asks
> - Checkup — once a year
> - When anything was last done — absolutely no idea
>
> **Build a bot:**
> - "Vaccination combo Jan 15 2025" — logged
> - "Weight 5.2kg" — logged
> - "Dewormer drontal Jan 5 2025" — logged
> - "Remind vaccination Jan 15 2026 14 days ahead" — and 14 days before, it'll also remind about the dewormer!
> - "History" — all records for Barsik
> - "When is the vaccination" — next one: Jan 15, 2026 (in 347 days)

**Stack**: `Python` `aiogram` `APScheduler`

---

### 17. 🌱 PLANTS (confessions of a serial ficus killer)

> Ficus #1 (2021): dried out. "Forgot to water it a couple times"
> Ficus #2 (2022): rotted. "I watered it every day, what's the problem?"
> Monstera (2023): turned yellow and died. Cause of death unknown.
> Aloe (2023): survived! (it's impossible to kill those)
> Orchid (2024): ... *silence*
>
> Girlfriend: "Let's get a plant"
> Me: "I'm a plant killer"
> "Come on, it's easy — just water it once a week"
> "What do you mean once a week?! Ficus — every 5 days! Aloe — every 2 weeks! Orchid — when the roots turn grey! How am I supposed to remember all that?!"
>
> **Build a caretaker bot:**
> - "Add: Ficus Benjamina, water every 5 days, bright light"
> - "Add: Aloe, water every 14 days, any light"
> - Every morning the bot says: "🌱 Water today: Ficus (last watered 5 days ago)"
> - I reply "watered" — timer resets
> - If I don't reply — evening reminder
> - "Stats":
>   ```
>   Ficus: on-time watering 70% ✅
>   Aloe: you're watering too often! 😱
>   ```

**Stack**: `Python` `aiogram` `APScheduler`

---

### 18. 🎮 BOARD GAMES (the Friday night dilemma)

> Friday, 7:00 PM. The boys are here. 30 boxes on the shelf.
>
> "What are we playing?"
> "Dunno, what haven't we played in a while?"
> "No idea"
> "How about Carcassonne?"
> "We've played it three weeks in a row"
> "Munchkin?"
> "Seryoga hates Munchkin"
> "Then what?"
> *staring at the shelf for 15 minutes*
> "Oh, Settlers of Catan!"
> "The rules take an hour to read"
> "Then..."
> *10 more minutes*
> "Alright, Carcassonne again"
>
> **Build a bot:**
> - Add games: name, min/max players, game length
> - After a game: "played Carcassonne 4 players Vasya won"
> - "Haven't played in a while" — sorted by last played date
> - "For 5 players under an hour" — filtered
> - "Random" — a random game that fits
> - "Win stats":
>   ```
>   🏆 Vasya: 15 wins
>   🥈 Petya: 12 wins
>   🥉 Me: 3 wins 😢
>   ```

**Stack**: `Python` `aiogram` `SQLite`

---

### 19. 📖 QUOTES (lost wisdom)

> I'm reading a book. A sentence so beautiful I stop. Read it again. One more time. I want to remember it forever.
>
> I jot it down in my phone notes between "buy milk" and "call the bank."
>
> A month later:
> "There was this phrase... about time... or memory... by someone... Tolstoy? Marquez? Maybe Dostoevsky?"
> *open notes*
> *200 notes*
> *half of them are grocery lists*
> *can't find it*
>
> **Build a CLI:**
> - `quote add "One Hundred Years of Solitude" "Marquez" "Many years later, as he faced the firing squad, Colonel Aureliano Buendia was to remember that distant afternoon when his father took him to discover ice."`
> - `quote tag last #opening #death #memory` — add tags
> - `quote random` — a random quote (for morning inspiration)
> - `quote search time` — all quotes containing the word "time"
> - `quote by "Marquez"` — all quotes by author
> - `quote tags #love` — everything about love

**Stack**: `Python` `click` `SQLite`

---

### 20. 😴 SLEEP (chronicles of sleep deprivation)

> 2:30 AM. "One more episode and then bed"
> 3:15 AM. "Okay, NOW I'm going to sleep"
> 3:40 AM. *scrolling Reddit*
> 4:00 AM. "That's it, sleeping"
> 7:00 AM. *alarm*
> 7:15. *second alarm*
> 7:30. *third alarm + phone call from mom "are you up?"*
>
> Three hours of sleep. Fifth day in a row.
>
> Look in the mirror: bags under my eyes, grey face, eyes like a panda — a sad one.
>
> "I need to sleep more" — I say every day.
> "Tonight I'll be in bed by 11" — I say every evening.
> 2:30 AM — *scrolling TikTok*
>
> I just want to at least SEE my shame in numbers.
>
> **Build a CLI:**
> - `sleep log 02:30 07:00` — logged the night (4.5 hours 😱)
> - `sleep week`:
>   ```
>   This week: average 4.8 hours
>   Mon: 5h | Tue: 4.5h | Wed: 6h | Thu: 4h | Fri: 4.5h
>
>   ⚠️ YOU SLEEP LESS THAN YOUR CAT
>   ```
> - `sleep month` — monthly stats
> - `sleep goal 7h` — set a goal
> - `sleep streak` — how many days in a row you hit your goal (0...)

**Stack**: `Python` `click` `JSON`

---

## 🚀 How to Work

```
1. Pick a project (whatever speaks to you)
2. Create a GitHub repository
3. Write BDD scenarios in .feature files FIRST THING
4. Show them to Claude, ask it to generate the code
5. Commit every 15-20 minutes (small steps!)
6. Write the README and CLAUDE.md
7. Make sure the tests pass
8. Submit the repository link
```

## 📁 Repository Structure

```
my-project/
├── README.md           # Description + how to run
├── CLAUDE.md           # How you worked with AI
├── requirements.txt    # Dependencies
├── src/
│   └── ...            # Code
├── tests/
│   ├── features/      # BDD .feature files
│   └── steps/         # Step definitions
└── .gitignore
```

---

**Good luck!** 🚀

*Graded by: Claude Opus 4.5 + Alexey Komissarov*
