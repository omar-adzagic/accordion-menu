<template>
    <div class="container">
        <div>
            <ul class="citruses">
                <li :class="{ 'height-change': citrus.isActive }"
                    :key="citrus.id"
                    v-for="citrus in citruses"
                    @click="toggleHeight(citrus)">
                    {{ citrus.name }}
                    <i class="fas fa-times" @click.stop="removeItem(citrus)"></i>
                </li>
            </ul>
            <div class="add-new-item">
                <input type="text"
                       v-model="newCitrus"
                       placeholder="Enter value">
                <button @click="addItem">Add new</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                newCitrus: '',
                citruses: [
                    { id: 1, name: 'orange', isActive: false },
                    { id: 2, name: 'lemon', isActive: false },
                    { id: 3, name: 'limetta', isActive: false },
                    { id: 4, name: 'grapefruit', isActive: false },
                    { id: 5, name: 'mandarin orange', isActive: false }
                ]
            };
        },
        methods: {
            toggleHeight(citrus) {
                this.citruses.map(item => {
                    if (item != citrus) {
                        item.isActive = false;
                    }
                });
                citrus.isActive = citrus.isActive == true ? false : true;
            },
            addItem() {
                if (this.newCitrus != '') {
                    const newCitrusObject = {
                        name: this.newCitrus,
                        isActive: false
                    };
                    this.citruses.push(newCitrusObject);
                    this.newCitrus = '';
                }
            },
            removeItem(citrus) {
                this.citruses.map(item => item.isActive = false);
                this.citruses.splice(this.citruses.indexOf(citrus), 1);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    body {
        font-family: 'Lato', sans-serif;
    }
    h1 {
        text-align: center;
    }
    button {
        background-color: #ddd;
        border: 1px solid #aaa;
    }
    button:active {
        /*transform: translateX(0);*/
    }
    #app {
        text-align: center;
    }
    .container {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-content: center;
    }
    .citruses {
        display: inline-block;
        list-style-type: none;
        padding: 0;
        .height-change {
            height: 80px;
            background-color: #ddd;
        }
        li {
            width: 250px;
            border: 1px solid #aaa;
            border-radius: 3px;
            margin-top: 6px;
            padding: 8px 15px;
            color: #333;
            cursor: pointer;
            transition: height 0.4s ease-in-out,
                        background-color 0.4s ease-in-out;
            height: 20px;
            &:hover {
                background-color: rgba(0,64,192,0.2);
            }
        }
        i {
            float: right;
            color: #555;
        }
    }

    .add-new-item {
        margin: auto;
        input {
            width: 250px;
            padding: 10px 15px;
            border: 1px solid #aaa;
            border-radius: 3px;
            &:hover {
                border-color: #2A7296;
            }
            &:focus {
                border-color: #2A7296;
            }
        }
        button {
            margin: 10px auto auto auto;
            display: block;
            width: 250px;
            padding: 5px 15px;
            border-radius: 4px;
            cursor: pointer;
            transition: box-shadow 0.15s ease-in-out;
            &:hover {
                box-shadow: 0 2px 4px 1px rgba(0,0,0,0.1),
                            0 4px 8px 1px rgba(0,0,0,0.1);
            }
            &:active {
                transform: translateY(1px);
                box-shadow: 0 1px 2px 1px rgba(0,0,0,0.1),
                            0 2px 4px 1px rgba(0,0,0,0.1);
            }
        }
    }
</style>
