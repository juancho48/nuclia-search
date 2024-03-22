<script>
export default {
    onMounted() {
        window.selectedModel = this.selectedModel;
    },

    methods: {
        async getModels() {
            const response = await fetch('https://api.nuclia.cloud/api/v1/models');
            const data = await response.json();
            this.models = data.models;
        },
        changeModel(event) {
          window.selectedModel = this.selectedModel;
          document.querySelector("body > nuclia-search-bar").setAttribute("generativemodel", this.selectedModel);
          document.querySelector("body > nuclia-search-bar").setAttribute("apiKey", process.env['TOKEN']);
        }
    },
    data() {
        return {
            models: [
                {key: 1, name: "chatgpt-azure"},
                {key: 2, name: "chatgpt-azure-3"},
                {key: 3, name: "Claude-3"},
                {key: 4, name: "gemini-pro"},
            ],
            selectedModel: "chatgpt-azure-3"
        }
    }
}
</script>

<template>
  <div id="app">
    <h1>To use the search, please select an engine first</h1>
      <div style="padding: 20px">
          <select v-model="selectedModel" @change="changeModel($event)">
              // eslint-disable-next-line vue/require-v-for-key
              <option v-for="model in models" :value="model.name" v-bind="model.key">{{model.name}}</option>
          </select>
          <div style="padding: 20px">Selected model key: {{selectedModel}}</div>
      </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}
</style>
