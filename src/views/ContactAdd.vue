<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="newContact" @submit:contact="addContact" />
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
      // Khởi tạo một đối tượng liên hệ rỗng để truyền xuống form
      newContact: {
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
    async addContact(data) {
      try {
        // Gọi API create để thêm mới thay vì update
        await ContactService.create(data);
        alert("Liên hệ được thêm mới thành công.");
        // Sau khi thêm thành công thì chuyển hướng về trang chủ Danh bạ
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
