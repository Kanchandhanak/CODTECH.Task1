#include “DHT.h”
#define DHTTYPE DHT11 // or DHT22, depending on your sensor
#define DHTPIN 2

DHT dht(DHTPIN, DHTTYPE);
Const int relayLight = 7;
Const int relayFan = 8;
Const int relayThermostat = 9;
Const float tempThreshold = 25.0;

Void setup() {
  Dht.begin();
  pinMode(relayLight, OUTPUT);
  pinMode(relayFan, OUTPUT);
  pinMode(relayThermostat, OUTPUT);
  digitalWrite(relayLight, HIGH);
  digitalWrite(relayFan, HIGH);
  digitalWrite(relayThermostat, HIGH);
  Serial.begin(9600);
}

Void loop() {
  Float humidity = dht.readHumidity();
  Float temperature = dht.readTemperature();
  If (isnan(humidity) || isnan(temperature)) {
    Serial.println(“Failed to read from DHT sensor!”);
    Return;
  }
  Serial.print(“Humidity: “);
  Serial.print(humidity);
  Serial.print(“ %\t”);
  Serial.print(“Temperature: “);
  Serial.print(temperature);
  Serial.println(“ *C”);
  digitalWrite(relayLight, LOW);
  delay(5000);  
  digitalWrite(relayLight, HIGH);
  delay(2000); 
  digitalWrite(relayFan, LOW); 
  delay(5000); 
  digitalWrite(relayFan, HIGH);
  delay(2000); 
  If (temperature > tempThreshold) {
    digitalWrite(relayThermostat, LOW); 
  } 
else 
{
    digitalWrite(relayThermostat, HIGH);
  }
  Delay(2000);
}
