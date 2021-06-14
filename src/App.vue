<template>
  <div id="app">
    <div class="c-dnd-container">
      <div class="c-dnd-column">
        <h2>Todo</h2>
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
        </ul>
      </div>
      <div class="c-dnd-column">
        <h2>Inprogress</h2>
        <ul>
          <li>Item 4</li>
          <li>Item 5</li>
          <li>Item 5</li>
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
  color: #f20;
  padding: 8px 4px;
  border: 1px solid red;
  margin: 4px 0;
}


</style>
