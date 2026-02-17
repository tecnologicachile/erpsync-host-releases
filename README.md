# ERP Sync Host - Guia de Instalacion

Software de sincronizacion entre sistemas ERP y plataformas de e-commerce. Se ejecuta como servicio de Windows y se administra desde un panel web.

## Requisitos

- Windows 10/11 o Windows Server 2016+
- Permisos de administrador (para instalar el servicio)
- Conexion a la base de datos del ERP (SQL Server)
- Conexion a internet (para e-commerce y actualizaciones)

## Instalacion

### 1. Descargar

Descargar el ZIP de la ultima version desde la seccion [Releases](https://github.com/tecnologicachile/erpsync-host-releases/releases).

### 2. Extraer

Extraer el contenido del ZIP en una carpeta, por ejemplo:

```
c:\erpsync-host\
```

La estructura debe quedar asi:

```
c:\erpsync-host\
├── erpsync-host-admin.exe    (ejecutable principal)
├── install-service.bat       (instalador del servicio)
├── uninstall-service.bat     (desinstalador)
├── change-port.bat           (cambiar puerto)
├── start_panel.bat           (iniciar sin servicio)
└── static\                   (archivos del panel web)
    ├── index.html
    ├── css\
    └── js\
```

### 3. Instalar como servicio

Ejecutar **como administrador**:

```
Click derecho en install-service.bat → Ejecutar como administrador
```

Esto instala el servicio `ErpsyncHostAdmin` con inicio automatico en el puerto **8080**.

> Si necesitas otro puerto, usar `install-service-custom.bat` en su lugar.

### 4. Verificar

Abrir en el navegador:

```
http://localhost:8080
```

Debe aparecer el panel de administracion de ERP Sync Host.

## Administracion del servicio

Desde una terminal con permisos de administrador:

| Accion | Comando |
|--------|---------|
| Ver estado | `sc query ErpsyncHostAdmin` |
| Detener | `net stop ErpsyncHostAdmin` |
| Iniciar | `net start ErpsyncHostAdmin` |
| Reiniciar | `net stop ErpsyncHostAdmin && net start ErpsyncHostAdmin` |

## Configuracion inicial

1. Abrir el panel web (`http://localhost:8080`)
2. Ir a la seccion **Integraciones**
3. Crear una nueva integracion con los datos de conexion al ERP y al e-commerce
4. Probar la conexion al origen (ERP) y al destino (e-commerce)
5. Ejecutar una tarea de sincronizacion de prueba

## Conexion a Central (soporte remoto)

Si se dispone de un codigo de activacion:

1. Ir a la seccion **Servidor Central** en el panel
2. Ingresar el codigo de activacion proporcionado
3. Aceptar el acuerdo de servicio
4. Activar la conexion

Esto permite recibir soporte remoto y actualizaciones automaticas.

## Actualizaciones

Las actualizaciones se reciben automaticamente a traves de Central. Tambien se puede actualizar manualmente:

1. Detener el servicio: `net stop ErpsyncHostAdmin`
2. Reemplazar `erpsync-host-admin.exe` y la carpeta `static\` con los archivos del nuevo ZIP
3. Iniciar el servicio: `net start ErpsyncHostAdmin`

## Desinstalacion

Ejecutar **como administrador**:

```
Click derecho en uninstall-service.bat → Ejecutar como administrador
```

Luego eliminar la carpeta `c:\erpsync-host\`.

## Solucion de problemas

| Problema | Solucion |
|----------|----------|
| El servicio no inicia | Verificar que se ejecuto como administrador |
| Puerto en uso | Usar `change-port.bat` para cambiar a otro puerto |
| No conecta al ERP | Verificar credenciales SQL Server y que el servidor sea accesible |
| Panel no carga | Verificar que la carpeta `static\` existe junto al ejecutable |

## Soporte

Para soporte tecnico, contactar al equipo de ERP Sync.
