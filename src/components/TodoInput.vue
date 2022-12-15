<template>
    <div class="container">
        <div class="add-item">
            <div class="add-icon" @click="addItem">
                <i>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle" viewBox="0 0 16 16">
                    <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
                    <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
                    </svg>
                </i>
            </div>
            <form @submit.prevent="addItem">
                <input type="text" placeholder="Aggiungi qualcosa da fare..." v-model="entry">
            </form>
            <div class="feature-icon" :class="{'red-bg' : entryFavorite}">
                <i v-if="!entryFavorite" @click="entryFavorite = !entryFavorite">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                    <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                    </svg>
                </i>
                <i v-else class="bi bi-star" @click="entryFavorite = !entryFavorite">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                    <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                    </svg>
                </i>
            </div>
        </div>
        <div class="todo-list">
            <div class="item" :class="{'show' : item.show}" v-for="(item, index) in todoList" :key="index">
                <div class="item-checkbox">
                    <i v-if="!item.complete" @click="completeItem(item)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-app" viewBox="0 0 16 16">
                        <path d="M11 2a3 3 0 0 1 3 3v6a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3V5a3 3 0 0 1 3-3h6zM5 1a4 4 0 0 0-4 4v6a4 4 0 0 0 4 4h6a4 4 0 0 0 4-4V5a4 4 0 0 0-4-4H5z"/>
                        </svg>
                    </i>
                    <i v-else @click="completeItem(item)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check-square" viewBox="0 0 16 16">
                        <path d="M14 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12zM2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2z"/>
                        <path d="M10.97 4.97a.75.75 0 0 1 1.071 1.05l-3.992 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.235.235 0 0 1 .02-.022z"/>
                        </svg>
                    </i>
                </div>
                <div class="item-title">
                    {{ item.title }}
                </div>
                <div class="feature-icon" :class="{'red-bg' : entryFavorite}">
                    <i v-if="!itemFavorite" class="bi bi-star" @click="setFavorite(item)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                        <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                        </svg>
                    </i>
                    <i v-else class="bi bi-star" @click="itemFavorite = !itemFavorite">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                        <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                        </svg>
                    </i>
                </div>
            </div>
        </div>
        <div class="show-completed" v-if="completedToDoList.length > 0">
            <div class="button" @click="showCompletedList = !showCompletedList">
                <span v-if="!showCompletedList">Mostra</span><span v-else>Nascondi</span>
                le cose fatte 
            </div>
        </div>
        <div class="todo-list complete-list" v-if="showCompletedList">
            <div class="item" :class="{'show': item.show}" v-for="(item, index) in completedToDoList" :key="index">
                <div class="item-checkbox">
                    <i v-if="!item.complete">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-app" viewBox="0 0 16 16">
                        <path d="M11 2a3 3 0 0 1 3 3v6a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3V5a3 3 0 0 1 3-3h6zM5 1a4 4 0 0 0-4 4v6a4 4 0 0 0 4 4h6a4 4 0 0 0 4-4V5a4 4 0 0 0-4-4H5z"/>
                        </svg>
                    </i>
                    <i v-else  @click="uncompleteItem(item)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check-square" viewBox="0 0 16 16">
                        <path d="M14 1a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h12zM2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2z"/>
                        <path d="M10.97 4.97a.75.75 0 0 1 1.071 1.05l-3.992 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.235.235 0 0 1 .02-.022z"/>
                        </svg>
                    </i>
                </div>
                <div class="item-title">
                    {{ item.title }}
                </div>
                <div class="feature-icon" :class="{'red-bg' : entryFavorite}">
                    <i v-if="!itemFavorite">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                        <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                        </svg>
                    </i>
                    <i v-else>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-star" viewBox="0 0 16 16">
                        <path d="M2.866 14.85c-.078.444.36.791.746.593l4.39-2.256 4.389 2.256c.386.198.824-.149.746-.592l-.83-4.73 3.522-3.356c.33-.314.16-.888-.282-.95l-4.898-.696L8.465.792a.513.513 0 0 0-.927 0L5.354 5.12l-4.898.696c-.441.062-.612.636-.283.95l3.523 3.356-.83 4.73zm4.905-2.767-3.686 1.894.694-3.957a.565.565 0 0 0-.163-.505L1.71 6.745l4.052-.576a.525.525 0 0 0 .393-.288L8 2.223l1.847 3.658a.525.525 0 0 0 .393.288l4.052.575-2.906 2.77a.565.565 0 0 0-.163.506l.694 3.957-3.686-1.894a.503.503 0 0 0-.461 0z"/>
                        </svg>
                    </i>
                </div>
            </div>
        </div>


    </div>

</template>

<script>
export default{
    data: () => {
        return {
            entry: '',
            entryFavorite: false,
            todoList: [],
            completedToDoList: [],
            showCompletedList: false,
        }
    },
    methods: {
        addItem(){
            if(this.entry !== ''){
                let date = new Date;
                let newEntry = {
                    id: date.getTime(),
                    title: this.entry,
                    favorite: this.entryFavorite,
                    complete: false,
                    show: false
                }

                if(newEntry.favorite){
                    // inserisce la card al primo posto
                    this.todoList.splice( 0, 0, newEntry);
                }
                else{
                    // inserisce la card all'ultimo posto
                    this.todoList.push(newEntry);
                }

                setTimeout(() => {
                    this.todoList.find(element => element.id === newEntry.id).show = true;
                }, 10);
            }

                this.entry = '';
                this.entryFavorite = false;
        },

        setFavorite(item){
            item.favorite = !item.favorite;
            item.show = false;
            
            setTimeout(() => {
                let index = this.todoList.findIndex(element => element.id === item.id);
                this.todoList.splice(index, 1);
                this.todoList.splice( 0, 0, item);
                item.show = true;
            }, 500);
        },
        completeItem(item) {
            item.complete = !item.complete;
            item.show = false;
            
            setTimeout(() => {
                this.completedToDoList.push(item);
                let index = this.todoList.findIndex(element => element.id === item.id);
                this.todoList.splice(index, 1);
                item.show = true;
            }, 500);
        },
        uncompleteItem(item) {
            item.favorite = !item.favorite;
            item.show = false;

            setTimeout(() => {
                if(item.favorite) {
                    this.todoList.splice( 0, 0, item);
                }
                else{
                    this.todoList.push(item);
                }

                let index = this.completedToDoList.findIndex(element => element.id === item.id);
                this.completedToDoList.splice(index, 1);
                item.show = true;
            }, 500);
        }
    }


}
</script>

<style lang="scss" scoped>
.container{
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100% - 20px);

    @mixin feature-icon($color){
        grid-column-start: 3;
        grid-column-end: 3;
        display: flex;
        justify-content: center;
        align-items: center;
        color: $color;
        font-size: 1.6rem;
        margin: 0 15px;
        cursor: pointer;
    }

    i{
        display: flex;
        justify-content: center;
        align-items: baseline;
    }

    .add-item{
        display: grid;
        grid-template-columns: 70px auto 70px;
        grid-template-rows: 60px;
        width: 100%;
        height: 60px;
        background: rgba($color: #000000, $alpha: .3);
        border-radius: 5px;
        overflow: hidden;

        .add-icon{
            grid-column-start: 1;
            grid-column-end: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #fff;
            font-size: 2rem;
            cursor: pointer;
        }

        input{
            grid-column-start: 2;
            grid-column-end: 2;
            background: none;
            border: none;
            width: 100%;
            height: 60px;
            color: #fff;
            font-size: 1.6rem;

            &::placeholder{
                color: #fff;
            }

            &:focus{
                outline: none;
            }
        }

        .feature-icon{
            @include feature-icon(#fff)
        }
    }

    .todo-list{
        padding-top: 20px;

        .item{
            display: grid;
            grid-template-columns: 70px auto 70px;
            grid-template-rows: 60px;
            width: 100%;
            height: 60px;
            margin-bottom: 2px;
            background: rgba($color: #fff, $alpha: .8);
            border-radius: 5px;
            overflow: hidden;
            opacity: 0;
            transition: all .5s linear;

            .item-checkbox{
                grid-column-start: 1;
                grid-column-end: 1;
                display: flex;
                justify-content: center;
                align-items: center;
                color: #99C191;
                font-size: 1.6rem;
                cursor: pointer;
            }

            .item-title{
                grid-column-start: 2;
                grid-column-end: 2;
                display: flex;
                justify-content: flex-start;
                align-items: center;
                font-size: 1.6rem;
            }

            .feature-icon{
                @include feature-icon(#333)
            }
        }

        .show{
            opacity: 1;
        }
    }

    .complete-list{
        .item{
            position: relative;
            background: rgba($color: #fff, $alpha: .4);

            &::before{
                content: '';
                position: absolute;
                top: 30px;
                width: calc(100% - 120px);
                margin: 0 60px;
                border-bottom: 2px solid #555;
            }
        }
    }

    .show-completed{
        display: flex;
        justify-content: center;
        align-items: center;
        padding-top: 20px;

        .button{
            color: #fff;
            padding: 10px;
            font-size: 1.3rem;
            text-transform: uppercase;
            background: rgba($color: #000000, $alpha: .3);
            border-radius: 5px;            
            overflow: hidden;
            cursor: pointer;
        }

    }

    .red-bg{
        background-color: red;
        color: #fff !important;
    }
}

</style>