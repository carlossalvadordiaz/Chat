## Resumen

- Importado el socket.io
    -io.on
    -io.emit
    -socket.on
    -socket.emit
    -socket.disconnect

- Chat creado en index.pug
    -inyectado un archivo <script>
    -Creado con elementos del DOM 

- Librería toastr utilizada (Junto a jQuery y los estilos css) [toastr]("https://codeseven.github.io/toastr/")




  //h3#numUsuarios
  .main
    ul#mensajes.mensajes
      li pepito: haasd
      li rosita: jsad
  .acciones
    .form-group
      label Nombre
      input#inputNombre.form-control(type="text")
    .form-group
      label mensaje
      input#inputMensaje.form-control(type="text")
    button#btnEnviar.btn.btn-info Enviar

  script.
    const socket = io();
    const inputNombre = document.getElementById('inputNombre')
    const inputMensaje = document.getElementById('inputMensaje')
    const btnEnviar = document.getElementById('btnEnviar')
    const sctMensajes = document.getElementById('mensajes')
    const numUsuarios = document.getElementById('numUsuarios')

    btnEnviar.addEventListener('click', ()=> {
      console.log('click')
      socket.emit('chat_mensaje', {
        nombre: inputNombre.value,
        mensaje: inputMensaje.value
      });
    })

    socket.on('chat_mensaje', data => {
      sctMensajes.innerHTML += `<li>${data.nombre}: ${data.mensaje}</li>`
      });
    
    socket.on('chat_usuarios', data => {
      numUsuarios.innerText = `Usuarios: ${data}`;
      toastr.info('Se ha conectado un nuevo usuario')
    })//

