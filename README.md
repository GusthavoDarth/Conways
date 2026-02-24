# Conway's Game of Life (Raylib)

![Demonstração do Jogo da Vida](LINK-DO-SEU-GIF-AQUI)

## 📋 Description

An interactive implementation of **Conway's Game of Life** built in C with the Raylib library. This project simulates cellular automaton where cells evolve based on simple rules, creating complex and often mesmerizing patterns. It strengthens skills in **state management**, **grid-based algorithms**, and **real-time interactive applications**.

## 🧠 How It Works

The simulation runs on a 2D grid where each cell is either **alive** or **dead**. The state of every cell updates simultaneously based on its eight neighbors, following these classic rules:

1.  A live cell with 2 or 3 live neighbors survives.
2.  A dead cell with exactly 3 live neighbors becomes alive.
3.  All other cells die or remain dead.

### Core Implementation

The logic is broken down into three key functions:

**1. Counting Neighbors**
```c
int checkNeighbours(int** matrix, int row, int col, int rows, int cols) {
    int x[] = {-1,-1,-1,0,0,1,1,1};
    int y[] = {-1,0,1,-1,1,-1,0,1};
    int count = 0;
    for(int i = 0; i < 8; i++) {
        int newRow = row + x[i];
        int newCol = col + y[i];
        if(newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols) {
            if (matrix[newRow][newCol] == 1) {
                count++;
            }
        }
    }
    return count;
}
```
**2. Updating Cell State Based on Rules**
```c
int stateUpdate(int cell, int neighbours) {
    if(cell == 1 && (neighbours == 2 || neighbours == 3)) {
        return 1; // Cell survives
    }
    else if(cell == 0 && neighbours == 3) {
        return 1; // Cell is born
    }
    else {
        return 0; // Cell dies
    }
}
```
**3. Computing the Next Generation**
```c
int** step(int** matrixA, int rows, int cols) {
    int** auxMatrix = initMatrix(rows, cols); // Allocate new matrix
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            int neigh = checkNeighbours(matrixA, i, j, rows, cols);
            int state = stateUpdate(matrixA[i][j], neigh);
            auxMatrix[i][j] = state;
        }
    }
    return auxMatrix;
}
```
## 🎮 Controls

- **Draw Cells:** `Left Click` on a white square to make it alive (black).
- **Run Simulation:** Hold `RIGHT ARROW` to iterate through generations.
- **Load Patterns:** Press `T` to spawn test patterns (oscillators, gliders, etc.) for demonstration.

## ✨ What I Learned & Key Challenges

- **Algorithm Implementation:** Translating Conway's rules into efficient C code deepened my understanding of cellular automata and state machines.
- **Matrix Management:** Using an auxiliary matrix for simultaneous updates was crucial to avoid race conditions and maintain correct simulation logic.
- **Real-time Interaction with Raylib:** Integrating mouse and keyboard input for drawing and controlling the simulation taught me about event handling and render loop design.
- **Performance Considerations:** For larger grids, I explored ways to optimize neighbor counting and avoid unnecessary memory allocations.

## 🚀 How to Run

### Dependencies
- **Raylib**: Install from [raylib.com](https://www.raylib.com/) or via package manager:
  - **Windows:** Download pre-compiled library or use vcpkg.
  - **Linux:** `sudo apt install libraylib-dev` (Debian/Ubuntu)
  - **macOS:** `brew install raylib`

### Compilation
This project includes a **Makefile**. After installing Raylib:
```bash
git clone https://github.com/GusthavoDarth/Conways.git
cd Conways
make
```
### Running
```bash
./Conway      # Linux/macOS
Conway.exe    # Windows
```
