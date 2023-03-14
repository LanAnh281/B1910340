<template>
    <Form
        @submit="submieContact"
        :validation-schema="contactFormSchema"
    >
    <div class="form-group">
        <label for="name">Tên</label>
        <Field
            name="name"
            type="text"
            class="form-control"
            v-model="contactLocal"
        >

        </Field>
        <ErrorMessge
            name="name" class="error-feedback"
        ></ErrorMessge>

        
    </div>
    <div class="form-group">
        <label for="email">E-mail</label>
        <Field
            name="email"
            type="email"
            class="form-control"
            v-model="contactLocal"
        >

        </Field>
        <ErrorMessge
            name="email" class="error-feedback"
        ></ErrorMessge>
    </div>
    <div class="form-group">
        <label for="address">Địa chỉ</label>
        <Field
            name="address"
            type="text"
            class="form-control"
            v-model="contactLocal"
        >

        </Field>
        <ErrorMessge
            name="address" class="error-feedback"
        ></ErrorMessge>
    </div>

    <div class="form-group">
        <label for="phone">Điện thoại</label>
        <Field
            name="phone"
            type="tel"
            class="form-control"
            v-model="contactLocal"
        >

        </Field>
        <ErrorMessge
            name="phone" class="error-feedback"
        ></ErrorMessge>
    </div>

    <div class="form-group form-check">
        <input type="checkbox" name="favorite" class="form-check-input" v-model="contactLocal">
        <label for="favorite" class="form-check-label">
            <strong>Liên hệ yêu thích</strong>
        </label>
    </div>
    
    </Form>
</template>
<script>
import * as yup from "yup";
import {Form,Field,ErrorMessage} from "vee-validate";
export default{
    components:{
        Form,
        Field,
        ErrorMessage,
    },
    emits:["submit:contact","delete:contact"],
    props:{
        contact:{
            type:Object,
            required:true
        }
    },
    data(){
        const contactFormSchema =yup.object().shape({
            name: yup
                .string()
                .required("Tên phải có giá trị")
                .min(2,"Tên phải ít nhất 2 ký tự")
                .max(50,"Tên có nhiều nhất 50 ký tự"),
            email: yup
                .string()
                .email("Email không đúng")
                .max(50,"Email có nhiều nhất 50 ký tự"),
            address:yup 
                .string()
                .max(100,"Địa chỉ  có tối đa 100 ký tự"),
            phone :yup 
                .string()
                .matches(
                    /((09|03|07|08|05|01)+([0-9]{8})\b)/g,
                    "số điện thoại không hợp lệ"
                ),
        });
        return {
            contactLocal:this.contact,
            contactFormSchema,
        };
    },
    methods:{
        submieContact(){
            this.$emit("submit:contact",this.contactLocal);
        },
        
    },
};
</script>