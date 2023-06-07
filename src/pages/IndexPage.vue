<template>
  <q-page class="flex flex-center justify-content-center align-items-center q-ma-md">
    <section
    v-for="item in resultAPI"
    :key = "item.id"
    class="bg-grey-12 q-ma-lg q-ml-lg item-class"
    >
      <article class="item-text">
        <header class="header-text">
          <span>Text: </span>
          {{ item.title }}
        </header>
        <div :class="{'header-text' :true, 'completed': item.completed ? true : false, 'false': item.completed == false ? true : false  }">
          <span>Completed: </span>
          {{ item.completed }}
        </div>
      </article>
    </section>
  </q-page>
</template>

<script>
import { defineComponent, onBeforeMount, ref } from 'vue'
import { api } from 'src/boot/axios'
export default defineComponent({
  name: 'IndexPage',
  setup () {
    const resultAPI = ref({})
    const typiCodeApi = api.get('https://jsonplaceholder.typicode.com/todos?_limit=10').then((data) => {
      resultAPI.value = data.data
      return data.data
    })
    onBeforeMount(async () => {
      console.log(resultAPI)
    })
    return {
      typiCodeApi,
      resultAPI
    }
  }
})
</script>

<style scoped>
  .item-class{
    display: flex;
    align-items: center;
    width: 100%;
    height: 150px;
    border-radius: 20px;
    box-shadow: 2px 2px 8px rgb(103, 103, 103);
    transition: all .6s;
  }

  .item-class:hover{
    transform: scale(1.02,1.02);
  }

  .item-text{
    display: flex;
    align-items: left;
    justify-content: center;
    flex-direction: column;
    padding-left: 40px;

    width: 60%;
    gap: 15px;

  }

  .header-text{
    display: flex;
    align-items: center;
    font-size: 16px;
  }

  .header-text>span{
    font-size: 16px;
    font-weight: bold;
    padding-right: 8px;
  }

  .completed{
    font-weight: bold;
    padding: 5px 10px;
    color: white;
    background-color: green;
    border-radius: 10px;
  }

  .false{
    font-weight: bold;
    padding: 5px 10px;
    color: white;
    border-radius: 10px;
    background-color: rgb(128, 0, 0);
  }

</style>
