<template>

    <template v-if="!isEdit">

        <div
            title="Для того, чтобы поменить выполение нажми сюда, 
            если хочешь вернуться к заданию - нажми еще раз"
            class="unit"
            @click="toggleClass()"
            :class="[isActive ? 'start' : 'done']"
        >

           {{ point }}

        </div>

        <br>
        
        <button @click="edit">
            Редактировать
        </button>

    </template>

    <template v-else>

        <input v-model="newPoint">

        <button @click="save">
            Сохранить
        </button>

    </template>

    <button @click="remove">
        Удалить
    </button>

    <hr>
    <br>

</template>

<script>

    export default {
        emits: ['remove', 'change'],
        props: {
            id: Number,
            point: String
        },
        data(){
            return {
                newPoint: this.point,
                isEdit: false,
                isActive: true
            }
        },
        methods: {
            remove() {
                this.$emit('remove', this.id, this.newPoint);
            },
            edit() {
                this.isEdit = true;
            },
            save(){
                this.isEdit = false;
                this.$emit('change', this.id, this.newPoint)
            },
            toggleClass(){
                this.isActive = !this.isActive;
            }
        }
    }

</script>

<style>
    .start{
        cursor: pointer;
        user-select: none;
    }
    .done{
        cursor: pointer;
        user-select: none;
        text-decoration: line-through;
    }
    .unit{
        display: inline-block;
    }
    button{
        cursor: pointer;
        background-color: blueviolet;
        margin-top: 0px;
        margin-left: 20px;
        border: 1.5px solid black;
        transition: all 0.38s ease;
        border-radius: 13px;
        height: 30px
    }
    button:hover{
        background-color:aqua;
    }  
</style>