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
            <div class="feature-icon">
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
                    <i>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-app" viewBox="0 0 16 16">
                        <path d="M11 2a3 3 0 0 1 3 3v6a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3V5a3 3 0 0 1 3-3h6zM5 1a4 4 0 0 0-4 4v6a4 4 0 0 0 4 4h6a4 4 0 0 0 4-4V5a4 4 0 0 0-4-4H5z"/>
                        </svg>
                    </i>
                </div>
                <div class="item-title">
                    {{ item.title }}
                </div>
                <div class="feature-icon">
                    <i v-if="!itemFavorite" class="bi bi-star" @click="itemFavorite = !itemFavorite">
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
    </div>

</template>

<script>
export default{
    data: () => {
        return {
            entry: '',
            entryFavorite: false,
            todoList: [],
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
                }, 10)

                this.entry = '';
                this.entryFavorite = false;
            }
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
        font-size: 2rem;
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
}

</style>