# CLAUDE.md

Statechart-driven UI routing for Fulcro. Depends on `com.fulcrologic/statecharts` and
`com.fulcrologic/fulcro`. Extracted from statecharts 1.4.0-RC20; namespaces kept as `com.fulcrologic.statecharts.integration.fulcro.routing*`.

- **ALWAYS run CLJ tests with guardrails enforcing mode before declaring tests pass.** CI runs:
  `clojure -J-Dguardrails.enabled=true -J-Dguardrails.config=guardrails-test.edn -M:dev:test:clj-tests`
  For a single namespace:
  `clojure -J-Dguardrails.enabled=true -J-Dguardrails.config=guardrails-test.edn -M:dev:test -e "(require '[kaocha.repl :as k]) (k/run 'your.ns-spec)"`
- The `:local-statecharts` alias (see `deps.edn`) overrides `com.fulcrologic/statecharts` with a local checkout, for unreleased changes.
- CLJS tests: `pnpm exec shadow-cljs -A:dev compile ci-tests && pnpm exec karma start --single-run`.

## File Map
- `routing.cljc` — Full routing API (chart DSL: `routes`, `rstate`, `istate`; `start!`; navigation; URL sync; validation; busy checking)
- `routing_options.cljc` — Component options (`sfro/`), RAD pattern
- `routing/url_codec.cljc` — URLCodec protocol
- `routing/url_codec_transit.cljc` — Default transit+base64 codec
- `routing/url_history.cljc` — URLHistoryProvider protocol + helpers
- `routing/browser_history.cljc` — Browser history (CLJS)
- `routing/simulated_history.cljc` — Simulated history (headless tests)
- `abort_tracker.cljc` — In-flight abort ID tracking per session
- `src/demo/.../routing_demo2` — Demo app (shadow build `:routing-demo2`, port 8092)

## Docs
- `Guide.adoc` — user documentation (`make docs/index.html`)
- `docs/ai/` — testing guides; `docs/ai/specs/` — specs carried over from statecharts (historical, mostly Done)
