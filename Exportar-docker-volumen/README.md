# Exportar-Docker-Volumen
Exportar docker con volumen incluido, muchas veces tenemos que exportar un contendor con una aplicacion instalada, la cual ya tiene configuraciones predeterminadas o modulos,librerias y frameworks instalados, los cuales residen el los volumentes en la maquina "host" si los volumenes los creamos previamente, dicha tarea se nos dificulta ya que los volumenes se puede llegar a complicar el poder exportarlos. 
Iniciamos partiendo de un contenedor ya creado y funcionando "produccion".

# listamos nuestros contenedores
Docker ps -a

# Listamos nuestras imagenes 
Docker images

# Detener contenedor 
docker stop $CONTENEDOR

# Exportar contenedor 
docker commit $CONTENEDOR $IMAGEN_NUEVA

# Salvar imagen en .tar
docker save $IMAGEN_NUEVA > $IMAGEN_NUEVA.tar 

# Salvamos los volumenes (tu puedes usar ".tar.gz" funciona igual)
docker-volumes.sh $CONTENEDOR save $CONTENEDOR-volumes.tar

# copiamos y pegamos  nuestras imagenes y volumenes en el host destino
scp $CONTAINER.tar $CONTAINER-volumes.tar $USER@$Host: (o puedes pasarlo en un pendrive)

# En el nuevo host:
docker load -i $IMAGEN_NUEVA.tar

NOTA: en casos uses docker-compose debes cambiar el nombre de la imgaen en tu archivo. 

docker create --name $CONTAINER [<PREVIOUS CONTAINER OPTIONS>] $CONTAINER

# Leeremos los volumenes 
docker-volumes.sh $CONTAINER load $CONTAINER-volumes.tar

# Inciaremos el container
docker start $CONTAINER
