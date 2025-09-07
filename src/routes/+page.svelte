<script lang="ts">
  import { browser } from "$app/environment";

  type cell = {
    x: number;
    y: number;
    value: string | null;
    possibleValues?: Set<string>;
  };
  //let cells: cell[] = [];
  let rows = 9;
  let cols = 9;

  //   for (let r = 1; r <= rows; r++) {
  //     let row = [];
  //     for (let c = 1; c <= cols; c++) {
  //       cells.push({ x: c, y: r, value: null });
  //     }
  //   }

  let cells = $state([]);

  cells = [
    {
      x: 1,
      y: 1,
      value: "1",
      possibleValues: new Set(["1"]),
    },
    {
      x: 2,
      y: 1,
      value: null,
    },
    {
      x: 3,
      y: 1,
      value: null,
    },
    {
      x: 4,
      y: 1,
      value: null,
    },
    {
      x: 5,
      y: 1,
      value: "6",
    },
    {
      x: 6,
      y: 1,
      value: null,
    },
    {
      x: 7,
      y: 1,
      value: null,
    },
    {
      x: 8,
      y: 1,
      value: null,
    },
    {
      x: 9,
      y: 1,
      value: null,
    },
    {
      x: 1,
      y: 2,
      value: null,
    },
    {
      x: 2,
      y: 2,
      value: "4",
    },
    {
      x: 3,
      y: 2,
      value: null,
    },
    {
      x: 4,
      y: 2,
      value: "1",
    },
    {
      x: 5,
      y: 2,
      value: "8",
    },
    {
      x: 6,
      y: 2,
      value: null,
    },
    {
      x: 7,
      y: 2,
      value: "6",
    },
    {
      x: 8,
      y: 2,
      value: null,
    },
    {
      x: 9,
      y: 2,
      value: null,
    },
    {
      x: 1,
      y: 3,
      value: "6",
    },
    {
      x: 2,
      y: 3,
      value: null,
    },
    {
      x: 3,
      y: 3,
      value: "9",
    },
    {
      x: 4,
      y: 3,
      value: null,
    },
    {
      x: 5,
      y: 3,
      value: "4",
    },
    {
      x: 6,
      y: 3,
      value: null,
    },
    {
      x: 7,
      y: 3,
      value: "1",
    },
    {
      x: 8,
      y: 3,
      value: null,
    },
    {
      x: 9,
      y: 3,
      value: null,
    },
    {
      x: 1,
      y: 4,
      value: "2",
    },
    {
      x: 2,
      y: 4,
      value: null,
    },
    {
      x: 3,
      y: 4,
      value: null,
    },
    {
      x: 4,
      y: 4,
      value: "6",
    },
    {
      x: 5,
      y: 4,
      value: null,
    },
    {
      x: 6,
      y: 4,
      value: null,
    },
    {
      x: 7,
      y: 4,
      value: null,
    },
    {
      x: 8,
      y: 4,
      value: null,
    },
    {
      x: 9,
      y: 4,
      value: null,
    },
    {
      x: 1,
      y: 5,
      value: null,
    },
    {
      x: 2,
      y: 5,
      value: "6",
    },
    {
      x: 3,
      y: 5,
      value: "4",
    },
    {
      x: 4,
      y: 5,
      value: "8",
    },
    {
      x: 5,
      y: 5,
      value: "5",
    },
    {
      x: 6,
      y: 5,
      value: null,
    },
    {
      x: 7,
      y: 5,
      value: "9",
    },
    {
      x: 8,
      y: 5,
      value: null,
    },
    {
      x: 9,
      y: 5,
      value: null,
    },
    {
      x: 1,
      y: 6,
      value: "9",
    },
    {
      x: 2,
      y: 6,
      value: null,
    },
    {
      x: 3,
      y: 6,
      value: null,
    },
    {
      x: 4,
      y: 6,
      value: "2",
    },
    {
      x: 5,
      y: 6,
      value: null,
    },
    {
      x: 6,
      y: 6,
      value: null,
    },
    {
      x: 7,
      y: 6,
      value: null,
    },
    {
      x: 8,
      y: 6,
      value: null,
    },
    {
      x: 9,
      y: 6,
      value: "6",
    },
    {
      x: 1,
      y: 7,
      value: null,
    },
    {
      x: 2,
      y: 7,
      value: "3",
    },
    {
      x: 3,
      y: 7,
      value: "6",
    },
    {
      x: 4,
      y: 7,
      value: null,
    },
    {
      x: 5,
      y: 7,
      value: null,
    },
    {
      x: 6,
      y: 7,
      value: "8",
    },
    {
      x: 7,
      y: 7,
      value: null,
    },
    {
      x: 8,
      y: 7,
      value: null,
    },
    {
      x: 9,
      y: 7,
      value: null,
    },
    {
      x: 1,
      y: 8,
      value: null,
    },
    {
      x: 2,
      y: 8,
      value: null,
    },
    {
      x: 3,
      y: 8,
      value: null,
    },
    {
      x: 4,
      y: 8,
      value: null,
    },
    {
      x: 5,
      y: 8,
      value: null,
    },
    {
      x: 6,
      y: 8,
      value: "6",
    },
    {
      x: 7,
      y: 8,
      value: null,
    },
    {
      x: 8,
      y: 8,
      value: null,
    },
    {
      x: 9,
      y: 8,
      value: null,
    },
    {
      x: 1,
      y: 9,
      value: null,
    },
    {
      x: 2,
      y: 9,
      value: null,
    },
    {
      x: 3,
      y: 9,
      value: null,
    },
    {
      x: 4,
      y: 9,
      value: null,
    },
    {
      x: 5,
      y: 9,
      value: null,
    },
    {
      x: 6,
      y: 9,
      value: null,
    },
    {
      x: 7,
      y: 9,
      value: "4",
    },
    {
      x: 8,
      y: 9,
      value: "6",
    },
    {
      x: 9,
      y: 9,
      value: null,
    },
  ];

  let topCornersOfGrayBoxes = [
    { x: 2, y: 2 },
    { x: 6, y: 2 },
    { x: 6, y: 6 },
    { x: 2, y: 6 },
  ];

  let grayCells = [];
  for (let corner of topCornersOfGrayBoxes) {
    for (let r = corner.y; r < corner.y + 3; r++) {
      for (let c = corner.x; c < corner.x + 3; c++) {
        grayCells.push({ x: c, y: r });
      }
    }
  }

  let groups: { name: string; cells: cell[] }[] = [];
  // Create groups for each 3x3 grid
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
      groups.push(group);
    }
  }

  i = 0;
  // Create groups for each row
  for (let r = 1; r <= 9; r++) {
    i++;
    let group = { row: r, name: `Row ${i}`, cells: [] };
    for (let c = 1; c <= 9; c++) {
      let cell = cells.find((cell) => cell.x === c && cell.y === r);
      if (cell) group.cells.push(cell);
    }
    groups.push(group);
  }

  // Create groups for each column
  i = 0;
  for (let c = 1; c <= 9; c++) {
    i++;
    let group = { col: c, name: `Col ${i}`, cells: [] };
    for (let r = 1; r <= 9; r++) {
      let cell = cells.find((cell) => cell.x === c && cell.y === r);
      if (cell) group.cells.push(cell);
    }
    groups.push(group);
  }

  i = 0;

  // Create groups for each gray cell area
  for (let corner of topCornersOfGrayBoxes) {
    i++;
    let group = { name: `GrayBox ${i} (${corner.x},${corner.y})`, cells: [] };
    for (let r = corner.y; r < corner.y + 3; r++) {
      for (let c = corner.x; c < corner.x + 3; c++) {
        let cell = cells.find((cell) => cell.x === c && cell.y === r);
        if (cell) group.cells.push(cell);
      }
    }
    groups.push(group);
  }

  async function solve() {
    console.log(groups);
    console.log(cells);
    let digitsAsStrings = ["1", "2", "3", "4", "5", "6", "7", "8", "9"];
    for (const cell of cells) {
      if (cell.value) {
        console.log(`cell ${cell.x},${cell.y} already has value`);
        continue;
      }
      console.log(`possible values cell ${cell.x},${cell.y}`);
      let possibleValues: Set<string> = new Set();
      for (const digit of digitsAsStrings) {
        let foundInGroup = false;
        for (const group of groups.filter((g) =>
          g.cells.some((c) => c.x == cell.x && c.y == cell.y)
        )) {
          if (group.cells.some((c) => c.value == digit)) {
            console.log(
              `Digit ${digit} found in group ${group.name} for cell ${cell.x},${cell.y}`
            );
            foundInGroup = true;
          }
          if (foundInGroup) continue;
        }
        if (!foundInGroup) {
          console.log(
            `Digit ${digit} not found in any group for cell ${cell.x},${cell.y}`
          );
          possibleValues.add(digit);
          break;
        }
      }
      console.log(
        `Possible values for cell ${cell.x},${cell.y}: ${Array.from(
          possibleValues
        ).join(", ")}`
      );
      cell.possibleValues = possibleValues;
    }

    for (const cell of cells) {
      if (cell.value) {
        console.log(`cell ${cell.x},${cell.y} already has value`);
        continue;
      }
      console.log(`possible values cell ${cell.x},${cell.y}`);
      let possibleValues: Set<string> = new Set();
      for (const digit of digitsAsStrings) {
        let foundInGroup = false;
        for (const group of groups.filter((g) =>
          g.cells.some((c) => c.x == cell.x && c.y == cell.y)
        )) {
          if (
            group.cells.some(
              (c) =>
                c.value == digit ||
                (c.possibleValues && c.possibleValues.has(digit))
            )
          ) {
            console.log(
              `Digit ${digit} found in group ${group.name} for cell ${cell.x},${cell.y}`
            );
            foundInGroup = true;
          }
          if (foundInGroup) break;
        }
        if (!foundInGroup) {
          console.log(
            `Digit ${digit} not found in any group for cell ${cell.x},${cell.y}`
          );
          possibleValues.add(digit);
          break;
        }
      }
      console.log(
        `FINAL Possible values for cell ${cell.x},${cell.y}: ${Array.from(
          possibleValues
        ).join(", ")}`
      );
      if (possibleValues.size === 1) {
        cell.value = Array.from(possibleValues)[0];
        setTimeout(solve, 100);
        return;
      }
    }
  }
</script>

<a
  onclick={solve}
  class="z-50 absolute top-4 right-4 p-2 bg-blue-500 hover:bg-blue-300 text-white rounded"
>
  Solve
</a>
<div
  class="absolute top-0 left-0 w-full h-full flex flex-col items-center justify-center"
>
  <h1 class="text-3xl mb-4">Grid</h1>
  <div class="grid grid-cols-9 grid-rows-9 gap-0 w-[400px]">
    {#each cells as cell}
      <input
        onchange={solve}
        class:bg-gray-200={grayCells.some(
          (c) => c.x === cell.x && c.y === cell.y
        )}
        class:border-t-2={cell.y == 1}
        class:border-b-2={cell.y % 3 == 0}
        class:border-l-2={cell.x == 1}
        class:border-r-2={cell.x % 3 == 0}
        class="border-1 h-10 w-10 flex text-center"
        bind:value={cell.value}
      />
    {/each}
  </div>
</div>
