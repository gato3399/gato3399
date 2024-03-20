const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const calendarioEscolar = {
  usuarios: {},
  actividades: {},
  registrar() {
    const preguntas = [
      { name: 'nombre', type: 'input', message: 'Ingrese su nombre: ' },
      { name: 'correo', type: 'input', message: 'Ingrese su correo electrónico: ' },
      { name: 'contraseña', type: 'password', message: 'Ingrese su contraseña: ' }
    ];

    rl.question('¿Ya tienes una cuenta? (s/n) ', (respuesta) => {
      if (respuesta.toLowerCase() !== 's') {
        rl.question('Ingrese la ruta de su archivo de usuarios: ', (ruta) => {
          try {
            const datos = fs.readFileSync(ruta, 'utf-8');
            this.usuarios = JSON.parse(datos);
            this.registrarUsuario();
            this.guardarUsuarios(ruta);
          } catch (error) {
            this.registrarUsuario();
            this.guardarUsuarios(ruta);
          }
          rl.close();
        });
      } else {
        this.iniciarSesion();
      }
   
