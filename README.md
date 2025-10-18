
---

# 5 — Rust-like Build Graph Visualizer (build_graph.py)

**File:** `src/build_graph.py`
```python
#!/usr/bin/env python3
"""
Build Graph Visualizer (generates DOT)
- Reads a simple manifest and outputs Graphviz DOT for visualization.
Run: python3 src/build_graph.py
"""
import json, os
from typing import Dict, List

SAMPLE = {
    "crateA": ["crateB", "crateC"],
    "crateB": ["crateD"],
    "crateC": ["crateD"],
    "crateD": []
}

def to_dot(graph: Dict[str, List[str]], directed=True, name="BuildGraph"):
    op = "digraph" if directed else "graph"
    edge = "->" if directed else "--"
    lines = [f'{op} "{name}" {{']
    for src, outs in graph.items():
        if not outs:
            lines.append(f'  "{src}";')
        for d in outs:
            lines.append(f'  "{src}" {edge} "{d}";')
    lines.append("}")
    return "\n".join(lines)

def demo():
    dot = to_dot(SAMPLE)
    print(dot)

if __name__ == "__main__":
    demo()
