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

### Paso 1 — Crear una carpeta de trabajo para la CA

<img width="707" height="118" alt="image" src="https://github.com/user-attachments/assets/f92d38e3-2319-4fd6-8b3a-21979663690f" />

* Qué deberías ver:

<img width="642" height="101" alt="image" src="https://github.com/user-attachments/assets/9952d724-5b75-4e3b-a7a8-491ae24d67db" />


### Paso 2 — Generar la clave privada de la CA

<img width="881" height="107" alt="image" src="https://github.com/user-attachments/assets/914a461b-8df5-4f35-bbca-2d8a0248bdaa" />


### Paso 3 — Crear el certificado raíz de la CA (autofirmado)

<img width="1100" height="182" alt="image" src="https://github.com/user-attachments/assets/160b327d-437c-4a9f-b259-eab171704ad4" />

### Paso 4 — Inspeccionar el certificado que acabas de crear
openssl x509 -in certs/ca.crt -noout -subject -issuer -dates

<img width="1067" height="145" alt="image" src="https://github.com/user-attachments/assets/440df121-8fd8-413d-af42-4d04cce552e8" />

openssl x509 -in certs/ca.crt -noout -text | grep -A1 'Basic Constraints'

<img width="1235" height="107" alt="image" src="https://github.com/user-attachments/assets/c679483b-f903-4f81-8b16-ef548380dc98" />

#### ¿Por qué coinciden Subject e Issuer? 
Coinciden porque se trata de un certificado raíz autofirmado.

#### ¿Hasta qué fecha es válida tu CA?
es válida hasta el 2036 

### Paso 5 — Clave privada del servidor y petición de certificado (CSR)

<img width="951" height="120" alt="image" src="https://github.com/user-attachments/assets/e58a7b01-f79f-41bd-8d15-31c7e1da3816" />

### Paso 6 — Indicar para qué nombres e IP es válido el certificado (SAN)

<img width="1223" height="226" alt="image" src="https://github.com/user-attachments/assets/82f1464f-145d-4f0f-8a67-bed72cf4417c" />

### Paso 7 — La CA firma el certificado del servidor
<img width="791" height="171" alt="image" src="https://github.com/user-attachments/assets/0950a185-50df-45c7-9286-7fa37f7ad0d5" />

 #### Anota en tu informe: ¿Por qué el certificado del servidor dura 365 días y el de la CA 10 años?
 - Porque la CA es la raíz de toda la infraestructura, el cambiarla en periodos cortos implica redistribuir su nuevo certificado a todos los que dependan de ello, por lo que se le asigna un periodo largo para que tenga estabilidad a largo plazo.
   
 - y los certificados del servidor duran menos por tema de seguridad.


### Paso 8 — Verificar la cadena de confianza

openssl puede comprobar que el certificado del servidor está firmado por la CA indicada. 
openssl verify -CAfile certs/ca.crt certs/srv.crt
 
 <img width="902" height="50" alt="image" src="https://github.com/user-attachments/assets/521231a1-d597-4791-827b-c43b5d2f21db" />

  openssl x509 -in certs/srv.crt -noout -subject -issuer -ext subjectAltName

  
<img width="1211" height="143" alt="image" src="https://github.com/user-attachments/assets/f6e50370-47e0-4f4e-bcdc-a2e8701e0881" />

### Paso 9 — Instalar el certificado en Apache

























