# Cellular-Automaton

### **General Structure:**
- The code is a **cellular automaton** simulation using an HTML canvas.
- The **CellularAutomaton** class encapsulates the logic for managing the grid, updating the cell values, rendering the grid to the canvas, and handling user interaction.
- The canvas covers the entire viewport, and when resized, the grid size automatically adjusts based on the window size.

### **Algorithms and Logic in the Code:**

1. **Grid Initialization (`initializeGrid`):**
   - When the automaton is initialized, a grid is created with random values (from 0 to 255). This is done using the `Array.from()` method to create a 2D array (`this.grid`), where each cell contains a random value.
   - **Random Initialization**: Each cell starts with a random value between 0 and 255, representing an intensity or color value that will later influence the display.

2. **Grid Update (`updateGrid`):**
   - The core logic of the cellular automaton update happens here.
   - **Neighboring Cell Sum**: For each cell (except the edges), the algorithm looks at a 3x3 grid of cells surrounding it (including itself). The values of these neighboring cells are summed up.
   - **Average of Neighbors**: The algorithm then takes the average of the 9 neighboring cells' values and assigns this value to the current cell.
     ```javascript
     newGrid[y][x] = Math.min(255, sum / 9);
     ```
     The `Math.min(255, sum / 9)` ensures the value doesn’t exceed 255 (as this could create invalid colors in the RGB scale).

3. **Rendering (`render`):**
   - The `render` method is responsible for drawing the grid on the canvas.
   - It uses `createImageData` to create an image object for the canvas, where each pixel corresponds to a cell.
   - For each cell, the value is used to set the pixel’s red, green, and blue channels. These colors are based on the cell value and generate a varying visual pattern.
     - Red (`data[index]`), Green (`data[index + 1]`), and Blue (`data[index + 2]`) are set using simple arithmetic.
     - The alpha channel is set to `255` to make the cells fully visible.

4. **Touch Handling (`handleTouch`):**
   - When the user clicks (or taps) anywhere on the canvas, the `handleTouch` method is triggered.
   - It calculates the position of the touch relative to the grid and "randomizes" the neighboring cells of the clicked cell, creating a new random value for a 5x5 region around the touched area. This creates an interactive effect where the user can "reset" the pattern in a local region of the grid.

5. **Animation Loop (`startAnimation`):**
   - The `startAnimation` method runs an animation loop using `requestAnimationFrame`.
   - Inside this loop:
     - The grid is updated by calling `updateGrid`.
     - The grid is rendered by calling `render`.
     - This loop continues indefinitely, updating and redrawing the grid continuously to create a smooth animation of the cellular automaton.

6. **Regeneration Button:**
   - The `Regenerate` button triggers a new random initialization of the grid. When clicked, it calls `automaton.initializeGrid()` to reset the grid with fresh random values.

### **Algorithm Summary:**
1. **Grid Update**: For each cell, average the values of its 8 neighbors (plus itself) and assign the new value to that cell.
2. **Rendering**: Translate the grid values into RGB color values and display them on the canvas.
3. **Touch Interaction**: When the user clicks on the canvas, reset the values of cells in a small region around the click, adding randomness and interactivity.
4. **Continuous Animation**: The system continuously updates the grid and re-renders it using an animation loop for smooth transitions.

### **Key Concepts:**
- **Cellular Automaton**: A mathematical model used to simulate a system of cells that evolve over time according to simple rules based on their neighbors.
- **2D Array for Grid**: The grid of cells is represented as a 2D array (rows x cols).
- **Neighboring Sum Rule**: The core update rule is to compute the average of neighboring cells and assign it to the current cell.
- **Canvas Rendering**: The use of `createImageData` and `putImageData` to display the grid on the canvas efficiently.

The code simulates a simple form of cellular automaton, where the colors of the cells evolve over time based on the surrounding cells' values, producing evolving patterns across the grid.
