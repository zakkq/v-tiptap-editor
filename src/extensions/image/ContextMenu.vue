<template lang="pug">
  div.d-flex
    v-menu(
      bottom
      offset-y
      nudge-bottom="6"
      :content-class="editor.options.includedClass"
    )
      template(#activator="{ on, attrs }")
        v-btn(
          text
          tabindex="-1"
          height="auto"
          min-width="auto"
          v-bind="attrs"
          v-on="on"
        )
          v-icon(
            v-if="iconOptions"
            v-bind="iconOptions.props"
            v-on="iconOptions.on"
            small
          ) {{ iconOptions.content }}

      v-list
        v-list-item(
          v-for="(item, idx) in items"
          v-bind="item.props"
          v-on="item.on"
          :key="idx"
        )
          v-list-item-action.mr-6
            v-icon {{ item.icon }}
          v-list-item-content
            v-list-item-title {{ item.title }}
</template>

<script>
export default {
  props: {
    editor: {
      type: Object,
      required: true,
    },
    iconOptions: {
      type: Object,
      default: null,
    },
  },
  computed: {
    items() {
      const { urlLink, tray } = this.editor.options.iconPack;
      return [
        {
          icon: tray,
          title: 'Загрузить из компьютера',
          props: {
            link: true,
            disabled: true,
          },
        },
        {
          icon: urlLink,
          title: 'Загрузить по URL-ссылке',
          props: {
            link: true,
          },
          on: {
            click: () => this.$emit('click:add-link'),
          },
        },
      ];
    },
  },
};
</script>
