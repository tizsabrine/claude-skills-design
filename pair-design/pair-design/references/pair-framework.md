# PAIR Framework Reference

Source: Google PAIR (People + AI Research) Guidebook — pair.withgoogle.com/guidebook
All 6 chapters. Use this as reference when generating design briefs.

---

## Chapter 1: User Needs + Defining Success

**Core question**: Does this feature justify AI, and what should it optimize for?

### When AI adds unique value (use AI)
- Recommending different content to different users (personalization)
- Prediction of future events
- Natural language understanding across varied inputs
- Recognition of a whole class of entities (not enumerable with rules)
- Detection of low-occurrence events that change over time
- Dynamic content surfacing where a static interface would fail

### When AI is probably NOT better (consider rule-based alternatives)
- Maintaining predictability / consistent affordances
- Static or limited information (e.g. form fields)
- When cost of errors is very high and outweighs small accuracy gains
- When complete transparency is required
- When people explicitly say they don't want the task automated

### Automation vs. Augmentation

**Automate when:**
- Task is boring, repetitive, awkward, or dangerous
- People lack knowledge or ability to do it well
- Scale makes human effort uneconomical
- There's consensus on the "correct" output
- Easy to offer human-in-the-loop override

**Augment when:**
- People enjoy the task or it carries social capital
- Personal responsibility for the outcome matters (legally, emotionally, financially)
- Stakes are high (health, safety, finance, relationships)
- Specific preferences are hard to communicate (creative work, taste)
- People don't agree on what "correct" looks like

**Key framing**: Augmentation gives users "superpowers" — automation replaces them. When in doubt, augment first.

### Reward Function Design

The reward function is how an AI defines success and failure internally. Naive metrics (clicks, completions, time-on-task) often diverge from actual user value.

**Design the reward function deliberately:**
- Identify what the AI is implicitly optimizing for
- Check whether that metric aligns with long-term user benefit
- Imagine the downstream effects: what behavior does this incentivize?
- Share the reward function logic with users when possible (helps set expectations)

**Common misalignments:**
- Optimizing for engagement → encourages addictive patterns
- Optimizing for task completion → encourages speed over quality
- Optimizing for explicit positive feedback → creates feedback desert (only extremes respond)

---

## Chapter 2: Data Collection + Evaluation

**Core question**: Is our training data appropriate, representative, and responsibly sourced?

### Data quality criteria
- Accurately represents real-world phenomenon
- Collected, stored, and used responsibly
- Representative of actual user population (not just easy-to-get subset)
- Documented (Data Cards)

### Data cascade risk
Poor data choices compound downstream. A dataset skewed toward a subset of users will create a product that works poorly for everyone else — often invisibly at first.

### Key data design decisions
- Scope of features (what signals are used): missing features cause systematic blind spots
- Quality of labels: subjective labels require clear criteria, well-designed labeler UX
- Representativeness: who is and isn't represented in training data
- What users are NOT telling the AI (their wider context the model can't know)

### Privacy & transparency
- Tell users what data the AI uses and what it doesn't have
- Explain: Scope (what's collected), Reach (personalized vs. aggregate), Removal (can user delete/reset?)
- Don't surprise users by revealing their own data to them in unexpected ways

---

## Chapter 3: Mental Models

**Core question**: What will users think this AI is, and how do we set accurate expectations?

### Mental model basics
A mental model is a person's understanding of how something works and how their actions affect it. Mismatched mental models cause: unmet expectations, frustration, misuse, abandonment.

Users bring mental models from:
- Analogous products they've used before
- Marketing messages (including misleading ones)
- Sci-fi AI tropes (often sets wildly unrealistic expectations)
- The manual/non-AI version of the task

### Setting expectations for adaptation
AI products change over time based on user behavior. Users need to understand:
- The product will adapt
- Their actions influence what it does
- They can actively shape it (not just passively consume)

### Onboarding framework (PAIR template)
> "This is [product/feature], and it'll help you by [core benefit]. Right now, it's not able to [primary limitation]. Over time, it'll change to become more relevant to you. You can help it get better by [specific user action]."

**Onboarding principles:**
- Explain the benefit, not the technology
- Don't lead with "AI" or "machine learning" — users care about what it does for them
- Keep initial onboarding short; use "inboarding" (contextual hints mid-use) instead
- Encourage low-risk experimentation early
- Let users know that early experimentation won't lock in future behavior

### Human-like framing risks
When AI feels too human:
- Users over-trust its judgment on things humans would be good at but the AI isn't
- Users feel deceived when limitations emerge
- Users may inappropriately apply social norms (apologizing to it, etc.)

**When to disclose AI**: Always, unless the AI nature is obvious. Frame it around user benefit ("this is powered by AI so it gets smarter over time") not technical description.

### Co-learning
The user's mental model and the AI both change over time. Design for:
- Making the feedback relationship legible ("this is how you teach it")
- Helping users understand when the model has updated
- Framing early failures as learning opportunities, not product failures

---

## Chapter 4: Explainability + Trust

**Core question**: How much should users trust this AI, and how do we communicate that calibration?

### Trust components
- **Ability**: Does the product actually solve the user's problem?
- **Reliability**: Does it work consistently across contexts?
- **Benevolence**: Does it clearly serve the user's interests, not just the product's?

### Trust calibration targets
Don't aim for maximum trust — aim for **correct** trust. Both over-trust and under-trust cause harm:
- Over-trust: user relies on AI in situations it can't handle → dangerous outcomes
- Under-trust: user ignores AI when it's actually reliable → wasted value, frustration

### When to explain
- **In-the-moment**: When the output was surprising or consequential
- **During onboarding**: Global properties of the model (strengths, limits, training)
- **At high-stakes moments**: When the user needs to decide whether to act on AI output
- **After errors**: When trust has been damaged

### What to explain
- What data the AI used to make this prediction
- What data it DIDN'T have (gaps in its knowledge)
- Why it made a particular recommendation (when knowable)
- Confidence level — but only when it meaningfully affects the user's decision

### Confidence display guidance
- Show confidence when: the user needs to decide whether to verify or trust the output
- Don't show confidence when: you'd just be showing "this is an AI" universally
- Calibrate: low-confidence outputs should either be suppressed, shown differently, or accompanied by a prompt to verify

### Data transparency keys: Scope / Reach / Removal
- **Scope**: What data about this user is being collected and used
- **Reach**: Is this personalized to them, or trained across all users?
- **Removal**: Can they delete or reset the data that's shaping their experience?

### Explanation quality spectrum (for a given output)
1. No explanation
2. "Here's what we recommended" (what)
3. "Based on your [X]" (what + partial why)
4. "Based on your [X], because [Y]" (full why)
5. "Based on your [X], because [Y]. Note: we don't have data on [Z]." (why + gap disclosure)

Use level 5 in high-stakes moments. Use level 2–3 in routine moments. Never use level 1 when the output is surprising or consequential.

---

## Chapter 5: Feedback + Control

**Core question**: How do users teach the AI, and how much control should they have over it?

### Implicit vs. explicit feedback

**Implicit feedback** = behavior signals collected automatically during product use
- Examples: which recommendations they acted on, how long they engaged, what they skipped
- Must be disclosed in terms of service
- Users should be able to opt out and see what's being collected

**Explicit feedback** = deliberate user input on AI output
- Thumbs up/down, ratings, corrections, category preferences
- Should be: easy to give, clearly tied to a benefit, mutually exclusive and collectively exhaustive choices

### Dual feedback trap
Sometimes a single action has both implicit and explicit signals simultaneously (e.g., a "Like" is both social communication and model training signal). Clarify in design: what does this action actually mean to the AI?

### Feedback acknowledgment spectrum
| Level | Copy | When to use |
|---|---|---|
| 1 | "Thanks for your feedback." | Never — too vague |
| 2 | "Thanks! Your feedback helps us improve future [X] recommendations." | OK for aggregate impact |
| 3 | "Thanks! We'll improve your [X] going forward." | Good default |
| 4 | "Thanks! Your next [X] won't include [Y]." | When you can be category-specific |
| 5 | "We've updated your [X]. Take a look." | Best — use when immediate update is possible |

### Why users give feedback (motivations)
- Material rewards (cash, discounts) — high volume, low quality, biased
- Symbolic rewards (badges, status) — works for social communities
- Personal utility (improves their own experience) — most reliable intrinsic motivation
- Altruism (helping others) — good for review platforms
- Intrinsic enjoyment — hard to design for, but powerful when authentic

**Design implication**: Frame feedback requests around personal utility when possible. "This helps us improve your recommendations" beats "Help us improve our AI."

### Control design
- Let users adjust the AI's behavior in ways that feel meaningful to them
- Distinguish: personalization preferences (what user wants) vs. model training signals (what AI needs)
- Provide opt-out paths that don't break the core experience
- Give feedback mechanisms that have immediate impact when possible (not just "we'll improve over time")

### Setting expectations for AI improvement
- AI improvements are often gradual and non-linear
- Each additional piece of feedback has diminishing marginal impact
- Don't over-promise ("one more rating and you'll get perfect recommendations")
- Under-promise, over-deliver on visible changes

---

## Chapter 6: Errors + Graceful Failure

**Core question**: What can go wrong, how do users perceive it, and how do we design paths forward?

### Error taxonomy

**From the user's perspective:**

**Context errors**: System is technically correct, but user perceives failure because:
- Action isn't well-explained
- It breaks the user's mental model
- It was based on incorrect assumptions about the user's context

**Failstates**: System has no answer or genuinely low-confidence output
- True negative: AI correctly recognizes it can't answer, but user expected it to
- Should be surfaced with honesty, not silent degradation

**False positives**: AI acts confidently on incorrect information
- Highest trust damage, especially in high-stakes situations

**False negatives**: AI misses something it should have caught
- Trust damage proportional to stakes — catastrophic in health/safety domains

**Background errors**: Neither user nor system registers an error — dangerous because invisible. Requires QA processes, not just UX design.

### Error stakes framework

**High-stakes errors** (require stronger design protection):
- Health, safety, financial decisions
- Sensitive social contexts
- User is a novice (less able to self-correct)
- Low user attention (multitasking)
- Narrow definition of "correct" output

**Lower-stakes errors** (graceful degradation is sufficient):
- Experimentation, play, creativity
- Lightweight entertainment
- Non-essential recommendations
- Expert user with high ability to self-correct

### Error timing matters
- Early in product use: users expect imperfection; errors are forgivable
- After extended use: users have higher expectations; errors feel like betrayal
- Design error messaging should account for where the user is in their journey

### Paths forward from failure (required elements)
1. **Acknowledge the error honestly** — don't hide it or blame the user
2. **Explain what went wrong** (at the right level of detail for the stakes)
3. **Give the user something to do** — a correction action, a feedback mechanism, a workaround
4. **Connect error to learning** — position it as the system getting better, not just breaking

### Error messaging formula
Avoid: "No results found." or "Something went wrong."
Aim for: "We couldn't [what] because [why]. Try [specific action] to [user benefit]."
High-stakes version: Add — "Note: [limitation of the system in this context]."

### Error types to proactively design for
1. No training data for user's actual context
2. User's context has changed in ways the model doesn't know (new job, new preferences)
3. Cultural/demographic patterns the model wasn't trained on
4. Edge cases at the boundaries of model competence
5. Simultaneous signals that contradict each other
