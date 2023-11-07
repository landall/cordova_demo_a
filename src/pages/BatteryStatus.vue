// some Vue file
// remember this is simply an example;
// only look at how we use the API described in the plugin's page;
// the rest of things here are of no importance

<template>
  <div>
    Battery status is: <strong>{{ batteryStatus }}</strong>
  </div>
</template>

<script>
import { ref, onBeforeUnmount } from 'vue'

export default {
  setup () {
    const batteryStatus = ref('determining...')

    function updateBatteryStatus (status) {
      batteryStatus.value = `Level: ${status.level}, plugged: ${status.isPlugged}`
    }

    // we register the event like on plugin's doc page
    window.addEventListener('batterystatus', updateBatteryStatus, false)

    onBeforeUnmount(() => {
      // we do some cleanup;
      // we need to remove the event listener
      window.removeEventListener('batterystatus', updateBatteryStatus, false)
    })

    return {
      batteryStatus
    }
  }
}
</script>
