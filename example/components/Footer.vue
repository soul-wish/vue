<template>
  <footer class="footer">
    <span class="todo-count">
      <strong>{{numActive}}</strong>
      {{numActive === 1 ? 'item' : 'items'}} left
    </span>
    <ul class="filters">
      <li>
        <a :class="{ selected: filter === SHOW_ALL }" href="/#">All</a>
      </li>
      <li>
        <a :class="{ selected: filter === SHOW_ACTIVE }" href="/#active">Active</a>
      </li>
      <li>
        <a :class="{ selected: filter === SHOW_COMPLETED }" href="/#completed">Completed</a>
      </li>
    </ul>
    <button
      v-if="numCompleted"
      class="clear-completed"
      @click="handleClearCompleted"
    >Clear completed</button>
  </footer>
</template>

<script>
import { mapState, mapDispatch } from '../../helpers'
import {
  SHOW_ALL,
  SHOW_ACTIVE,
  SHOW_COMPLETED
} from "../constants/TodoFilters";

export default {
  data() {
    return {
      SHOW_ALL,
      SHOW_ACTIVE,
      SHOW_COMPLETED
    };
  },
  computed: mapState({
    filter: 'filter',
    numCompleted: state => state.todos.filter(todo => todo.completed).length,
    numActive: state => state.todos.filter(todo => !todo.completed).length
  }),
  methods: mapDispatch({
    handleClearCompleted: "todo/clear_completed",
  }),
};
</script>
