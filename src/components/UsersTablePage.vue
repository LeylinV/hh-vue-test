<template>
  <div class="hello">
    <ButtonUI class="add-button" @click="toggleModal">Добавить</ButtonUI>
    <UsersTable :users="sortedUsers" @selectedSort="setSort" />
    <ModalUI :showModal="showModal" modalName="Добавление пользователя" @close="toggleModal">
      <AddUserForm :users="extractUsers" @addUser="addUser"/>
    </ModalUI>
  </div>
</template>

<script>
import ButtonUI from "./ui/ButtonUI/ButtonUI.vue";
import ModalUI from "./ui/ModalUI/ModalUI.vue";
import AddUserForm from "./AddUserForm/AddUserForm.vue";
import UsersTable from "./UsersTable/UsersTable.vue";

export default {
  name: 'UsersTablePage',
  components: {UsersTable, ModalUI, ButtonUI, AddUserForm},
  data () {
    return {
      showModal: false,
      selectedSort: '',
      isSortReversed: false,
      users: [
        {
          "name": "Алексей",
          "tel": "+7 123 456 78 90",
          "id": 1693000852513,
          "subordinates": []
        },
        {
          "name": "Василий",
          "tel": "+7 234 567 89 01",
          "id": 1693000874692,
          "subordinates": []
        },
        {
          "name": "Георгий",
          "tel": "+7 987 654 32 10",
          "id": 1693000891056,
          "subordinates": []
        }
      ],
      isChanged: false // Костыль с глубоким отслеживанием =)
    }
  },
  computed: {
    sortedUsers() {
      this.isChanged = Boolean(this.isChanged) // Костыль с глубоким отслеживанием =)
      const sortedUsers = JSON.parse(JSON.stringify(this.users))
      if (this.selectedSort) {
        const stack = [sortedUsers]
        while (stack.length > 0) {
          const currentUsers = stack.pop()
          currentUsers.sort((a, b) => {
            return this.isSortReversed
              ? a[this.selectedSort].localeCompare(b[this.selectedSort])
              : b[this.selectedSort].localeCompare(a[this.selectedSort])
          })
          for (const user of currentUsers) {
            if (user.subordinates && user.subordinates.length > 0) {
              stack.push(user.subordinates)
            }
          }
        }
      }
      return sortedUsers;
    },

    extractUsers() {
      this.isChanged = Boolean(this.isChanged) // Костыль с глубоким отслеживанием =)
      const stack = JSON.parse(JSON.stringify(this.users));
      const result = [];

      while (stack.length > 0) {
        const user = stack.pop()
        result.push(user)
        stack.push(...user.subordinates)
      }

      return result.sort((a,b) => a.name.localeCompare(b.name))
    }
  },
  methods: {
    toggleModal(){
      this.showModal = !this.showModal
    },

    setSort(sort){
      if (this.selectedSort === sort){
        this.isSortReversed = !this.isSortReversed
      }
      this.selectedSort = sort;
    },

    addUser(user, boss){
      this.toggleModal()
      if (boss){
        const bossOfUser = this.findUserByID(boss)
        bossOfUser.subordinates.push(user)
      } else{
        this.users.push(user)
      }
      this.saveToLocaleStorage()
      this.isChanged = !this.isChanged
    },

    findUserByID(id) {
      const stack = [...this.users]
      while (stack.length > 0) {
        const user = stack.pop();
        if (user.id === +id) {
          return user
        }
        stack.push(...user.subordinates);
      }
    },

    saveToLocaleStorage(){
      localStorage.setItem('users', JSON.stringify(this.users))
    }
  },
  mounted() {
    if (JSON.parse(localStorage.getItem('users'))){
     this.users = JSON.parse(localStorage.getItem('users'))
    }
  }
}
</script>

<style scoped>
.add-button{
  margin: 15px 0;
}
</style>
