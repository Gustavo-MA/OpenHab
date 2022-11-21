# OpenHab
Instalacion y Ejemplos (temp,...etc)


Instalacion

## Instalación de OpenHab

1. Comprobar la instalación de Java
- java --version
- En caso de no contar con Java
	sudo apt install default-jre
	
2. Instala OpenHab
- curl -fsSL "https://openhab.jfrog.io/artifactory/api/gpg/key/public" | gpg --dearmor > openhab.gpg
- sudo mkdir /usr/share/keyrings
- sudo mv openhab.gpg /usr/share/keyrings
- sudo chmod u=rw,g=r,o=r /usr/share/keyrings/openhab.gpg
- echo 'deb [signed-by=/usr/share/keyrings/openhab.gpg] https://openhab.jfrog.io/artifactory/openhab-linuxpkg stable main' | sudo tee /etc/apt/sources.list.d/openhab.list
- sudo apt-get update
- sudo apt-get install openhab

3. Configurar el Modo de Arranque de OpenHab
- Al inicio del sistema
	sudo /bin/systemctl daemon-reload
        sudo /bin/systemctl enable openhab.service
        
- Modo Manual
	sudo /bin/systemctl daemon-reload
            sudo /bin/systemctl enable openhab.service
![image](https://user-images.githubusercontent.com/111370930/202962701-a35bc6a8-d0ac-4196-9dcc-b789ca092c9d.png)
![image](https://user-images.githubusercontent.com/111370930/202962804-3a0bed9c-ed51-49db-a6b4-b24a5eaecb36.png)
![image](https://user-images.githubusercontent.com/111370930/202963012-d873ca0b-b681-46df-aa3b-ce530d6bbfee.png)
![image](https://user-images.githubusercontent.com/111370930/202963071-eebe7762-727b-42bf-a8f0-78e42291e184.png)
![image](https://user-images.githubusercontent.com/111370930/202963107-85b1b908-b29a-47cb-9181-f06e0d40e3f7.png)


1. Arrancar openHab
- sudo /bin/systemctl enable openhab.service

2. Entrar a openHab
- localhost:8080

3. Comprobar que la sesión esté iniciada

4. Crear un binding haciendo clic en la sección settings, things, +, Install Bindings, pestaña de busqueda. Buscar MQTT binding y hacer clic en el boton instalar

5. Agregar in Bridge haciendo clic en Settigs, Things, +, MQTT Binding.
	Seleccionar un Broker MQTT
	Configurar el puente
	
Broker MQTT
Unique ID: brokerMQTT
Indentifier: mqtt:broker:brokerMQTT
Label: MQTT Broker
Location: Departamento
IP: 127.0.0.1
Port: 1883
Eliminar nombre de usuario y contraseña

6. Crear un Thing haciendo clic en el boton settings, things, +, MQTT Binding, Generic MQTT Thing.

Unique ID: tempSensor
Identifier: mqtt:topic:tempSensor
Labe: Sensor de Temperatura
Location: Escritorio
Bridge: MQTT Broker

7. Crear un canal en el Thing recientemente creado haciendo clic en Things, Sensor de Temperatura, Pestaña Channels, Add Channel

Channel Identifier: sensorTempChannel
Channel Type: Number Value
MQTT State Topic: codigoIoT/openHab/departamento/sala/escritorio/sensorTemp
Absolute Minimum: 0
Absolute Maximum: 50
Delta Value: 0.1
Unit Of Measurement: °C

8. Crear una locación haciendo clic en el boton Model, Add Location

Name: DepartamentoLocation
Label: Departamento Location
Type: Group
Category: Casa
Semantic Class: Apartment

9. Crear una sub locación haciendo clic en la locación raíz, add Location

Name: SalaLocation
Label: Sala Location
Type: Group
Category: Habitación
Semantic Class: LivingRoom

10. Crear un equipamiento que represente al sensor de temperatura haciendo clic en la sublocación y luego en el boton Add Equipment from Thing

Thing: Sensor de Temperatura
Name: SensordeTemperaturaEquipment
Label: Equipamiento Sensor de Temperatura
Category: temperature
Semantic Class: Sensor
Channel: Sensot Temperatura Channel
Name: SensordeTemperaturaEquipment_SensotTemperaturaChannel
Label: Sensot Temperatura Channel Equipment
Category: Temperature
Semantic Class: Measurement
Semantic Property: Temperature

11. Enviar un valor al canal del equipamiento
- mosquitto_pub -h localhost -t codigoIoT/openHab/departamento/sala/escritorio/sensorTemp -m 22.8
- ![image](https://user-images.githubusercontent.com/111370930/202964946-c10e6206-2ff5-42e6-b111-1997a2a05c49.png)
- ![image](https://user-images.githubusercontent.com/111370930/202964976-1c055cd0-e294-4e4b-b190-cd781f4841a8.png)
![image](https://user-images.githubusercontent.com/111370930/202964989-c5a1a901-479e-45e5-9ae4-b5fe35941cf7.png)




