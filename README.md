# sim-elh-explainer-to-text
# Full Prompt

Input structure:
You are given 2 things:
1. Graph: A pair of knowledge graphs.
2. Explanation: A list of structured tuples that shown similarity scores and the reason how the score was calculated from:
[A*parent node][B*parent node] —> (1. Final similarity score, 2. {parent node A}, 3. {relationship from A}, 4. {existing duplicated embeddings})
[A*leaf node][B*leaf node] —> (1. Similarity score, 2. {node A}, 3. {relationship from A}, 4. {existing duplicated embeddings})
[A*leaf node][B*leaf node]—> (1. Similarity score, 2. {node A}, 3. {relationship from A}, 4. {existing duplicated embeddings}) and so on (if any).
Note:
1. [A][B] means comparing from  Graph A to Graph B. 
2. We can have more than one parent node, node, relationship, and embeddings.
Example of input structured tuples:
[G1*ActivePlace][G2*Mangrove] —> (0.62, {G1*Place},{∃{G1*canWalk, G1*canMoveWithLeg}.Trekking,∃G1*canTravelWithSail.Kayaking}, {canMoveWithLeg, canTravelWithSail})
[G1*Trekking][G2*Trekking] —> (1.0, {G1*Trekking}, { } , { } )
[G1*Kayaking][G2*Trekking] —> (0.97, {G1*Kayaking}, { } , {Kayaking,Trekking } ) 
Output format (Must Follow This Format Exactly):
ActivePlace and Mangrove are 62% similar meaning. 
Summary Explanation: They are 62% similar because
Their Top Parent node comparison: 1 of 1 matched 100%
Their Path comparison: 1 of 2 matched 100%
Detailed Explanation: They are 62% similar because
They share top parent node: Place (100% match)
They share exactly the same “path” from Graph ActivePlace to Graph Mangrove:
100% match: (Place, {canWalk, canMoveWithLeg}, Trekking) and (Place, {canWalk, canMoveWithLeg}, Trekking)
They share the similar “path” from Graph  ActivePlace to Graph Mangrove:
97% match: (Place, {canSail}, Kayaking) and (Place, {canWalk, canMoveWithLeg}, Trekking) 
Table Explanation:
#, "Node or Path from
Graph 1: ActivePlace" "Node or Path from
Graph 2: Mangrove" "Similarity
Result" Embeddings value
1 Place Place Same
2 (Place, {canWalk, canMoveWithLeg}, Trekking) (Place, {canWalk, canMoveWithLeg}, Trekking) Same
3 (Place, {canSail}, Kayaking) (Place, {canWalk, canMoveWithLeg}, Trekking) 97% {Kayaking, Trekking}
Your task: generate a friendly, human-readable explanation based on the input below, using the exact format provided.
Input:
