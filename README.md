# Quimey-desafio1

*Solicitar informacion del usuario
read -p "Ingrese el nombre de login: " login
read -p "Ingrese el nombre: " nombre
read -p "Ingrese el apellido: " apellido
read -p "Ingrese el departamento: " departamento

* Verificar si el usuario ya existe
if id "$login" &>/dev/null; then
    echo "El usuario $login ya existe. Por favor, elija otro nombre de login."
    exit 1
fi

* Generar contraseña segura
password=$(openssl rand -base64 12)

* Crear usuario con los requisitos 
sudo useradd -m -c "$nombre $apellido, $departamento" -s /bin/bash "$login"

* Asignar contraseña al usuario
echo "$login:$password" | sudo chpasswd

* Mostrar información del usuario creado
echo "Usuario $login creado correctamente."
echo "Contraseña generada para $login: $password"
