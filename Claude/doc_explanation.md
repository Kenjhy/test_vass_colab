https://claude.ai/code/artifact/68dc9e63-6182-44e4-8cb3-8f984ce203d3


Ya con el notebook resuelto (PRUEBACANDITATO_4.ipynb, celdas 7-8), esto es lo que encontré y cómo se corrigió:

1. Duplicados — tabla pedidos, columna pedido_id

Valor problemático: 91 filas con pedido_id repetido (1270 filas totales, solo 1179 pedido_id únicos).
Por qué: un mismo pedido contado varias veces infla las ventas al sumar total_neto.
Línea que lo resolvió (celda 8): pedidos_limpio.drop_duplicates(subset=['pedido_id'], keep='last')
2. Categorías inconsistentes — columna pais_envio

Valores originales: [' Colombia ', 'Argentina', 'COL', 'Chile', 'Colombia', 'Ecuador', 'México', 'Perú', 'colombia'] — "Colombia" aparece como 4 variantes distintas (espacios, minúsculas, sigla "COL").
Por qué: al agrupar por país, cada variante cuenta como un país distinto y reparte mal las ventas de Colombia.
Línea que lo resolvió (celda 8): pedidos_limpio['pais_envio'].astype('string').str.strip().str.lower().replace({'col': 'colombia'}).str.title()
3. Categorías inconsistentes — columna canal

Valores originales: ['TIENDA_FISICA', 'Tienda_Fisica', 'marketplace', 'mobile', 'tienda fisica', 'tienda_fisica', 'web'] — "tienda física" en 4 formatos distintos.
Por qué: mismo problema que el país, distorsiona el ranking de canales.
Línea que lo resolvió (celda 8): pedidos_limpio['canal'].astype('string').str.strip().str.lower().replace({'tienda fisica': 'tienda_fisica'})
4. Nulos — columna total_neto

Valor problemático: 51 filas con total_neto nulo (detectado con pedidos['total_neto'].isna().sum() en la celda 7).
Por qué: no se rellenaron con un valor inventado (habría alucinado ventas); se descartaron por no ser confiables.
Línea que lo resolvió (celda 8): pedidos_limpio.dropna(subset=['pedido_id', 'fecha_pedido', 'pais_envio', 'canal', 'total_neto'])
Resultado: de 1270 filas originales quedaron 1136 filas limpias, cada una con un pedido_id único, país y canal normalizados, y total_neto válido.