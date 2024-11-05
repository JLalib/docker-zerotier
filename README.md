# ZeroTier | La VPN sin PortForwarding

ZeroTier es una superposición de red segura que le permite administrar todos los recursos de su red como si estuvieran en la misma LAN. ZeroTier está hecho para gente "normal" que no tiene ni idea de como funciona una VPN o simplemente, alguien como nosotros, que quiere algo que funcione en 5 minutos y simplemente, que funcione.

El funcionamiento de ZeroTier es el siguiente:

Creas una subred que tendrá el llamado Network ID. Un identificador de la Red
Instalas en todas las máquinas que deseas tener bajo esta nueva subred, ZeroTier.
El servidor de ZeroTier, que no está en nuestra máquina, está en sus servidores y es la que nos ha dado el Network ID, igual que sucede con servicios como Syncthing o Plex, conecta todos aquellos clientes que tiene en mismo Network ID y estén online, conectados a internet en ese momento.
El servidor central de ZeroTier, localiza las ip's de todos los dispositivos que están conectados a internet, gracias a la app de ZeroTier y los conecta creando una red.

El tráfico va totalmente cifrado de extremo a extremo. Los servidores de ZeroTier, única y exclusivamente, se encargan de localizar y conectar los clientes, no pasan los datos por sus servidores. Si eso es así, la verdad es que este servicio es alucinante.

Otro punto fuerte de ZeroTier, es que podemos instalarlo en todos los dispositivos. Windows, Linux, Mac, Android, IOS, Raspberry, placa con arquitectura ARM, etc.
### Pasos configuración básica ZeroTier
Después de levantar el contenedor, acceder al mismo; docker exec -ti zerotier-one sh

Seguir los pasos para añadir nuestro nodo a una red Zerotier:

  zerotier-cli info
  
  zerotier-cli status
  
  zerotier-cli listnetworks
  
  zerotier-cli join ID_NETWORK
  
  zerotier-cli listnetworks
  
  ping IP_ZEROTIER_NODE

El proceso en un único comando desde tu host: docker exec -it zerotier-one zerotier-cli join ID_NETWORK

## Exit Node
Para configurar "Exit Node", es decir, salir a Internet con la misma IP que nuestro nodo/servidor principal, debemos añadir ciertas reglas;

sudo nano /etc/sysctl.conf

Añadir ó descomentar la línea; net.ipv4.ip_forward = 1

Aplicar los cambios: sudo sysctl -p

Verificar los cambios: sudo sysctl net.ipv4.ip_forward

Comando para ver las Redes y conocer la nuestra. Importante apuntar el nombe de la interfaz WAN y ZEROTIER. La WAN será eth0 o ens... y la de ZeroTier ver con comando  zerotier-cli listnetworks

ip link show

Establecer las variables de Network y WAN

export ZT_IF=

export WAN_IF=

Habilitar NAT y enmascaramiento de IP:

sudo iptables -t nat -A POSTROUTING -o $WAN_IF -j MASQUERADE

Permitir reenvío de tráfico:

sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

Permitir el reenvío de tráfico desde la interfaz ZeroTier a la interfaz WAN:

sudo iptables -A FORWARD -i $ZT_IF -o $WAN_IF -j ACCEPT

Hacer que las reglas de iptables persistan después del reinicio:

sudo apt-get install iptables-persistent

Guarde sus nuevas reglas de iptables:

sudo netfilter-persistent save


Ahora que su nodo de salida está configurado, necesitamos configurar su red ZeroTier para anunciar una ruta predeterminada para que otros nodos sepan que el nodo de salida puede enrutar el tráfico a Internet.

Central > Network > Settings > Managed Routes

0.0.0.0/0 via IP_NODO-SERVER_ZEROTIER


![ZT full logo gold white](https://github.com/user-attachments/assets/fb3963df-9112-468f-8513-de3702d249b2)

  Fuente:
  
  https://docs.zerotier.com/start
  
  https://www.zerotier.com/download/
  
  https://docs.zerotier.com/exitnode/

  https://github.com/zyclonite/zerotier-docker
