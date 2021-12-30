<template>
    <div class="row justify-content-center m-3">
        <div class="card col-12 col-lg-3">
            <img :src="img">
        </div>
        <ul class="list-group col-12 col-lg-3">
            <li class="list-group-item d-flex justify-content-between align-items-center"  v-for="abilitie in abilities" :key="abilitie.stat.name">
                {{abilitie.stat.name}}
                <span class="badge bg-primary rounded-pill">{{abilitie.base_stat}}</span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Response",
    props:{
        abilities: {
            type: Array,
            default: () => []
        },
        img: {
            type: String,
            default: ""
        }
    },
}

</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>