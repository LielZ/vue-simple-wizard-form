<template>


    <div class="buttons">
        <div v-for="(item, id) in items" :key="id" class="d-inline-block col-6">
            <button v-on:click="update(item); $event.target.classList.toggle('active'); updateEmits();"
                    class="styled-button" :disabled="buttonDisable">
                <i :class="'bi bi-'+ item.icon "></i>
                {{item.title}}
            </button>
        </div>

        <div class="d-inline-block col-6">
            <button v-on:click="$event.target.classList.toggle('active'); disableButtons();" class="styled-button">
                <i class="bi bi-dash-circle"></i>
                אין לי
            </button>
        </div>
    </div>


</template>

<script>
    export default {
        name: "step2",
        emits: [
            'update:values'
        ],
        data() {
            return {
                buttonDisable: 0,
                items: [
                    {
                        id: 1,
                        icon: 'currency-exchange',
                        title: 'חסכון בשקלים'
                    },
                    {
                        id: 2,
                        icon: 'currency-dollar',
                        title: 'חסכון בדולר'
                    },
                    {
                        id: 3,
                        icon: 'currency-pound',
                        title: 'חסכון בפאונד'
                    },
                    {
                        id: 4,
                        icon: 'currency-yen',
                        title: 'חסכון ביין'
                    },
                    {
                        id: 5,
                        icon: 'currency-bitcoin',
                        title: 'חסכון בביטקוין'
                    },
                ],
                isClicked: []
            }
        },
        methods: {
            update(item) {
                var valObj = this.isClicked.filter(function (elem) {
                    if (elem.id == item.id) return elem.id;
                });

                if (valObj.length > 0) {
                    for (var i = this.isClicked.length - 1; i >= 0; --i) {
                        if (this.isClicked[i].id == item.id) {
                            this.isClicked.splice(i, 1);
                        }
                    }
                } else {
                    this.isClicked.push({id: item.id, title: item.title})
                }
                console.log(this.isClicked)
            },
            updateEmits() {
                this.$emit('update:values', this.isClicked)
            },
            disableButtons() {
                if (this.buttonDisable === 0) {
                    this.buttonDisable = +1;
                    this.isClicked.push({id: 99, title: 'אין לי'});
                    this.$emit('update:values', this.isClicked);
                } else {
                    this.$emit('update:values', this.isClicked);
                    for (var i = this.isClicked.length - 1; i >= 0; --i) {
                        if (this.isClicked[i].id == 99) {
                            this.isClicked.splice(i, 1);
                        }
                    }
                    this.buttonDisable = 0
                }
            }
        },
    }
</script>

<style scoped>
    @import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.7.2/font/bootstrap-icons.css");

    i {
        z-index: -1;
        font-size: 4rem;
        display: block;
        position: relative;
    }

    .styled-button {
        height: 130px;
        margin: 5px;
        width: 80%;
        background: #ffffff00;
        border: 2px #000 solid;
        border-radius: 5px;
    }

    .active.styled-button {
        color: #7878dc;
        border: 2px #7878dc solid;
    }

    button:disabled,
    button[disabled] {
        color: #696969 !important;
        border: 2px #696969 solid !important;
    }
</style>
