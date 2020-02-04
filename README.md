
# Notas

Notas sobre distintas aplicaciones de DresiSS

## TAPE BACKUPS

* Activar compresión del drive (Hardware)

mt -f /dev/nst0 compression 1
* Comprobar parámetros del drive

tapeinfo -f /dev/nst0
* Posición de la cinta

mt -f /dev/st0
* Listar cintas en una librería

mtx -f /dev/tape/by-id/scsi-1IBM_3573-TL_00X2U78CG231_LL0 status
* Parámetros para el drive en  Bacula (EOF, MTIOCGET...)

Hardware End of File = no

Use MTIOCGET = no;

TWO EOF = yes

Fast Forward Space File = yes

## NFS
* Ejemplo para fstab
servidor:/rutaNFS /RutaLocal nfs rsize=8192,wsize=8192,timeo=14,intr
