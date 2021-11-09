<script>
export default {
  computed: {
    todaysDay() {

      const local = new Date();
      local.setMinutes(local.getMinutes() - local.getTimezoneOffset());

      return local.toJSON().slice(0,10);
    }
  }
}
</script>