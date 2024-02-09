<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Base de Datos - Mi Sitio</title>
    <script src="https://apis.google.com/js/api.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
        }
        
        h1 {
            text-align: center;
            color: #333;
        }
        
        #registroContainer {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            grid-gap: 20px;
            margin-bottom: 20px;
        }
        
        .registroItem {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .registroItem label {
            display: block;
            margin-bottom: 5px;
            color: #333;
        }
        
        .registroItem input,
        .registroItem textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        
        .registroItem button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        
        .registroItem button:hover {
            background-color: #45a049;
        }
        
        #inventarioContainer {
            display: none; /* Ocultar el inventario por defecto */
        }
    </style>
    <script>
        // Configurar cliente de Google Drive API
        function initClient() {
            gapi.client.init({
                apiKey: '', // No es necesario para esta autenticación
                clientId: '527346036157-ab701j0da2su1c5l3u85ogkkap928i2j.apps.googleusercontent.com',
                discoveryDocs: ['https://www.googleapis.com/discovery/v1/apis/drive/v3/rest'],
                scope: 'https://www.googleapis.com/auth/drive.file'
            }).then(function () {
                console.log('Google Drive API initialized');
            }, function(error) {
                console.error('Error initializing Google Drive API:', error);
            });
        }

        // Subir inventario a Google Drive
        function subirInventario() {
            var inventarioData = JSON.stringify(inventario); // Convertir el inventario a JSON
            
            var fileMetadata = {
                'name': 'inventario.json' // Nombre del archivo en Google Drive
            };
            var media = {
                mimeType: 'application/json',
                body: inventarioData
            };
            
            gapi.client.drive.files.create({
                resource: fileMetadata,
                media: media,
                fields: 'id'
            }).then(function(response) {
                console.log('Archivo subido:', response);
                alert('El inventario se ha guardado en Google Drive.');
            }, function(error) {
                console.error('Error al subir archivo:', error);
                alert('Ha ocurrido un error al guardar el inventario.');
            });
        }

        // Cargar cliente de Google Drive API
        gapi.load('client', initClient);
        
        // Función para mostrar notificación de registro exitoso
        function registroExitoso() {
            alert('¡Registro exitoso! Puedes proceder al siguiente paso.');
        }
    </script>
</head>
<body>
    <h1>Mi Base de Datos</h1>
    
    <!-- Formulario para agregar una entrada -->
    <div id="registroContainer">
        <div class="registroItem">
            <h2>Agregar Entrada</h2>
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" required><br>
            <label for="dni">DNI:</label>
            <input type="text" id="dni" name="dni" required><br>
            <label for="telefono">Teléfono:</label>
            <input type="tel" id="telefono" name="telefono" required><br>
            <label for="modelo">Modelo/Marca:</label>
            <input type="text" id="modelo" name="modelo" required><br>
            <label for="aRealizar">A Realizar:</label>
            <input type="text" id="aRealizar" name="aRealizar" required><br>
            <label for="observaciones">Observaciones:</label>
            <textarea id="observaciones" name="observaciones" required></textarea><br>
            <label for="observacionCliente">Observación del Cliente:</label>
            <textarea id="observacionCliente" name="observacionCliente" required></textarea><br>
            <label for="fecha">Fecha:</label>
            <input type="date" id="fecha" name="fecha" required><br>
            <button type="submit" onclick="registroExitoso()">Agregar Entrada</button>
        </div>
        
        <!-- Búsqueda por nombre o DNI -->
        <div class="registroItem">
            <h2>Búsqueda por Nombre o DNI</h2>
            <label for="busqueda">Buscar:</label>
            <input type="text" id="busqueda">
            <button onclick="buscar()">Buscar</button>
        </div>
    </div>
    
    <!-- Botón para descargar el inventario como Excel -->
    <h2>Descargar Inventario</h2>
    <button onclick="descargarInventario()">Descargar como Excel</button>
    
    <!-- Sección para ver el inventario (oculta por defecto) -->
    <div id="inventarioContainer">
        <h2>Inventario</h2>
        <ul id="inventario">
            <!-- Aquí se mostrará el inventario generado dinámicamente con JavaScript -->
        </ul>
    </div>
    
    <!-- Botón para guardar el inventario en Google Drive -->
    <h2>Guardar Inventario en Google Drive</h2>
