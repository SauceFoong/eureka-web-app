<template>
  <div class='tag-input'>
    <div v-for='(tag, index) in tags' :key='tag' class='tag-input__tag mar__t--1 text--white'>
      <span @click="removeTag(index)" class="cursor__pointer">x</span>
      {{ tag }}
    </div>
    <input type='text' placeholder="Enter a Tag" class='tag-input__text' @keydown="addTag" @keydown.delete="removeLastTag"/>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  props: {
      limit : {
          type: Number,
          default: 10 // default limit is 10 tags
      }
  },
  data() {
    return {
      tags: ['HTML', 'CSS'] as Array<string>
    }
  },
  methods: {
      addTag(event:any) {        
        if(event.code == 'Comma' || event.code == 'Enter'){
            event.preventDefault();
            var val = event.target.value.trim()
            if(this.tags.length < this.limit && val.length > 0 && ! this.tags.includes(val.toUpperCase())){
                this.tags.push(val.toUpperCase())
                event.target.value = ''
            }
        }

      },
      removeTag(index:number) {
          this.tags.splice(index,1)
      },
      removeLastTag(event:any){
          if(event.target.value.length === 0) {
              this.removeTag(this.tags.length - 1)
          }
      }

  }
})
</script>

<style lang="scss" scoped>
.tag-input {
    width: $tag-input-width;
    border: $tag-input-border-radius solid $color-bg-hover;
    height: $tag-input-height;
    box-sizing: border-box;
    padding: $tag-input-padding;
    display:table;
    &__tag {
        height: $tag-input-tag-height;
        float: left;
        margin-right: $tag-input-tag-margin-right;
        background-color: $color-brand;
        line-height: $tag-input-tag-line-height;
        padding: $tag-input-tag-padding;
        border-radius: $app-border-radius-sm;
        & > span {
            opacity: $tag-input-tag-span-opacity;
        }
    }
    &__text {
        border: none;
        outline: none;
        line-height: $tag-input-text-line-height;
        background: none;
    }
}
</style>