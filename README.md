# sqldeveloper
saltar al contenido
Buscar o saltar a...
Solicitudes de extracción
Cuestiones
Mercado
Explorar
 
@yemonterouser 
github
/
códigoql
Público
Código
Cuestiones
462
Solicitudes de extracción
228
Discusiones
Comportamiento
Proyectos
Seguridad
Perspectivas
códigoql/.github/flujos de trabajo/ codeql-análisis.yml
@hvitved
Hvitved C#: Usar .NET 6
Última confirmación d7eeb1f on 28 Jan
 Historia
 4 colaboradores
@hvitved@aeisenberg@tibbes@tamasvajk
62 líneas (50 sloc)  1.57 KB
   
nombre : " Escaneo de código - acción "

en :
  empujar :
    ramas :
      - principal
      - ' rc/* '
  pull_request :
    ramas :
      - principal
      - ' rc/* '
    caminos :
      - ' csharp/** '
      - ' .github/codeql/** '
      - ' .github/workflows/codeql-análisis.yml '
  horario :
    - cron : ' 0 9 * * 1 '

trabajos :
  CodeQL-Construir :

    se ejecuta en : ubuntu-latest

    permisos :
      contenido : leer
      eventos de seguridad : escribir
      solicitudes de extracción : leer

    pasos :
    - nombre : Configuración dotnet
      usos : acciones/setup-dotnet@v1
      con :
        versión dotnet : 6.0.101

    - nombre : Repositorio de pago
      usos : acciones/checkout@v2

    # Inicializa las herramientas de CodeQL para escanear.
    - nombre : Inicializar CodeQL
      usos : github/codeql-action/init@main
      # Anule la selección de idioma descomentando esto y eligiendo sus idiomas
      con :
        Idiomas : csharp
        archivo de configuración : ./.github/codeql/codeql-config.yml

    # Autobuild intenta construir cualquier lenguaje compilado (C/C++, C# o Java).
    # Si este paso falla, debe eliminarlo y ejecutar la compilación manualmente (ver más abajo)
    # - nombre: Autoconstrucción
    #   usos: github/codeql-action/autobuild@main

    # ℹ️ Programas de línea de comandos para ejecutar usando el shell del sistema operativo.
    # 📚 https://git.io/JvXDl

    # ✏️ Si el Autobuild falla arriba, elimínelo y descomente las siguientes tres líneas
    #     y modifíquelos (o agregue más) para construir su código si su proyecto
    #     usa un lenguaje compilado

    - ejecutar : |
       dotnet build csharp /p:UseSharedCompilation=false
    - nombre : Realizar análisis de CodeQL
      usos : github/codeql-action/analyze@main
© 2022 GitHub, Inc.
Términos
Privacidad
Seguridad
Estado
Documentos
Póngase en contacto con GitHub
Precios
API
Capacitación
Blog
Acerca de
