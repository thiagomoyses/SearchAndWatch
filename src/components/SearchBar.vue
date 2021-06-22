<template>
    <div>
        <input @input="OnInput"/>
    </div>
</template>

<script>
export default{ 
    name: 'SearchBar',
    methods: {
        OnInput: function(event){
            this.$emit('termChange', event.target.value);
        }
    },
}
</script>

<style scoped>
    input{
        width: 75%;
    }
    div{
        text-align: center;
        margin: 20px;
    }

</style>