
# Configuración de ACL en Linux

Tarea 1 — Preparar el entorno

Primero creo los grupos: 
<img width="495" height="117" alt="image" src="https://github.com/user-attachments/assets/0472ed54-9347-446f-accb-5406bc93dde1" />

Creo los usuarios de operarios y los meto al grupo: 

<img width="588" height="88" alt="image" src="https://github.com/user-attachments/assets/b44c12ec-5157-4e94-9ae0-105bee2ab4b2" />

Lo mismo con los usuarios de ingenieria: 

<img width="617" height="93" alt="image" src="https://github.com/user-attachments/assets/d2148b0f-0493-4580-b229-c640040716b0" />

Y lo mismo con supervisores: 

<img width="603" height="75" alt="image" src="https://github.com/user-attachments/assets/f49f925f-7a3a-44b6-a09b-e573a55747e6" />

primero creo el hmi_planta y solo le dejo los permisos al propietario:

<img width="530" height="100" alt="image" src="https://github.com/user-attachments/assets/e707508c-4c13-4a97-b29e-fd429e984b2d" />


luego creo la carpeta planos con un mkdir y dentro de planos creo los archivos.dwg
<img width="517" height="25" alt="image" src="https://github.com/user-attachments/assets/0be34499-4eea-44db-9310-341640264f00" />

<img width="912" height="55" alt="image" src="https://github.com/user-attachments/assets/1dec9717-fe99-4a47-a867-91c803ed78e8" />

Ahora le damos los permisos necesarios a la carpeta con un 700 y un 600 a los archivos .dwg por seguridad:

<img width="551" height="112" alt="image" src="https://github.com/user-attachments/assets/90576326-8027-45c3-bcf6-17d1d711e831" />

Tarea 3 — Configurar las ACL con setfacl


Ahora le doy permisos a los operarios en hmi_planta que es solo de ejecución:


<img width="631" height="271" alt="image" src="https://github.com/user-attachments/assets/b61bf56d-81ce-4af1-bdc7-c1ec12303b6a" />

con el comando de getfacl sobre hmi_planta vemos los cambios.

En el grupo de ingeniería:
Nestor solo puede leer y ejecutar:

<img width="552" height="33" alt="image" src="https://github.com/user-attachments/assets/3776f138-ff3a-4003-9fd8-45a9a6916ebf" />

Compruebo:

<img width="169" height="102" alt="image" src="https://github.com/user-attachments/assets/4d991024-6f55-41e8-b409-3e75a084752c" />

Lucía tiene todos los permisos:

<img width="546" height="27" alt="image" src="https://github.com/user-attachments/assets/e40af996-917a-4764-9f21-7857fed8d49b" />

Compruebo:

<img width="159" height="108" alt="image" src="https://github.com/user-attachments/assets/d4f9875c-7dd0-454f-9a18-84af18d63577" />


PERMISOS SOBRE PLANOS:
1. Lucía solo tiene permiso de escribir y leer sobre autocclave.dwg:

<img width="642" height="31" alt="image" src="https://github.com/user-attachments/assets/c268243c-9cc4-4a97-bdd7-b6c9c003e4d8" />


Compruebo:


<img width="444" height="168" alt="image" src="https://github.com/user-attachments/assets/ee528dea-edfc-4a29-87b3-99218a25a11e" />




2. Victor tiene permisos de leer, escribir y ejecutar sobre la carpeta de planos:
Por este momento solo le daré permisos recursivos a Victor, si se crea otro archivo dentro de planos ya se verá si tendrá los permisos hereditarios en ello o no:

 <img width="558" height="31" alt="image" src="https://github.com/user-attachments/assets/402c3cb9-cce1-4afe-90d9-c06ebffa3fc9" />

 Comprobamos:

 <img width="279" height="156" alt="image" src="https://github.com/user-attachments/assets/38a1f125-8317-4c45-a821-d4d54ea80053" />

 Ahora con el grupo de supervisores que todos tienen permisos de lectura y ejecución:

 
<img width="593" height="27" alt="image" src="https://github.com/user-attachments/assets/7b031652-026c-4de1-af6f-839eed945f32" />

Comprobamos:

<img width="254" height="173" alt="image" src="https://github.com/user-attachments/assets/63e9ec5d-c3b8-41e8-a241-7b1e769ddeb7" />

vamos con Albero de Operarios que solo necesita permisos de lectura en autoclave.dwg:

<img width="492" height="31" alt="image" src="https://github.com/user-attachments/assets/8b84f33b-079b-45f7-97a4-ed7ac703e685" />



Comprobamos: 

<img width="298" height="188" alt="image" src="https://github.com/user-attachments/assets/fc099810-f195-4da8-8dec-425d1f581028" />

Por último Oscar, que también solo necesita permisos de  lectura en el archivo de caldera.dwg

<img width="564" height="206" alt="image" src="https://github.com/user-attachments/assets/4ce6efda-438e-4e76-8569-f3698a187844" />

Comprobaciones con los usuarios:

vemos con Victor:

<img width="495" height="30" alt="image" src="https://github.com/user-attachments/assets/87ad88d2-52db-4a2a-b544-313f20f54bea" />

<img width="585" height="115" alt="image" src="https://github.com/user-attachments/assets/9052e9a0-54b7-4c4f-9f6f-f8c104e6eaf4" />

<img width="470" height="44" alt="image" src="https://github.com/user-attachments/assets/82add367-dbfb-45a3-b442-1440fe5ced58" />


6. Preguntas de reflexión

* ¿Por qué no bastan los permisos clásicos de Unix (usuario / grupo / resto) para implementar el esquema del diagrama? Pon un ejemplo concreto de este caso.

- Justamente porque solo permite esos tres: propietario, grupo  y otros, en el esquema se ve que algunos grupos hasta incluso usuarios necesitan permisos independiente, con lo que, con  los permisos clásicos no daría abasto.
 
- Por ejemplo, le damos permiso al grupo de ingenieros, los otros dos quedarían fuera, y si decides ponerlos en (otros) pues se colará todo el mundo, no es exclusivo.
  

* ¿Qué es la máscara (mask) de una ACL y cómo afecta a los permisos efectivos de un usuario o grupo, aunque su entrada de ACL indique más permisos?

 - La máscara es como el permiso máximo permitido para todos los usuarios y grupos que hemos añadido en ACL, menos para el propietario.
   
 - Pues supongamos de que a un usuario le doy todos los permisos rwx en un archivo, pero en la máscara del archivo solo solo coloco r-x, la máscara es lo que se impone, por lo que solo el usuario y los demás se limitaría a r-x, aunque tengan un rwx porque no se puede tener más permisos de lo que marca el límite global de ese archivo.
  
* ¿Qué diferencia hay entre una ACL de acceso y una ACL por defecto? ¿Cuándo se aplica cada una?

- el ACL de acceso es la regla que se aplica de inmediato y directa a un archivo o directorio que ya existe. Se aplica cuando se quiere configurar los permisos de los ficheros o carpetas que ya han sido creadas.

- el ACL por defecto es como una plantilla de permisos especiales que solo se pueden aplicar a los directorios, eso no afecta a los que ya estaban, si no que cada vez que se cree un nuevo archivo o subcarpeta dentro de ese directorio, hereda esos permisos ya establecidos como su ACL de acceso. Se aplica cuando se quiere asegurar de que los futuros archivos que se añadan a una carpeta mantengan la misma estructura de seguridad sin tener que estar configurándolos en cada creación.
  
* Si mañana se incorpora un nuevo operario, ¿qué pasos tendrías que repetir para darle exactamente el mismo acceso que al resto de operarios?

  - En caso de archivos, solo bastaría con darle los permisos al grupo.
  sudo setfacl  -m g:operarios:--x hmi_planta

con eso, si añadimos a un nuevo usuario a operarios, ya tendría los permisos heredados del grupo.

Si fuese sobre un directorio, ya cambia un poquito.

Le aplico los permisos a los archivo y carpetas que ya existen, la -R que es la recursiva dice que se aplica la misma regla a todos lo que está dentro de ese directorio.

sudo setfacl -R -m g:operarios:r-x planos/

Aquí es donde configuramos los permisos para el futuro, la -d es de default es el que hace la magia:

sudo setfacl -R -d -m g:operarios:r-x planos/
A partir de eso, si entrase un nuevo usuario de operario, tendría por defecto los permisos de leer y ejecutar sobre ese directorio.








 



































