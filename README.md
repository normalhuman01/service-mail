# Service Mail

Este servicio proporciona un sistema de envío de correos electrónicos con integración de RabbitMQ y MailDev. Es ideal para entornos de desarrollo y pruebas.

## Preparación del Entorno

### Requisitos Previos
- Docker y Docker Compose
- Node.js y Yarn

### Instrucciones para Ejecutar

1. **Iniciar servicios con Docker**
   Ejecuta `docker-compose up -d` para iniciar MailDev y RabbitMQ.

2. **Instalar dependencias**
   Ejecuta `yarn` para instalar las dependencias necesarias.

3. **Iniciar el servicio en modo depuración**
   Ejecuta `yarn start:debug`. En este modo, se utilizará el archivo `./nodemon-debug.json`.

### Configuración

- **Variables de entorno**: Encuentra las variables de entorno en el archivo `.env.dist`. Configúralas según tus necesidades.
- **Directorio de configuración**: `./config`.
- **Directorio de plantillas**: `./templates`. Las plantillas se copian automáticamente al directorio `dist` después de ejecutar `yarn build`.

## Interfaz de Usuario

- **RabbitMQ UI**
  - **Host**: http://localhost:15672
  - **Username**: onsweb-mail
  - **Password**: password

- **MailDev UI**
  - **Host**: http://localhost:1080
  - **Username**: admin
  - **Password**: password

## Uso

Envía mensajes a través de RabbitMQ utilizando el siguiente formato JSON:

```json
{
  "templateName": "nombre_plantilla",
  "to": "destinatario@example.com",
  "data": {
    "subject": "Asunto",
    "exampleParameter": "Valor de ejemplo"
  },
  "language": "en",
  "from": "remitente@example.com",
  "cc": ["cc@example.com"],
  "bcc": ["bcc@example.com"],
  "attachments": [
    {
      "filename": "archivo.zip",
      "content": "BASE64_STRING",
      "encoding": "base64",
      "contentType": "application/zip"
    }
  ]
}
```

## Notas Adicionales

- **Intercambio en RabbitMQ**: Utiliza el nombre `send-email`, definido en `./src/lib/amqp/exchange.enum.ts` como `mailExchange`.
- **Plantillas de Correo**: Actualmente soportamos plantillas simples como `test`, `default` y `new-document`.



