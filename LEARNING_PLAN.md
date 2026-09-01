# LEARNING_PLAN.md — 30 sessions to a working ISMS

One session per sitting (60–90 min). Each has: **Concept** (what you must understand
before touching the app), **Build/Task** (what happens in the app — some sessions I
build a module, some sessions you fill it in), and **Quiz** (five questions).

**Answers are deliberately not in this file.** Answer in chat; I grade against the
clause and tell you where a certification auditor would push back.

Clause numbers refer to ISO/IEC 27001:2022. Annex A control IDs are from the same
edition (93 controls, 4 themes). ISO/IEC 27005:2022 is referenced for risk method.

Legend: 🔨 = I build a module · ✍️ = you produce the content · 🎤 = auditor mode

---

## Week 1 — The management system (clauses 4–6)

### Session 1 — Clause 4: context, interested parties, scope 🔨
**Concept.** Clause 4 answers *why this ISMS, for this organisation*. 4.1 issues,
4.2 interested parties and which of their expectations become requirements, 4.3 the
scope (mandatory documented information, must consider 4.1, 4.2 and interfaces with
other organisations), 4.4 the ISMS itself. Everything downstream inherits from here.
**Build/Task.** Scope module is live. ✍️ Complete every `[YOU]` field: the scope
statement decision on OT, the exclusion justification, the boundary-risk note, 5
issues and 4 interested parties.
**Quiz.**
1. Why does clause 4.3 explicitly require you to consider interfaces and dependencies with other organisations — what failure is that requirement designed to prevent?
2. GFS wants to exclude the Jebel Ali office from scope. It shares the M365 tenant and Entra ID directory with in-scope sites. Is the exclusion defensible? Argue both sides, then decide.
3. What is the difference between an "interested party expectation" and an "ISMS requirement", and what does clause 4.2(c) make you do about it?
4. An auditor reads your 4.1 table and asks, "show me where this issue produced something." What are the three legitimate destinations an issue can flow into?
5. If GFS puts the warehouse control system out of scope, name two specific things that become *harder* to claim in front of an EU customer.

### Session 2 — Clause 5: leadership, policy, roles
**Concept.** Leadership is not a signature; clause 5.1 lists what top management must
demonstrably do. 5.2 sets what the information security policy must contain. 5.3
requires assigned and communicated roles, responsibilities and authorities.
**Task.** ✍️ Draft the GFS top-management commitment evidence list: what artefacts
would prove each 5.1 sub-requirement? Draft the RACI for ISMS roles at 250 people
with no dedicated security function.
**Quiz.**
1. Give three artefacts that evidence clause 5.1 without any of them being a policy document.
2. Clause 5.2 requires the policy to include specific things. Name four of them.
3. Who can be the "risk owner" at GFS for a risk about the warehouse control system, and why is the IT manager probably the wrong answer?
4. What is the difference between clause 5.3 and control A.5.2?
5. Top management delegates the whole ISMS to the IT manager and never attends a review. Which clause fails first, and is it major or minor? Justify.

### Session 3 — Clause 6.1.1–6.1.2: risk criteria and the assessment process
**Concept.** Before any risk is written you must define the process: risk acceptance
criteria, criteria for performing assessments, and a method that produces consistent,
valid and comparable results. This is where most homemade risk registers fail.
**Task.** ✍️ Write the GFS risk assessment methodology: scales for likelihood and
impact (define each level in business terms — AED, hours of stoppage, records), the
risk matrix, and the acceptance threshold the board will approve.
**Quiz.**
1. What does "consistent, valid and comparable" actually mean in practice, and how would an auditor test it?
2. Why must risk acceptance criteria be set *before* the risk assessment, not after?
3. Your impact scale says "High = significant business impact." Why will that fail an audit, and how do you fix it in one sentence?
4. GFS's service credits are capped at 5% of contract value. How does that fact change your impact scale?
5. Is a 5×5 matrix required by ISO 27001? What is required?

### Session 4 — Information assets 🔨
**Concept.** ISO 27001:2022 does not require an asset register in the body of the
standard, but A.5.9 (inventory of information and other associated assets) does, and
risk identification is unworkable without one. Asset owner ≠ risk owner ≠ custodian.
**Build/Task.** I build the asset register (owner, classification, location, type,
CIA ratings). ✍️ You add ten GFS assets I did not seed, including at least two OT
assets and one that is not a system (e.g. a process or a paper record).
**Quiz.**
1. Distinguish asset owner, risk owner, and system administrator with a GFS example of each.
2. Why is "the customer portal" a poor asset entry, and what would you replace it with?
3. What does A.5.9 require that a CMDB typically does not give you?
4. Classification: give the four-level scheme you would set for GFS and the handling rule that makes the top level meaningful.
5. Name an information asset at GFS that has high integrity requirements but low confidentiality requirements.

### Session 5 — ISO 27005: identifying risk 🎤
**Concept.** Event-based vs asset-based risk identification. A usable risk statement
has a threat source, an exploitable weakness, an affected asset, and a consequence.
"Ransomware" is not a risk; it is a word.
**Task.** ✍️ Rewrite five badly-worded risks I will give you into proper scenarios.
Then write three GFS risks of your own in the same form.
**Quiz.**
1. Give the four components of a well-formed risk scenario and apply them to the vendor's standing VPN into the OT network.
2. What is the difference between a threat, a vulnerability and a risk source?
3. When is event-based identification better than asset-based? Give a GFS example.
4. Why is "we might fail the audit" not a valid entry in an information security risk register?
5. Turn this into a risk statement: "No one has tested the backups."

### Session 6 — Clause 6.1.2: analysis, evaluation, inherent vs residual 🔨
**Concept.** Analyse consequences and likelihood, determine risk levels, compare
against criteria, prioritise for treatment. Inherent risk = before controls;
residual = after the controls you actually operate (not the ones you plan).
**Build/Task.** I build the risk register with scoring and the heatmap. ✍️ You score
the residual risk on the 15 seeded risks and write 10 more.
**Quiz.**
1. Why does the standard care about the *difference* between inherent and residual, and what happens if you only record residual?
2. You have implemented MFA but 12 service accounts are exempt. What is the honest effect on residual likelihood?
3. Two risks both score 12. One is a data breach, one is a 3-day warehouse stoppage. What does the matrix fail to tell you?
4. Who approves a residual risk that sits above the acceptance threshold, and what is the artefact called?
5. An auditor asks why R-04 dropped from 20 to 6. What evidence must exist for that drop to be legitimate?

### Session 7 — Clause 6.1.3: treatment, Annex A comparison, SoA input
**Concept.** The sequence the standard actually mandates: choose treatment options →
determine necessary controls → *compare with Annex A to check nothing was omitted* →
produce the SoA → formulate a treatment plan → get risk owners' approval of the plan
and acceptance of residual risk. Annex A is a checklist against omission, not a menu
you start from.
**Task.** ✍️ Take your five highest risks and complete a full treatment record:
option (modify / retain / avoid / share), controls, owner, due date, expected residual.
**Quiz.**
1. Name the four risk treatment options and give a GFS example where "share" is the right answer.
2. Why does the standard put "compare with Annex A" *after* determining necessary controls?
3. What two distinct approvals does clause 6.1.3 require, and from whom?
4. A control you selected is not in Annex A. Is that a problem? What must you do?
5. Your treatment plan has 40 actions all due "Q4". What is the finding, and is it a nonconformity or an observation?

---

## Week 2 — Support, operation, and the control themes (clauses 7 and Annex A)

### Session 8 — Clause 6.2 objectives and 6.3 planning of changes
**Concept.** Objectives must be measurable, consistent with the policy, monitored,
communicated and updated, and each needs the what/who/when/resources/evaluation plan.
6.3 (new in 2022) requires changes to the ISMS to be planned.
**Task.** ✍️ Write four GFS information security objectives with metrics and targets
that a board would accept and an auditor could test.
**Quiz.**
1. Why is "improve security awareness" not an objective?
2. What five things does clause 6.2 require you to plan for each objective?
3. Give an objective that is measurable but useless. Why is measurability not enough?
4. How do objectives connect to clause 9.1 and to the management review?
5. What sort of change triggers clause 6.3 — give two GFS examples.

### Session 9 — Clause 7.1–7.3: resources, competence, awareness
**Concept.** Competence (7.2) is about the people doing the work being able to do it,
evidenced by records. Awareness (7.3) is about everyone else knowing the policy, their
contribution, and the implications of not conforming. Different requirements,
different evidence.
**Task.** ✍️ Design the GFS awareness programme for a multilingual warehouse workforce
with 25% turnover, and define what competence evidence exists for the 4-person IT team.
**Quiz.**
1. Competence vs awareness: give the evidence an auditor would ask for, for each.
2. A warehouse picker cannot name the information security policy. Is that a nonconformity? Under which clause?
3. Training completion is 100% but the phishing simulation failure rate is 31%. What does clause 7.3 say about that, and what does 9.1 say?
4. Name three ways to establish competence other than training.
5. Why does 7.3(c) matter to HR and disciplinary process, and which Annex A control pairs with it?

### Session 10 — Clause 7.4 communication and 7.5 documented information
**Concept.** 7.5 is the clause that produces "document control" findings: creation and
update (identification, format, review and approval), and control of availability,
protection, distribution, storage, versioning and retention — including documents of
external origin.
**Task.** ✍️ Define the GFS documented information control scheme, then list every
document ISO 27001 *requires* you to hold. (There are more than you think.)
**Quiz.**
1. List six pieces of documented information explicitly required by the body of ISO 27001.
2. What is the difference between a "document" and a "record" in ISO terms, and does the 2022 edition use those words?
3. Your policies live in SharePoint with version history. What is still missing for 7.5.3?
4. Clause 7.4 asks what, when, with whom and how to communicate. Give the GFS answer for a confirmed data breach.
5. An auditor finds an uncontrolled printed copy of the access control policy in the warehouse. Finding or not? Argue it.

### Session 11 — Annex A: structure, and Organizational controls part 1 🔨
**Concept.** 93 controls in 4 themes: Organizational (37), People (8), Physical (14),
Technological (34). Each control also carries attributes (control type, information
security properties, cybersecurity concepts, operational capabilities, security
domains) — useful for filtering, not required to be used.
**Build/Task.** I build the control library with all 93 controls, plain-English
explanation, example evidence, and status. ✍️ You set the status of A.5.1–A.5.18 for
GFS honestly, including "partial", and note the evidence that would exist today.
**Quiz.**
1. Name the four themes and the number of controls in each.
2. What replaced the 14 clauses of the 2013 Annex A, and what happened to the count?
3. What is a "control attribute", and is using them mandatory?
4. A.5.1 and clause 5.2 both concern policy. What is the difference?
5. Which Annex A control would you use to manage the vendor's standing OT access, and why is it not A.8.2?

### Session 12 — Organizational controls part 2 (A.5.19–A.5.37)
**Concept.** Supplier relationships, cloud services (A.5.23, new), incident management
(A.5.24–A.5.28), continuity (A.5.29–A.5.30, and ICT readiness is new), legal and
compliance (A.5.31–A.5.37).
**Task.** ✍️ Status and evidence notes for A.5.19–A.5.37 for GFS.
**Quiz.**
1. A.5.23 is new in 2022. What does it require that A.5.19–A.5.22 does not cover?
2. Difference between A.5.29 and A.5.30 in one sentence each.
3. What is the "collection of evidence" control and when does it bite in a logistics company?
4. A.5.31 asks for identification of legal, statutory, regulatory and contractual requirements. How does that relate to your clause 4.2 table?
5. Which control covers the classification of information — and which covers labelling? Why are they separate?

### Session 13 — People controls (A.6.1–A.6.8)
**Concept.** Screening, terms of employment, awareness, disciplinary process, post-
employment responsibilities, confidentiality agreements, remote working, and event
reporting. Cheap controls with the highest failure rate in practice.
**Task.** ✍️ Status for all 8; design the JML (joiner–mover–leaver) evidence trail
for a warehouse worker who leaves without notice.
**Quiz.**
1. A.6.1 screening in the UAE: what constraints exist, and what would you actually do?
2. Why does A.6.4 (disciplinary process) exist as a security control at all?
3. What does A.6.5 require after employment ends, and what is the classic gap?
4. A.6.8 event reporting: what makes a reporting channel actually get used?
5. Contractors from the labour agency are not GFS employees. Which of the eight controls still apply, and how?

### Session 14 — Physical controls (A.7.1–A.7.14)
**Concept.** Perimeters, entry, offices, monitoring (A.7.4 is new), physical threats,
secure areas, clear desk, equipment siting, utilities, cabling, maintenance, disposal,
off-site assets, unattended equipment, storage media.
**Task.** ✍️ Walk the fictional KIZAD warehouse: which of the 14 are strong, which are
theatre, and which are missing? Write the physical security section of the risk register.
**Quiz.**
1. A.7.4 is new in 2022. What does it require and what evidence would you show?
2. Comms room at Mussafah shares a wall with a loading bay. Which controls are engaged?
3. What is the difference between A.7.9 and A.7.13?
4. Why does A.7.11 (supporting utilities) matter more in Abu Dhabi than in Frankfurt?
5. A driver's handheld terminal is stolen from a van. Which physical and technological controls should have already applied?

### Session 15 — Technological controls part 1 (A.8.1–A.8.16)
**Concept.** Endpoints, privileged access, information access restriction, source code,
secure authentication, capacity, malware, technical vulnerabilities, configuration,
deletion, masking, DLP, backup, redundancy, logging, monitoring activities.
**Task.** ✍️ Status and evidence for A.8.1–A.8.16 for GFS as described.
**Quiz.**
1. A.8.2 vs A.8.3 vs A.8.18: three access-related controls. Distinguish them.
2. A.8.9 configuration management is new. What does it require beyond a hardening standard?
3. What does A.8.13 require you to do that having backups does not satisfy?
4. A.8.16 monitoring activities: what is the minimum credible implementation for a 4-person IT team?
5. A.8.12 DLP is often marked "not applicable" by small companies. When is that defensible and when is it evasion?

### Session 16 — Technological controls part 2 (A.8.17–A.8.34)
**Concept.** Clock sync, privileged utilities, software installation, network security
and segregation, web filtering, cryptography, secure development lifecycle,
outsourced development, separation of environments, change management, test
information, and audit test protection.
**Task.** ✍️ Status and evidence for A.8.17–A.8.34. Pay attention to A.8.22
(segregation of networks) — this is the OT question again.
**Quiz.**
1. Why is A.8.22 the single most consequential control for GFS?
2. A.8.25–A.8.29 concern development. GFS's portal was built by a contractor in 2019. Which apply, and how do you evidence them retroactively?
3. What is A.8.31 and why does it fail so often in small companies?
4. A.8.24 use of cryptography: what does the control require you to have that is not a TLS configuration?
5. A.8.34 protects systems during audit testing. What is the risk it addresses?

---

## Week 3 — Applicability, policy, and operation

### Session 17 — Statement of Applicability 🔨
**Concept.** The SoA is the ISMS's spine: for all 93 controls, whether it is necessary
(and why), whether it is implemented, and the justification for excluding any control.
It is the document a certification body reads first, and it is a mandatory output of
clause 6.1.3(d).
**Build/Task.** I build the SoA generated from the control library. ✍️ You write the
justification for every control you marked not applicable.
**Quiz.**
1. Why must an SoA justify *inclusions* as well as exclusions?
2. What is the difference between "not applicable" and "not implemented"?
3. Where must the justification for inclusion point back to, to be credible?
4. GFS marks A.8.26 (application security requirements) not applicable "because we don't develop software". Attack that justification.
5. Can the SoA be a spreadsheet? What are the version control implications for a document that changes with every risk treatment decision?

### Session 18 — SoA quality and the risk treatment plan
**Concept.** The RTP and the SoA are different documents doing different jobs. The RTP
is the plan (actions, owners, dates, resources); the SoA is the standing statement.
**Task.** ✍️ Produce the GFS risk treatment plan from your risk register, and reconcile
it against the SoA. Find at least two contradictions — there will be some.
**Quiz.**
1. Name three ways an SoA and a risk register can contradict each other.
2. If a control is "implemented" in the SoA but the corresponding risk is still above threshold, what has gone wrong?
3. Who signs the RTP and who signs the acceptance of residual risk?
4. How often must the SoA be reviewed? What does the standard actually say?
5. A new EU customer requires a control not in Annex A. Where does it live?

### Session 19 — Policy hierarchy; the InfoSec Policy 🔨
**Concept.** Policy (what and why, board-owned) → standard (mandatory specifics) →
procedure (how) → record (proof). A.5.1 requires topic-specific policies to be defined,
approved, published, communicated, acknowledged and reviewed.
**Build/Task.** I write the full GFS Information Security Policy as the worked example
and give you outlines for the other five. ✍️ You review mine and mark three things you
would challenge as an auditor.
**Quiz.**
1. What must A.5.1 be able to evidence beyond the document existing?
2. Where does an acceptable-use rule belong: policy, standard or procedure? Defend it.
3. Your policy says "all systems must be patched within 14 days." Why is that sentence dangerous?
4. Who should own the information security policy at GFS, and who should approve it?
5. What triggers a policy review other than the calendar?

### Session 20 — Access Control Policy ✍️
**Concept.** A.5.15–A.5.18 plus A.8.2, A.8.3, A.8.5. Access control policy is where
the identity lifecycle, privilege model and authentication requirements get committed.
**Task.** ✍️ You write it, using my outline. Cover joiners/movers/leavers, privileged
access, service accounts, the OT exception, and periodic review.
**Quiz.**
1. Which Annex A controls must your policy be able to point at?
2. How do you write a rule for the vendor's standing OT access that is honest and auditable?
3. What is the review cycle for access rights, and what is the evidence?
4. Service accounts cannot use MFA. Write the compensating rule.
5. What does "need to know" mean operationally in a warehouse where staff share terminals?

### Session 21 — Acceptable Use and asset handling ✍️
**Concept.** A.5.10 acceptable use, A.5.11 return of assets, A.7.7 clear desk,
A.7.9/A.7.10 off-site assets and storage media.
**Task.** ✍️ Write the acceptable use policy for a workforce that is 60% operational
and reads limited English. Length is a design constraint, not a virtue.
**Quiz.**
1. What makes an AUP enforceable in a disciplinary process?
2. Personal phones are used to scan barcodes. Policy position?
3. What is the relationship between A.5.10 and A.6.4?
4. Which controls cover removable media at GFS, and what is your position on USB?
5. How do you evidence acknowledgement across 250 people including agency staff?

### Session 22 — Incident Response ✍️ 🎤
**Concept.** A.5.24–A.5.28: planning and preparation, assessment and decision, response,
learning, evidence collection. Plus clause 10.2 (nonconformity and corrective action)
and the contractual 24-hour customer notification GFS signed up to.
**Task.** ✍️ Write the incident response policy and the severity matrix. Then I run a
tabletop as auditor: ransomware on the WMS at 02:00 during peak season.
**Quiz.**
1. Distinguish event, incident, and nonconformity.
2. What decision must be made within the first hour under A.5.25, and by whom?
3. GDPR gives 72 hours; your contract says 24. Which drives the procedure, and what does UAE PDPL add?
4. Why is A.5.28 (evidence collection) more than "keep the logs"?
5. What is the ISO 27001 requirement that turns an incident into an improvement?

### Session 23 — Supplier security ✍️
**Concept.** A.5.19–A.5.23: supplier relationships, addressing security within
agreements, ICT supply chain, monitoring and review, cloud services.
**Task.** ✍️ Write the supplier security policy and produce the tiering model. Apply it
to Microsoft, the OT vendor, the last-mile subcontractors and the labour agency.
**Quiz.**
1. Why does the same policy have to treat Microsoft and a two-van delivery subcontractor differently?
2. What does A.5.21 require about the ICT supply chain that A.5.19 does not?
3. The OT vendor refuses security clauses. What are your actual options, in order?
4. What evidence proves A.5.22 (monitoring and review) is operating?
5. Shared responsibility: name three things in Azure that remain GFS's responsibility.

### Session 24 — Business continuity and ICT readiness ✍️
**Concept.** A.5.29 (continuity of information security during disruption) and A.5.30
(ICT readiness for business continuity), plus the availability side of your risk
register. RTO/RPO are business decisions, not IT preferences.
**Task.** ✍️ Write the BCP outline, set RTO/RPO for the portal, the WMS and the OT
system, and design the backup restore test that A.8.13 needs.
**Quiz.**
1. What is the difference between A.5.29 and A.5.30, precisely?
2. Who sets the RTO for the warehouse control system at GFS?
3. Why is "we have backups in Azure" not an answer to A.5.30?
4. What must a restore test produce as evidence?
5. Does ISO 27001 require a BIA? Does anything require it?

---

## Week 4 — Checking, auditing, and improving (clauses 8–10)

### Session 25 — Clause 8: operation
**Concept.** 8.1 plan, implement and control processes and keep documented information
to have confidence they were carried out; control planned changes and review
unintended ones; control externally provided processes. 8.2 perform risk assessments
at planned intervals or on significant change. 8.3 implement the treatment plan.
**Task.** ✍️ For five controls you marked "implemented", identify the artefact that
proves operation, not existence. Notice how many produce nothing.
**Quiz.**
1. What does clause 8.1 mean by "confidence that the processes have been carried out as planned"?
2. What triggers a risk reassessment under 8.2 other than the calendar?
3. Externally provided processes: which GFS processes does 8.1 catch?
4. Give an example of a control that is implemented but produces no evidence, and fix it.
5. What is the difference between evidence of design and evidence of operating effectiveness?

### Session 26 — Clause 9.1: monitoring, measurement, analysis, evaluation
**Concept.** You must determine what needs monitoring, the methods, when, by whom, and
when results are analysed and evaluated — and the methods must produce comparable and
reproducible results.
**Task.** ✍️ Design the GFS security KPI set: no more than eight, each with a source,
an owner, a frequency, a target, and a decision it informs.
**Quiz.**
1. Why is "number of blocked emails" a bad KPI and what is a good one near it?
2. What does "comparable and reproducible" exclude?
3. Which KPIs would you show a board that has never seen one?
4. How do KPIs feed the management review, and which input of 9.3 are they?
5. Distinguish a metric, a KPI, and a control effectiveness measure.

### Session 27 — Clause 9.2: internal audit 🔨
**Concept.** An internal audit programme (frequency, methods, responsibilities,
planning, reporting) considering importance and previous results; auditors must be
objective and impartial; results reported to relevant management; documented evidence
of the programme and results.
**Build/Task.** I build the internal audit module. ✍️ You write the annual audit
programme for GFS and the checklist for one clause-4 audit.
**Quiz.**
1. Can the IT manager audit the IT department? What exactly does the standard require?
2. What is the difference between the audit programme and the audit plan?
3. What must an internal audit cover — the standard, your own requirements, or both?
4. How does "importance of the processes concerned" change the audit frequency at GFS?
5. Your internal auditor is your ISO consultant who wrote the ISMS. Problem?

### Session 28 — Findings, root cause, and clause 10.2 corrective action
**Concept.** Major nonconformity (a systemic failure, or absence of a required
element), minor (an isolated lapse), observation / opportunity for improvement.
Clause 10.2 requires reaction, evaluation of the need to eliminate the cause so it
does not recur, implementation, review of effectiveness, and records of both.
**Task.** ✍️ Grade ten findings I will give you as major/minor/observation and justify
each. Then write two corrective actions with genuine root cause, not "staff reminded".
**Quiz.**
1. Give the test you apply to decide major vs minor.
2. Why is "we retrained the employee" almost never a corrective action?
3. What is the difference between correction and corrective action?
4. What does clause 10.2 require you to record?
5. Three minor nonconformities against the same clause across three departments. What have you actually got?

### Session 29 — Clause 9.3: management review 🔨
**Concept.** Fixed required inputs (status of prior actions, changes in issues and
interested parties, feedback on performance including nonconformities, monitoring
results, audit results, fulfilment of objectives, feedback from interested parties,
risk assessment results and treatment plan status, opportunities for improvement) and
required outputs (decisions on improvement and any need for change to the ISMS).
**Build/Task.** I build the one-page board briefing generator. ✍️ You chair the review:
write the minutes and the decisions, using the generated pack.
**Quiz.**
1. List six of the required inputs to management review from memory.
2. What are the required *outputs*, and why do minutes that only record discussion fail?
3. How often must management review happen? What does the standard say, and what do auditors expect?
4. Which 9.3 input comes directly from your clause 4 tables, and why is that link deliberate?
5. Your review pack shows all objectives met and no findings. What should an auditor suspect?

### Session 30 — Clause 10, certification, and the mock audit 🎤
**Concept.** 10.1 continual improvement, 10.2 nonconformity and corrective action.
Then the certification cycle: Stage 1 (documentation and readiness, usually including
scope, SoA, risk assessment, internal audit and management review), Stage 2 (evidence
of operation), surveillance years 1 and 2, recertification at year 3.
**Task.** 🎤 Full mock Stage 2 audit. I audit; you produce evidence from the app.
**Quiz.**
1. What does a Stage 1 auditor look for, and what is the most common reason for a delayed Stage 2?
2. How long must the ISMS have been operating before Stage 2 is credible, and why?
3. What is the difference between continual improvement (10.1) and corrective action (10.2)?
4. What happens to your certificate if a major nonconformity is raised at surveillance?
5. GFS's scope statement excludes OT. An EU customer asks whether their goods are safe from a warehouse ransomware event. Answer as the ISMS manager, honestly.

---

## How to use auditor mode

At any point, run a session against `auditor/AUDITOR_MODE.md`. Sessions 5, 22 and 30
have it built in, but the highest-value use is unscheduled: pick a control you claim
is implemented and try to survive the questioning.
