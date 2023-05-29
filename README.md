# PD_03_E1

Comando para cargar csv:

LOAD CSV FROM "file:///soc-sign-bitcoinalpha.csv" AS line
MERGE (a:user {id: line[0]})
MERGE (b: user { id: line[1]})
MERGE ((a)-[:rate{cost: toInteger(line[2])}]->(b))


Comando para ejecutar el algoritmo:

CALL gds.graph.project( 'mygraph','user', 'rate',{ relationshipProperties: toInteger('cost') }
) YIELD
  graphName, nodeProjection, nodeCount, relationshipProjection, relationshipCount, projectMillis




MATCH (source:user {id: '10'}), (target:user {id: '20'})
CALL gds.shortestPath.dijkstra.stream('mygraph', {
   sourceNode: id(source),
   targetNode: id(target)
})
YIELD nodeIds, costs
RETURN [id IN nodeIds | gds.util.asNode(id).id] AS path, costs;





