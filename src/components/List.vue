<script lang="ts">
interface User {
  id: number;
  name: string;
  username: string;
  email: string;
  phone: string;
  website: string;
}

export default {
  data(): { users: User[] } {
    return {
      users: []
    }
  },
  methods: {
    async getUsers(): Promise<void> {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await response.json()
        this.users = data
      } catch (error) {
        console.log(error)
      }
    }
  },
  created() {
    this.getUsers()
  }
}
</script>


<template>
  <div class="container">
    <ul class="grid">
      <li v-for="user in users" :key="user.id" class="card">
        <div class="image">
          <img :src="`https://robohash.org/${user.id}?set=set4`" :alt="user.name" height=150 width="150" />
        </div>
        <h2>{{ user.name }}</h2>
        <p>{{ user.email }}</p>
        <p>{{ user.username }}</p>
        <p>{{ user.website }}</p>
      </li>
    </ul>
  </div>
</template>


<style scoped>
.container {
  margin: 0 auto;
  width: min(90%, 1000px);
}
.grid {
  display: grid;
  grid-template-columns: repeat(1, 300px);
  justify-content:center;
  justify-items: center;
  gap: 2rem;
}

@media screen and (min-width: 600px) {
  .grid {
    grid-template-columns: repeat(2, 300px);
  }
}

@media screen and (min-width: 900px) {
  .grid {
    grid-template-columns: repeat(3, 300px);
  }
}


.image {
  width: 100%;
  /* write me margin bottom 1rem and left and right auto */
  margin: 0 auto 1rem auto;
}

.image img {
  margin: 0 auto;
}
.card {
  width: 100%;
  padding: 1rem;
  background: gray;
}

h2, p {
  text-align: center;
}
</style>