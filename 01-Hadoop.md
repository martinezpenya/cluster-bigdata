![Hadoop Logo](./imgs/hadoop.webp)
## Consideraciones

- Instalaremos todo en `/opt`
- Utilizaremos el usuario `hadoop`
- Los datos se guardarán en `/datos`

## Creación usuario hadoop

`adduser hadoop`

## Descargamos hadoop

Como root:

```
## Vamos al directorio de trabajo
cd /opt/
wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz

## Descomprimimos
tar -zxvf hadoop-3.3.6.tar.gz
ls -la

## Creamos un enlace para trabajar de manera más cómoda
ln -s hadoop-3.3.6 hadoop
ls -la

## Cambiamos el propietario y grupo de la carpeta y enlace creado
chown -R hadoop:hadoop hadoop-3.3.6 hadoop

## Entramos a la carpeta descomprimida (a través del enlace creado)
cd hadoop
```

## Configuración hadoop

```
cd /opt/hadoop/etc/hadoop/
```

Editamos el archivo `core-site.xml` (nano, vi... )

Editamos el archivo `hdfs-site.xml`

Editamos el archivo `mapred-site.xml`


## Creación carpeta de datos

Como root

```
mkdir -p /datos/{namenode,datanode}
chown -R hadoop:hadoop /datos
```

Formateamos con HDFS
```hdfs namenode -format```

## SSH sin contraseña
El servidor (cloniciabd) ha de poder conectarse a los nodos sin contraseña.

Con el usuario hadoop:
```cd
ssh-keygen -t rsa

cat .ssh/id_rsa.pub >> .ssh/authorized_keys

scp .ssh/authorized_keys hadoop@nuc1:/home/hadoop/.ssh/authorized_keys
scp .ssh/authorized_keys hadoop@nuc2:/home/hadoop/.ssh/authorized_keys
scp .ssh/authorized_keys hadoop@nuc3:/home/hadoop/.ssh/authorized_keys
scp .ssh/authorized_keys hadoop@nuc4:/home/hadoop/.ssh/authorized_keys
```

Ahora ya podremos hacer un ssh sin contraseña
```
ssh nuc1
ssh nuc2
```


