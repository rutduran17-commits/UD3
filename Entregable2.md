# Contraseñas, MFA y privilegios justos
Con el siguiente comando compruebo de que libpam se encuentra activo en la configuración de la RAM:

cat /etc/pam.d/common-password | grep pwquality

<img width="755" height="76" alt="image" src="https://github.com/user-attachments/assets/7d353c0f-500d-4eb6-8e76-7ff7e65747fb" />

Como se ve, la línea existe por lo que ya está activa.


1.3 Práctica guiada — aplicar la política
dentro de  /etc/security/pwquality.conf  fijamos los valores:

* Mínimo de caracteres: 12
  
<img width="621" height="76" alt="image" src="https://github.com/user-attachments/assets/17a80018-2179-4dda-81c3-c841e0e0b4b4" />
* Tipos de caracteres diferentes: 3
  
<img width="568" height="69" alt="image" src="https://github.com/user-attachments/assets/bb7f9a4f-81f7-4094-9b05-a6f3eaec3ee4" />

* Existen al menos un dígito: -1 cada uno

<img width="638" height="334" alt="image" src="https://github.com/user-attachments/assets/482687e1-f351-40fb-a953-6dffac22385d" />

* dictcheck

<img width="498" height="56" alt="image" src="https://github.com/user-attachments/assets/37a12d6f-e375-4bae-98a8-44d8aea33305" />

* maxrepeat

<img width="645" height="58" alt="image" src="https://github.com/user-attachments/assets/7c3144b5-d794-4986-875c-12687631d337" />


*enforce_for_root

<img width="450" height="56" alt="image" src="https://github.com/user-attachments/assets/d03fceae-051f-45fb-938b-34956fe3cc1c" />













