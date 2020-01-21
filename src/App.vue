<template>
  <v-app>
    <v-app-bar app color="#80CBC4">
      <v-toolbar-title>itotepc-todolist</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-card class="col-md-10 ml-auto mr-auto">
          <v-card-text>
            <v-text-field
              clearable
              v-model="newText"
              label="เพิ่มสิ่งที่ต้องทำ"
              :append-outer-icon="newText ? 'mdi-send' : 'mdi-microphone'"
              :prepend-icon= "icon"
              :rules="[rules.required]"
              hint="กด shitf+delete เพื่อเคลียร์ข้อความ"
              @keyup.enter="addItem"
              @keyup.shift.delete="clrText"
              @click:prepend="changeIcon"
              @click:append-outer="sendMessage">
              
            </v-text-field>
          </v-card-text>

          <v-list>
            <v-list-item v-for="(item,index) in items" :key="index">
              <v-list-item-action>
                <v-icon>
                  mdi-file-settings-outline
                </v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title>{{ item }}</v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn text icon color="red" @click="delItem(index)">
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list>
        </v-card>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',


  data: () => ({
    //
    items: [],
    newText: '',
    iconIndex: 0,
    icons: [
      'mdi-emoticon',
      'mdi-emoticon-cool',
      'mdi-emoticon-dead',
      'mdi-emoticon-excited',
      'mdi-emoticon-happy',
      'mdi-emoticon-neutral',
      'mdi-emoticon-sad',
      'mdi-emoticon-tongue',
    ],
    rules: {
      required: value => !! value || 'กรุณากรอกข้อความ.',
    }
  }),

  computed: {
    icon() {
      return this.icons[this.iconIndex]
    },
  },

  methods: {
    addItem(){
      if(this.newText)
      {
        this.items.push(this.newText);
        this.newText = ''
      }
      this.resetIcon()
    },

    clrText(){
      this.newText = ''
      this.resetIcon()
    },

    delItem(index){
      this.items.splice(index, 1);
    },

    
    resetIcon () {
      this.iconIndex = 0
    },

    changeIcon () {
      this.iconIndex === this.icons.length - 1 ? this.iconIndex = 0 : this.iconIndex++
    },

    sendMessage () {
        this.addItem()
        this.resetIcon()
        this.clrText()
    },

  },
};
</script>
