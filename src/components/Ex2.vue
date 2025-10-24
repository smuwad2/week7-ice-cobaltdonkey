<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                newItem: ""
            }
            
        },
        methods: {
            addItem() {
                if (this.newItem.trim() != "") {
                    this.items.push(this.newItem.trim());
                    this.newItem = "";
                }
            },
            removeItem(idx) {
                this.items.splice(idx,1);
            }
        }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
     <ul>
        <li v-for="(item, idx) in items" :key="idx">
            {{ item }}
            <button @click="removeItem(idx)">Delete!</button>
        </li>
     </ul>
     <input type="text" v-model="newItem">
     <button @click="addItem">Add!</button>
</template>
