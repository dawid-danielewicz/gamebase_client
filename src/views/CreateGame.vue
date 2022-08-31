<template>
  <h1 class="page-header">Create game</h1>
  <form action="#" @submit.prevent="createGame()">
    <div class="form-section">
      <label>Name:</label>
      <input type="text" name="name" v-model="name">
      <p v-if="name_error" class="error">{{ name_error }}</p>
    </div>

    <div class="form-section">
      <label>Description:</label>
      <input type="text" name="name" v-model="description">
      <p v-if="description_error" class="error">{{ description_error }}</p>
    </div>

    <div class="form-section">
      <label>Age:</label>
      <input type="number" name="name" v-model="age">
      <p v-if="age_error" class="error">{{ age_error }}</p>
    </div>

    <div class="form-section">
      <label>Year:</label>
      <input type="number" name="name" v-model="year">
      <p v-if="year_error" class="error">{{ year_error }}</p>
    </div>

    <div class="form-section">
      <label>Category:</label>
      <select name="category" v-model="category_id">
        <option v-for="category in categories" :key="category.id" :value="category.id">{{ category.name }}</option>
      </select>
    </div>

    <input type="submit" class="btn" value="Create">
  </form>
</template>

<script>
import gql from 'graphql-tag';

export default {
  name: "CreateGame",
  data() {
    return {
      name: '',
      description: '',
      age: null,
      year: null,
      category_id: 1,
      name_error: null,
      description_error: null,
      age_error: null,
      year_error: null
    };
  },
  apollo: {
    categories: gql`
        query {
            categories {
                id
                name
            }
        }
    `
  },
  methods: {
    createGame() {
     this.$apollo.mutate({
        mutation: gql`
            mutation createGameResolver($name: String! $description: String! $age: Int! $year: Int! $category_id: ID! $platform_id: ID!) {
                createGameResolver(name: $name, description: $description, age: $age, year: $year, category_id: $category_id, platform_id: $platform_id ) {
                    id
                    name
                }
            }
        `,
        variables: {
          name: this.name,
          description: this.description,
          age: this.age,
          year: this.year,
          category_id: this.category_id,
          platform_id: 1
        }
      }).then(data => {
        console.log(data)
        this.$router.push('/games')
     }).catch(error => {
       console.log(error.graphQLErrors[0].extensions.validation)
       if(error.graphQLErrors[0].extensions.validation.name)
        this.name_error = error.graphQLErrors[0].extensions.validation.name[0]
       if(error.graphQLErrors[0].extensions.validation.description)
        this.description_error = error.graphQLErrors[0].extensions.validation.description[0]
       if(error.graphQLErrors[0].extensions.validation.age !== undefined)
        this.age_error = error.graphQLErrors[0].extensions.validation.age[0]
       if(error.graphQLErrors[0].extensions.validation.year !== undefined)
       this.year_error = error.graphQLErrors[0].extensions.validation.year[0]
     })
    }
  }
}
</script>

<style scoped>
.page-header {
  margin: 50px 0;
}

.form-section {
  width: 80%;
  margin: 20px auto;
  text-align: start;
}

.form-section label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

.form-section input {
  width: 100%;
  background-color: #474787;
  height: 30px;
  border-radius: 6px;
  border: #2c2c54 2px solid;
  color: #fff;
}

.form-section select {
  width: 100%;
  background-color: #474787;
  height: 40px;
  border-radius: 6px;
  border: #2c2c54 2px solid;
  color: #fff;
}

.form-section input:focus {
  outline: none;
  border-color: #B33771;
}

.form-section select:focus {
  outline: none;
  border-color: #B33771;
}

form {
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}

.btn {
  background-color: #B33771;
  color: #fff;
  padding: 15px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
}

.btn:hover {
  background-color: #6D214F;
}

.error {
  color: #B33771;
  font-weight: bold;
  margin: 10px 0;
}
</style>