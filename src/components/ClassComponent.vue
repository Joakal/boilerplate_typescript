<template>
  <div>
    <p>{{ title }}</p>
    <ul>
      <li v-for="todo in todos" :key="todo.id" @click="increment">
        {{ todo.id }} - {{ todo.content }}
      </li>
    </ul>
    <p>Count: {{ todoCount }} / {{ meta.totalCount }}</p>
    <p>Active: {{ active ? 'yes' : 'no' }}</p>
    <p>Clicks on todos: {{ clickCount }}</p>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import { Todo, Meta } from './models';

@Component
export default class ClassComponent extends Vue {
  @Prop({ type: String, required: true }) readonly title!: string;
  @Prop({ type: Array, default: () => [] }) readonly todos!: Todo[];
  @Prop({ type: Object, required: true }) readonly meta!: Meta;
  @Prop(Boolean) readonly active!: boolean;

  clickCount = 0;
  numberVar = 5;

  increment() {
    this.clickCount += 1;

    // This should show an error
    this.numberVar = "number";

    // These two shouldn't show an error
    this.$axios.post('/login').then(res => console.log('You are logged in!', res)).catch(err => console.log('Oh no, rejected!', err))
    this.$q.notify({
      color: 'negative',
      position: 'top',
      message: 'This is a notification',
      icon: 'report_problem'
    })
  }

  get todoCount() {
    return this.todos.length;
  }
}
</script>
