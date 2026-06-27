# F2 Control — Home Assistant add-on repository

One-click install for the **f2-control** crop-steering engine — the autonomous P0→P1→P2→P3
irrigation controller from [HA-Irrigation-Strategy](https://github.com/JakeTheRabbit/HA-Irrigation-Strategy).

## Install (one-click, by URL)

1. In Home Assistant: **Settings → Add-ons → Add-on Store → ⋮ (top-right) → Repositories**.
2. Paste this URL and **Add**:
   ```
   https://github.com/JakeTheRabbit/f2-control
   ```
3. Close the dialog — **F2 Control** now appears in the store. Open it → **Install**.

> This is the *add-on repository* — paste the URL above into the **Add-on Store → Repositories**
> dialog (not HACS, and not a subfolder URL).

## After installing

1. **Kill switch.** Create `input_boolean.f2_control_enabled` (a Helper, or deploy
   `f2_control/f2_control_package.yaml` to `/config/packages` then reload). **OFF = safe** — the
   add-on reads, computes and notifies but never opens a valve.
2. **Configure** (add-on → Configuration): `lights_on_hour` / `lights_off_hour`, your
   `notify_service`, and the feed EC/pH sensors if they differ from the defaults. The token is
   automatic (`homeassistant_api: true`).
3. **Start** it. The log shows `starting | kill-switch … | token present: True`.
4. Watch a photoperiod with the kill switch OFF, then flip it ON to go live.

You also need the companion **Crop Steering integration** (entities + setup wizard + dashboards) —
install it via HACS from the main repo. Full step-by-step:
**https://github.com/JakeTheRabbit/HA-Irrigation-Strategy** → `docs/AGENT_INSTALL.md`.

## Updating

The add-on bakes its code at build time, so when a new version ships, use the add-on's **Update**
(or **⋮ → Rebuild**) — a plain Restart keeps the old code.

---

*The add-on source is developed in the main monorepo at `addons/f2_control/` and published here on
each release (`scripts/publish_addon.sh`). File issues on the
[main repo](https://github.com/JakeTheRabbit/HA-Irrigation-Strategy/issues).*
