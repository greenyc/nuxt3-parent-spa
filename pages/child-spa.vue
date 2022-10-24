<template>
  <div>
    pages/child-spa.vue
  </div>
</template>

<script>
import {
  registerApplication,
  unregisterApplication,
  getAppNames,
} from "single-spa"

export default {
  name: "child-spa",
  async destroyed() {
    await unregisterApplication("child-spa")
  },
  created() {
    if (!getAppNames().includes("child-spa")) {
      registerApplication({
        name: "child-spa",
        app: async () => await import("ciarangreen_child-spa"),
        activeWhen: ["/child-spa"],
      })
    }
  },
}
</script>
