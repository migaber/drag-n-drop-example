<template>
  <div id="app">
    <div class="c-dnd-container">
      <div class="c-dnd-column">
        <h2>Todo</h2>
        <ul>
          <li draggable="true">Item 1</li>
          <li draggable="true">Item 2</li>
          <li draggable="true">Item 3</li>
        </ul>
      </div>
      <div class="c-dnd-column">
        <h2>Inprogress</h2>
        <ul>
          <li draggable="true">Item 4</li>
          <li draggable="true">Item 5</li>
          <li draggable="true">Item 6</li>
        </ul>
      </div>
      <div class="c-dnd-column">
        <h2>Done</h2>
        <ul>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  mounted() {
    console.log('mounted');
    const draggables = document.querySelectorAll('[draggable=true]'); // all draggable items
    const columns = document.querySelectorAll('.c-dnd-column'); // statuses columns

    draggables.forEach(draggableItem => {
      draggableItem.addEventListener('dragstart', () => {
        draggableItem.classList.add('is-dragging');
      })

      draggableItem.addEventListener('dragend', () => {
        draggableItem.classList.remove('is-dragging');
      })
    });

    columns.forEach(column => {
      column.addEventListener('dragover', (e) => {

        const nextElementToDraggableItem = this.getIsDraggingNextElement(column, e.clientY);
        const draggableItem = document.querySelector('.is-dragging');

        if (!nextElementToDraggableItem) {
          column.querySelector('ul').appendChild(draggableItem);
        } else {
          column.querySelector('ul').insertBefore(draggableItem, nextElementToDraggableItem)
        }

        console.log(nextElementToDraggableItem);
      });
    })
  },
  methods: {
    getIsDraggingNextElement(column, yPosition) {
      const draggableItemsInCurrentContainer = [...column.querySelectorAll('[draggable=true]:not(.is-dragging)')];

      return draggableItemsInCurrentContainer.reduce((closest, child) => {
        // get dimentions of not draggable items in current container
        const childBounds = child.getBoundingClientRect();

        const offset = yPosition - childBounds.top

        if (offset < 0 && offset > closest.offset) {
          return {
            offset,
            element: child
          }
        } else {
          return closest;
        }
      }, { offset: Number.NEGATIVE_INFINITY}).element
    }
  }
}
</script>

<style>
.c-dnd-container {
  display: flex;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

.c-dnd-column {
  border: 1px solid #dfdfdf;
  margin-right: 16px;
  flex: 1;
  padding-left: 8px;
}

.c-dnd-column:last-of-type {
  margin-right: 0;
}

h2 {
  padding: 0 0 8px 0;
  margin: 0;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.c-dnd-column li {
  color: #ff2200;
  padding: 8px 4px;
  border: 1px solid #ac1700;
  margin: 4px 0;
  cursor: move;
}

.c-dnd-column li.is-dragging {
  border-color: #fcb0a4;
  background-color: #f5f5f5;
}


</style>
