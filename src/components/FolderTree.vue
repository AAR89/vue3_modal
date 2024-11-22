<template>
  <ul>
    <li v-for="folder in folders" :key="folder.id">
      <div class="tree">
        <div>
          <span class="tree-span" @click="toggle(folder)"
            >{{ folder.name }}
            <span>
              <input
                v-if="!folder.children.length"
                type="radio"
                :name="folder.id"
                :value="folder.id"
                v-model="selectedFolderId"
              /> </span
          ></span>

          <ul v-if="folder.isOpen">
            <FolderTree :folders="folder.children" @select-folder="selectFolder" />
          </ul>
        </div>
      </div>
    </li>
  </ul>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue'

interface Folder {
  id: string
  name: string
  children: Folder[]
  isOpen?: boolean
}

defineProps<{
  folders: Folder[]
}>()

const emit = defineEmits<{
  (event: 'select-folder', folderId: string): void
}>()

const selectedFolderId = ref<string | null>(null)

function toggle(folder: Folder) {
  folder.isOpen = !folder.isOpen
}

function selectFolder(folderId: string) {
  emit('select-folder', folderId)
}
</script>

<style scoped>
.tree span {
  display: flex;
  align-items: center;
  gap: 10px;
}

.tree ul {
  display: flex;
  flex-direction: column;
  margin-left: 30px;
}

ul,
li {
  list-style-type: none !important;
  padding-left: 0 !important;
}

.folder-item {
  display: flex;
  align-items: center;
  margin: 5px 0;
}

.folder-content {
  display: flex;
  align-items: center;
  justify-content: center;
}

.folder-name {
  cursor: pointer;
  margin-right: 10px;
}

.folder-radio {
  margin-left: 10px;
}
</style>
