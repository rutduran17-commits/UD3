# Contraseñas, MFA y privilegios justos
Con el siguiente comando compruebo de que libpam se encuentra activo en la configuración de la RAM:

cat /etc/pam.d/common-password | grep pwquality

<img width="755" height="76" alt="image" src="https://github.com/user-attachments/assets/7d353c0f-500d-4eb6-8e76-7ff7e65747fb" />

Como se ve, la línea existe por lo que ya está activa.


1.3 Práctica guiada — aplicar la política






