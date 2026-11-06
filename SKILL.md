---
name: motion-design
description: Implement or review interface motion using precise timing, trigger-based transitions, gesture physics, and shared-object continuity. Use for dropdowns, popovers, state changes, press feedback, draggable controls, and animated reveals.
---

# Motion Design

Make motion explain where an element came from, what changed, and where it went. Treat the values below as the user's motion defaults; adapt them when an existing product convention or explicit request calls for something else. Apply only patterns relevant to the interaction.

## Choose the behavior

Before editing, inspect the existing motion system and identify the trigger, entering and leaving states, spatial origin, and interruption behavior. Use the project's current animation tools. For a review, report concrete mismatches and proposed values; for implementation, wire the full interaction through exit and interruption.

## Timing and easing

| Situation | Default |
| --- | --- |
| Entrance | Ease out: arrive promptly and decelerate into place. |
| Movement between visible positions | Ease in-out: accelerate and decelerate smoothly. |
| Dropdown entrance | 150–250 ms; start at 200 ms when no duration exists. |
| Exit | About 80% of the entrance duration; a 200 ms entrance gets a 160 ms exit. |
| List entrance | Offset consecutive rows by 30 ms. |
| State replacement | Start the incoming state as the outgoing state leaves. |

Use non-overshooting easing for everyday transitions. Reserve spring bounce for deliberately expressive moments or physical interactions that justify it. Keep user-controlled motion directly attached to input; smoothing belongs in the release and settle phase.

## Origins and continuity

- **Popovers:** start at scale `0.95`. Set transform origin to the trigger-facing edge or anchor, accounting for placement and collision flips. Expand from the trigger and collapse back toward it. Opacity may support the transition, but avoid an unanchored fade into the center.
- **Object travel:** use a restrained arc when an object moves between destinations and its path communicates the relationship. Keep ordinary panel alignment and constrained controls on their natural axes.
- **Shared objects:** preserve identity across views with the same layout ID or the animation system's equivalent. Keep IDs unique among unrelated objects; scope repeated instances. Match source and destination geometry so continuity survives the handoff.
- **Reveals and color changes:** reveal through a mask or clipped overlay. Keep the final surface underneath and animate the reveal boundary; use a simple immediate change when the reveal adds no meaning.
- **Settling details:** let the primary surface establish itself, then stagger its secondary details. Use 30 ms row offsets for lists; avoid layering a second stagger over the same rows. Keep the sequence short enough that controls remain responsive.

## Feedback and physicality

- **Buttons:** scale to `0.97` while pressed and restore on release or cancellation. Apply the transform to a visual layer when scaling the hit target would destabilize input. Support keyboard activation as well as pointer input.
- **Moving knobs:** stretch by 12% along the direction of travel (`1.12` on that axis), then return to `1` as movement settles. Keep the track position and hit area stable. Avoid a permanent stretch at rest.
- **Success:** use one brief pulse after confirmed success, then return to the resting state. Preserve a visible or announced success message so the pulse is supplemental feedback.
- **Icon changes:** overlap outgoing and incoming icons, crossfading with subtle scale and blur. Keep their shared container dimensions stable; end with one crisp icon. Use opacity and scale alone if blur renders poorly.
- **Drag boundaries:** apply increasing resistance beyond the bounds rather than a hard stop. A useful displacement mapping is `sign(d) * L * abs(d) / (L + abs(d))`, where `d` is overshoot and `L` limits visual stretch. Keep the committed value clamped and settle the visual back inside on release.
- **Handheld motion:** interpret this as motion attached to a held pointer or touch gesture unless context specifies a handheld-camera effect. While held, track input directly without a time-based tween that chases the pointer. On release, use velocity-aware settling. Preserve authored camera irregularity if handheld-camera motion is intended.

## Ship the complete interaction

Animate transforms and opacity where possible; profile masks, blur, and layout transitions on the affected device rather than assuming they are cheap. New input must interrupt from the current visual state without snapping or waiting in a queue. Cancel stale completion callbacks when an interaction reverses.

For reduced motion, remove travel, stretch, blur, stagger, and pulses; present the final state immediately or with a short opacity change. Keep focus, keyboard operation, hit targets, and status announcements intact throughout transitions.

Verify opening, closing, rapid reversal, repeated activation, keyboard use, reduced motion, and touch or drag cancellation where relevant. Inspect the actual interaction at normal speed: confirm its origin, exit destination, overlapping state handoff, and settled geometry. Report what changed and what was verified; identify any behavior that could not be exercised.
