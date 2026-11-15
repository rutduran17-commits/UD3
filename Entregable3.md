# Certificados y HTTPS: de nuestra propia CA a Let’s Encrypt


### 0.1 Antes de empezar: qué necesitas

H e escogido la opción B ya que ya tenía el adaptador de NAT por lo que activé otro adaptador de solo anfitrión, le configuré la IP de forma estática:

IP de la red NAT en la interfaz de enp0s8:
<img width="842" height="174" alt="image" src="https://github.com/user-attachments/assets/dd277a84-a543-4253-b81c-d5ebda492034" />
dentro del archivo de /etc/netplan/01-network-manager-all.yaml configuré la IP del uso con el anfitrión. IP del servidor 192.168.56.100
<img width="862" height="240" alt="image" src="https://github.com/user-attachments/assets/f2613024-3073-4212-9943-dba00dfea294" />

<img width="826" height="99" alt="image" src="https://github.com/user-attachments/assets/9793c27e-0930-4c6e-8855-11dde3e0c4fe" />

## PARTE 1 Nuestra propia autoridad de certificación

### 1.2 Paso a paso
$ systemctl status apache2 --no-pager

<img width="1110" height="457" alt="image" src="https://github.com/user-attachments/assets/7c314153-cc37-4209-85ab-b26c547863e9" />

$ sudo ss -tlnp | grep ':80'

<img width="1797" height="121" alt="image" src="https://github.com/user-attachments/assets/4775d428-3df3-4881-ab58-d2edf1c44b76" />

###  Anota en tu informe

<img width="653" height="656" alt="image" src="https://github.com/user-attachments/assets/db92f015-21a9-4388-8dfd-2f48c006ee6a" />


 ###¿Qué indica el navegador sobre la seguridad de la conexión y por qué?

 Dice que la conexión no es segura y no hay ningún candado, porque estoy accediendo con el protocolo de HTTP por el puerto 80.

## Paso 1 — Crear una carpeta de trabajo para la CA



