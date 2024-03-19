# code-for-web-bluetooth

**JAVA SCRIPT CODE FOR WEB BLUETOOTH**
<form>
  <button>Connect with BLE device</button>
</form>

<script>
  var deviceName = 'N-TESTER 0000'

  function isWebBluetoothEnabled() {
    if (!navigator.bluetooth) {
      console.log('Web Bluetooth API is not available in this browser!')
      return false
      }

    return true
  }
  function getDeviceInfo() {
    let options = {
      // acceptAllDevices: true // Option to accept all devices
      "filters": [
        { "name": deviceName }
      ]
    }

    console.log('Requesting Bluetooth Device...')
    navigator.bluetooth.requestDevice(options).then(device => {
      console.log('> Name: ' + device.name)
    }).catch(error => {
      console.log('Argh! ' + error)
    })
  }

  document.querySelector('form').addEventListener('submit', function(event) {
    event.stopPropagation()
    event.preventDefault()

    if (isWebBluetoothEnabled()) {
      getDeviceInfo()
    }
  })
</script>
