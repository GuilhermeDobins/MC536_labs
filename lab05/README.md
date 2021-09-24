# Lab05 - Marcadores e Taxonomia em Cypher


# Aluno
* 236129: Guilherme Zeferino Rodrigues Dobins

## Tarefa de Cypher sobre Marcadores e Taxonomia

## Tarefa 1

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, sem considerar as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador) -[:Pertence]->(c:Categoria {id:"Serviços"})
RETURN m, c
~~~

## Tarefa 2

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, considerando as categorias subordinadas.

### Resolução
~~~cypher
MATCH (csub1:Categoria)-[:Superior]->(csup1:Categoria {id:"Serviços"})
MATCH (csub2:Categoria)-[:Superior]->(csup2:Categoria)
MATCH (m: Marcador)-[:Pertence]->(c:Categoria)
WHERE ((csup2.id=csub1.id OR csup2.id=csup1.id) AND (c.id=csup1.id OR c.id=csub1.id OR c.id=csub2.id))
RETURN m,c,csub1, csub2
~~~