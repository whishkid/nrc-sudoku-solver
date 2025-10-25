# NRC Sudoku Solver

An interactive web application that helps you solve NRC Sudoku puzzles from [NRC Handelsblad](https://www.nrc.nl/puzzels/sudoku).

![NRC Sudoku Screenshot](./screenshot.png)
*Screenshot of the NRC Sudoku Solver interface*

## What is NRC Sudoku?

NRC Sudoku is a challenging variant of the classic Sudoku puzzle, originally published by the Dutch newspaper NRC Handelsblad. It features additional constraints that make it more complex and engaging than standard Sudoku.

### Rules of the Game

NRC Sudoku follows the basic Sudoku rules with an important twist:

1. **Standard Rules:**
   - Fill a 9×9 grid with digits from 1 to 9
   - Each row must contain all digits 1-9 without repetition
   - Each column must contain all digits 1-9 without repetition
   - Each of the nine 3×3 boxes must contain all digits 1-9 without repetition

2. **NRC Special Rules:**
   - In addition to the nine standard 3×3 boxes, there are **four extra 3×3 regions** (highlighted in gray)
   - These four additional regions are positioned at:
     - Top-left corner starting at position (2,2)
     - Top-right corner starting at position (6,2)
     - Bottom-left corner starting at position (2,6)
     - Bottom-right corner starting at position (6,6)
   - Each of these four gray regions must also contain all digits 1-9 without repetition

This means NRC Sudoku has **13 regions** in total (9 standard boxes + 4 NRC boxes) that must satisfy the uniqueness constraint, making it significantly more challenging than regular Sudoku!

Learn more and play online: [https://www.nrc.nl/puzzels/sudoku](https://www.nrc.nl/puzzels/sudoku)

## Features

- 🎯 Interactive 9×9 Sudoku grid with visual distinction for NRC regions (gray boxes)
- ⌨️ Keyboard navigation using arrow keys
- 🔢 Easy number input
- 🤖 Automatic solver using logical deduction algorithms
- 📱 Responsive design that works on desktop and mobile devices

## How to Use

1. **Input your puzzle:** Click on any cell and type a number (1-9) to fill in the initial puzzle clues
2. **Navigate:** Use arrow keys to move between cells, or click directly on any cell
3. **Clear a cell:** Press Backspace to remove a number
4. **Solve:** Click the "Solve" button to automatically solve the puzzle using logical deduction
5. **Watch it solve:** The solver fills in cells step-by-step, allowing you to see the solution process

## Development

This project is built with:
- [SvelteKit](https://kit.svelte.dev/) - The web framework
- [TypeScript](https://www.typescriptlang.org/) - Type safety
- [Tailwind CSS](https://tailwindcss.com/) - Styling
- [Vite](https://vitejs.dev/) - Build tool

### Getting Started

Install dependencies:
```bash
npm install
```

Start the development server:
```bash
npm run dev
```

Build for production:
```bash
npm run build
```

Preview the production build:
```bash
npm run preview
```

Type checking:
```bash
npm run check
```

## License

This project is open source and available for educational purposes.
