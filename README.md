# 🧩 Sudoku Solver - Dancing Links (DLX) Algorithm

A high-performance, Sudoku solver built with the **Dancing Links (DLX)** algorithm implementing **Algorithm X**. This interactive web-based tool visualizes the exact-cover problem-solving process in real-time.

## ✨ Features

- **⚡ Lightning-Fast Solver**: Solves most 9×9 Sudoku puzzles in <50ms using the Dancing Links algorithm
- **👁️ Step-by-Step Visualization**: Watch the algorithm explore the search space with real-time column and row highlighting
- **📊 Performance Metrics**: Track recursive calls, nodes visited, and execution time
- **🎮 Interactive Controls**: Play, pause, step through, and adjust visualization speed
- **📋 Sample Puzzles**: Three difficulty levels (Easy, Hard, Expert) to test
- **🔬 Algorithm Transparency**: See exactly which constraints are covered/uncovered and how the search tree is explored

## 🚀 Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- No installation required - runs entirely in the browser

### Usage

1. **Open the Application**
   - Simply open `index.html` in your web browser

2. **Load a Puzzle**
   - Select a difficulty level from the dropdown (Easy, Hard, Expert)
   - Or manually enter numbers in the grid (1-9 only)

3. **Solve**
   - Click **"Solve (Fast)"** for instant solving
   - Click **"Visualize"** to watch the algorithm step-by-step
   - Adjust **Speed** slider to control visualization speed

4. **Controls During Visualization**
   - **Pause**: Freeze the algorithm at any point
   - **Resume**: Continue from where you paused
   - **Step**: Advance one decision at a time
   - **Clear**: Reset the grid

## 🔍 How It Works

### Problem Formulation
Sudoku is converted into an **Exact Cover Problem**:
- **729 candidates**: 9 rows × 9 columns × 9 digits
- **324 constraints**: 
  - 81 cell constraints (each cell must have exactly one value)
  - 81 row constraints (each row must have 1-9)
  - 81 column constraints (each column must have 1-9)
  - 81 box constraints (each 3×3 box must have 1-9)

### Algorithm X (with Dancing Links)
choose_column(c)  // minimum-size heuristic
cover(c)

for each row in c:
    solution.add(row)
    for each column in row:
        cover(column)
    
    if Algorithm_X(remaining_matrix):
        return true
    
    solution.remove(row)
    for each column in row:
        uncover(column)

uncover(c)
return false


### Dancing Links (DLX)

The key innovation: use bidirectional circular linked lists to achieve **O(1) cover/uncover operations**.

Instead of:
- Removing rows/columns from arrays: O(N)
- Shifting remaining elements: O(N)

With DLX:
- Simply unlink pointers: O(1)
- Reverse operation for backtracking: O(1)

This makes the algorithm practical despite the exponential worst-case complexity.

## 📊 Complexity Analysis

| Operation | Time | Space | Description |
|-----------|------|-------|-------------|
| **Cover/Uncover** | O(1) | O(1) | DLX pointer manipulation |
| **ChooseColumn** | O(C) | O(1) | C = 324 constraints |
| **Search** | O(b^d) | O(d) | Depth d ≈ N², branching b ≈ N |
| **BuildDLX** | O(N³) | O(N³) | ~2,700 nodes for 9×9 |
| **Overall** | **O(b^d)** | **O(N³)** | Exponential worst-case |

### Key Insights

- **Theoretical**: Exact Cover is Non P-Complete; no polynomial algorithm known
- **Practical**: Minimum-column heuristic exponentially prunes the search tree
- **DLX**: Constant-time pointer operations make the algorithm fast in practice
- **Most puzzles**: Solve in <50ms despite exponential worst-case

## 🎨 UI Features

### Main Puzzle Grid
- **9×9 Sudoku grid** with 3×3 box borders
- **Real-time highlighting**:
  - 🟨 Yellow: Candidate being explored
  - 🔴 Red/Muted: Cells eliminated due to constraints
  - 🟧 Orange boxes: Active constraint columns

### Visualization Panel
- **324 constraint columns** shown as small boxes
- Color changes as constraints are covered/uncovered
- **Execution log** showing each decision and backtrack

### Performance Dashboard
- ⏱️ Execution time (milliseconds)
- 📞 Recursive call count
- 🔍 Nodes visited in search tree
- 📊 DLX column count

### Complexity Section
- Time and space complexity breakdown
- Operation-by-operation analysis table
- Key insights about the algorithm

## 🎛️ Controls

### Solver Buttons
| Button | Action |
|--------|--------|
| ⚡ Solve (Fast) | Solve instantly without visualization |
| 👁️ Visualize | Solve with step-by-step animation |
| ⏸️ Pause | Pause visualization |
| ⏭️ Step | Advance one step at a time |
| 🗑️ Clear | Reset the grid |

### Speed Slider
- Range: 10-500ms per step
- Default: 50ms
- Only affects visualization mode

## 📁 Project Structure
Sudoku-Solver-DLX/ 
                 ├── index.html 
                 └── README.md 
                 
## 🧠 Educational Value

This project demonstrates:
1. **Algorithm design**: Exact Cover and Algorithm X
2. **Data structures**: Circular doubly-linked lists (toroidal topology)
3. **Search techniques**: Backtracking with heuristics
4. **Complexity analysis**: Exponential time with practical optimizations
5. **Visualization**: Real-time algorithm tracing

## 🔗 Resources

### Papers & References
- **Donald Knuth**: "Dancing Links" (2000)
  - Original paper introducing DLX
  - Knuth's Algorithm X for exact cover problems

- **Sudoku as Exact Cover**
  - Convert Sudoku constraints into exact cover formulation
  - 729 candidates, 324 constraints

### Further Reading
- Exact Cover Problem (Wikipedia)
- Algorithm X (Wikipedia)
- Constraint Satisfaction Problems (CSP)
- NP-Complete Problems

## ⚙️ Technical Details

### Data Structures
- **ColumnNode**: Represents constraint columns
- **Node**: Represents candidates in the exact-cover matrix
- **Circular doubly-linked lists**: Toroidal topology for O(1) operations

### Key Functions
- `buildDLX(board)`: Convert Sudoku to exact-cover matrix
- `cover(column)`: Remove column and related rows
- `uncover(column)`: Restore column and related rows
- `search(k)`: Main Algorithm X recursion
- `chooseColumn()`: Minimum-size heuristic

### Visualization
- Real-time DOM updates for highlighting
- Constraint column visualization
- Execution log with decision tree
- Performance metrics display

## 🎯 Performance Benchmarks

Typical solving times (on modern hardware):
| Difficulty | Time | Recursive Calls | Nodes Visited |
|-----------|------|-----------------|---------------|
| Easy | 2-5ms | 50-200 | 100-500 |
| Hard | 10-30ms | 500-2000 | 1000-5000 |
| Expert | 20-50ms | 1000-5000 | 5000-10000 |

*Times vary based on puzzle structure and heuristic effectiveness*

## 🐛 Troubleshooting

### Grid Not Loading
- Clear browser cache and refresh
- Ensure JavaScript is enabled
- Try a different browser

### Visualization Too Fast/Slow
- Use the Speed slider to adjust
- Default 50ms is recommended
- Lower values = faster visualization

### Invalid Input
- Only digits 1-9 are allowed
- Empty cells are treated as 0
- Non-numeric input is ignored
