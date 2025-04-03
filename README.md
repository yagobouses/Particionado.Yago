## Práctica de Particionado en GPT y MBR

Tanto en GPT como en MBR los comandos son iguales.

### 1. Ver las particiones de la máquina:
```bash
lsblk
```
![lsblk](/capturas/1-2.png)
SDB es el disco con la particiones DOS (MBR) y SDC es el disco con las particiones GPT

### 2. Entrar con `fdisk` al disco que queremos seleccionar para hacer las particiones:
```bash
sudo fdisk /dev/sdX
```
- `o` para que la partición esté en formato DOS (MBR).
- `g` para que la partición esté en formato GPT.
- `n` para ver las particiones que tenemos.
- `p` para la partición primaria.
- `e` para las extendidas.
- `w` para guardar la configuración y particiones.<BR><BR>

MBR:

![lsblk](/capturas/5.png)
![lsblk](/capturas/7.png)
![lsblk](/capturas/8.png)
![lsblk](/capturas/9.png)
![lsblk](/capturas/10.png)
![lsblk](/capturas/11.png)
![lsblk](/capturas/12.png)
![lsblk](/capturas/13.png)
![lsblk](/capturas/14.png)
![lsblk](/capturas/15.png)
![lsblk](/capturas/16.png)
![lsblk](/capturas/17.png)
![lsblk](/capturas/18.png)
![lsblk](/capturas/19.png)
<BR><BR>
GPT:<BR>

![lsblk](/capturas/1-1.png)
![lsblk](/capturas/1-2.png)
![lsblk](/capturas/1-8.png)
![lsblk](/capturas/1-9.png)
![lsblk](/capturas/1-10.png)

### 3. Formatear todas las particiones con el formato EXT-4:
```bash
mkfs.ext4 /dev/sdX
```
<BR>

MBR:
![lsblk](/capturas/20.png)
![lsblk](/capturas/21.png)
<BR>
GPT:
<BR>
![lsblk](/capturas/1-12.png)

### 4. Montar las particiones y crear en la ruta `/media/datos1`:
```bash
mkdir /media/datos1 && mount /dev/sdb1 /media/datos1
mount | grep /dev/sdb1
```
<BR>MBR:<BR>

![lsblk](/capturas/24.png)<BR>
GPT:<BR>
![lsblk](/capturas/1-14.png)
### 5. Crear contenido dentro de la carpeta:
```bash
for i in $(seq 1 10); do echo "Fichero ${i}" > fichero${i}.txt; done
``` 

![lsblk](/capturas/1-17.png)


### 6. Añadir en una nueva entrada del `/etc/fstab` el identificador de la partición:
Dentro de `/etc/fstab`, la entrada tendrá 6 columnas de datos:
- UUID
- Opciones de montaje
- Opción dump
- Opción pass

```bash
blkid | grep sdb | awk -F ' ' '{print $2}' | sed 's/"//g'
nano /etc/fstab  # O usar cat para comprobar
cat /etc/fstab
``` 
MBR:
![lsblk](/capturas/22.png)
GPT:
![lsblk](/capturas/1-11.png)
### 7. Si hubiera algún error en la configuración del `/etc/fstab`:
```bash
mount -a
ls /media/sdb*
cat /media/sdb5/prueba/prueba.txt>
```
![lsblk](/capturas/1-16.png)

![lsblk](/capturas/1-18.png)
![lsblk](/capturas/1-19.png)
![lsblk](/capturas/26.png)
![lsblk](/capturas/27.png)
### 8. meter una frase dentro de la carpea:
Dentro de `/etc/fstab`, una frase:

```bash
echo"texto" | sudo tee 
``` 
![lsblk](/capturas/1-20.png)
![lsblk](/capturas/1-21.png)

### 8. FIN:
![lsblk](/capturas/1-22.png)
