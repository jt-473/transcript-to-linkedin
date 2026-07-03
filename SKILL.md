---
name: transcript-to-linkedin
description: Turns a spoken transcript (voice memo, rant, recorded thought, recap of a day/internship/project) into an authentic, non-AI-sounding LinkedIn post for personal branding — built especially for students and early-career people who want to grow their LinkedIn presence without sounding corporate or robotic. If the user doesn't already have a transcript, this skill interviews them with three quick spoken prompts (a story question, an opinion question, and a voice-calibration question) to generate the raw material and capture their real speaking voice. Use this whenever someone pastes or points to a transcript and wants a LinkedIn post out of it, asks to "turn this into a LinkedIn post," "make this sound good for LinkedIn," wants help "growing my LinkedIn," or has rambling voice-memo text they want shaped into something postable — and also whenever someone wants to start a LinkedIn post from scratch but doesn't have a transcript ready, since this skill can generate one through its interview questions. Trigger even if they don't say "LinkedIn" explicitly but describe wanting to share a lesson, story, or win from something they said out loud.
---

# Transcript to LinkedIn

Students lose to two failure modes on LinkedIn: they never post because writing from scratch is slow and they don't know what to say, or they post and it reads like ChatGPT wrote it — generic, over-formatted, humble-bragging in a corporate voice that isn't theirs. This skill fixes both. It takes something they already said out loud (which is naturally specific and personal) and reshapes it into a post, while deliberately fighting the pull toward AI-sounding output at every step.

The core idea: **a transcript already has the two things a good post needs — specificity and a real voice.** The job here is to find the actual thread buried in the rambling, not to launder it into something generic. Every step below is designed to protect the specific/authentic material in the transcript rather than sand it down.

## Step 1: Get the material

Most people don't have a transcript sitting around — they need to be prompted into producing one. If the user already pasted a full raw transcript or pointed to a file, skip straight to that and move to Step 2. Otherwise, ask them to answer three questions out loud (record a voice memo and transcribe it, or just type it stream-of-consciousness — either works, the point is unpolished and spoken-register, not written-register). Ask all three at once so it's one round trip, not three:

1. **The story question** — designed to pull out a concrete scene: *"Tell me about something specific that happened recently — a win, a fail, an awkward moment, a conversation that stuck with you. Doesn't need to be impressive, just talk like you're telling a friend what happened."* This is the raw material for Steps 2-4 below.
2. **The opinion/insight question** — designed to pull out a point of view, separate from the story: *"What's something you've learned, or something you believe about [their field/school/work — ask what it is if you don't know], that you think most people get wrong or haven't realized yet?"* This gives you a second option for the thread in Step 2, and it's what makes the contrarian or listicle structures possible even when the story answer is thin on a "lesson."
3. **The voice question** — not for content at all, purely to hear how they actually talk: *"One unrelated thing — what's a small thing that annoyed you or made you happy today? Answer in a sentence or two, like you're texting a friend."* Never pull content from this answer into the post. Use it only to notice their real patterns — sentence length, filler words, how blunt or hedgy they are, punctuation habits, words they actually use vs. words a generic post would use — and match those patterns when you draft. This is what makes the final post sound like *them* specifically instead of "a student" in the abstract.

Treat the combined answers to questions 1 and 2 as the transcript for everything below. Keep question 3's answer only as a style reference in your head — don't quote it or reference its content in the output.

## Step 2: Find the real thread

Read all the material before doing anything else. People ramble when they talk — they circle back, go on tangents, undersell the interesting part and oversell a boring one. Your job is to find the moment that actually has a point to it, not to average across everything they said.

Look for:
- A specific concrete detail (a number, a name, a moment, a mistake, a quote someone said to them) — these are gold and almost never survive a bad summarization pass. Keep them.
- The turn — where their thinking changed, where something failed then worked, where they realized something they didn't expect.
- What they'd actually say if a friend asked "so how'd it go?" — that's usually the real post, not the most "impressive" sentence in the transcript.

The story answer (question 1) will usually carry the scene, and the opinion answer (question 2) will usually carry the point — but don't force both in if only one has real material. If the story answer already contains its own lesson, question 2's answer might just confirm the angle rather than add new content. If the transcript material rambles across multiple unrelated topics, pick the one with the most specific detail and the clearest turn, rather than trying to cram all of it in. One sharp post beats one bloated one.

## Step 3: Pick a structure

Read `references/structures.md` for the four structures with full templates and examples of what to avoid. Pick based on what the transcript actually is:

- **Storytelling** — transcript centers on one specific moment or scene (an internship day, a conversation, a decision). Default choice when the content is narrative.
- **Listicle/tactical** — transcript is mostly "here's what I did / here's what worked" advice with several distinct takeaways. Default choice when the content is instructional.
- **Contrarian/hot take** — transcript includes the person pushing back on common advice or expressing a strong, slightly unpopular opinion.
- **Before/after (lesson from a mistake)** — transcript centers on something that went wrong and what changed after.

If the user names a structure, use it even if another would technically fit better — ask only if the transcript genuinely can't support their choice (e.g. they ask for "contrarian" but there's no opinion anywhere in the transcript).

If nothing is specified, pick the best fit yourself and briefly say which one you picked and why — don't make the user choose up front.

## Step 4: Draft in that structure

Write the draft using the real details pulled in Step 2. A few things that matter regardless of structure:

- **First person, casual register.** Contractions, sentence fragments where a real person would use them, the actual words the transcript used where they're distinctive (if they said "I panicked," don't upgrade it to "I experienced significant anxiety").
- **Specific beats vague.** "I bombed the first two questions of my PM interview at [Company]" beats "I faced some challenges during a recent interview process."
- **Student voice, not executive voice.** This is personal branding for someone early in their career — the tone should read as humble-but-confident and relatable to peers, not like a VP thought-leadership post. No "I'm thrilled to announce," no "humbled and honored," no talking down to the reader from a position of authority they don't have yet.
- **Length**: aim under ~1,300 characters for tactical/contrarian/before-after posts, since that's what performs best in-feed. Storytelling posts can run longer if the story needs the room — don't cut a good story short just to hit a number, but don't pad a short story either.
- **Formatting**: avoid the AI tics — no wall of bolded headers, no emoji bullet lists standing in for sentences, no "🚀" or "✨" scattered around. Line breaks for pacing are fine and normal for LinkedIn; heavy markdown structure is not.
- **CTA**: end soft if at all — a real question, an invitation to share their own experience, or just let the post land without one. Never "Let's connect!" or "Thoughts?" as a bare tacked-on line.

## Step 5: Run the authenticity pass — always invoke `humanizer`

This step is never skipped, regardless of how clean the draft from Step 4 looks. Before showing the draft to the user, hand it to the `humanizer` skill and run its actual process on it — not just a mental checklist inspired by it, the real draft → audit → final-rewrite loop it defines:

1. Read the Step 4 draft as the "before" text.
2. Write a **draft rewrite** through humanizer's lens, checking it against its full pattern list — inflated significance, promotional language, superficial "-ing" tacked-on analysis, vague attributions, rule-of-three, AI vocabulary (*delve, crucial, testament, underscore, vibrant,* etc.), copula avoidance, negative parallelisms, hedging, filler phrases, sycophantic tone, and generic upbeat closers.
3. Apply humanizer's **hard constraint on em/en dashes**: the final draft contains zero `—` or `–`. Scan for them explicitly before finishing — this is the single most common AI tell and the one most likely to slip through if the drafting step above used one.
4. Ask humanizer's own question: *"What makes this so obviously AI generated?"* — answer it honestly against the draft, then fix whatever it surfaces.
5. Produce the **final rewrite** — this is what moves on to Step 6, not the Step 4 draft.

A few things specific to a LinkedIn post that humanizer's general checklist won't automatically catch, so watch for these too:
- Any sentence that could be published by literally anyone with the names swapped out — if a line doesn't need the specific details from this transcript to be true, cut or sharpen it.
- LinkedIn-native slop that isn't in humanizer's generic list but is just as much a tell here: "I'm thrilled to announce," "humbled and honored," "excited to share," a bare "Thoughts?" as a CTA, or a paragraph that exists only to restate the hook in fancier words.

Per humanizer's own guidance, don't over-correct signs of real human writing — the specific, hard-to-fabricate details pulled in Step 2 (a name, a number, an exact thing someone said) are exactly what should survive this pass untouched. This step's job is to strip the AI patterns layered on top of those details, not to sand the details themselves down into something safer and blander.

If the structure is storytelling, also check the hook against the `viral-hooks` skill and the overall arc against the `storytelling` skill before running humanizer — the opening line is what earns the "…see more" click on LinkedIn, and it's the easiest place for a draft to go generic. Run humanizer last, after those two, so it's the final filter the post passes through.

## Step 6: Deliver

Give the user:
1. The post draft itself, ready to copy-paste.
2. 2-3 hashtags that are actually specific to the content (not `#motivation #hustle #grindset` — pull from the actual field/topic/school/company mentioned).
3. One line naming which structure you used and why, so the user learns the pattern for next time.

If anything in the draft required inventing a detail that wasn't in the transcript (a number, a name, an outcome), flag it plainly so the user can fix or confirm it before posting — never let a fabricated specific slip through disguised as something from their own life.

If the user wants a different structure or a different angle after seeing the draft, redo Step 3 onward — don't just patch the existing draft, since a different structure usually means a genuinely different opening and shape, not a find-and-replace.
