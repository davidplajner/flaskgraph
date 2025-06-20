# FlaskGraph

FlaskGraph makes it dead simple to drop [Chart.js](https://www.chartjs.org/) charts into your Flask app without touching JavaScript. You just write Python, pass it to your template, and you're done.

---

## 🔧 Installation

```bash
pip install flaskgraph
```

---

## ⚡ Quickstart

### 1. Import & Use in Flask

```python
from flaskgraph import graph

@app.route("/")
def dashboard():
    chart = graph.bar(
        ['Jan', 'Feb', 'Mar'],
        {"Appointments": [27, 35, 12]}, # pass data as dict for descriptive tooltip
        legend=False,
        label_color='standard',
        grid=False,
        colortheme='sky'
    )
    return render_template("dashboard.html", chart=chart)
```

### 2. In Your Template

**Include Chart.js in your HTML `<head>`:**

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

**Render the chart inside a container with a set width (the canvas is included automatically):**

```html
<div style="width: 100%; max-width: 600px;">
  {{ chart|safe }}
</div>
```

---

## 📊 Supported Chart Types

```python
graph.bar(labels, data, ...)
graph.line(labels, data, ...)
graph.donut(labels, data, ...)
graph.scatter(labels, data, ...)
```

Each method returns a fully ready-to-render HTML `<canvas>` with a Chart.js config script.

---

## 🎨 Parameters

| Parameter     | Type    | Description                                                  |
|---------------|---------|--------------------------------------------------------------|
| `labels`      | list    | X-axis labels                                                |
| `data`        | list    | Y-axis values                                                |
| `label_color` | str     | Label color: `"standard"`, `"dark"`, or `"light"`            |
| `legend`      | bool    | Show/hide the legend                                         |
| `grid`        | bool    | Show/hide background grid lines                              |
| `colortheme`  | str     | One of the predefined themes below                           |

---

## 🌈 Available Color Themes

```
blue, green, red, yellow, orange,
purple, pink, teal, sky, lime,
slate, gray, zinc,
neon-green, neon-pink, neon-blue
```

---

## ✅ Example

```python
revenue = graph.line(
    ['Q1', 'Q2', 'Q3', 'Q4'],
    {"revenue": [5000, 7000, 4000, 6500]},
    label_color='dark',
    legend=True,
    grid=True,
    colortheme='lime'
)
```

```html
<div style="max-width: 700px;">
  {{ revenue|safe }}
</div>
```

That's it. No JavaScript. No extra config.
