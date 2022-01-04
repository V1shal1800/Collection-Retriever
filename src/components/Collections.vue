<template>
    <header>
        <div :key="collection.id" v-for="collection in collections">
            <Collection
                :collection="collection"
            />
        </div>
    </header>
</template>

<script>
import Collection from './Collection'
export default {
  name: 'Collections',
  props: {
    collections: Array,
  },
  components: {
    Collection,
  },
}
</script>