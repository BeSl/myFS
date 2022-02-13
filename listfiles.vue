<template>
 <div>
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>

  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Название
          </th>
          <th class="text-left">
            Описание
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in desserts"
          :key="item.title"
        >
          <td>{{ item.name }}</td>
          <td>{{ item.fullpath }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  </div>
  <button @click="$fetch">Refresh</button>
  </div>
</template>

<script>
  export default {
    name: 'listfilesPage',
    data() {
      return {
        desserts: []
      }
    },
    async fetch() {
      this.desserts = await fetch('http://192.168.1.115/adminSite/hs/fileSys').then(res =>
        res.json()
      )
    },
  fetchOnServer: true,
  // multiple components can return the same `fetchKey` and Nuxt will track them both separately
  fetchKey: 'site-sidebar',
  // alternatively, for more control, a function can be passed with access to the component instance
  // It will be called in `created` and must not depend on fetched data
  fetchKey(getCounter) {
    // getCounter is a method that can be called to get the next number in a sequence
    // as part of generating a unique fetchKey.
    return this.someOtherData + getCounter('sidebar')
  }    
  }
</script>


