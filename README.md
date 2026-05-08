# Matheo

Matheo is a single-page offline math workspace with a calculator, paper-style expression rendering, and a Desmos-style graphing view. It is built as a tiny static PWA: no build step, no framework, and no external runtime dependencies.

## Features

- Calculator with typed input and keypad input.
- Paper-style rendering for numbers, variables, functions, fractions, powers, roots, and absolute values.
- Step panel for focused simplification rules.
- Canvas graphing for expressions in `x`.
- Calculator-to-graph sync: expressions like `y=x^2`, `sin(x)`, or `x^3 - 2x` automatically appear in the graph view.
- Four keypad layers: Basic, More, Advanced, and Symbols.
- Long-press or right-click the `x` key to choose another variable.
- Unicode math input normalization for symbols such as pi, square root, infinity, multiply, divide, superscript 2/3, and common Greek variable letters.
- PWA install support with offline caching.

## Files

```text
index.html            App shell, CSS, JavaScript, math engine, renderer, keypad, graph engine
manifest.webmanifest  PWA metadata
service-worker.js     Cache-first offline shell
LICENSE               Apache-2.0 license
```

## Run Locally

Serve the folder over HTTP. Service workers do not run correctly from `file://`.

```bash
python -m http.server 5173
```

Open:

```text
http://127.0.0.1:5173/index.html
```

## Test

Matheo has an inline math-engine smoke test suite. Open:

```text
http://127.0.0.1:5173/index.html?test=1
```

The current suite covers arithmetic precedence, implicit multiplication, trig, roots, powers, factorial, combinatorics, rounding functions, min/max, Unicode math input, and symbolic expressions.

## Supported Syntax

Examples:

```text
2(3+4)
(3/4 + sqrt(16))^2
sin(pi/2)
cos(2)^2
root(2,16)
ncr(5,2)
npr(5,2)
sqrt(16) + 3^2
y=x^3
```

Supported function names include:

```text
sin cos tan sec csc cot
asin acos atan
sinh cosh tanh
sqrt root log ln exp abs
floor ceil round min max
ncr npr
```

## Graphing

The graph view plots expressions in `x`.

- Type `y=sin(x)` or `x^2 - 4` in the calculator page to sync it into the graph page.
- Add more equations directly from the graph page.
- Drag to pan.
- Use wheel or pinch to zoom.
- Reset returns to the default viewport.

## PWA Notes

A real PWA needs a separate manifest and service worker URL, so Matheo uses three static files instead of forcing everything into one HTML file. The app logic, UI, CSS, parser, renderer, and graph engine are all contained in `index.html`.

When changing cached assets, bump the cache name in `service-worker.js` so installed browsers pick up the new shell.

## Current Limits

- Matheo is not a full computer algebra system.
- Simplification is intentionally scoped to arithmetic evaluation, constant folding, fraction handling, basic powers, and a few symbolic patterns.
- Graphing supports explicit `y=f(x)` style functions, not implicit relations like `x^2 + y^2 = 1`.
- Very broad mathematical notation is normalized where practical, but the parser remains intentionally small and local.

## License

Apache-2.0. See [LICENSE](LICENSE).
