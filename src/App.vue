<template>
  <v-app>
    <v-main>
      <v-container>
        <v-btn
          dark
          color="green"
          @click="showDialog('Text')"
        >
          show Text dialog !
        </v-btn>
        <v-dialog
          max-width="500"
          v-model="roroTextDialog"
        >
          <roro-dialog
            header-title="텍스트"
            @hide="hideDialog('Text')"
            @submit="submitDialog('Text')"
          >
            <template v-slot:body>
              <v-text-field
                  placeholder="내용을 입력하세요"
              />
            </template>
          </roro-dialog>
        </v-dialog>
        <v-btn
          dark
          color="blue"
          class="mx-2"
          @click="showDialog('List')"
        >
          show List dialog !
        </v-btn>
        <v-dialog
          max-width="500"
          v-model="roroListDialog"
        >
          <roro-dialog
            header-title="좋아하는 음식"
            :footer-submit="false"
            @hide="hideDialog('List')"
            @submit="submitDialog('List')"
          >
            <template v-slot:body>
              <v-list>
                <v-list-item-group v-model="item" color="primary">
                  <v-list-item
                    v-for="(item, i) in items"
                    :key="i"
                  >
                    <v-list-item-content>
                      <v-list-item-title v-text="item.text" />
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </template>
          </roro-dialog>
        </v-dialog>
        <v-btn
          dark
          color="red"
          @click="showDialog('Image')"
        >
          show Image dialog !
        </v-btn>
        <v-dialog
          max-width="500"
          v-model="roroImageDialog"
        >
          <roro-dialog
            header-title="사진"
            footer-submit-title="선택"
            @hide="hideDialog('Image')"
            @submit="submitDialog('Image')"
          >
            <template v-slot:body>
              <v-row>
                <v-col
                  v-for="n in 9"
                  :key="n"
                  class="d-flex child-flex"
                  cols="4"
                >
                  <v-card flat tile class="d-flex">
                    <v-img
                      :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
                      :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
                      aspect-ratio="1"
                      class="grey lighten-2"
                    >
                      <template v-slot:placeholder>
                        <v-row
                          class="fill-height ma-0"
                          align="center"
                          justify="center"
                        >
                          <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                        </v-row>
                      </template>
                    </v-img>
                  </v-card>
                </v-col>
              </v-row>
            </template>
          </roro-dialog>
        </v-dialog>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import RoroDialog from './components/RoroDialog'

export default {
  name: 'App',
  components: {
    RoroDialog,
  },
  data: () => ({
    roroTextDialog: false,
    roroListDialog: false,
    roroImageDialog: false,
    item: 1,
      items: [
        { text: '피자' },
        { text: '라떼' },
        { text: '짜글이' },
      ],
  }),
  methods: {
    showDialog(type) {
      this[`roro${type}Dialog`] = true
    },
    hideDialog(type) {
      this[`roro${type}Dialog`] = false
    },
    submitDialog(type) {
      console.log('submit 완료!')
      this.hideDialog(type)
    },
  }
}
</script>
