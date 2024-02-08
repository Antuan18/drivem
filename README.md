<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Base de Datos - Mi Sitio</title>
    <style>
        /* Estilos CSS */
        /* Aquí puedes agregar tus estilos CSS para personalizar la apariencia de la página */
    </style>
</head>
<body>
    <h1>Mi Base de Datos</h1>
    
    <!-- Formulario para agregar una persona -->
    <h2>Agregar Persona</h2>
    <form id="personaForm">
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" name="nombre" required>
        <label for="edad">Edad:</label>
        <input type="number" id="edad" name="edad" required>
        <button type="submit">Agregar Persona</button>
    </form>
    
    <!-- Formulario para agregar una opción diaria -->
    <h2>Agregar Opción Diaria</h2>
    <form id="opcionForm">
        <label for="opcion">Opción:</label>
        <input type="text" id="opcion" name="opcion" required>
        <button type="submit">Agregar Opción</button>
    </form>
    
    <!-- Sección para ver el inventario mensual -->
    <h2>Inventario Mensual</h2>
    <ul id="inventario">
        <!-- Aquí se mostrará el inventario generado dinámicamente con JavaScript -->
    </ul>
    
    <script>
        // JavaScript para manejar la interactividad de la página
        document.getElementById("personaForm").addEventListener("submit", function(event) {
            event.preventDefault(); // Evitar que el formulario se envíe de forma predeterminada
            
            // Obtener los valores del formulario
            var nombre = document.getElementById("nombre").value;
            var edad = document.getElementById("edad").value;
            
            // Crear un nuevo elemento de lista con los datos de la persona y agregarlo al inventario
            var nuevoItem = document.createElement("li");
            nuevoItem.textContent = "Nombre: " + nombre + ", Edad: " + edad;
            document.getElementById("inventario").appendChild(nuevoItem);
            
            // Limpiar el formulario
            document.getElementById("nombre").value = "";
            document.getElementById("edad").value = "";
        });
        
        document.getElementById("opcionForm").addEventListener("submit", function(event) {
            event.preventDefault(); // Evitar que el formulario se envíe de forma predeterminada
            
            // Obtener el valor del campo de opción
            var opcion = document.getElementById("opcion").value;
            
            // Crear un nuevo elemento de lista con la opción y agregarlo al inventario
            var nuevoItem = document.createElement("li");
            nuevoItem.textContent = "Opción: " + opcion;
            document.getElementById("inventario").appendChild(nuevoItem);
            
            // Limpiar el formulario
            document.getElementById("opcion").value = "";
        });
    </script>
</body>
</html>
theme: jekyll-theme-THEME-NAME
