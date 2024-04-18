

## Archivo workers


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


## Problema con webdfs
Al subir archivos por webdfs nos podemos encontrar con un problema CORS.
Para solucionarlo modificamos core-site.xml y añadimos las siguientes propiedades.
https://developer.mozilla.org/es/docs/Web/HTTP/CORS

`core-site.xml`
```
	<property>
            <name>hadoop.http.cross-origin.enabled</name>
            <value>false</value>
    </property>
    <property>
            <name>hadoop.http.cross-origin.allowed-origins</name>
            <value>*</value>
    </property>
    <property>
            <name>hadoop.http.cross-origin.allowed-methods</name>
            <value>GET,POST,HEAD</value>
    </property>
    <property>
            <name>hadoop.http.cross-origin.allowed-headers</name>
            <value>X-Requested-With,Content-Type,Accept,Origin</value>
    </property>
    <property>
            <name>hadoop.http.cross-origin.max-age</name>
            <value>1800</value>
    </property>
```

Hay que copiar el archivo en todos los equipos:
```
$ cd /opt/hadoop/etc/hadoop/
$ scp core-site.xml nuc1:/opt/hadoop/etc/hadoop/
$ scp core-site.xml nuc2:/opt/hadoop/etc/hadoop/
$ scp core-site.xml nuc3:/opt/hadoop/etc/hadoop/
$ scp core-site.xml nuc4:/opt/hadoop/etc/hadoop/

```
