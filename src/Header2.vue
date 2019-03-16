<template>
    <div>
        <div class="sc-header" :style="{background: colors.header.bg, color: colors.header.text}">
            <img class="sc-header--img" :src="imageUrl" alt="" v-if="imageUrl" />
            <div class="sc-header--title" @click="toggleUserList"> {{title}}</div>

            <div class="sc-header--close-button" @click="onClose">
                <img src="./assets/close-icon.png" alt="" />
            </div>
        </div>
        <div>
            <v-list style="padding-top: 0">
                <v-list-tile style="box-shadow: 0 4px 2px -2px #cccccc;">

                    <v-list-tile-content>
                        <v-list-tile-title>{{ sendUserName }}</v-list-tile-title>
                        <v-list-tile-sub-title>{{ sendUserFullName }}</v-list-tile-sub-title>
                    </v-list-tile-content>

                </v-list-tile>
            </v-list>

        </div>
    </div>
</template>
<script>

    export default {
        props: {
            imageUrl: {
                type: String,
                required: true
            },
            title: {
                type: String
            },
            sendUserName: {
                type: String
            },
            sendUserFullName: {
                type: String
            },
            onClose: {
                type: Function,
                required: true
            },
            colors: {
                type: Object,
                required: true
            }
        },
        methods: {
            toggleUserList() {
                this.inUserList = !this.inUserList
                this.$emit("userList", this.inUserList)
                Event.$emit("clearMessage")
            }
        },
        data() {
            return {
                inUserList: false
            }
        }
    }
</script>
<style scoped>
    .sc-header {
        min-height: 75px;
        border-top-left-radius: 9px;
        border-top-right-radius: 9px;
        padding: 10px;
        box-shadow: 0 1px 4px rgba(0,0,0,.2);
        position: relative;
        box-sizing: border-box;
        display: flex;
    }

    .sc-header--img {
        border-radius: 50%;
        align-self: center;
        padding: 10px;
    }

    .sc-header--title {
        align-self: center;
        padding: 10px;
        flex: 1;
        user-select: none;
        cursor: pointer;
        border-radius: 5px;
    }

    .sc-header--title:hover {
        box-shadow: 0px 2px 5px rgba(0.2, 0.2, 0.5, .1);
    }

    .sc-header--close-button {
        width: 40px;
        align-self: center;
        height: 40px;
        margin-right: 10px;
        box-sizing: border-box;
        cursor: pointer;
        border-radius: 5px;
    }

    .sc-header--close-button:hover {
        box-shadow: 0px 2px 5px rgba(0.2, 0.2, 0.5, .1);
    }

    .sc-header--close-button img {
        width: 100%;
        height: 100%;
        padding: 13px;
        box-sizing: border-box;
    }

    @media (max-width: 450px) {
        .sc-header {
            border-radius: 0px;
        }
    }
</style>
