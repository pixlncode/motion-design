# Motion Design

A reusable agent skill for purposeful interface motion: precise timing, anchored transitions, gesture feedback, and shared-object continuity.

The skill includes ease-out entrances, 150–250 ms dropdowns, 30 ms list staggering, 0.97 button press scale, 12% knob stretch, shorter exits, overlapping state changes, masked reveals, icon transitions, rubberbanding, and shared layout identity. It also covers interruption, reduced motion, and verification.

## Install

Copy this repository into your agent's skills directory as `motion-design`. The repository root contains `SKILL.md` and optional Codex interface metadata in `agents/openai.yaml`.

For Codex, use `$CODEX_HOME/skills/motion-design`, or `~/.codex/skills/motion-design` if `CODEX_HOME` is unset. Restart your agent session after installation if needed.

## Use

Invoke `$motion-design` to implement or review an interaction, for example:

> Use $motion-design to implement this popover's entrance, exit, and interruption behavior.

Read the complete instructions in [SKILL.md](SKILL.md).

## License

[MIT](LICENSE)
