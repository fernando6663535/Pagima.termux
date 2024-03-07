<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mis Videos</title>
    <style>
        .boton {
            display: inline-block;
            padding: 10px 20px;
            font-size: 16px;
            color: #fff;
            text-align: center;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #ff0000; /* Rojo */
        }
        
        #videoContainer {
            max-width: 100%;
            max-height: 50vh; /* Altura máxima del contenedor de video */
            overflow: auto;
        }
        
        #videoContainer video {
            max-width: 100%;
            max-height: 100%; /* Altura máxima del video */
            width: auto;
            height: auto; /* Altura automática del video */
        }
    </style>
</head>
<body>
    <h1>Mis Videos</h1>
    <p>Selecciona un video:</p>
    
    <input type="file" accept="video/*" id="videoInput">
    <button class="boton" onclick="cargarVideo()">Subir Video</button>
    
    <div id="videoContainer"></div>
    
    <script>
        let timeoutID = null;

        function cargarVideo() {
            const input = document.getElementById('videoInput');
            const videoContainer = document.getElementById('videoContainer');
            
            const file = input.files[0];
            if (!file) {
                alert("Por favor, selecciona un video.");
                return;
            }
            
            const videoURL = URL.createObjectURL(file);
            
            const video = document.createElement('video');
            video.src = videoURL;
            video.controls = true;
            
            videoContainer.innerHTML = '';
            videoContainer.appendChild(video);

            timeoutID = setTimeout(function() {
                // Abrir el anuncio en otra pestaña después de 6 segundos
                window.open('https://www.ejemplo.com/anuncio', '_blank');
            }, 6000); // 6 segundos
        }

        // Función para cancelar el temporizador si se carga un nuevo video antes de los 6 segundos
        function cancelarTemporizador() {
            if (timeoutID) {
                clearTimeout(timeoutID);
            }
        }

        // Función para evitar que al retroceder se vuelva a cargar la página de inicio
        window.history.replaceState(null, document.title, window.location.href);
    </script>
</body>
</html>
