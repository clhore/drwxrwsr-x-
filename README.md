# drwxrwsr-x+

Al intentar modificar los permisos de un directorio creado con ubuntu server y compartido en samba, haciendo uso de la herramienta RSAT nos encontramos con un error de windows que nos cierra el administrador de archivos y nos deja la pantalla en negro durante unos segundos.

Para solucionar este problema deveremos cambiar algunos premisos desde el propio ububntu server.

    $ chmod 775 <directory> 
    $ setfacl -m "group:users:r-x" <directory>
    $ setfacl -m "group::r-x" <directory>
    $ setfacl -m "group:3000000:rwx" <directory>
    $ setfacl -m "mask::rwx" <directory>
    $ setfacl -m "default:user::rwx" <directory>
    $ setfacl -m "default:user:3000000:rwx" <directory>
    $ setfacl -m "default:group::r-x" <directory>
    $ setfacl -m "default:group:users:r-x" <directori>
    $ setfacl -m "default:mask::rwx" <directori>
    $ setfacl -m "default:other::r-x" <directori>
    $ sudo chown 3000000:users <directori>
        
Para comprender el error debemos primero entender que al crear una carpeta desde Windows con la herramienta RSAT el permiso asignado es 'drwxrwsr-x+'donde el + nos indica que hay permisos ACL asignados.

    lujan@nodo:/datos$ getfacl share/prueba
    # file: share/prueba/
    # owner: 3000000
    # group: users  
    # flags: -s-
    user::rwx
    group::r-x
    group:users:r-x
    group:3000000:rwx
    mask::rwx
    other::r-x
    default:user::rwx
    default:user:3000000:rwx
    default:group::r-x
    default:group:users:r-x
    default:mask::rwx
    default:other::r-x
        
Además si revisamos el propietario del archivo obtenemos que el usuario es '3000000' y el grupo es 'users'. Por lo que hay que establecer los permisos adecuados y sobre todo el usuario y grupo adecuados.

    lujan@nodo:/datos$ ls -l share/
    total 64
    drwxrwsr-x+ 4 3000000 users 4096 Feb  8 10:07 prueba


 
