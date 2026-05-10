# Matheo

Matheo is a static offline math workspace with a paper-style calculator and a graph view.  
It ships as a small PWA with no build step and no runtime dependencies.

## Highlights

- Paper-style expression rendering in the main output area.
- Keypad + typed input workflow.
- Dedicated `Solve` action button.
- Equation solving in `x` for real and complex polynomial roots.
- Calculus helpers: derivative, integral, and limit.
- Graph view with pan/zoom and equation list editing.
- Dedicated function page for evaluating `f(x)`, making value tables, and graphing functions.
- Dedicated logic page with truth-table generation.
- Calculator-to-graph linking for expressions in `x` and `y=...`.
- PWA install + offline cache shell.

## Project Files

```text
index.html            App shell, styles, parser, evaluator, simplifier, renderer, solver, graph logic
manifest.webmanifest  PWA metadata
service-worker.js     Cache-first offline shell
README.md             Project documentation
LICENSE               Apache-2.0 license
```

## Run Locally

Serve over HTTP (`file://` is not enough for service workers):

```bash
python -m http.server 5173
```

Open:

```text
http://127.0.0.1:5173/index.html
```

## Testing

Run the built-in test suite:

```text
http://127.0.0.1:5173/index.html?test=1
```

Current tests cover:

- arithmetic precedence and implicit multiplication
- trig, inverse trig, hyperbolic, and logs
- roots, powers, factorial, combinatorics
- derivative, integral, limit
- boolean/comparison expressions
- equation solving including complex polynomial roots
- symbolic result rendering expectations

## Syntax Notes

Examples:

```text
2(3+4)
(3/4 + sqrt(16))^2
sin(pi/2)
root(2,16)
ncr(5,2)
deriv(x^2,3)
integral(x,0,2)
limit(sin(x)/x,0)
x^2+1=0
y=x^3-2x
```

Supported function names (complete parser list):

```text
sin cos tan sec csc cot
asin acos atan
sinh cosh tanh
sqrt root log ln exp abs
floor ceil round min max
sum
ncr npr
deriv integral limit
```

Supported operators and comparison/logical tokens:

```text
+ - * / ^ !
= == != > < >= <=
and or not
```

Supported constants and literals:

```text
pi e Infinity true false
```

## Calculator + Solve

- `=` inserts equality for expressions/equations.
- `Solve` evaluates numeric expressions or solves equations.
- For equations in `x`, Matheo solves polynomial roots and can return complex roots (for example `x^2+1=0`).

## Function Page

- The `Func` tab evaluates and analyzes functions in `x`.
- Enter forms such as `x^2 - 4`, `sin(x)`, `f(x)=x^3-2x`, or `y=cos(x)`.
- It evaluates `f(x)` at the selected input value and generates a table using custom min/max/step controls.
- It reports y-intercept, sampled roots, sampled range, quadratic vertex when detected, critical points, increasing/decreasing intervals, first derivative, second derivative, and tangent line at the selected `x`.
- Use `Graph` to send the current function to the graph page.

## Logic Page

- The `Logic` tab is a separate truth-table workspace.
- Use it for expressions like `(p and q) or not r`, `(p ∧ q) ∨ ¬r`, and boolean comparisons.
- The page includes logic tokens plus shortcuts for common math predicates (`^`, `sin`, `cos`, `tan`, derivative, integral, limit).
- Use the `Calc` button on the Logic page to return to the full calculator for normal power, trigonometry, calculus, and equation solving.

## Graph View

- Graph tab plots equations in `x`.
- Expressions like `y=sin(x)` or `x^2-4` can be synced from calculator input.
- Drag to pan, wheel/pinch to zoom, and use `Reset` to restore viewport.

## Current Limits

- Not a full CAS.
- Best solver coverage is for polynomial equations in `x`; non-polynomial equations use numeric scanning fallback.
- Graphing is function-oriented (`y=f(x)` / expression-in-`x`), not full implicit relation plotting.

## License

Apache-2.0. See [LICENSE](LICENSE).
