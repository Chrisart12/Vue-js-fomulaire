<template>
    <form @submit.prevent="handleSubmit">
        <label for="email">Email :</label>
        <input type="email" required v-model="email">
        <div>
            <label for="password">Password :</label>
            <input type="password" required v-model="password">
            <span class="error" v-if="passwordError">{{ passwordError  }} </span>
        </div>
        <div>
            <label for="role">Role :</label>
            <select v-model="role">
                <option value="developer">Web developer</option>
                <option value="designer">Web designer</option>
                <option value="fullstack">Web FullStack</option>
            </select>
        </div>
       

        <label for="">Skills</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
            <span @click="removeSkill(skill)">{{ skill }}</span>
            
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label for="">Accept terms and conditions</label>
        </div>

        <div>
            <input type="checkbox" value="mangue" v-model="names">
            <label for="">Mangue</label>
        </div>
        <div>
            <input type="checkbox" value="banane" v-model="names">
            <label for="">Banane</label>
        </div>
        <div>
            <input type="checkbox" value="ananas" v-model="names">
            <label for="">Ananas</label>
        </div>
        <div class="submit">
            <button>Create an form</button>

        </div>
    </form>

    <p>Email : {{ email }}</p>
    <p>Password : {{ password }}</p>
    <p>Role : {{ role }}</p>
    <p>Terms : {{ terms }}</p>
    <!-- <p>Choix : 
        <ul>
            <li v-for="name in names">
                    {{ name  }}
            </li>
        </ul>
    </p> -->
    <!-- <p>tempSkill : 
        <ul>
            <li v-for="skill in skills" :key="skill" class="pill">
                    {{ skill  }}
            </li>
        </ul>
    </p> -->


    
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'fullstack',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: ''
            // names: []
        }
    },
    methods: {
        addSkill(e) {
            if(e.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill.slice(0, -1))) {
                    this.skills.push(this.tempSkill.slice(0, -1))
                }
    
                this.tempSkill = ''
            }
        },

        removeSkill(skill) {
               this.skills = this.skills.filter((item) => {
                   return skill !== item
               })
        },

        handleSubmit() {
            // Validate password
            this.passwordError = this.password.length >= 6 ? '' : 'Le mot de passe ne doit pas être de moins de 6 caractères'
             console.log("cccccccccc", this.passwordError)
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: aliceblue;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
        }
        label {
            color: #aaa;
            display: inline-block;
            margin: 25px 0 15px;
            font-size: 0.6em;
            letter-spacing: 1px;
            font-weight: bold;
        }
        input, select {
            display: block;
            padding: 10px 6px;
            width: 100%;
            box-sizing: border-box;
            border: none;
            border-bottom: 1px solid #ddd;
            color: #555;
        }

        input[type="checkbox"] {
            display: inline-block;
            width: 16px;
            margin: 0 10px 0 0;
            position: relative;
            top: 2px;
        }
        .pill {
            display: inline-block;
            margin: 20px 10px 0 0;
            padding: 6px 12px;
            background: #eee;
            border-radius: 20px;
            letter-spacing: 1px;
            font-weight:  bold;
            color: #777;
            cursor: pointer;
        }

        button {
            background: #0b6dff;
            border: 0;
            padding: 10px 20px;
            margin-top: 20px;
            color: white;
            border-radius: 10px
        }

        .submit {
            text-align: center;
        }

        .error {
            color: red;
            font-size: 0.6em;
            margin-top: 1px;
        }
        
</style>