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

3. Como el usuario hugo (grupo operarios, creado ayer en la práctica de ACL), intenta cambiarle la contraseña por algo débil y observa el rechazo:

<img width="737" height="160" alt="image" src="https://github.com/user-attachments/assets/a8dd66bd-3091-4221-a82d-b31164b41de8" />

Ahora prueba escribiendo una contraseña que cumpla con lo que pida PAM:

<img width="627" height="110" alt="image" src="https://github.com/user-attachments/assets/200a584f-e94a-4293-b796-1e90413f9286" />

Prueba con root:

<img width="686" height="117" alt="image" src="https://github.com/user-attachments/assets/bec3e033-e3f0-49cb-b199-b8a3cffb3c8f" />


Al final, cumpliendo con los requisitos si me dejó:

<img width="867" height="172" alt="image" src="https://github.com/user-attachments/assets/86c2b578-8f2c-444d-aef3-14dea230f32b" />



1.4 Caducidad y aviso con chage

* Para el grupo de ingeniería y supervisores caducan cada 60 días, con 7 días de aviso previo:

<img width="745" height="91" alt="image" src="https://github.com/user-attachments/assets/ea5c04f4-1a1a-480c-9f6e-b542c325584a" />

























