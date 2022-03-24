<template>
<div>
    <button class="btn btn-sm btn-primary" @click="$router.push({name : 'NewBookmark'})">Ekle</button>
<table class="table table-striped table-hover">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Başlık</th>
      <th scope="col">URL</th>
      <th scope="col" style="width:50px">Sil</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="bookmark in bookmarkList" :key="bookmark.id">
      <th scope="row">{{bookmark.id}}</th>
      <td>{{bookmark.title}}</td>
      <td>{{bookmark.url}}</td>
      <td><button @click="deleteBookmark(bookmark)" class="btn btn-sm btn-danger">Sil</button></td>
    </tr>
  </tbody>
</table>
</div>
</template>

<script>
export default {
  data(){
    return{
      bookmarkList:[]
    }
  },
  created(){
    this.$appAxios.get("/bookmarks").then(response => {
      this.bookmarkList= response.data || [];
    })
  },
  methods:{
    deleteBookmark(item){
      this.$appAxios.delete(`/bookmarks/${item.id}`).then(response => {
        if(response.status === 200){
            this.bookmarkList = this.bookmarkList.filter(x => x.id !== item.id);
        }
      })
    }
  }
}
</script>