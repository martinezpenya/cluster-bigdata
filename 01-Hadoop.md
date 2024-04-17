**Instalaremos todo en /opt**
**Utilizaremos el usuario hadoop**
**Los datos se guardarán en /datos**

## Creación usuario hadoop

``adduser hadoop

## Descargamos hadoop

``cd /opt/
``wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz

Descomprimimos
``tar -zxvf hadoop-3.3.6.tar.gz
``ls -la

Creamos un enlace para trabajar de manera más cómoda
``ln -s hadoop-3.3.6 hadoop
``ls -la

Cambiamos el propietario y grupo de la carpeta y enlace creado
``chown -R hadoop:hadoop hadoop-3.3.6 hadoop

Entramos a la carpeta descomprimida (a través del enlace creado)
``cd hadoop
