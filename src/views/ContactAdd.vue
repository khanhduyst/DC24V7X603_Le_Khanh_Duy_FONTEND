<template>
    <div class="page">
        <h4>Thêm Liên hệ mới</h4>
        <ContactForm :contact="contact" @submit:contact="saveContact" />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async saveContact(data) {
            try {
                console.log("Dữ liệu chuẩn bị gửi đi:", data);
                await ContactService.create(data);
                this.message = "Liên hệ được thêm mới thành công.";

                setTimeout(() => {
                    this.$router.push({ name: "contactbook" });
                }, 1000);

            } catch (error) {
                console.log("Lỗi tại ContactAdd:", error);
                this.message = "Có lỗi xảy ra khi thêm liên hệ.";
            }
        }
    },
};
</script>