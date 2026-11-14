
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



















