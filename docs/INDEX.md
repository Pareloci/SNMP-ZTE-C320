# ZTE C320 - Documentación del índice interno de ONUs

## Objetivo

Documentar el formato del índice utilizado por las tablas privadas del árbol:

1.3.6.1.4.1.3902.1012.3

Este índice es utilizado de forma consistente por las tablas:

- 28
- 30
- 31
- 32
- 50

permitiendo relacionar toda la información perteneciente a una misma ONU.

---

## Estructura observada

Las entradas de las tablas utilizan un índice compuesto por dos partes.

Ejemplo:

268503808.6

donde

268503808  -> índice interno del puerto GPON

6          -> ONU-ID

---

## Ejemplo

ONU física

gpon-onu_1/1/11:6

produce índices como

.28.1.1.1.268503808.6

.30.1.1.2.268503808.6.1

.31.4.1.7.268503808.6

.32.5.1.3.268503808.6.1

.50.11.2.1.1.268503808.6

Por lo tanto:

Índice GPON = 268503808

ONU = 6

---

## Otros ejemplos encontrados

Puerto GPON     Índice

1/1/1           268501248

1/1/2           268501504

1/1/7           268502784

1/1/11          268503808

Todos utilizan exactamente el mismo formato.

---

## Relación entre tablas

La misma ONU puede localizarse simultáneamente en:

Tabla 28

268503808.6

↓

Tabla 30

268503808.6.1

↓

Tabla 31

268503808.6

↓

Tabla 32

268503808.6.1

↓

Tabla 50

268503808.6

Esto confirma que todas las tablas describen el mismo objeto lógico (ONU).

---

## Índice secundario

Las tablas 30 y 32 agregan un índice adicional.

Ejemplo

268503808.6.1

donde

268503808 -> Puerto GPON

6          -> ONU

1          -> GEM / VPORT / Puerto Ethernet (según la tabla)

Este tercer índice deberá conservarse durante el procesamiento del exporter.

---

## Hipótesis actual

Hasta este punto del proyecto se confirma que:

• El índice GPON identifica unívocamente un puerto PON.

• El segundo índice identifica la ONU.

• El tercer índice identifica un recurso interno dependiente de la ONU
(GEM Port, VPORT o puerto Ethernet).

La codificación exacta utilizada para obtener el valor
268503808 aún no ha sido determinada.

Sin embargo, no es necesario conocer dicha codificación para construir
el SNMP Exporter, ya que basta con utilizar el índice completo como clave
de correlación entre tablas.

---

## Estado

✔ Confirmado experimentalmente

✔ Utilizado por tablas 28,30,31,32 y 50

✔ Puede emplearse como índice principal del exporter

Pendiente:

- Descifrar la codificación del índice GPON.
- Verificar si el Frame forma parte del cálculo.
- Determinar si existen diferencias entre tarjetas GPON y XG-PON.
