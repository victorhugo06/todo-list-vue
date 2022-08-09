<template>
    <div class="pag">
        <div class="titulo">
            <h2>{{ title }}</h2>
        </div>

       <div class="row campos">
            <div class="col-8">
                <form class="form form-inline">
                    <input type="text" class="form-control" placeholder="Filtro nome" v-model="filter" style="border-radius: 2rem;">
                </form>
            </div>
            <div class="col">
                <form class="form form-inline" v-on:submit.prevent="onSubmit">
                    <input type="text" placeholder="Nova tarefa" class="form-control" v-model="task.name" style="border-radius: 2rem;">
                    <button type="submit" class="btn btn-primary" style="border-radius: 2rem;">Enviar</button>
                </form>
            </div>
       </div>

        <table class="table table-dark">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>NOME</th>
                    <th width="280px">Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task,index) in filteredItems" :key="index">
                    <td>{{ task.id }}</td>
                    <td>{{ task.name }}</td>
                    <td>
                        <a href="#" @click.prevent="edit(task.id)" class="btn btn-info" style="border-radius: 2rem;">Editar</a>
                        <a href="#" @click.prevent="deleteTask(task.id)" class="btn btn-danger" style="border-radius: 2rem;">Deletar</a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                title: 'Lista de Tarefas',
                tasks: [],
                task: {
                    id: '',
                    name: ''
                },
                updating: false,
                updateIndex: '',
                filter: ''
            }
        },
        methods: {
            onSubmit () {
                if ( this.updating ){
                    this.update()

                    return
                }
                this.save()
            },
            save () {
                this.task.id = this.tasks.length + 1
                this.tasks.push(this.task)

               this.clearForm ()
            },
            edit (id) {
                this.updateIndex = this.findIndexItem(id)
                
                this.task = this.tasks[this.updateIndex]

                this.updating = true
            },
            update () {
                this.tasks[this.updateIndex] = this.task

                this.updating = false

                this.clearForm ()
            },
            clearForm () {
                this.task = {
                    id: '',
                    name: ''
                }
            },
            deleteTask (id) {
                let index = this.findIndexItem(id)
                this.tasks.splice(index, 1)
            },
            findIndexItem (id) {
                for (let index = 0; index < this.tasks.length - 1; index++) {
                    if(this.tasks[index].id == id)
                        return index
                }
            }
        },
        computed: {
            filteredItems () {
                if (this.filter === '') 
                    return this.tasks

                let vm = this
                return this.tasks.filter(task => {
                    return task.name.toLowerCase().indexOf(vm.filter.toLowerCase()) > -1
                })
                
                /* return this.tasks.filter(task => {
                    return task.name.indexOf(vm.filter) > -1
                }) */

                /*  return this.tasks.filter(task => {
                    return task['name'].includes(vm.filter)
                }) */
            }
        }
    }
</script>

<style scoped>

form {
    margin: 20px 0;
    border-radius: 10px;
}
.table {
    border-radius: 2rem;
}
.pag {
    border-radius: 10px;
    text-align: center;
}

.campos{
    border-radius: 2rem;
    height: 5rem;
    margin: 10px 0;
}

.titulo {
    background-color: black;
    border-radius: 2rem;
    margin: 10px 0;
    color: white;
}
</style>