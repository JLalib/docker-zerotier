# ZeroTier como contenedor en Docker

ZeroTier es una superposición de red segura que le permite administrar todos los recursos de su red como si estuvieran en la misma LAN. ZeroTier está hecho para gente "normal" que no tiene ni idea de como funciona una VPN o simplemente, alguien como nosotros, que quiere algo que funcione en 5 minutos y simplemente, que funcione.

El funcionamiento de ZeroTier es el siguiente:

Creas una subred que tendrá el llamado Network ID. Un identificador de la Red
Instalas en todas las máquinas que deseas tener bajo esta nueva subred, ZeroTier.
El servidor de ZeroTier, que no está en nuestra máquina, está en sus servidores y es la que nos ha dado el Network ID, igual que sucede con servicios como Syncthing o Plex, conecta todos aquellos clientes que tiene en mismo Network ID y estén online, conectados a internet en ese momento.
El servidor central de ZeroTier, localiza las ip's de todos los dispositivos que están conectados a internet, gracias a la app de ZeroTier y los conecta creando una red.

El tráfico va totalmente cifrado de extremo a extremo. Tal como comenta Mc Josan en su vídeo, los servidores de ZeroTier, única y exclusivamente, se encargan de localizar y conectar los clientes, no pasan los datos por sus servidores. Si eso es así, la verdad es que este servicio es alucinante.

Otro punto fuerte de ZeroTier, es que podemos instalarlo en todos los dispositivos. Windows, Linux, Mac, Android, IOS, Raspberry, placa con arquitectura ARM, etc.
### Pasos
Después de levantar el contenedor, acceder al mismo; docker exec -ti zerotier-one sh

Seguir los pasos para añadir nuestro nodo a una red Zerotier:

  zerotier-cli info
  
  zerotier-cli status
  
  zerotier-cli listnetworks
  
  zerotier-cli join ID_NETWORK
  
  zerotier-cli listnetworks
  
  ping IP_ZEROTIER_NODE

El proceso en un único comando desde tu host: docker exec -it zerotier-one zerotier-cli join ID_NETWORK

![ZT full logo gold white](https://github.com/user-attachments/assets/fb3963df-9112-468f-8513-de3702d249b2)

  Fuente:
  
  https://docs.zerotier.com/start
  
  https://www.zerotier.com/download/

  https://github.com/zyclonite/zerotier-docker
