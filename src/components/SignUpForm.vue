<template>
    <form @submit.prevent="handleSubmit">
        <label>Email</label>
        <input type="email" required v-model="email"/>

        <label>password</label>
        <input type="password" required v-model="password"/>
        <!-- <button v-if="showPass" @click="togglePassword">Hide Pass </button> -->
        <input type="checkbox" @click="togglePassword"><label>Show password</label>
        <span v-if="showPass">  {{ password }} </span>
        <!-- <button  v-else @click="togglePassword">Show Pass </button> -->
        <div v-if="passwordError" class="error">{{ passwordError }} </div>

        <br>
        <label>Role :</label>
        <select v-model="role">
            <option value="Develop">Web Developer</option>
            <option value="Design">Web Designer</option>
        </select>

        

        <div>
            <label> Skills :</label>
            <input type="text" v-model="tempSkill" @keyup="addSkill">
            
        </div>

        <div>
            <input type="checkbox" value="HTML" v-model="skills">
            <label for="HTML">HTML</label>&nbsp;&nbsp;

            <input type="checkbox" value="CSS" v-model="skills">
            <label for="CSS">CSS</label>&nbsp;&nbsp;
        
            <input type="checkbox" value="JavaScript" v-model="skills">
            <label for="JS">JS</label>&nbsp;&nbsp;

            <input type="checkbox" value="React" v-model="skills">
            <label for="React">React</label>&nbsp;&nbsp;

            <input type="checkbox" value="VueJs" v-model="skills">
            <label for="VueJs">VueJs</label>&nbsp;&nbsp;
        </div>
        <div v-for="skill in skills" :key="skill" class="pill" >
                <div @click="removeSkill(skill)" >
                    {{ skill }}
                </div>
            </div>

        <div>
        <input type="checkbox" v-model="terms" required>
        <label>Accept Terms and Conditions</label>
        </div>

        <div class="submit">
            <button >Create Account</button>
        </div>
        
        
    </form>
    
    
</template>

<script>

export default{
    data(){
        return{
            email:'',
            password:'',
            passwordError:'',
            showPass:false,
            role:'Design',
            terms:false,
            tempSkill:'',
            skills:[]
        }
    },
    methods:{
        togglePassword(){
            this.showPass=!this.showPass  
        },
        addSkill(e){
            if (e.key===" " && this.tempSkill){
                if (!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill=""
            }
        },
        removeSkill(skill){
            this.skills=this.skills.filter((item)=>{
                return skill!==item
            })
            console.log(skill)
        },
        handleSubmit(){
            this.passwordError=this.password.length>5 ?
            "" : "Password must be atleast 6 char long"
            if (!this.passwordError){
                console.log('Email: ',this.email )
                console.log('Role: ',this.role )
                console.log('Terms Accepted: ',this.terms)
                console.log('Skills: ',this.skills )
            }
        }
    }

}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    border-radius: 5px;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
button{
    margin-top: 20px;
    padding: 10px 20px;
    background: #0b6dff;
    border: 0;
    color: white;
    border-radius: 10px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 10px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}

</style>