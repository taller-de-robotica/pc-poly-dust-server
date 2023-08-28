# Servidor poly_dust ros2

Contiene el espacio de trabajo necesario para poder compilar y ejecutar el servidor que corre la red neuronal para interpretar la suciedad de los paneles solares

## Como compilar y ejecutar el servidor:

### Crear espacio de trabajo 

Crea una carpeta para hospedar el espacio de trabajo para este servidor: 

````bash
mkdir -vp  ~/poly_dust_server/src
cd ~/poly_dust_server/src
# Clonar el espacio de trabajo a la carpeta src
git clone <repository_url> .
````

#### Descargar los pesos de la red neuronal
Los pesos de la red neuronal se pueden descargar de : [sm_unet4_03.hdf5](https://quetzalcoatl.fciencias.unam.mx/taller/1erTaller/sm_unet4_03.hdf5) o puedes ejecutar el siguiente comando:


```bash
wget -P ~/poly_dust_server/src/poly_dust/poly_dust https://quetzalcoatl.fciencias.unam.mx/taller/1erTaller/sm_unet4_03.hdf5
```

#### Instalar requerimientos de python

Hemos encontrado problemas a la hora de usar ros2 y ambientes virtuales de python, por lo que recomendamos realizar la instalación a nivel del python de usuario. 

```bash
pip install -r requirements.txt
```



#### Compilar nodos

```baash
# Sourcea ros
source source /opt/ros/<ros_version>/setup.bash

colcon build --packages-select solar_interfaces
colcon build --symlink-install --packages-select poly_dust
```

#### Ejecutar los nodos:

```
# Sourcea ros
ros2 run poly_dust poly_dust_server
```
`Importante:` Este servidor  no funcionará a menos que previamente se encuentre corriendo el nodo deliver_service en la rasperry.

## Arquitectura de la solución
![](/arquitectura.png)

## Diagnostico del servidor

Tambien se proporciona un cliente para el servidor, para poder determinar si su funcionamiento es correcto:

```bash
# Sourcea ros
ros2 run poly_dust poly_dust_cliente <photo_id>
```