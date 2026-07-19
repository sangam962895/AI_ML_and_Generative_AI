# Saanjh.ai (NVLife) — Interview Prep
### For: Generative AI / ML Engineer role | Sangam Kumar Gupt

---

## 1. Company Snapshot (Read this twice before the call)

- **What they are:** "The World's First Health Restoration Institute" — 16-year research initiative on natural health restoration (distress → disorder → disease). Now TRL-6 deep tech, collaborating with **IIT Jodhpur** (Dr. Mitali Mukerji, Dr. Mayank Vatsa — computer vision/ML professor, Dr. Anand Mishra — vision/language/learning).
- **Founder:** Naveen Varshneya ("NV") — 16-year foundational science developer, B.E. Thapar University. Referred to reverently as "NV masters" in testimonials.
- **Core framework — SBD (Sleep-Breath-Desire):** health restores in a "regenerative state" reached via deep sleep or meditation (Yog Nidra), where breath slows to ~8 breaths/min. Rooted in Swar Yog and Yog Sutra concepts (mann, chitt, buddhi, ahankar).
- **The tech pitch (from JD):** an LLM trained on *your* data only, mapping life-events → a "causative model" (why you suffer) and a "mechanistic model" (SBD axis) → personalized restoration insights. Sleep-tracker app launching beta in **August**. Long-term: their own **low-compute, Nvidia-based** parallel computing setup.
- **AI platform lead:** Lipika Jain (IIM Indore, Marktech/AI-driven marketing background — so the AI vision is being driven with a business/product lens, not a pure-ML lens). This tells you: they'll value someone who can **translate deep-tech science into a working product**, not just cite papers.
- **Tone of the company:** spiritual, calm, non-clinical language. Words like "suffering," "regulation," "restoration," "root cause," "energy," "alignment" are used instead of "bug," "failure," "problem," "issue." They actively avoid negativity — testimonials read like healing journeys, not case studies.

**Takeaway for you:** This interviewer likely isn't grilling you on LeetCode-style DSA. They're checking (a) can you actually build LLM/RAG systems, and (b) do you *resonate* with turning deeply personal, sensitive human data into a private, restorative, non-generic AI. Calm, humble, values-aligned energy will land better than aggressive "I optimized X by Y%" corporate energy — keep your quantified wins, but deliver them softly.

---

## 2. How to Carry Yourself (Tone Playbook)

- Speak slower than your normal pace. Don't rush to prove yourself.
- Avoid words like "attack," "kill the bug," "crush the deadline," "brute force." Use "work through," "resolve," "refine," "understand the root cause."
- If you don't know something, say: *"I haven't worked with that directly, but here's how I'd approach learning it"* — humility fits their culture much better than bluffing.
- When they describe their science, **don't debate or challenge it** even if parts sound unfamiliar to your engineering background. Nod to the intent (personalization, privacy, root-cause thinking) — that's genuinely aligned with real ML/RAG principles, so you don't need to fake anything.
- End answers on a constructive/forward note, not a flat stop.

---

## 3. "Tell Me About Yourself" — Your Answer (30-40 seconds, say it naturally, don't rush)

> "I'm Sangam, a Computer Science graduate specializing in Data Science, and I've spent the last year building end-to-end Generative AI systems — from ML models to LLM-integrated products.
>
> My most recent work was during my AI/ML internship at SmartBridge, where I built PlantCareAI — a system that takes a plant image, detects the disease using a CNN, and then uses an LLM to generate a personalized treatment plan for that specific case, not a generic answer.
>
> Alongside that, I've built two RAG-based projects on my own — SummarAIze, which lets you have a grounded conversation with your own documents instead of a generic chatbot, and Talk2Tube, which does the same for YouTube videos. Both taught me how to make an LLM's answers accurate and personal to one person's data, using retrieval instead of just relying on the model's general knowledge.
>
> That's actually what drew me to this role — you're solving the same core problem I've been drawn to: making AI genuinely personal and private to one person's data, just in a much deeper and more meaningful domain. I'd love to bring that RAG/LLM experience here."

**Why this works:** Present → Past → Future structure, under 45 seconds, every line traces straight back to your resume (SmartBridge, PlantCareAI, SummarAIze, Talk2Tube), and it lands on their exact language — "personalized," "private," "one person's data" — without sounding rehearsed or fake.

---

## 4. Technical Questions (from your resume) — Likely + Smart Answers

**Q1: Walk me through your RAG pipeline in SummarAIze.**
> "SummarAIze takes long PDFs or text documents, chunks them, and converts each chunk into embeddings which are stored in a FAISS vector database. When a user asks a question, I embed their query the same way, retrieve the most semantically relevant chunks using similarity search, and pass just those chunks — not the whole document — to the LLM through Groq API. That keeps responses grounded in the actual source and keeps latency under 2 seconds even for 100k+ token documents."

**Q2: Why FAISS in one project and ChromaDB in another?**
> "FAISS is very fast for pure similarity search over a static, one-time-indexed corpus like a PDF — that suited SummarAIze. ChromaDB was better for Talk2Tube because it handles metadata alongside embeddings more naturally, which I needed for timestamp-linked transcript chunks so I could return the exact video moment an answer came from."

**Q3: How would you personalize an LLM's output per user without retraining the model?**
*(This is close to what Saanjh actually needs — answer carefully.)*
> "The most practical way is RAG over a **private, per-user vector store** — every user's data (their events, history, inputs) gets embedded and stored in an isolated namespace or index, so retrieval only ever pulls from that one person's data. The LLM itself stays generic and untouched; the personalization happens entirely at the retrieval layer. This also naturally gives you the privacy property — one user's data literally can't leak into another's context window, since it's never retrieved for them. I did a lighter version of this in PlantCareAI, where I maintained session-based context per user so the model's advice adapted to that user's ongoing conversation instead of giving generic answers every time."

**Q4: The JD mentions "low compute" — how would you approach building an LLM system that's not resource-heavy?**
> "A few levers: use smaller, fine-tuned or distilled open models instead of large general-purpose ones for narrow tasks; keep the heavy lifting in retrieval (RAG) rather than in model size, since retrieval is cheap and precise; cache embeddings instead of recomputing them; and where possible, use quantized models for on-device or edge inference. In my projects I already lean on this pattern — Groq API specifically because it's optimized for low-latency, efficient inference rather than throwing compute at the problem."

**Q5: How do you evaluate whether a RAG system's answers are trustworthy / not hallucinated?**
> "By checking retrieval quality first — are the right chunks even being retrieved — then checking whether the generated answer is fully traceable back to those chunks. In Talk2Tube I optimized chunk size and embedding overlap specifically to improve retrieval accuracy, which I benchmarked at 90%+ for timestamped retrieval. If retrieval is solid, hallucination drops sharply because the model has less room to improvise."

**Q6: Transfer learning — explain what you did in PlantCareAI.**
> "I used a pre-trained CNN backbone and fine-tuned it on a plant-disease image dataset rather than training from scratch, which let me hit 95%+ accuracy across 40+ diseases without needing massive labeled data or compute. That inference feeds into an LLM (Gemini Pro) which turns the raw prediction into a personalized, explained treatment plan — so the ML model diagnoses, and the LLM communicates and personalizes."

**Q7: Have you worked with time-series or sensor/wearable data?**
*(Likely gap — answer honestly, bridge to what you do know.)*
> "Not directly yet — my hands-on work has been with text and image data. But structurally, time-series from a sleep tracker isn't too different from what I already do: it's still about turning raw signals into an embedding-like representation and detecting patterns over time. I'd approach it by first understanding the domain-specific features (sleep stages, breath rate patterns) with your science team, then building the pipeline around that — I see it as a natural next step from the RAG/embeddings work I've already done, not a totally new skill."

**Q8: Prompt engineering — give an example of a prompt you iterated on.**
> Use your Gemini Pro treatment-generation prompt as the example: describe how you structured it to take (disease name + confidence + crop type) and return personalized, non-generic advice, and how you iterated to stop it from giving repetitive or overly generic responses.

---

## 5. Company-Fit / "Soul" Questions — Likely + Smart Answers

**Q9: Why do you want to work here specifically, and not a regular AI company?**
> "Most GenAI roles right now are building yet another chatbot or copilot on top of the same foundation models. What stood out to me here is that you're not just wrapping an LLM — you're building the *causative and mechanistic layer underneath it* from 16 years of real, verified data, so the AI's output actually means something specific to that one person instead of being generic advice. That's a much harder and more meaningful problem — personalization that's genuinely private and rooted in someone's real life events, not just their last five chat messages. I want to build AI where the personalization is the product, not a feature."

**Q10: Health/wellness data is very sensitive. How do you think about privacy here?**
> "The JD already gets this right conceptually — one user's data being useless to another isn't just a privacy feature, it should be architectural: per-user isolated retrieval, no cross-user embedding spaces, and the base model never being fine-tuned on individual identifiable data. I'd want privacy to be a property of the system design, not a policy layered on top afterward."

**Q11: We deal with people's suffering and emotional data — how do you personally approach sensitive topics?**
> "I try to stay grounded and non-judgmental — the goal isn't to diagnose or label someone, it's to reflect their own patterns back to them clearly enough that it helps. That's actually consistent with how I'd want any AI system here to behave: surface insight, don't impose conclusions."

**Q12: Are you comfortable with ambiguity / a very early-stage, small-team environment?**
> "Yes — I like that the JD is upfront that this is foundational-stage work, not a big process-heavy org. I've built each of my projects solo end-to-end, from data pipeline to deployment, so I'm used to owning the full stack of a problem rather than one narrow slice of it."

**Q13 (curveball): This all sounds unconventional/spiritual for an engineering role — does that concern you?**
> "Not at all — the underlying engineering problem (personalization, retrieval, privacy, low-compute inference) is very real and very familiar to me regardless of the philosophy behind why you're solving it. I'm here to build the technology faithfully to your science, not to evaluate the science itself."

---

## 6. Smart Questions YOU Should Ask Them

Asking good questions signals seriousness — pick 2-3:
1. "Where are you in the LLM training/fine-tuning process right now — is the causative-model mapping from life events already structured as data, or is that still being formalized?"
2. "For the low-compute, on-prem Nvidia setup you mentioned — is that something the AI/ML hire would help architect, or is that a later-stage infra decision?"
3. "How is the sleep-tracker beta data (launching August) expected to feed into the LLM training loop — is there a human-in-the-loop review before it shapes the model's insights?"
4. "What does the small founding team's day-to-day collaboration look like once you're co-located?"

---

## 7. Last-Minute Reminders

- Keep your **PlantCareAI, SummarAIze, Talk2Tube** stories crisp — 60-90 seconds each, lead with the problem, then approach, then result.
- Don't over-claim health-domain experience you don't have — bridge honestly (see Q7 style) instead.
- Match their calm tone — no rushed, hyper-corporate energy.
- Carry printed/PDF resume copy; mention GitHub/portfolio links naturally if asked to elaborate on a project.

Good luck, Sangam — you've got the technical foundation; just deliver it in their language.
