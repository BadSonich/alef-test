<template>
  <div>
    <div class="parent-block">
      <h3>Персональные данные</h3>
      <div class="parent-form">
        <label>
          <span>Имя</span>
          <input type="text" name="parent-name" v-model="formParent.name">
        </label>
        <label>
          <span>Возраст</span>
          <input type="number" name="parent-age" v-model="formParent.age">
        </label>
      </div>
    </div>
    <div class="children-block">
      <div class="children-block__header">
        <h3>Дети (макс. 5)</h3>
        <button v-if="formChildren.length < 5" @click="addChild()" type="button">
          <span></span>
          Добавить ребенка
        </button>
      </div>
      <div class="children-block__body">
        <div v-for="(child,index) in formChildren" :key="'child' + index" class="child-form">
          <label>
            <span>Имя</span>
            <input type="text" name="child-name" v-model="child.name">
          </label>
          <label>
            <span>Возраст</span>
            <input type="number" name="child-age" v-model="child.age">
          </label>
          <button @click="deleteChild(index)" type="button">Удалить</button>
        </div>
      </div>
      <button @click="saveAll" type="button">Сохранить</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "site-form",
    props: ['parent', 'children'],
    data() {
      return {
        formParent: this.parent,
        formChildren: this.children,
      }
    },
    methods: {
      addChild() {
        this.formChildren.push({name: "", age: ""});
      },
      deleteChild(index) {
        this.formChildren.splice(index, 1);
      },
      saveAll() {
        localStorage.setItem('user-info', JSON.stringify(
            {
              parent: this.formParent,
              children: this.formChildren
            }
        ))
      }
    }
  }
</script>