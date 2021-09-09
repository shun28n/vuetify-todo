<template>
  <v-dialog
    :value="true"
    persistent
    max-width="290"
  >
    <v-card>
      <v-card-title class="headline">
        タスクを編集しますか？
      </v-card-title>
      <v-card-text>
        このタスクのタイトルを編集します。
        <v-text-field 
        v-model="taskTitle"
        @keyup.enter="saveTask"
         />
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          @click="$emit('close')"
          text
        >
          キャンセル
        </v-btn>
        <v-btn
          @click="saveTask"
          :disabled="taskTitleInvalid"
          color="primary darken-6"
          text
        >
          保存
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ['task'],
  data(){
    return{
      taskTitle:''
    }
  },
  computed:{
      taskTitleInvalid(){
        return !this.taskTitle || this.task.title === this.taskTitle
      }
  },
  methods:{
    saveTask(){
      if(!this.taskTitleInvalid){
        let payload = {
          id: this.task.id,
          title: this.taskTitle
        }
        this.$store.dispatch('updateTaskTitle', payload)
        this.$emit('close')
      }
    }
  },
  mounted(){
    this.taskTitle = this.task.title
  }
}
</script>

<style>

</style>