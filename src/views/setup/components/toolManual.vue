<template>
  <div class="toolsMetadata">
    <div class="field">
      <label class="label" :for="tool.id"
        >Tool: {{ tool.name }} Version: {{ tool.actual }}</label
      >
      <div class="field is-grouped align-center">
        <div class="control expanded">
          <input
            type="text"
            class="input is-small"
            v-model="tool.path"
            :id="tool.id"
            @change="setToolsAreInValid"
            @keydown="setToolsAreInValid"
          />
        </div>
        <div class="control">
          <div class="icon is-large is-size-4">
            <iconify-icon :icon="tool.doesToolExist ? 'check' : 'close'" />
          </div>
        </div>
      </div>
    </div>
    <div v-for="(item, key) in tool.env" :key="key">
      <div class="field">
        <label :for="key" class="label">Environment variable {{ key }}:</label>
        <div class="control expanded">
          <input
            type="text"
            class="input is-small env-input"
            v-model="tool.env[key]"
            :id="key"
            @change="setToolsAreInValid"
            @keydown="setToolsAreInValid"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { Mutation, State } from "vuex-class";
import { IEspIdfTool } from "../types";

@Component
export default class PreviousTool extends Vue {
  @Prop() tool: IEspIdfTool;
  @Mutation private setToolsAreValid;

  setToolsAreInValid() {
    this.tool.doesToolExist = false;
  }
}
</script>

<style scoped>
.toolsMetadata {
  width: 100%;
}
.env-input {
  margin-right: 5%;
}
</style>
