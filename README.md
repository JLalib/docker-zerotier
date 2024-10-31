# ZeroTier

ZeroTier es una superposición de red segura que le permite administrar todos los recursos de su red como si estuvieran en la misma LAN. ZeroTier está hecho para gente "normal" que no tiene ni idea de como funciona una VPN o simplemente, alguien como nosotros, que quiere algo que funcione en 5 minutos y simplemente, que funcione.

El funcionamiento de ZeroTier es el siguiente:

Creas una subred que tendrá el llamado Network ID. Un identificador de la Red
Instalas en todas las máquinas que deseas tener bajo esta nueva subred, ZeroTier.
El servidor de ZeroTier, que no está en nuestra máquina, está en sus servidores y es la que nos ha dado el Network ID, igual que sucede con servicios como Syncthing o Plex, conecta todos aquellos clientes que tiene en mismo Network ID y estén online, conectados a internet en ese momento.
El servidor central de ZeroTier, localiza las ip's de todos los dispositivos que están conectados a internet, gracias a la app de ZeroTier y los conecta creando una red.

Para gestionar nuestras subredes creadas, nos conectaremos a: https://my.zerotier.com/

Está genial, ya que podemos montar un servidor con ciertos servicios y compartirlo con familiares, sin necesidad de montar una VPN y darle todos los privilegios de tener a ese familiar dentro de nuestra red local.

El tráfico va totalmente cifrado de extremo a extremo. Tal como comenta Mc Josan en su vídeo, los servidores de ZeroTier, única y exclusivamente, se encargan de localizar y conectar los clientes, no pasan los datos por sus servidores. Si eso es así, la verdad es que este servicio es alucinante.

Otro punto fuerte de ZeroTier, es que podemos instalarlo en todos los dispositivos. Windows, Linux, Mac, Android, IOS, Raspberry, placa con arquitectura ARM…

![ZT full logo gold white](https://github.com/user-attachments/assets/fb3963df-9112-468f-8513-de3702d249b2)
