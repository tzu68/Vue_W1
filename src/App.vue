<script setup>
import { ref } from 'vue'
// 引入 Bootstrap CSS
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap-icons/font/bootstrap-icons.css'

const data = ref([
  {
    id: 1,
    title: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    title: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    title: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    title: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    title: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    title: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    title: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    title: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

const temp = ref({})

function editItem(id) {
  const index = data.value.findIndex((item) => item.id == id)
  temp.value = { ...data.value[index] }
}

function editFinish() {
  const index = data.value.findIndex((item) => item.id == temp.value.id)
  data.value[index].title = temp.value.title
  temp.value = {}
}
</script>

<template>
  <div class="container container-fluid">
    <div class="row">
      <div class="col">
        <table class="table table-success table-striped table-hover">
          <thead>
            <tr>
              <th scope="col"><p>品項</p></th>
              <th scope="col"><p>狀態</p></th>
              <th scope="col"><p>描述</p></th>
              <th scope="col"><p>價格</p></th>
              <th scope="col"><p>庫存</p></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, key) in data" key="{{item.id}}">
              <td class="w-25">
                <input type="text" v-if="temp.id === item.id" v-model="temp.title" />
                <p v-if="temp.id !== item.id">{{ item.title }}</p>
              </td>
              <td>
                <button
                  v-if="temp.id !== item.id"
                  class="btn btn-success d-inline-block"
                  type="button"
                  @click.prevent="editItem(item.id)"
                >
                  編輯品項名稱
                </button>
                <button
                  v-if="temp.id === item.id"
                  class="btn btn-success d-inline-block me-md-1"
                  type="button"
                  @click.prevent="editFinish()"
                >
                  確認
                </button>
                <button
                  v-if="temp.id === item.id"
                  class="btn btn-danger d-inline-block"
                  type="button"
                  @click.prevent="temp = {}"
                >
                  取消
                </button>
              </td>
              <td>
                <p>{{ item.description }}</p>
              </td>
              <td>
                <p>{{ item.price }}</p>
              </td>
              <td>
                <div class="stockDiv">
                  <button
                    type="buton"
                    class="btn btn-success d-block btn-sm"
                    @click="item.stock > 0 ? item.stock-- : 0"
                  >
                    <i class="bi bi-dash"></i>
                  </button>
                  <p class="stock">{{ item.stock }}</p>
                  <button type="buton" class="btn btn-success d-block btn-sm" @click="item.stock++">
                    <i class="bi bi-plus"></i>
                  </button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
td,
th {
  text-align: center;
  vertical-align: middle;
}

td p,
th p {
  margin: auto 0px;
}

.stockDiv {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.stockDiv .stock {
  min-width: 3rem;
}
</style>
