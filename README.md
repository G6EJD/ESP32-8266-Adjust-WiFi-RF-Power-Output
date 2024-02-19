# ESP32-8266-Adjust-WiFi-RF-Power-Output
How to adjust the ESP32 or 8266 Wi-Fi RF power output

Adjust the WiFi RF power output on the ESP32:

    Lowest RF power output
    WiFi.setTxPower(WIFI_POWER_MINUS_1dBm); // Set WiFi RF power output to lowest level

    Highest RF power output
    WiFi.setTxPower(WIFI_POWER_19_5dBm);    // Set WiFi RF power output to highest level

*Use one of the following parameters to change the power output:

 *  Available ESP32 RF power parameters:
    WIFI_POWER_19_5dBm    // 19.5dBm (19.5dBm output, highest supply current ~150mA)
    WIFI_POWER_19dBm      // 19dBm
    WIFI_POWER_18_5dBm    // 18.5dBm
    WIFI_POWER_17dBm      // 17dBm
    WIFI_POWER_15dBm      // 15dBm
    WIFI_POWER_13dBm      // 13dBm
    WIFI_POWER_11dBm      // 11dBm
    WIFI_POWER_8_5dBm     //  8dBm
    WIFI_POWER_7dBm       //  7dBm
    WIFI_POWER_5dBm       //  5dBm
    WIFI_POWER_2dBm       //  2dBm
    WIFI_POWER_MINUS_1dBm // -1dBm (For -1dBm output, lowest supply current ~120mA)

Adjust the WiFi RF power output on the ESP32:

Available ESP8266 RF power parameters:
    Lowest RF power output
    WiFi.setOutputPower(0); // Sets WiFi RF power output to lowest level, lowest RF power usage

    Highest RF power output
    WiFi.setOutputPower(20.5);    // Sets WiFi RF power output to highest level, highest RF power usage

*Adjust the parameter value in 0.5dBm increments to suit your needs:

    0    (for lowest RF power output, supply current ~ 70mA
    20.5 (for highest RF power output, supply current ~ 80mA

Example:
```c
void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_AP_STA);
  // Now get the ESP to create a test network so you can see the difference in RF power / signal strength
  WiFi.softAP("TestNetwork", "password"); // Monitor the WiFi signal strength of the ESP generated Network called 'TestNetwork'
  WiFi.begin("yourSSID", "yourPASSWORD");
  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(100);
  }
  Serial.println("\nWiFi connected at: " + WiFi.localIP().toString());
  
  #ifdef ESP32
    WiFi.setTxPower(WIFI_POWER_MINUS_1dBm); // Sets WiFi RF power output to lowest level, lowest RF power usage
    delay(60000);
    Serial.println("Now switching to HIGH power mode");
    WiFi.setTxPower(WIFI_POWER_19_5dBm);    // Sets WiFi RF power output to highest level, highest RF power usage
  #else
    WiFi.setOutputPower(0); // Sets WiFi RF power output to lowest level, lowest RF power usage
    delay(60000);
    Serial.println("Now switching to HIGH power mode");
    WiFi.setOutputPower(20.5);    // Sets WiFi RF power output to highest level, highest RF power usage
  #endif  
}
```
