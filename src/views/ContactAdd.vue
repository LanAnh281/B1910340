<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="createContact"
            
        >
        </ContactForm>
        <p>{{message}}</p>
    </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default{
    components:{
        ContactForm,
    },
    data(){
        return{
            contact:{
                name:"",
                address:"",
                phone:"",
                email:"",
                favorite:""
            },
            message:""
        };
    },
    methods:{
       
        async createContact(data){
            console.log(data);
            try {
                await ContactService.create(data);
                this.message="Liên hệ được thêm thành công";
                this.$router.push({name:"contactbook"});

            } catch (error) {
                console.log(error);
            }
        },
    },
    created(){
        this.message="";
    }

}
</script>