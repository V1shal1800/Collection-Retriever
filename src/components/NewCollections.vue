<template>
    <header>
        <div :key="collection.id" v-for="collection in newCollections">
            <NewCollection
                :collection="collection"
            />
        </div>
    </header>
</template>

<script>
import NewCollection from './NewCollection'
export default {
  name: 'NewCollections',
  props: {
    newCollections: Array,
  },
  components: {
    NewCollection,
  },
}
</script>