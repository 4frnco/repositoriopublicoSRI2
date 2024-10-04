# repositoriopublicoSRI2
1. Comprobar que tienes la imagen httpd:
Primero, debes comprobar si tienes la imagen de Apache (httpd) en tu equipo. Para hacerlo, ejecuta docker images y verifica si aparece la imagen httpd. Si no la tienes, puedes descargarla con el comando docker pull httpd.

2. Crear un contenedor de nombre 'asir_httpd' y mapear el puerto 8080 al 80:
Una vez descargada la imagen, procede a crear un contenedor con el nombre asir_httpd. Este contenedor debe tener el puerto 80 del contenedor mapeado al puerto 8080 de tu máquina local, lo que se hace ejecutando docker run -d --name asir_httpd -p 8080:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. En este comando, el directorio local htdocs se montará en el directorio htdocs del contenedor Apache, permitiendo que los archivos locales sean accesibles en el servidor web.

3. Montar un volumen en el directorio htdocs de Apache:
El montaje de volúmenes se realiza con la opción -v, que en este caso vincula el directorio local "$PWD"/htdocs con el directorio htdocs dentro del contenedor (/usr/local/apache2/htdocs/). Esto te permitirá manejar los archivos web desde tu máquina local y que sean servidos por el contenedor de Apache. Asegúrate de que el directorio local htdocs contenga una página HTML, como un archivo index.html, para poder acceder a él desde el servidor web.

4. Mostrar una página HTML alojada en Apache desde el navegador:
Luego, abre tu navegador y accede a http://localhost:8080 para verificar que la página HTML se está sirviendo correctamente. Si todo está configurado bien, deberías ver la página que creaste en tu directorio local.

5. Crear un contenedor 'asir_web1' que use el mismo directorio para htdocs y el puerto 8000:
Después, crea otro contenedor llamado asir_web1, que utilice el mismo directorio local para htdocs y que esté mapeado al puerto 8000. Esto se hace ejecutando el comando docker run -d --name asir_web1 -p 8000:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. Ahora, tu contenedor asir_web1 utilizará el mismo directorio local para los archivos web, pero servirá las páginas en el puerto 8000 en lugar del 8080.

6. Crear otro contenedor 'asir_web2' con el mismo directorio y el puerto 8090:
Finalmente, crea un tercer contenedor con el nombre asir_web2, utilizando también el mismo directorio local para htdocs, pero mapeando el puerto 8090. Esto se hace con el comando docker run -d --name asir_web2 -p 8090:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. Ahora tendrás tres contenedores sirviendo la misma página HTML, pero en diferentes puertos: 8080, 8000 y 8090.

7. Comprobar que ambos servidores muestran la misma página:
Para comprobar que los tres servidores están funcionando correctamente y mostrando la misma página, abre tu navegador y accede a http://localhost:8000 y http://localhost:8090. Ambos servidores deberían mostrar la misma página HTML, ya que están utilizando el mismo volumen montado para los archivos web.
