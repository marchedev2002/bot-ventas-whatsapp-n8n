# Estructura de la planilla (Google Sheets)

Datos de ejemplo ficticios.

| Hoja | Columnas | Uso |
|---|---|---|
| **STOCK** | RESPONSABLE, LUGAR, MARCA, MODELO, CODIGO, PESO, PRECIO_MAYORISTA, PRECIO_MINORISTA, FORMA, TIPO, LINK, DOLAR, ESTADO | Una fila por paleta física. `ESTADO` = DISPONIBLE / VENDIDA |
| **PEDIDOS** | FECHA, TELEFONO, MODELO, CANTIDAD, TIPOCLIENTE, RESPONSABLE, CODIGO, NUMERO_VENTA, ESTADO_ENVIO, NUMERO_SEGUIMIENTO | Una fila por paleta vendida. Dispara la notificación al dueño |
| **MAYORISTAS** | CODIGO, TELEFONO, NOMBRE, APELLIDO | Si el teléfono está acá, el cliente es mayorista |
| **EN CAMINO** | MODELO, PRECIO, LINK, FECHA | Mercadería próxima a ingresar |
| **RECLAMOS** | (según flujo) | Reclamos derivados a un humano |
| **LOCKS** | TELEFONO, LOCKED, UPDATED_AT | Mutex por cliente |
| **CHATWOOT** | TELEFONO, CONTACT_IDENTIFIER, CONVERSATION_ID | Mapeo cliente ↔ conversación |
| **CONTACTOS DESACTIVADOS** | TELEFONO, NOMBRE, APELLIDO | Contactos a los que el bot no responde |
| **RECUENTO STOCK** | MARCA + MODELO, CANTIDAD | Calculada con `QUERY` sobre STOCK (solo DISPONIBLE) |
| **CONTROL PRECIOS** | PALETA, PRECIO MAYORISTA, PRECIO MINORISTA, CANTIDAD, ALERTA | Informativa: detecta precios distintos para un mismo modelo |

Ejemplo de `QUERY` de RECUENTO STOCK:

```
=QUERY(STOCK!A:M; "select C, D, count(D) where M='DISPONIBLE' group by C, D label count(D) 'CANTIDAD'"; 1)
```

Ejemplo de alerta en CONTROL PRECIOS:

```
=ARRAYFORMULA(IF(A2:A="";"";IF(COUNTIF(A2:A;A2:A)>1;"⚠ PRECIOS DISTINTOS";"")))
```
