---
name: transcript-to-linkedin
description: Turns a spoken transcript (voice memo, rant, recorded thought, recap of a day/internship/project) into an authentic, non-AI-sounding LinkedIn post for personal branding — built especially for students and early-career people who want to grow their LinkedIn presence without sounding corporate or robotic. If the user doesn't already have a transcript, this skill interviews them with three quick spoken prompts (a story question, an opinion question, and a voice-calibration question) to generate the raw material and capture their real speaking voice, and it remembers that voice across sessions. Use this whenever someone pastes or points to a transcript and wants a LinkedIn post out of it, asks to "turn this into a LinkedIn post," "make this sound good for LinkedIn," wants help "growing my LinkedIn," or has rambling voice-memo text they want shaped into something postable — and also whenever someone wants to start a LinkedIn post from scratch but doesn't have a transcript ready, since this skill can generate one through its interview questions. Trigger even if they don't say "LinkedIn" explicitly but describe wanting to share a lesson, story, or win from something they said out loud.
---

# Transcript to LinkedIn

Students lose to two failure modes on LinkedIn: they never post because writing from scratch is slow and they don't know what to say, or they post and it reads like ChatGPT wrote it — generic, over-formatted, humble-bragging in a corporate voice that isn't theirs. This skill fixes both. It takes something they already said out loud (which is naturally specific and personal) and reshapes it into a post, while deliberately fighting the pull toward AI-sounding output at every step.

The core idea: **a transcript already has the two things a good post needs — specificity and a real voice.** The job here is to find the actual thread buried in the rambling, not to launder it into something generic. Every step below is designed to protect the specific/authentic material rather than sand it down.

## Step 1: Get the material

Most people don't have a transcript sitting around — they need to be prompted into producing one. If the user already pasted a full raw transcript or pointed to a file, skip straight to that and move to Step 2. Otherwise, ask them to answer three questions out loud (record a voice memo and transcribe it, or just type it stream-of-consciousness — either works, the point is unpolished and spoken-register, not written-register). Ask all three at once so it's one round trip, not three:

1. **The story question** — designed to pull out a concrete scene: *"Tell me about something specific that happened recently — a win, a fail, an awkward moment, a conversation that stuck with you. Doesn't need to be impressive, just talk like you're telling a friend what happened."* This is the raw material for Steps 3-5 below.
2. **The opinion/insight question** — designed to pull out a point of view, separate from the story: *"What's something you've learned, or something you believe about [their field/school/work — ask what it is if you don't know], that you think most people get wrong or haven't realized yet?"* This gives you a second option for the thread in Step 3, and it's what makes the contrarian or listicle structures possible even when the story answer is thin on a "lesson."
3. **The voice question** — content is secondary here, the real point is hearing how they actually talk: *"One unrelated thing — what's a small thing that annoyed you or made you happy today? Answer in a sentence or two, like you're texting a friend."* Don't pull its content into the post. Use it, plus the natural phrasing scattered through answers 1 and 2, to build the voice profile in Step 2.

Treat the combined answers to questions 1 and 2 as the transcript for everything below.

## Step 2: Build or update the voice profile

This is what makes post #5 sound more like the user than post #1 did, instead of every session starting from zero. Maintain a small file at `~/.claude/transcript-to-linkedin-voice-profile.md` — outside the skill's own folder, never inside it, since the skill folder may be a public repo and this file holds someone's personal speech fingerprint.

1. Check whether the file already exists and read it if so.
2. From today's answers (all three, not just the voice question — real patterns show up everywhere someone talks), note: sentence length and rhythm, hedging vs. bluntness, recurring words or verbal tics, punctuation habits, capitalization habits (some people naturally type in all-lowercase even in unpolished text — that's a real register, not a typo, and worth carrying into the draft if it's consistent), how they open thoughts, how blunt or soft they are when disagreeing with something.
3. Merge these observations into the file rather than overwriting it — if today's answers confirm a pattern already noted, leave it; if something new or contradicting shows up, update it. Keep the whole file to a paragraph or short bullet list of *patterns*, not a transcript archive — never store the actual content of what they said (their internship, their opinion, their day), only how they said it. The content is temporary; the voice fingerprint is the durable asset.
4. If this is the first time the file is being created, say so briefly to the user — they should know this is now persistent and will keep sharpening the voice match on future runs, and that they can ask to see or reset it any time.

Use this file, not just today's isolated answers, as the voice reference for every drafting and editing step below.

## Step 3: Find the real thread

Read all the material before doing anything else. People ramble when they talk — they circle back, go on tangents, undersell the interesting part and oversell a boring one. Your job is to find the moment that actually has a point to it, not to average across everything they said.

Look for:
- A specific concrete detail (a number, a name, a moment, a mistake, a quote someone said to them) — these are gold and almost never survive a bad summarization pass. Keep them.
- The turn — where their thinking changed, where something failed then worked, where they realized something they didn't expect.
- What they'd actually say if a friend asked "so how'd it go?" — that's usually the real post, not the most "impressive" sentence in the transcript.

The story answer will usually carry the scene, and the opinion answer will usually carry the point — but don't force both in if only one has real material. If the transcript material rambles across multiple unrelated topics, pick the one with the most specific detail and the clearest turn, rather than trying to cram all of it in.

## Step 4: Let the user pick the structure

Read `references/structures.md` for the four structures with full templates and examples of what to avoid. None of the four is objectively "the best fit" — they're different framings of the same material, and which one lands is a matter of the user's taste and what they feel like putting their name on, not something to decide for them. Present all four, neutrally, and let them choose:

- **Storytelling** — centers on one specific moment or scene.
- **Listicle/tactical** — "here's what I did / what worked," a few distinct takeaways.
- **Contrarian/hot take** — pushes back on common advice or states a strong, slightly unpopular opinion.
- **Before/after (lesson from a mistake)** — something went wrong, then what changed.
- **Milestone/gratitude announcement** — a new job, offer, graduation, or acceptance, with real people to credit. Only offer this one when the material actually has a milestone in it.

If the material genuinely can't support one of the four (e.g. there's no opinion anywhere for contrarian, or no scene for storytelling), say so plainly rather than silently dropping it from the list — let the user know why it's off the table if they ask for it anyway.

Ask whether they want one structure or two to compare side by side — both are fine, don't default to two without asking. If they say "you pick" or don't have a preference, then and only then choose for them, and say briefly why.

While you're asking, also ask how long they want the post — this is the user's call, not a fixed rule per structure. Give them a feel for the range rather than making them guess a character count:

- **Short/punchy** — a few tight lines, the kind that reads in one glance without expanding "…see more." Best when the point is sharp enough not to need room to build.
- **Standard** — roughly what fits before or just past the fold, the common length for tactical/contrarian/before-after posts on LinkedIn.
- **Long-form** — as much room as the story needs to breathe, common for storytelling posts with a scene worth slowing down for.

If they don't have a preference, default to standard length for listicle/contrarian/before-after and long-form for storytelling — but treat that as a fallback, not a rule to argue them out of if they want something different. A short contrarian take and a long, unrushed story are both legitimate; don't quietly pad a short answer or trim a long one back toward the "expected" length for that structure.

## Step 5: Draft the chosen structure(s)

Write each requested draft using the real details pulled in Step 3, calibrated to the voice profile from Step 2 and the length the user chose in Step 4. A few things that matter regardless of structure:

- **First person, casual register.** Contractions, sentence fragments where a real person would use them, the actual words the transcript used where they're distinctive (if they said "I panicked," don't upgrade it to "I experienced significant anxiety").
- **Specific beats vague.** "I bombed the first two questions of my PM interview at [Company]" beats "I faced some challenges during a recent interview process."
- **Student voice, not executive voice.** This is personal branding for someone early in their career — the tone should read as humble-but-confident and relatable to peers, not like a VP thought-leadership post. No "I'm thrilled to announce," no "humbled and honored," no talking down to the reader from a position of authority they don't have yet.
- **Length**: hold to whatever the user chose in Step 4. If a detail doesn't fit within a short/punchy length, cut it rather than quietly running long; if long-form was chosen, don't pad with filler just to fill the space — extra length should come from earning the story room, not stretching sentences.
- **Formatting**: avoid the AI tics — no wall of bolded headers, no emoji bullet lists standing in for sentences, no scattered emoji. What actually performs on LinkedIn is short, single-thought lines with real whitespace between them rather than dense paragraphs — one idea per line break, not one idea per paragraph. This isn't the same thing as AI-style over-formatting: there are no bolded headers or bullet icons doing the sentence's job, just a person pausing between thoughts the way they would talking. A numbered or slash-numbered list (`1/ 2/ 3/`) is a normal, non-AI way to present a few takeaways — it's the inline-bolded-header version (`**Takeaway 1:** ...`) that's the tell, not numbering itself.
- **CTA**: three options, pick whichever fits the structure and what the material can support — don't default to the same one every time. A soft question or invitation to share their own experience. A direct, specific comment prompt (e.g. asking readers to comment their own answer, city, or role) when the post is genuinely built to start a conversation, not tacked on as an afterthought. Or no CTA at all, letting the post land on its own. Never a bare "Thoughts?" or "Let's connect!" — those aren't real prompts, they're filler.

## Step 6: Hook check — every draft, every structure

Every structure lives behind LinkedIn's "…see more" fold, not just storytelling posts — a flat opener kills a listicle or a contrarian take just as fast as it kills a story. Run the `viral-hooks` skill against the first 1-2 lines of **each** draft before moving on. For any draft using the storytelling structure, also check its overall arc against the `storytelling` skill.

## Step 7: Authenticity pass — humanizer, then anti-ai-writing, on every draft

Never skipped, regardless of how clean a draft looks after Step 6. Run two passes, in this order, on each draft:

**Pass 1 — `humanizer`.** Run its actual draft → audit → final-rewrite loop, not a mental checklist inspired by it:
1. Treat the Step 5/6 draft as the "before" text.
2. Write a draft rewrite checked against humanizer's full pattern list — inflated significance, promotional language, superficial "-ing" tacked-on analysis, vague attributions, rule-of-three, AI vocabulary (*delve, crucial, testament, underscore, vibrant,* etc.), copula avoidance, negative parallelisms, hedging, filler phrases, sycophantic tone, generic upbeat closers.
3. Enforce humanizer's hard constraint: zero `—` or `–` in the final text. Scan for them explicitly.
4. Ask humanizer's own question — *"What makes this so obviously AI generated?"* — and fix whatever it surfaces.

**Pass 2 — `anti-ai-writing`.** This skill names itself the final filter for exactly this kind of content, so it runs last. Diagnose against its five diseases — vagueness compression, significance inflation, hedged confidence, rhythmic flatness, borrowed authority — and check the draft has a specificity and voice "moat": would this sentence survive with the names swapped out, or could literally anyone have posted it? If it would survive unchanged, cut or sharpen it.

A couple of LinkedIn-specific tells worth a manual check on top of both skills: "I'm thrilled to announce," "humbled and honored," "excited to share," and any paragraph that exists only to restate the hook in fancier words.

Per both skills' own guidance, don't over-correct signs of real human writing — the specific, hard-to-fabricate details pulled in Step 3 (a name, a number, an exact thing someone said) should survive both passes untouched. The job is stripping AI patterns layered on top of those details, not sanding the details themselves into something safer and blander.

## Step 8: Pre-delivery QA checklist

Before showing the user anything, check each draft against this list and fix anything that fails rather than delivering it with a caveat:

- [ ] At least one specific, hard-to-fabricate detail from the material survived (not generalized away)
- [ ] Nothing was invented that isn't flagged for the user to confirm
- [ ] Length matches what the user chose in Step 4
- [ ] Hook passes the Step 6 check
- [ ] Zero em/en dashes remain
- [ ] The draft actually sounds like the voice profile, not a generic student

## Step 9: Deliver

For each draft delivered, give the user:
1. The post itself, ready to copy-paste.
2. 2-3 hashtags specific to the content (not `#motivation #hustle #grindset` — pull from the actual field/topic/school/company mentioned).
3. One line naming the structure/angle, so the user learns the pattern for next time.

Then:
- Flag plainly anything that required inventing a detail not present in the material (a number, a name, an outcome) — never let a fabricated specific slip through disguised as something from their own life.
- If this session created or updated the voice profile file, mention that briefly (see Step 2).
- If they only asked for one structure, ask if they'd like to see it in a different one too, without pushing it.

If the user wants a different structure or angle after seeing a draft, redo Step 4 onward — don't just patch the existing text, since a different structure usually means a genuinely different opening and shape, not a find-and-replace.
