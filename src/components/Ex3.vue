<script>
import axios from 'axios';

    export default { 

       // add code here
       data() {
            return {
                subject: "",
                entry: "",
                moods: ['Happy', 'Sad', 'Angry'],
                selectedMood: "",
                outputMsg: ""
            }
       },
       computed:{
        baseUrl() {
            if (window.location.hostname == 'localhost') {
                return 'https://localhost:3000/is216/blog'
            } else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return 'https://localhost/is216/blog';
            }
        }
       },
       methods: {
            addPost() {
                axios.get(`${this.baseUrl}/addPost`, {
                    params: {
                        subject: this.subject,
                        entry: this.entry,
                        mood: this.selectedMood
                    }
                })
                .then(response => {
                    this.outputMsg = response.data.message;
                    this.subject = "";
                    this.entry = "".
                    this.selectedMood = "";
                })
                .catch(error => {
                    console.error('Error adding post:', error);
                })
            }
    }
}
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <!-- TODO: Build a dropdown list here for selecting the mood -->
        <select v-model="selectedMood">
            <option v-for="mood in moods">
                {{ mood }}
            </option>
        </select>
        <br>

        <br>
        <p v-if="outputMsg">{{ outputMsg }}</p>
        <button @click="addPost">Submit New Post</button>
        
        <hr> Click  <a><router-link to="/ViewPosts/">here</router-link></a>  to return to Main Page
       
    </div>
</template>

