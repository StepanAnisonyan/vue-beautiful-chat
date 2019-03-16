<template>
  <div class="user-list">
    <!--<table class="" style="padding-top: 5px">-->
      <!--<tbody>-->
        <!--<tr v-for="user in participants" :key="user.id">-->
            <!--<td style="text-align: center;"><img :src="user.imageUrl" class="img-msg"/></td>-->
            <!--<td>{{user.name}}</td>-->
        <!--</tr>-->
      <!--</tbody>-->
  <!--</table>-->
      <v-list subheader>
          <v-subheader>В сети</v-subheader>
          <v-list-tile
                  v-for="item in participants"
                  :key="item.id"
                  v-if="item.active"
                  avatar
                  @click="userSend(item)"
          >
              <v-list-tile-action>
                  <v-icon :color="item.active ? 'teal' : 'grey'">chat_bubble</v-icon>
              </v-list-tile-action>

              <v-list-tile-content>
                  <v-badge rigth color="orange">
                     <span v-if="item.newMessNum != null" slot="badge">{{item.newMessNum}}</span>
                      <v-list-tile-title v-html="item.name"></v-list-tile-title>
                  </v-badge>
              </v-list-tile-content>

          </v-list-tile>
      </v-list>
      <v-divider></v-divider>
      <v-list subheader>
          <v-subheader>Не в сети</v-subheader>
          <v-list-tile
                  v-for="item in participants"
                  :key="item.id"
                  v-if="!item.active"
                  avatar
                  @click="userSend(item)"
          >
              <v-list-tile-action>
                  <v-icon :color="item.active ? 'teal' : 'grey'">chat_bubble</v-icon>
              </v-list-tile-action>

              <v-list-tile-content>
                  <v-badge rigth color="orange">
                      <span v-if="item.newMessNum != null" slot="badge">{{item.newMessNum}}</span>
                      <v-list-tile-title v-html="item.name"></v-list-tile-title>
                  </v-badge>
              </v-list-tile-content>

          </v-list-tile>
      </v-list>
  </div>
</template>
<script>
export default {
  props: {
    participants: {
      type: Array,
      required: true
    },
  },
    methods: {
        userSend(item) {
            this.inUserList = !this.inUserList
            this.$emit("userList", this.inUserList)
            Event.$emit("sendUser", item)
        },
    },
    data() {
        return {
            inUserList: false
        }
    },

}
</script>
<style scoped>
  .user-list {
    height: 100%;
    overflow: auto;
    padding-left: 5px;
    padding-top: 8px;
  }
  .img-msg {
    border-radius: 50%;
    width: 50px;
    margin-right: 5px;
  }
</style>
