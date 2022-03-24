<template>
  <div class="form-area">
    <div class="mb-3">
      <label for="title" class="form-label"
        >Title</label
      >
      <input
        type="text"
        class="form-control"
        id="title"
        v-model="userData.title"
        placeholder="Title metni..."
      />
    </div>
    <div class="mb-3">
      <label for="url" class="form-label"
        >URL</label
      >
      <input
        type="text"
        class="form-control"
        id="url"
        v-model="userData.url"
        placeholder="https://www.example.com"
      />
    </div>
        <div class="mb-3">
      <label for="description" class="form-label"
        >Açıklama</label
      >
      <textarea
        type="text"
        class="form-control"
        id="description"
        v-model="userData.description"
        placeholder="Açıklama..."
      ></textarea>
    </div>
    <button class="btn btn-sm btn-primary me-2" @click="onSave">KAYDET</button>
    <button class="btn btn-sm btn-danger" @click=" $router.push({name: 'HomePage'})">İPTAL</button>
  </div>
</template>


<script>
export default {
    data(){
        return{
            userData:{
                title:null,
                url:null,
                description:null
            }
        }
    },
    methods:{
        onSave(){
            console.log(this.userData)
            this.$appAxios.post("/bookmarks", this.userData).then(response => {
                console.log(response);
                this.resetData();
                this.$router.push({name:"HomePage"})
            })
        },
        resetData(){
            Object.keys(this.userData).forEach(key => (this.userData[key] = null));
        }
    }
}
</script>