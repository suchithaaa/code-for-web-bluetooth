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


#include <bluefruit.h>

void setup() {
  Serial.begin(115200);
  delay(500);
  Serial.println("Start!");

  Bluefruit.begin();
  Bluefruit.setName("Palm");

  startAdv();
}

void loop() { }

void startAdv(void) {
  Bluefruit.Advertising.addFlags(BLE_GAP_ADV_FLAGS_LE_ONLY_GENERAL_DISC_MODE);
  Bluefruit.Advertising.addTxPower();
  Bluefruit.Advertising.addName();
  Bluefruit.Advertising.restartOnDisconnect(true);
  Bluefruit.Advertising.setInterval(32, 244);
  Bluefruit.Advertising.setFastTimeout(30);
  Bluefruit.Advertising.start(0);
}
