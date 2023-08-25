<template>
  <div>
    <InputUI label="Имя" placeholder="Введите имя" v-model="user.name" />
    <InputUI label="Телефон" placeholder="Введите телефон" v-model="user.tel"/>
    <SelectUI label="Начальник" :options="bossOptions" v-model="boss"/>
    <ButtonUI @click="addUser">Добавить пользователя</ButtonUI>
  </div>
</template>

<script>
import InputUI from "../ui/InputUI/InputUI.vue";
import ButtonUI from "../ui/ButtonUI/ButtonUI.vue";
import SelectUI from "../ui/SelectUI/SelectUI.vue";

export default {
  name: 'AddUserForm',
  components: {SelectUI, ButtonUI, InputUI},
  props: {
    users: Array
  },
  data(){
    return{
      user:{
        name: '',
        tel: '',
      },
      boss: ''
    }
  },
  computed:{
    bossOptions(){
      const settings = []
      this.users.forEach(us => {
        settings.push({
          value: us.id,
          label: us.name
        })
      })
      return settings
    }
  },
  methods: {
    addUser(){
      this.user.id = Date.now()
      this.user.subordinates = []
      this.$emit('addUser', this.user, this.boss)
      this.user = {
        name: '',
        tel: '',
      }
      this.boss = ''
    }
  }
}
</script>

<style lang="css" scoped>

</style>
