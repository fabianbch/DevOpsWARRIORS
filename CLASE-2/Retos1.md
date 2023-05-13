#Reto 1 - Linux
Ejercicio 1 - Manejo de archivos
Crea mediante comandos de bash la siguiente jerarquía de ficheros y directorios.
foo/
|─- dummy/ 
│  |-─ file1.txt 
│  |─- file2.txt
|-─ empty/

Donde file1.txt debe contener el siguiente texto: Me encanta bash!! Y file2.txt debe permanecer vacío.

#!/bin/bash
mkdir foo
cd foo
mkdir dummy empty
touch dummy/file1.txt dummy/file2.txt
echo "Directorios y archivos creados correctamente."

texto="Me encanta bash!!"
echo "$texto" > dummy/file1.txt
echo "Texto escrito correctamente en file1.txt"

echo "Contenido de file1.txt:"
cat dummy/file1.txt
echo "Contenido de file2.txt:"
cat dummy/file2.txt

cd ..
echo "El script ha finalizado correctamente."
exit 0

 
Ejercicio 2 - Manejo de contenido de archivos
Mediante comandos de bash, vuelca el contenido de file1.txt a file2.txt y mueve file2.txt a la carpeta empty. El resultado de los comandos ejecutados sobre la jerarquía anterior debe dar el siguiente resultado.
foo/
|-─ dummy/
│  |-─ file1.txt
|-─ empty/
|  |-─ file2.txt

Donde file1.txt y file2.txt deben contener el siguiente texto: Me encanta bash!!

#!/bin/bash
mkdir foo
cd foo
mkdir dummy empty
touch dummy/file1.txt dummy/file2.txt
echo "Directorios y archivos creados correctamente."

texto1="Me encanta bash!!"
echo "$texto1" > dummy/file1.txt
echo "Texto escrito correctamente en file1.txt"
texto2=$(cat dummy/file1.txt)
echo "$texto2" > dummy/file2.txt
echo "Texto de file1.txt volcado correctamente en file2.txt"

mv dummy/file2.txt empty/
echo "Archivo file2.txt movido correctamente a la carpeta empty."

echo "Contenido de file1.txt:"
cat dummy/file1.txt
echo "Contenido de file2.txt:"
cat empty/file2.txt

cd ..
echo "El script ha finalizado correctamente."
exit 0

 
Ejercicio 3 - Argumentos del script
Crear un script de bash que agrupe los pasos de los ejercicios anteriores y además permita establecer el texto de file1.txt alimentándose como parámetro al invocarlo. Si se le pasa un texto vacío al invocar el script, el texto de los ficheros, el texto por defecto será: Que me gusta bash!!!!

#!/bin/bash
mkdir foo
cd foo
mkdir dummy empty
touch dummy/file1.txt dummy/file2.txt
echo "Directorios y archivos creados correctamente."

read -p "Ingrese el texto para el archivo file1.txt: " texto1
if [ -z "$texto1" ]
    then
        texto1="Que me gusta bash!!"
    fi
        echo "$texto1" > dummy/file1.txt
echo "Texto escrito correctamente en file1.txt"
texto2=$(cat dummy/file1.txt)
echo "$texto2" > dummy/file2.txt
echo "Texto de file1.txt volcado correctamente en file2.txt"

mv dummy/file2.txt empty/
echo "Archivo file2.txt movido correctamente a la carpeta empty."

echo "Contenido de file1.txt:"
cat dummy/file1.txt
echo "Contenido de file2.txt:"
cat empty/file2.txt

cd ..
echo "El script ha finalizado correctamente."
exit 0

 
Ejercicio 4 - Opcional
Crea un script de bash que descargue el contenido de una página web a un fichero, por ejemplo "https://es.wikipedia.org/wiki/DevOps" Una vez descargado el fichero, que busque en el mismo una palabra dada (esta se pasará por parámetro) y muestre por pantalla el número de línea donde aparece.

#!/bin/bash
echo "Ingresa la URL de la página Web a descargar: "
read url

wget -q -O temp.html $url

echo "Ingrese la palabra que desea buscar en el archivo descargado: "
read palabra

num_lineas=$(grep -c "$palabra" temp.html)

echo "La palabra '$palabra' aparece en $num_lineas líneas en el archivo descargado."
rm temp.html
exit 0

