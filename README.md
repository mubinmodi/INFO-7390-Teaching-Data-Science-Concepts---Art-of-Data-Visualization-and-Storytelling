# INFO-7390-Teaching-Data-Science-Concepts---Art-of-Data-Visualization-and-Storytelling

# Advanced Data Visualization Teaching Module 📊

> **Perception-Driven Data Visualization & Storytelling for Data Scientists**

A comprehensive teaching module for INFO 7390 (Advanced Data Science and Architecture) that teaches evidence-based visualization design principles, interactive exploration techniques, and data storytelling skills using Python.

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Plotly](https://img.shields.io/badge/Plotly-5.x-3F4F75.svg)](https://plotly.com/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

---

## 🎯 Overview

This module teaches **how to design effective visualizations** grounded in cognitive psychology and perceptual science, not just how to make charts "look pretty." Students learn to:

- Apply Cleveland & McGill's perceptual hierarchy to choose optimal encodings
- Use logarithmic scales appropriately for skewed data
- Create interactive exploratory dashboards with ipywidgets
- Tell compelling data stories with annotated visualizations
- Avoid common pitfalls (misleading axes, 3D pie charts, dual y-axes)

**Key Innovation:** Combines rigorous perceptual theory with hands-on coding practice, culminating in authentic storytelling assessments that mirror real-world data science communication.

---

## 🎓 Learning Objectives

By completing this module, you will be able to:

### Knowledge (Understand)
- ✅ Explain why position encoding is more accurate than area or color
- ✅ Identify when logarithmic scales are appropriate vs. linear scales
- ✅ Describe Tufte's data-ink ratio and its application

### Skills (Apply/Analyze)
- ✅ Select optimal chart types based on data characteristics
- ✅ Construct perception-aware visualizations using Plotly Express
- ✅ Implement interactive widgets for exploratory data analysis
- ✅ Critique visualizations using evidence-based design principles

### Synthesis (Create/Evaluate)
- ✅ Design annotated visualizations that tell coherent data stories
- ✅ Evaluate trade-offs between static and interactive approaches
- ✅ Defend design decisions using perceptual and cognitive research

---

## 📦 What's Included
```
advanced-data-visualization/
│
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── LICENSE                            # MIT License
│
├── notebooks/
│   └── Data_Visualization_Teaching_Notebook.ipynb  # Main teaching notebook
│
├── docs/
│   ├── Tutorial_Documentation.pdf     # Complete tutorial guide
│   └── Pedagogical_Report.pdf         # Teaching philosophy & assessment
│
├── data/
│   └── gapminder.csv                  # Sample dataset (or downloads automatically)
│
└── assets/
    ├── diagrams/                      # Visual aids and flowcharts
    └── examples/                      # Reference visualizations
```

---

## 🚀 Installation

### Option 1: Google Colab (Recommended - Zero Setup!)

1. Click here: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
2. Upload `Data_Visualization_Teaching_Notebook.ipynb`
3. Run the first cell to install dependencies
4. Start learning!

### Option 2: Local Jupyter Installation

**Prerequisites:**
- Python 3.8 or higher
- pip package manager

**Steps:**
```bash
# 1. Clone the repository
git clone https://github.com/yourusername/advanced-data-visualization.git
cd advanced-data-visualization

# 2. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Enable Jupyter widgets
jupyter nbextension enable --py widgetsnbextension

# 5. Launch Jupyter Notebook
jupyter notebook notebooks/Data_Visualization_Teaching_Notebook.ipynb
```

### Option 3: Docker (Isolated Environment)
```bash
# Build and run
docker build -t data-viz-module .
docker run -p 8888:8888 data-viz-module
```

---

## 📚 Usage Examples

### Example 1: Perception-Aware Scatter Plot
```python
import plotly.express as px

# Load data
df = px.data.gapminder()
df_2007 = df[df.year == 2007]

# Create scatter plot with log scale for skewed GDP data
fig = px.scatter(
    df_2007,
    x='gdpPercap',
    y='lifeExp',
    size='pop',
    color='continent',
    hover_name='country',
    log_x=True,  # Log scale for data spanning orders of magnitude
    title='Wealth vs Health: GDP per Capita vs Life Expectancy (2007)'
)

fig.update_layout(
    template='simple_white',  # High data-ink ratio
    xaxis_title='GDP per Capita (log scale)',
    yaxis_title='Life Expectancy (years)'
)

fig.show()
```

### Example 2: Interactive Widget for Exploration
```python
from ipywidgets import interact, IntSlider, SelectMultiple

@interact(
    year=IntSlider(min=1952, max=2007, step=5, value=2007, description='Year'),
    continents=SelectMultiple(
        options=['Africa', 'Americas', 'Asia', 'Europe', 'Oceania'],
        value=['Asia', 'Europe'],
        description='Continents'
    )
)
def explore_data(year, continents):
    filtered = df[(df.year == year) & (df.continent.isin(continents))]
    
    fig = px.scatter(
        filtered,
        x='gdpPercap', y='lifeExp',
        size='pop', color='continent',
        log_x=True,
        title=f'GDP vs Life Expectancy ({year})'
    )
    fig.show()
```

### Example 3: Annotated Storytelling
```python
# Create base visualization
fig = px.scatter(
    df_2007, x='gdpPercap', y='lifeExp',
    size='pop', color='continent',
    hover_name='country', log_x=True
)

# Add annotation to highlight insight
fig.add_annotation(
    x=8948,  # Cuba's GDP
    y=78.3,  # Cuba's life expectancy
    text='Cuba: High health outcomes<br>despite moderate wealth',
    showarrow=True,
    arrowhead=2,
    bgcolor='rgba(255,255,255,0.8)',
    bordercolor='#ff0000'
)

fig.update_layout(
    title='The Healthcare Paradox: Wealth Doesn\'t Always Equal Health'
)

fig.show()
```

---

## 🎥 Video Walkthrough

📹 **Watch the complete tutorial:** [YouTube Link - Advanced Data Visualization Module](https://youtu.be/your-video-id)

**Chapters:**
- 0:00 - Introduction & Learning Objectives
- 5:30 - Perceptual Hierarchy (Cleveland & McGill)
- 15:20 - When and Why to Use Log Scales
- 28:45 - Building Interactive Widgets
- 42:10 - Data Storytelling Framework
- 58:30 - Exercise Walkthrough

---

## 📋 Requirements

### Python Dependencies

See [`requirements.txt`](requirements.txt) for complete list. Key packages:
```txt
# Core Dependencies
python>=3.8
jupyter>=1.0.0
notebook>=6.5.0

# Data & Visualization
pandas>=1.5.0
numpy>=1.24.0
plotly>=5.14.0

# Interactivity
ipywidgets>=7.7.1
ipython>=7.34.0

# Optional (for extended features)
matplotlib>=3.7.0
seaborn>=0.12.0
```

### System Requirements

- **RAM:** 4GB minimum, 8GB recommended
- **Storage:** 500MB for notebooks and dependencies
- **Browser:** Modern browser (Chrome, Firefox, Safari, Edge)
- **Internet:** Required for initial package downloads

---

## 🗂️ Module Structure

### Part 1: Theoretical Foundations (30 mins)
- Perception hierarchy (position > length > area > color)
- Logarithmic vs. linear scales
- Data-ink ratio and chart junk
- Common visualization pitfalls

### Part 2: Static Visualizations (45 mins)
- Scatter plots with appropriate encodings
- Horizontal bar charts for rankings
- Line charts for time series
- Small multiples for comparisons

### Part 3: Interactive Exploration (45 mins)
- ipywidgets basics (sliders, dropdowns, multi-select)
- Callback patterns and state management
- Building exploratory dashboards
- When to use interactivity vs. static

### Part 4: Data Storytelling (60 mins)
- Narrative structure (setup, conflict, resolution)
- Annotation techniques
- Story panels with key insights
- Exercise: Create your own data story

---

## 🎓 Pedagogy

**Teaching Philosophy:** Perception-first, practice-driven learning

**Approach:**
1. **Theory First:** Ground design in cognitive science
2. **Immediate Application:** Each concept followed by code example
3. **Progressive Complexity:** 5-line examples → 50-line stories
4. **Authentic Assessment:** Storytelling mirrors real-world communication

**Learning Styles Supported:**
- **Visual Learners (60%):** Diagrams, flowcharts, side-by-side comparisons
- **Kinesthetic Learners (30%):** Interactive widgets, hands-on exercises
- **Reading/Writing Learners (10%):** Detailed explanations, reflection prompts

---

## 🏆 Exercises

### Exercise 1: Beginner (⭐)
**Task:** Create a horizontal bar chart showing top 10 countries by population (2007)

**Skills:** Chart selection, basic Plotly syntax, axis labeling

**Time:** 15 minutes

### Exercise 2: Intermediate (⭐⭐)
**Task:** Build an animated scatter plot showing GDP vs. Life Expectancy over time

**Skills:** Animation, widget implementation, understanding trade-offs

**Time:** 30 minutes

### Exercise 3: Advanced (⭐⭐⭐)
**Task:** Identify a surprising pattern in the data and create a 3-part narrative with annotated visualizations

**Skills:** Pattern discovery, storytelling, annotation, design justification

**Time:** 60 minutes

**Grading Rubric Provided:** See Pedagogical Report for detailed assessment criteria

---

## 🛠️ Troubleshooting

### Widgets Not Displaying
```python
# In Google Colab
from google.colab import output
output.enable_custom_widget_manager()

# In Jupyter Notebook
jupyter nbextension enable --py widgetsnbextension

# In JupyterLab
jupyter labextension install @jupyter-widgets/jupyterlab-manager
```

### Plotly Charts Not Rendering
```bash
# Upgrade Plotly
pip install plotly --upgrade

# For JupyterLab, install extension
jupyter labextension install jupyterlab-plotly
```

### Import Errors
```bash
# Ensure all dependencies installed
pip install -r requirements.txt --upgrade

# If specific package missing
pip install package-name
```

### Data File Not Found

The notebook automatically downloads the Gapminder dataset if not found locally. If issues persist:
```python
# Manual download
import plotly.express as px
df = px.data.gapminder()
df.to_csv('data/gapminder.csv', index=False)
```

---

## 🤝 Contributing

Contributions welcome! Please follow these guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-addition`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to branch (`git push origin feature/amazing-addition`)
5. **Open** a Pull Request

**Areas for Contribution:**
- Additional datasets (healthcare, finance, climate)
- Domain-specific examples
- Translation to other languages
- Video tutorials
- Bug fixes and documentation improvements

---

## 📖 Additional Resources

### Recommended Reading
- **Cleveland & McGill (1984):** "Graphical Perception: Theory, Experimentation, and Application"
- **Tufte (1983):** "The Visual Display of Quantitative Information"
- **Knaflic (2015):** "Storytelling with Data"
- **Munzner (2014):** "Visualization Analysis and Design"

### Online Tools
- [Plotly Documentation](https://plotly.com/python/)
- [ColorBrewer](https://colorbrewer2.org/) - Colorblind-friendly palettes
- [Data Viz Catalogue](https://datavizcatalogue.com/) - Chart selection guide
- [From Data to Viz](https://www.data-to-viz.com/) - Decision tree for viz types

### Related Courses
- **CS 171:** Visualization (Harvard)
- **CSE 512:** Data Visualization (UW)
- **6.859:** Interactive Data Visualization (MIT)

---

## 📄 Citation

If you use this module in your teaching or research, please cite:
```bibtex
@misc{modi2025dataviz,
  author = {Modi, Mubin},
  title = {Advanced Data Visualization Teaching Module: Perception-Driven Design and Storytelling},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/yourusername/advanced-data-visualization}},
  note = {INFO 7390 – Advanced Data Science and Architecture}
}
```

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.
```
MIT License

Copyright (c) 2025 Mubin Modi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```


**Built with ❤️ for data science education**

*Empowering students to transform data into insights, and insights into action.*
