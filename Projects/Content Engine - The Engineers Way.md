# Content Engine — The Engineer's Way
*How to have a massive social media presence without becoming a content creator.*

---

## THE PROBLEM, STATED HONESTLY

You can code for 12 hours straight. You can write 5,000 words in a sitting. You can train until your legs give out and film every second of it. But the moment you sit down to "edit for virality" — pick a trending sound, cut to the beat, add hooks, study what the algorithm wants — you shut down. It feels fake. It feels like a waste of your engineering hours. And you're right.

**The math:**
- 1 hour of coding = features shipped, app closer to launch
- 1 hour of writing = 500-1,000 words of IXNAH content
- 1 hour of training = stronger body, new footage
- 1 hour of editing a TikTok = maybe 500 views, maybe 50,000, who knows

Your instinct is correct: the ROI on "trying to go viral" is garbage compared to building real things. The problem is you still need distribution. Nobody downloads an app they've never heard of.

**The solution: automate the content, don't create it.**

You're an AI engineer. Build systems that turn your existing work (training footage, writing, app data) into content automatically. Your job is to train, code, and write. The system's job is to post.

---

## STRATEGY 1: THE AUTOMATED CLIP PIPELINE

### What You Build (Once)

A Python script or Shortcuts automation that:

1. Takes a raw training video from your camera roll
2. Crops it to 9:16 (vertical)
3. Adds a text overlay from a pre-written list (posture name + time + day count)
4. Adds a simple caption from a template
5. Exports it ready to post

### How It Works

**Your input:** Drop a raw clip into a folder. That's it.

**The automation does:**
- Crop/resize to vertical
- Overlay text (from a .json or .csv of pre-written overlays)
- Add a subtle watermark ("El Templo" or your handle)
- Export to camera roll, ready to upload

### Tools

- **FFmpeg** — You know this. Command-line video processing. Crop, overlay text, resize, trim. One script handles everything.
- **Python + moviepy** — If you want more control. Read a config file, batch process clips.
- **Apple Shortcuts** — If you want it on-device. Can trigger from a folder in Files app.

### Example FFmpeg one-liner:
```bash
ffmpeg -i raw_clip.mp4 -vf "crop=ih*9/16:ih,drawtext=text='Ma Bu — Día 147 — 3:00':fontsize=48:fontcolor=white:x=(w-text_w)/2:y=h-100:borderw=2" -t 60 output.mp4
```

**Time investment:**
- Build the pipeline: 2-4 hours (one time)
- Per video after that: 2 minutes (drop clip, run script, upload)

---

## STRATEGY 2: THE WRITING-TO-VIDEO CONVERTER

You write thousands of words. You hate editing video. Solution: turn your writing into video content automatically.

### What You Build

A script that:

1. Takes a text snippet (one of your philosophical one-liners or essay excerpts)
2. Renders it as animated text over a background video (slowed-down training footage)
3. Adds atmospheric music from a royalty-free library or your own tracks
4. Exports as a 30-60 second reel

### How It Works

**Your input:** Add a line to a text file. Example:
```
"Una gran responsabilidad conlleva un gran poder."
"Tu sistema nervioso tiene dos modos: guerrero y místico."
"Bienestar no es felicidad. Bienestar es un estado."
```

**The automation does:**
- Picks a random background clip from your footage library
- Slows it to 50% speed, adds slight color grade
- Renders the text with a typewriter or fade-in animation
- Adds ambient music track
- Exports

### Tools

- **Python + moviepy + Pillow** — Full control over text rendering, timing, effects
- **Remotion** — If you want to go React-based (JS framework for programmatic video)
- **Revideo** — Open source, code-driven video creation

**Time investment:**
- Build: 4-6 hours (one time)
- Per video: 30 seconds (add a line of text, run the script)

---

## STRATEGY 3: APP-GENERATED CONTENT

This is the one nobody else can do. Your app generates data. Data becomes content. Automatically.

### What El Templo Can Auto-Generate

**Personal progress cards:**
When YOU complete a session in the app, it auto-generates a shareable image:
```
┌──────────────────────────┐
│  EL TEMPLO               │
│                          │
│  Ma Bu — 3:42            │
│  Dead Hang — 2:15        │
│  Forward Fold — 1:30     │
│                          │
│  🔥 Racha: 47 días       │
│  📅 15 Feb 2026          │
└──────────────────────────┘
```

Export to camera roll → post to stories. Zero editing. The app makes the content.

**Aggregate user stats (once you have users):**
```
"El 68% de los usuarios de El Templo logran 2 minutos en Ma Bu antes del día 30."
"Los usuarios que entrenan Dead Hang reportan menos dolor de espalda en 14 días."
```

This is content that builds credibility AND promotes the app. And it comes from data you're already collecting.

**Weekly auto-generated recap:**
The app sends YOU a weekly summary of your training. Screenshot it. Post it. Done.

### Build This Into El Templo v1.0

Add a "Share" button on the session complete screen. It generates a card image (like Strava's post-run card or Spotify Wrapped). Users post their own progress → free marketing. You post yours → consistent content.

**Time investment:**
- Build the share card feature: 4-8 hours (one time)
- Per content piece: literally zero. The app does it.

---

## STRATEGY 4: THE BATCH RECORDING PROTOCOL

You said you can train hard and record without an issue. The problem is turning 45 minutes of raw footage into 10 videos. Solution: record with the edit already built in.

### The Protocol

**When you train, set up ONE phone angle. Don't move it. Don't think about framing. Just press record.**

Then, every Sunday, run this process:

1. **Import the week's raw footage into a folder** (5 minutes)
2. **Run a script that splits the video at silence/stillness gaps** — Python + scene detection. It auto-cuts your training footage into individual exercise clips. (2 minutes)
3. **Review the clips. Delete trash. Keep 5-10 good ones.** (10 minutes)
4. **Run the overlay pipeline (Strategy 1) on the keepers.** (5 minutes)
5. **Schedule them across the week.** (5 minutes)

**Total Sunday session: 30 minutes for a full week of content.**

### The Scene Detection Script

```python
# Concept — uses scenedetect library
from scenedetect import detect, ContentDetector
scene_list = detect('weekly_training.mp4', ContentDetector(threshold=30))
# Each scene = one exercise clip
# Auto-export each scene as a separate file
```

You can refine the threshold to match your training rhythm. Between sets = stillness = scene break.

**Time investment:**
- Build the splitter: 2-3 hours (one time)
- Per week: 30 minutes

---

## STRATEGY 5: AI-ASSISTED CAPTION GENERATION

You write well but you hate writing captions and hashtags. Automate it.

### What You Build

A simple script that:

1. Takes the video filename or a 1-line description ("Ma Bu hold, day 147, 3 minutes")
2. Sends it to Claude/GPT API with a pre-written system prompt
3. Returns a caption in your voice (Spanish, short, no hype, body-first)
4. Returns relevant hashtags

### The System Prompt (Write Once, Use Forever)

```
You are writing social media captions for Ricardo Bustos, a martial artist and
engineer who teaches physical mastery through the IXNAH system. His app is
called El Templo.

Rules:
- Spanish only
- Maximum 2 sentences
- No spiritual language, no hype
- Body-first: what does the posture do to your body
- Never use emojis except 🔥 occasionally
- End with "El Templo — link en bio" on 1 out of every 3 posts
- Hashtags: #IXNAH #ElTemplo #EntrenamientoReal + 2-3 relevant ones
```

### Example Output

Input: "Ma Bu hold, day 147, 3 minutes"

Output:
```
3 minutos en Ma Bu. Las piernas ya no tiemblan.
Día 147. #IXNAH #ElTemplo #EntrenamientoReal #MaBu #ArtesMarciales
```

**Time investment:**
- Build: 1 hour (one API call script with a system prompt)
- Per caption: 10 seconds

---

## STRATEGY 6: THE GITHUB-STYLE CONTRIBUTION GRAPH

This one is for Twitter/X. You're an engineer. Engineers understand contribution graphs.

### The Idea

Build a public dashboard (simple web page or even a GitHub repo) that tracks:

- Days trained (green squares)
- Postures mastered (badges)
- Weight progression (line chart)
- Streaks

Post a screenshot of it weekly. "Semana 23. Sin faltar." That IS the content. No editing, no hooks, no trends. Just a graph that proves consistency.

Engineers, developers, and productivity-obsessed people will love this. It speaks their language.

### How to Build It

- A GitHub repo where you commit a daily log file → the contribution graph fills up automatically
- Or: a simple HTML page that reads from a JSON file you update daily
- Or: El Templo app generates it from your training data

**Time investment:**
- Build: 2-4 hours
- Per week: screenshot and post (30 seconds)

---

## STRATEGY 7: LET THE TRAINING BE THE CONTENT (ZERO EDITING)

The most radical approach: post raw, unedited training clips. No overlay. No music. No caption beyond the posture name. Just... what happened.

### Why This Works

1. **Algorithmic truth:** TikTok and Reels actually reward raw content over polished content in fitness/training niches. The algorithm detects "authentic" content and pushes it.

2. **The bar is already low:** Go look at the most successful calisthenics accounts in Latin America. Half of them are shaky phone footage in a park with zero editing. It's the TRAINING that's impressive, not the production.

3. **Your footage is inherently interesting.** A guy doing kung fu stances in his house with a timer is unusual enough to make people stop scrolling. You don't need a hook. The posture IS the hook.

### The Protocol

- Train. Phone is recording.
- After training, pick the best 30-60 second clip.
- Trim start and end only. No overlay, no music.
- Post with 1-line caption.
- Total editing time: under 60 seconds.

### When to Add Production Value

Only when you have DATA showing it works. If raw clips get 500 views and overlaid clips get 5,000 views — then invest in overlays. But test raw first. You might be surprised.

---

## STRATEGY 8: THE WEEKLY THREAD (TWITTER/X)

You can write. Twitter rewards writers. Skip video entirely on this platform.

### The Format

Every Monday, post a thread:

**Tweet 1 (hook):** One sentence from your philosophy. The Spider-Man inversion. A nervous system insight. A training principle.

**Tweet 2-5:** Expand. Keep each tweet under 280 characters. Short, punchy, Spanish.

**Tweet 6:** "Estoy construyendo El Templo — una app para dominar tu cuerpo como entrenas tu mente. [link]"

### Automation

Write 4-8 threads in one sitting on a Sunday. Schedule them with TweetDeck or Typefully for the whole month. One hour per month of writing → consistent Twitter presence.

---

## THE FULL AUTOMATED STACK

Here's what your content workflow looks like once everything is built:

```
DAILY:
  Train → phone records → clip auto-saved to folder

SUNDAY (30 minutes total):
  1. Run scene splitter on week's footage → 10-15 clips
  2. Pick best 5 → run overlay pipeline → 5 ready-to-post videos
  3. Run caption generator → 5 captions
  4. Schedule Mon/Tue/Wed/Thu/Fri across TikTok + IG + YouTube
  5. Write 1 Twitter thread (or pull from existing essays)
  6. Screenshot El Templo weekly progress card → post to stories

MONTHLY (1 hour):
  Write 4 Twitter threads for the month → schedule all of them
  Review: which clips got traction? Adjust the overlay templates if needed.

NEVER:
  - Study trending sounds
  - Learn video editing software
  - Watch "how to grow on TikTok" videos
  - Spend more than 30 minutes/week on content
```

---

## WHAT TO BUILD FIRST (Priority Order)

### Week 1: The FFmpeg overlay pipeline
- One script. Vertical crop + text overlay + export.
- This alone eliminates 90% of your editing pain.
- 2-4 hours to build. Saves 30+ minutes per video forever.

### Week 2: The caption generator
- One API call script with your system prompt.
- 1 hour to build. Saves 5 minutes per post forever.

### Week 3: The share card in El Templo
- Build the post-session shareable image.
- 4-8 hours to build. Generates infinite content from app usage.

### Week 4: The scene splitter
- Auto-cuts raw training footage into individual clips.
- 2-3 hours to build. Turns 1 hour of footage into 10 videos.

**Total engineering investment: ~15-20 hours over 4 weeks.**
**Result: a content machine that runs on 30 minutes/week of your time.**

---

## THE MINDSET SHIFT

You're not becoming a content creator. You're building a **content generation system.**

Content creators edit. Engineers automate.
Content creators chase trends. Engineers build pipelines.
Content creators spend hours per video. Engineers spend hours once, then run the script.

Your social media presence should feel like a CI/CD pipeline:
- Raw footage = source code
- Overlay script = build step
- Caption generator = docs generation
- Scheduled posts = deployment
- Analytics = monitoring

You never touch the production line. You just feed it raw material (training footage + writing) and it outputs content.

**The only manual work that remains:**
1. Train (you're doing this anyway)
2. Record while training (press one button)
3. Write IXNAH content (you need to do this for the book/app regardless)
4. 30-minute Sunday batch (run scripts, review, schedule)

Everything else is automated. That's how an engineer does content.

---

## BONUS: THINGS YOUR AI ENGINEERING SKILLS UNLOCK THAT NOBODY ELSE CAN DO

1. **Computer vision for form checking.** Down the road: use MediaPipe/PoseNet to analyze training footage and detect posture errors. Build it into El Templo. Users record themselves doing Ma Bu → the app tells them their knees are caving in. That's a feature worth paying $8/month for.

2. **Auto-generated training plans.** User inputs: current stage, goals, available time. El Templo generates a personalized weekly plan. Basic recommendation engine. You can build this.

3. **Voice-to-content pipeline.** Record yourself talking during a walk (you don't have to be on camera). Whisper API transcribes it → Claude cleans it into an essay or caption → pipeline turns it into text-on-video content. You never type, never edit, never think about "content." You just talk and the system handles the rest.

4. **Training footage auto-highlights.** Run your raw training videos through a simple motion detection model. High-motion moments = the interesting parts. Auto-extract those as clips. Zero manual review needed.

5. **Automated A/B testing.** Post the same clip with two different overlays/captions on different days. Track which performs better. Feed that data back into your caption generator prompt. Self-improving content system.

You have skills that would cost a content creator $5,000-10,000/month to hire. You have them for free. Use them to build the machine, not to do the labor.

---

## THE ORIGIN STORY — YOUR MOST POWERFUL ASSET (USE IT ONCE, USE IT RIGHT)

127kg. Depression. Alcoholism. Tobacco. Weed. Psychedelics. Couldn't move. A DMT vision cracked everything open. Now 89kg, training daily, building an app, writing books, working as an AI engineer.

That's not a social media bio. That's the kind of story that makes someone stop scrolling and never forget your name.

### How to Use It Without Becoming a "Vulnerability Influencer"

You don't appear on camera. You don't monologue about your feelings. Good. Here's how to deploy this story with the same engineering precision as everything else:

**Use it ONCE, publicly, as a text post or narrated video.**
Write 200-300 words. The facts. No drama. No "I hit rock bottom and then..." storytelling voice. Just:

- Where you started (numbers, substances, state)
- What broke it open (the vision — you don't have to explain DMT, just say "tuve una visión")
- What you built (the system, the training, the app)
- Where you are now (89kg, engineer, building El Templo)

Post it. Pin it to your profile. That's your origin story forever. You never have to tell it again.

**After that, the BODY tells the story.**
Every training clip you post — the stances, the holds, the progression — is a silent statement: "I was 127kg and couldn't move. Now watch this." You never say it. People who read the pinned post will know. New followers will discover it. The contrast between the pinned origin story and the daily training clips does all the work.

**Never:**
- Turn your addiction story into regular content
- Post "one year sober" anniversary content
- Use your mental health history as a hook for views
- Let the story become bigger than the system

**The story is the DOOR. IXNAH is the ROOM. The app is the HOUSE.**
People enter through the story. They stay for the system. They pay for the tool.

### The One Video That Matters Most

If you make ONE produced piece of content in your entire life, make this:

**A 60-90 second reel. No face. Just:**
- Old footage/photos from your heaviest (if you have any)
- Text: "127 kg. No me podía mover."
- Cut to recent training footage — stances, holds, calisthenics
- Text: "89 kg. Construí un sistema. Se llama IXNAH."
- Cut to the app on a phone screen
- Text: "Lo convertí en una app. Se llama El Templo."
- Final text: "El cuerpo va primero. La consciencia sigue."
- Black screen. Logo or handle.

That video, with the right atmospheric music (maybe your own track), will be the most viewed thing you ever post. And you only have to make it once. Your automated pipeline handles everything after that.
