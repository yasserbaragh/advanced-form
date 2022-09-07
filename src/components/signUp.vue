<template>
    <form @submit.prevent="submitt">
        <p class="login">Do You Have An Account ? 
            <a href="">Log In</a></p>
            <h3>Personal Inforamtions</h3>
            <div class="name">
                <section class="personal">
                    <input type="text" required v-model="firstName">
                    <label>First Name</label>
                </section>
                <section class="personal">
                    <input type="text" required v-model="lastName">
                    <label>Last Name</label>
                </section>
            </div>
            <section class="personal">
                <input type="email" required ref="email"
                v-model="email" @keydown="validateEmail">
                <label>Email</label>
            </section>
            <div class="error">{{errors.email}}</div>
            
            <section class="personal">
                <input type="number" v-model="number">
                <label>Phone Number</label>
            </section>
            

            <section class="personal">
                <input type="password" required 
                v-model="password" class="input"
                ref="password" @keyup="passCH">
                <label class="label">Password</label>
            </section>
            <div class="error">{{passErr}}</div>
            <section class="personal">
                <input type="password" required v-model="passwordConfirm">
                <label>Repeat Password</label>
            </section>
            <div class="error">{{secpassErr}}</div>

            

            <h3>Work Inforamtions</h3>

            <label class="role">Role</label>
            <br>
            <select class="select">
                <option value="webDevelper">Web Develper</option>
                <option value="appDeveloper">App Developer</option>
                <option value="gameDeveloper">Game Developer</option>
                <option value="aiDeveloper">AI Develper</option>
            </select>
            
            <section class="personal">
                <input type="text" v-model="tempSkill" @keyup.space="addSkill">
                <label>Skills</label>
            </section>
            
            <span class="skills">Skills : <p v-for="skill in skills" 
                :key="skil">{{skill}}
                <fa icon="fa-solid fa-xmark" @click="deleteSkill(skill)"/></p></span>
            <br>
            <input type="checkbox" required v-model="terms">
            <label class="terms">Terms and Conditions</label>

            <div class="submit">
                <button>Sign Up</button>
            </div>
        </form>
</template>

<script>
export default {
    data() {
        return {
            firstName: "",
            lastName: "",
            email: "",
            number: "",
            password: "",
            passwordConfirm: "",
            tempSkill: "",
            skills: [],
            role: "",
            terms: false,
            passErr: "",
            secpassErr:"",
            errors: {
                    email: ""
            }
            
        }
    },
    methods: {
        addSkill(e) {
            if(this.tempSkill && this.tempSkill !== " ") {
                if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ""
            }
            
        },
        deleteSkill (skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },  
        validateEmail() {
            let validEmail = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/
            if(this.email.match(validEmail)) {
                this.errors.email = ""
            } else {
                this.errors.email = "Invalid Email"
            }

            if(this.errors.email) {
                this.$refs.email.classList.add("err")
                this.$refs.email.classList.remove("good")
            } else {
                this.$refs.email.classList.add("good")
                this.$refs.email.classList.remove("err")
            }
        },
        passCH() {
            const spcialChars = /[`!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?~]/;

            if(this.password.length < 8 ) {
                this.passErr = "Password must contains 8 letters at least"
            } else if(!(/\d/.test(this.password))) {
                this.passErr = "Password must contains at least 1 number"
            }else if(!spcialChars.test(this.password)) {
                this.passErr = "Password must contains special characters"
            }else if(this.password[0].toUpperCase() !== this.password[0]) {
                this.passErr = "Password must begins with capital letter"
            }else {
                this.passErr = ""
                
            }


            if(this.passErr) {
                this.$refs.password.classList.add("err")
                this.$refs.password.classList.remove("good")
            } else {
                this.$refs.password.classList.add("good")
                this.$refs.password.classList.remove("err")
            }
        },
        submitt() {

            this.secpassErr = this.passwordConfirm === this.password ?
            "" : "It doesn't match password"

            if(!this.passErr && !this.secpassErr && !this.errors.email) {
                console.log(this.email + this.password)
            }
        }
    }
}

</script>

<style lang="scss">
    
    form {
        margin: auto;
        text-align: left;
    }
    .login {
        margin-top: 50px;
        color: black;
        a {
            text-decoration: none;
            color: #4178BF;
        }

    }
    h3 {
        color: #8C615D;
        text-transform: uppercase;
        margin: 50px 0;
        text-align: center;
    }
    .name {
        display: flex;
        
        input {
            margin-right: 15px;
            margin-top: 10px;
            margin-bottom: 10px;
            width: 252px;
        }
    }
    
    input {
        font-size: 1.5rem;
        margin: 20px 0;
        border-radius: 20px;
        padding: 10px 20px;
        position: relative;
        border: 1px solid #4178BF;
        width: 522px;
    }
    .personal {
        position: relative;
        
        label {
        position: absolute;
        top: 33px;
        left: 39;
        z-index: 1;
        font-size: 1.4rem;
        transition: all ease;
        transition-duration: 0.5s;
        color: #4178BF;
        font-weight: bold;
        }
    }
    .name{
        .personal {
            label {
                top: 24px;
                left: 30px;
            }
        }
    }

    .personal {
        input:focus ~ label, 
        input:not(:placeholder-shown)
        ~ label {
            top: 13px;
            font-size: 0.8rem;
            left: 39px;
            background-color: white;
            padding: 0 10px;
        }
    }
    
    .name{
        .personal {
            input:focus ~ label, 
        input:not(:placeholder-shown)
        ~ label {
            top: 1px;
            left: 30px;
        }
        }
    }
    .skills {
        p{
            display: inline-block;
            padding: 5px 15px;
            background-color: grey;
            border-radius: 10px;
            margin: 5px;

            div {
                height: 5px;
                width: 5px;
                background: black;
            }
        }
    }
    .err {
        border-color: red;
    }

    .err:focus {
            outline-color: red;
            border-color: red;
    }

    .good {
        border-color: green;
    }

    .good:focus {
            outline-color: green;
            border-color: green;
    }

    .error {
        color: red;
    }

    .role {
        color: #4178BF;
        font-weight: bold;
        margin: auto;
    }
    .select {
        margin-top: 20px;
        padding: 10px;
        background-color: #7EAED9;
        border: none;
        color: white;
        margin: auto;
        margin-top: 20px;
        margin-bottom: 20px;
    }
    
    input[type="checkbox"] {
        width: 30px;
        margin: 30px 0;
    }

    .terms {
        font-size: 1.1rem;
    }

    .submit {
        display: flex;
        justify-content: center;
    }
    button {
        margin: 20px;
        padding: 10px 20px;
        background-color:#8C615D;
        border: none;
        color:white;
        font-weight: bold;
        font-size: 1.1rem;
        border-radius: 10px;
        cursor: pointer;
        transition: all 2ms ease;

        &:hover {
            background-color: white;
            color:#8C615D;

        }
    }

// responsive 

@media(max-width: 991px) {
    form {
        margin: auto;
        text-align: center;
    }
}

@media(max-width: 767px) {
    .name {
        input {
            margin-right: 5px;
            margin-top: 10px;
            margin-bottom: 10px;
            width: 147px;
        }
    }
    
    input {
        font-size: 1.5rem;
        margin: 20px 0;
        border-radius: 20px;
        padding: 10px 20px;
        position: relative;
        border: 1px solid #4178BF;
        width: 300px;
    }
}
</style>