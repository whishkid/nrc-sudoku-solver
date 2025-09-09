<script lang="ts">
  type cell = {
    x: number;
    y: number;
    value: string | null;
    possibleValues?: Set<string>;
  };

  type group = {
    name: string;
    cells: cell[];
  };

  let cells: cell[] = $state([]);
  let cellHtmlObjects: { [key: string]: HTMLDivElement } = $state({});
  let grayCells: { x: number; y: number }[] = $state([]);
  let groups: group[] = [];

  let topCornersOfGrayBoxes = [
    { x: 2, y: 2 },
    { x: 6, y: 2 },
    { x: 6, y: 6 },
    { x: 2, y: 6 },
  ];

  cells = createCells();
  grayCells = getGrayCells();
  groups = [
    ...getMain3x3GridGroups(),
    ...getRows(),
    ...getColumns(),
    ...getGrayCellGroups(),
  ];

  function createCells() {
    const rows = 9;
    const cols = 9;
    const ret = [];
    for (let r = 1; r <= rows; r++) {
      for (let c = 1; c <= cols; c++) {
        ret.push({ x: c, y: r, value: null });
      }
    }
    return ret;
  }

  function getGrayCells() {
    let ret: { x: number; y: number }[] = [];
    for (let corner of topCornersOfGrayBoxes) {
      for (let r = corner.y; r < corner.y + 3; r++) {
        for (let c = corner.x; c < corner.x + 3; c++) {
          ret.push({ x: c, y: r });
        }
      }
    }

    return ret;
  }

  function getMain3x3GridGroups() {
    let ret = [];
    let i = 0;
    for (let gridRow = 0; gridRow < 3; gridRow++) {
      for (let gridCol = 0; gridCol < 3; gridCol++) {
        i++;
        let group = { name: `MainGrid ${i}`, cells: [] };
        for (let r = gridRow * 3 + 1; r <= gridRow * 3 + 3; r++) {
          for (let c = gridCol * 3 + 1; c <= gridCol * 3 + 3; c++) {
            let cell = cells.find((cell) => cell.x === c && cell.y === r);
            if (cell) group.cells.push(cell);
          }
        }
        ret.push(group);
      }
    }
    return ret;
  }

  function getRows() {
    let ret = [];
    let i = 0;
    for (let r = 1; r <= 9; r++) {
      i++;
      let group: group & { row: number } = {
        row: r,
        name: `Row ${i}`,
        cells: [],
      };
      for (let c = 1; c <= 9; c++) {
        let cell = cells.find((cell) => cell.x === c && cell.y === r);
        if (cell) group.cells.push(cell);
      }
      ret.push(group);
    }
    return ret;
  }

  function getColumns() {
    let ret = [];
    let i = 0;
    for (let c = 1; c <= 9; c++) {
      i++;
      let group: group & { col: number } = {
        col: c,
        name: `Col ${i}`,
        cells: [],
      };
      for (let r = 1; r <= 9; r++) {
        let cell = cells.find((cell) => cell.x === c && cell.y === r);
        if (cell) group.cells.push(cell);
      }
      ret.push(group);
    }
    return ret;
  }

  function getGrayCellGroups() {
    let ret: group[] = [];
    let i = 0;
    for (let corner of topCornersOfGrayBoxes) {
      i++;
      let group: group & { corner: { x: number; y: number } } = {
        name: `GrayBox ${i} (${corner.x},${corner.y})`,
        cells: [],
        corner,
      };
      for (let r = corner.y; r < corner.y + 3; r++) {
        for (let c = corner.x; c < corner.x + 3; c++) {
          let cell = cells.find((cell) => cell.x === c && cell.y === r);
          if (cell) group.cells.push(cell);
        }
      }
      ret.push(group);
    }
    return ret;
  }

  function keyboardNav(e: KeyboardEvent, cell: cell) {
    if (e.key >= "1" && e.key <= "9") {
      return;
    } else if (e.key === "Backspace") {
      return;
    } else if (e.key === "ArrowRight") {
      const nextCell = cells.find((c) => c.x === cell.x + 1 && c.y === cell.y);
      if (nextCell) {
        const nextCellObject =
          cellHtmlObjects[`cell-${nextCell.x}-${nextCell.y}`];
        nextCellObject?.focus();
      }
    } else if (e.key === "ArrowLeft") {
      const prevCell = cells.find((c) => c.x === cell.x - 1 && c.y === cell.y);
      if (prevCell) {
        const prevCellObject =
          cellHtmlObjects[`cell-${prevCell.x}-${prevCell.y}`];
        prevCellObject?.focus();
      }
    } else if (e.key === "ArrowDown") {
      const nextCell = cells.find((c) => c.x === cell.x && c.y === cell.y + 1);
      if (nextCell) {
        const nextCellObject =
          cellHtmlObjects[`cell-${nextCell.x}-${nextCell.y}`];
        nextCellObject?.focus();
      }
    } else if (e.key === "ArrowUp") {
      const prevCell = cells.find((c) => c.x === cell.x && c.y === cell.y - 1);
      if (prevCell) {
        const prevCellObject =
          cellHtmlObjects[`cell-${prevCell.x}-${prevCell.y}`];
        prevCellObject?.focus();
      }
    } else if (e.key === "Tab") {
      //default tab and shift tab behavior is to move focus, so just
      return;
    }
    e.preventDefault();
  }

  async function solve() {
    let digitsAsStrings = ["1", "2", "3", "4", "5", "6", "7", "8", "9"];

    // Set cell values where this cell only has one possible value
    for (const cell of cells) {
      if (cell.value) {
        cell.possibleValues = new Set([cell.value]);
        continue;
      }

      let possibleValues: Set<string> = new Set();
      for (const digit of digitsAsStrings) {
        let foundInGroup = false;
        const relevantGroups = groups.filter((g) =>
          g.cells.some((c) => c.x == cell.x && c.y == cell.y)
        );
        for (const group of relevantGroups) {
          if (group.cells.some((c) => c.value == digit)) {
            foundInGroup = true;
          }
          if (foundInGroup) break;
        }
        if (!foundInGroup) {
          possibleValues.add(digit);
        }
      }
      cell.possibleValues = possibleValues;
      if (possibleValues.size === 1) {
        cell.value = Array.from(possibleValues)[0];
        setTimeout(solve, 1);
        return;
      }
    }

    // Set cell values where this cell is only cell allowed to use that value
    for (const cell of cells) {
      if (cell.value) {
        continue;
      }
      for (const digit of cell.possibleValues || []) {
        const relevantGroups = groups.filter((g) =>
          g.cells.some((c) => c.x == cell.x && c.y == cell.y)
        );
        for (const group of relevantGroups) {
          let cellsWithThisDigit = group.cells
            .filter((c) => !c.value)
            .filter((c) => !!c.possibleValues)
            .filter((c) => !!c.possibleValues?.has(digit));
          if (cellsWithThisDigit.length === 1) {
            cell.value = digit;
            setTimeout(solve, 1);

            return;
          }
        }
      }
    }
  }
</script>

<div
  class="relative mx-auto"
  style="
    width: min(90vw, 80vh, 1000px);
  "
>
  <h1 class=" text-xl xl:text-4xl font-bold text-center mt-8 mb-4">
    NRC SUDOKU Solver
  </h1>

  <button
    onclick={solve}
    class="z-50 absolute top-4 right-4 p-2 bg-blue-500 hover:bg-blue-300 text-white rounded"
  >
    Solve
  </button>
</div>
<div
  class="relative mx-auto"
  style="
    width: min(90vw, 80vh, 1000px);
    height: min(90vw, 80vh, 1000px);
  "
>
  <div class="grid w-full h-full grid-cols-9 grid-rows-9 mt-10 border-2">
    {#each cells as cell}
      <input
        class:bg-gray-200={grayCells.some(
          (c) => c.x === cell.x && c.y === cell.y
        )}
        onkeydown={(e) => keyboardNav(e, cell)}
        bind:this={cellHtmlObjects[`cell-${cell.x}-${cell.y}`]}
        class:border-t-2={cell.y == 1}
        class:border-b-2={cell.y % 3 == 0 && cell.y != 1}
        class:border-l-2={cell.x == 1}
        class:border-r-2={cell.x % 3 == 0 && cell.x != 1}
        class="border h-full w-full text-center outline-none"
        bind:value={cell.value}
      />
    {/each}
  </div>
</div>
