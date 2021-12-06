<template> 
    <div>
    <h3 style="text-align:center;">Contact View</h3>
    <table class="table">
    <thead><tr>
    <th style="width: 260px">Name</th>
    <th style="width: 80px">Id</th>
    <th>Phone</th>
    <th>Mobile</th>
    <th>Email</th>
    <th><button class="btn btn-outline-primary btn-sm " v-on:click="refresh()">
        <i class="fa fa-refresh"></i></button>
   </th>  
    </tr></thead>
    <tbody>
    <tr class="fbox" >
        <td><input type="text" class="input-sm tfield" style="width: 260px"  v-model="contact.name" /></td>
        <td><input type="text" class="input-sm tfield"  style="width: 220px" disabled /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.phone" /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.mobile" /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.email" /></td>
        <td><button class="btn btn-outline-primary btn-sm " v-on:click="add()">
        <i class="fa fa-plus"></i></button></td>
    </tr>
    <tr class="fbox" v-for="contact in contacts" :key="contact.id">
        <td><input type="text" class="input-sm tfield" style="width: 260px"  v-model="contact.name" /></td>
        <td><input type="text" class="input-sm tfield"  style="width: 220px" v-model="contact._id" /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.phone" /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.mobile" /></td>
        <td><input type="text" class="input-sm tfield"  v-model="contact.email" /></td>
        <td><button class="btn btn-outline-primary btn-sm " v-on:click="del(contact._id)">
        <i class="fa fa-minus"></i></button></td>
    </tr>
    </tbody></table>
</div>
</template>

<script>
import axios from 'axios'

export default {
name: 'contact', 
    data: function() {
        return { 
        contact: {},
        contacts: { results: [] },
        result: {}
        } 
    },

    created: function () {
    this.refresh()
    },

    methods: {
    refresh: function() {
        axios.get('/contacts').then(
        result => this.contacts = result.data,
            result => alert("Contact status "+result.status) 
            )
    },
    del: function(id) {
        axios.delete('/contacts/'+id).then(
        result => { this.result = result.data; this.refresh() },
            result => alert("Contact status "+result.status) 
            )
        },
    add: function() {
        axios.post('/contacts',this.contact).then(
        result => { this.result = result.data; this.refresh() },
            result => alert("Contact status "+result.status) 
            )
        },
    },
}
</script>
    