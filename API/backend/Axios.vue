<script>
import axios from "axios";

export default {
  data() {
    return {
      students: [],
    };
  },
  methods: {
    async fetchStudents() {
      try {
        const response = await axios.get("http://localhost:3000/students");

        // ✅ correction ici
        this.students = response.data;

      } catch (error) {
        console.error("Erreur Axios :", error);
      }
    },
  },
};
</script>