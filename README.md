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
![image](https://user-images.githubusercontent.com/111370930/202965539-6b3660ab-8d2f-49fe-bca5-21f39d6c1888.png)

-------------------------------------------------------------------------------

Open Had + Mosquito MQTT

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
![image](https://user-images.githubusercontent.com/111370930/202966012-9dc3a394-18a9-4667-9bc5-5777d1b2e0f8.png)
![image](https://user-images.githubusercontent.com/111370930/202966034-99e948f7-f4bb-4bae-a664-a4f2d671a27a.png)
![image](https://user-images.githubusercontent.com/111370930/202966047-911597a1-5e5a-4bbd-83e2-dd75c7908a9e.png)
![image](https://user-images.githubusercontent.com/111370930/202966065-177afdd9-2411-4987-a434-3591e6816310.png)
![image](https://user-images.githubusercontent.com/111370930/202966083-2e6dbee1-6c59-45c0-ae64-e2728ed4617e.png)
![image](https://user-images.githubusercontent.com/111370930/202966111-e0bd4cf9-571d-4323-b4b0-042bb883335c.png)
![image](https://user-images.githubusercontent.com/111370930/202966155-e98ade95-f5ce-493e-8261-c121bb6c621f.png)
![image](https://user-images.githubusercontent.com/111370930/202966176-e93c10ba-7507-48a6-82d9-1f666d36e563.png)
![image](https://user-images.githubusercontent.com/111370930/202966181-d7e3cd49-40ba-4eb7-bb80-2256612af699.png)
![image](https://user-images.githubusercontent.com/111370930/202966267-b448ac39-13e5-4305-9d11-4851f1bddf25.png)
![image](https://user-images.githubusercontent.com/111370930/202966303-c45e8365-a5ef-4514-a6d1-99a26c9880a3.png)
![image](https://user-images.githubusercontent.com/111370930/202966333-28813269-402a-4bc2-81a3-5dcf894f1bf2.png)

![image](https://user-images.githubusercontent.com/111370930/202966359-89230241-a284-4246-9006-751c0c12de38.png)

![image](https://user-images.githubusercontent.com/111370930/202966382-46ac7c3b-4fb0-4707-a459-711cd6fa95e2.png)
![image](https://user-images.githubusercontent.com/111370930/202966425-fd401969-0a9e-4f7d-b10b-8cdfa64c97df.png)
![image](https://user-images.githubusercontent.com/111370930/202966464-b0ca423d-cffc-4565-88ff-fd15f2a05faf.png)

/////////////////////////////////////////////////////////////////////////////////////////////////////

INDICADOR LED

////////////////////////////////////////////////////////////////////////////////////////////////////

1. Arrancar OpenHab
- sudo systemctl start openhab.service

2. Agregar un led a la sala

Thing
Unique ID: LEDSala
Identifier: mqtt:topic:LEDSala
Label: LED Sala
Location: Sala Location
Bridge: MQTT Broker

Channel
Channel Identifier: LEDSalaChannelIdentifier
Label: LED Sala Channel Identifier
Channel Type: On/Off Switch

MQTT StateTopic: codigoIoT/openHab/Departamento/Sala/Escritorio/LED01

Equipment
Thing: LED Sala
Name: LEDSalaEquipment
Label: LED Sala Equipment
Category: Light
Semantic Class: Lightbulb
Channel: LED Sala Channel Identifier
Name: LEDSalaEquipment_LEDSalaChannelIdentifier
Label: LED Sala Channel Identifier
Type: Switch
Category: Light
Semantic Class: Switch
Semantic Property: Light

3. Enviar el estatus del LED
- mosquitto_pub -h localhost -t codigoIoT/openHab/Departamento/Sala/Escritorio/LED01 -m "ON"

4. Agregar un Switch a la sala
- Configurar correctamente el Type a Switch
- Configurar correctamente el tema a Command
- Activar la casilla Is Command


![image](https://user-images.githubusercontent.com/111370930/203386588-75b3a5fb-d376-46bf-b6f8-58838e0f11f8.png)
![image](https://user-images.githubusercontent.com/111370930/203386984-5d968d61-adb5-455e-a16f-f5ebf7185443.png)











