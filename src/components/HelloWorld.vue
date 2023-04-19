<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title class="headline">
            URL Opener
          </v-card-title>
          <v-card-text>
            <v-form>
              <v-textarea
                label="請貼上您要開啟的網址："
                v-model="urls"
              ></v-textarea>
              <v-btn color="primary" class="mr-3" @click="openUrls()">
                開啟網址
              </v-btn>
              <v-btn class="mr-3" @click="closeWindows()">
                關閉所有視窗
              </v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const urls = ref("");
let windows = [];

const openUrls = () => {
  const urlList = urls.value
    .replace(/\n/g, " ")
    .split(" ")
    .filter((url) => url.trim() !== "");

  urlList.forEach((url) => {
    const newWindow = window.open(url, "_blank");

    if (newWindow) {
      windows.push(newWindow);
    }
  });
};

const closeWindows = () => {
  windows.forEach((window) => window.close());
};
</script>