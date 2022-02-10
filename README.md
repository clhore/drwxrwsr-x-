# drwxrwsr-x+

Al intentar modificar los permisos de un directorio creado con ubuntu server y compartido en samba, haciendo uso de la herramienta RSAT nos encontramos con un error de windows que nos cierra el administrador de archivos y nos deja la pantalla en negro durante unos segundos.

Para solucionar este problema deveremos cambiar algunos premisos desde el propio ububntu server.

    $ chmod 775 <directory> 
    $ setfacl -m "group:users:r-x" <directory>
    $ setfacl -m "group:3000000:rwx" <directory>
    $ setfacl -m "mask::rwx" <directory>
    $ setfacl -m "default:user::rwx" <directory>
    $ setfacl -m "default:user:3000000:rwx" <directory>
    $ setfacl -m "default:group::r-x" <directory>
    $ setfacl -m "default:group:users:r-x" <directori>
    $ setfacl -m "default:mask::rwx" <directori>
    $ setfacl -m "default:other::r-x" <directori>
    $ sudo chown 3000000:users <directori>
