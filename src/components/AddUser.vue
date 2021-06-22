<template>
    <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Name</label>
      <input type="text" v-model="name" name="name" placeholder="Name here" />
    </div>
    <div class="form-control">
      <label>Email</label>
      <input
        type="text"
        v-model="email"
        name="email"
        placeholder="Email"
      />
    </div>
    <div class="form-control form-control-check">
      <label>active</label>
      <input type="checkbox" v-model="active" name="active" />
    </div>

    <input type="submit" value="Save User" class="btn btn-block" />
  </form>
</template>

<script>


export default {
    name : 'Add User',
    data() {
        return{
          name : '',
          email: '',
          active: false  
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault();
            if(!this.name){
                alert('please add a User')
                return
            }
            const newUser = {
                id: Math.floor(Math.random() * 100000),
                name: this.name,
                email: this.email,
                active: this.active

                
            }
            this.$emit('add-User',newUser);
            this.name = ''
            this.email = ''
            this.active = false
        }

    }
    
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>