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

