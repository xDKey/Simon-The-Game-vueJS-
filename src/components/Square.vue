<template>
      <div class='square' :style='{backgroundColor: this.color}' @click='this.choise'></div>
</template>
<script>
export default {
    props: ['props'],

    data(){
        return{
            id: this.props.id,
            color : this.props.color,
        }
    },

    methods:{
        choise(){
            this.$emit('choise', this.id)
        }
    }
}
</script>

<style scoped>
.square{
  width: 100px;
  height: 100px;
  margin: 10px;
  cursor: pointer;
}
</style>