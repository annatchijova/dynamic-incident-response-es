---
author: Joshua Wright
date: 2026-09-16
title: "Response Actions Loop: Step-by-Step"
---

<figure>
<img src="../images/dair-responseactions.png"
alt="dair responseactions" />
</figure>

The following steps provide a condensed reference for response actions
loop activities. Each step corresponds to topics covered in the Response
Actions Loop chapter of *Dynamic Incident Response*
([www.dynamicincidentresponse.com](https://www.dynamicincidentresponse.com)),
organized for use when managing the iterative cycle of scoping,
containment, eradication, and recovery. The chapters that follow examine
each activity in greater depth.

The loop is inherently iterative: a single pass rarely produces a
complete response because initial understanding is partial, new insights
surface during eradication, and evidence analysis reveals previously
unknown attack vectors. Expect to cycle through the loop multiple times,
with each activity expanding in sophistication as understanding
improves.

# Step 1. Run the Loop Expecting Each Activity to Deepen Across Iterations

Representative principles include:

- The four constituent activities (scope, contain, eradicate, recover)
  are owned by their own chapter step-by-step sections; this guide
  focuses on what is unique to running them as a loop. Refer to the
  individual scope, contain, eradicate, and recover step-by-step guides
  for the per-activity work.

- Sequence depends on incident state, not on a fixed order: scope is
  usually the first activity in any iteration but contain may precede or
  run in parallel when an active threat requires it.

- Each subsequent iteration should produce more sophisticated and
  complete results than the previous one as understanding accumulates.

# Step 2. Identify Iteration Triggers Requiring Additional Response Cycles

Representative iteration triggers include:

- New indicators of compromise were discovered during analysis.

- Evidence of incomplete eradication or reinfection.

- Revelations from forensic analysis that require expanded scoping.

- Changing business priorities or regulatory requirements.

# Step 3. Maintain Cross-Phase Documentation and Communication

The loop owns the cross-phase communication cadence; the per-activity
documentation steps in scope, contain, eradicate, and recover feed into
this cadence. Representative activities include:

- Record decision documentation for each activity (what, when, who,
  rationale).

- Track the impact assessment of response actions on business processes
  and system availability.

- Provide stakeholder communication tailored to different audiences
  (executive summaries, technical briefings, user notifications).

- Maintain documentation continuity across iterations, linking related
  findings and actions.

- Adjust communication frequency and detail based on incident severity
  and stakeholder needs.

# Step 4. Build Cumulative Understanding Across Iterations

Representative activities include:

- Document findings from each iteration to support the overall incident
  narrative.

- Link new discoveries to prior iterations for continuity.

- Ensure knowledge transfer between shifts through coordinated
  documentation.

# Step 5. Monitor for Technical Indicators of Resolution

Representative indicators include:

- No new IOCs discovered during scoping activities.

- Monitoring shows no signs of attacker activity.

- Eradication verification confirms threat removal.

- Systems are operating normally after recovery.

# Step 6. Assess Business Indicators for Loop Conclusion

Representative indicators include:

- Operational objectives are met.

- Acceptable risk level has been achieved.

- Cost-benefit analysis supports concluding the active response.

- Resource constraints require prioritization of decisions.

# Step 7. Engage Decision-Makers for Loop Exit Determination

Representative activities include:

- Present technical and business indicators to leadership.

- Discuss risk acceptance for residual uncertainties.

- Confirm regulatory requirements for incident closure are met.

- Establish ongoing monitoring plans for continued vigilance.

# Step 8. Address Practical Considerations Throughout Iterations

Representative considerations include:

- Manage team fatigue through rotation and rest periods to maintain
  effectiveness across multiple cycles.

- Account for budget constraints and tool limitations that may affect
  iteration speed, particularly time-consuming forensic analysis or
  evidence collection.

- Balance documentation requirements with active response efforts,
  avoiding excessive documentation that detracts from active response.

- Manage stakeholder patience as iterations continue. Leadership may
  view repeated cycles as poor execution rather than as the natural
  progression of incident understanding.

- Communicate progress to stakeholders to manage expectations, explain
  the value of iterative learning, and address business pressure for
  faster resolution.
