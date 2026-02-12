# Kallisti-theory-of-mind
Python package. Lets user plug in vectorized data about situations, states, and get cognitively-motivated predictions of actions. and theory-of-mind inferences, using ACT-R style memory and similarity-based retrieval.

The package will have 3 to 4 pieces 

Dimensionality reduction first: 
- - Same package, different module. 
- - We use it as a processing step before the data enters memory. 
- - We feed information to brain voxels/vectors. 
- - Dimensionality reduction compresses into a smaller vector. 
- - The vector becomes the feature for storage to memory.

1. Similarity Utility Module (similarity.py) 
Note goal: Defines how we measure similarity between vectors. When an agent tries to recall a memory, similarity asks how similar this new situation is to the past situation. 
- - Cosine similarity → measures angle between two vectors.
- - Dot product → how much the vectors point in the same direction 
- - Euclidean distance → how far apart they are the geometric distance between the vectors 
- - Correlation → ignores magnitude focuses on shape, it is applicable i think for pattern similarity not like absolute values 

2. Memory module with ACT-R-like activation
Note goal: Takes a new situation (feature vector), retrieves similar past experiences based on both recency and relevance, and uses them to score possible actions.
- - How memories are stored and retrieved - we define memory first
  - Experiences are stored as traces grouped by action.
  - Each trace contains: feature vector, reward, timestamp, and adaptive decay parameter.
  - Retrieval operates over traces associated with each candidate action.
- - ACT -R principle that retreaval depends both on recency and relavance
  - Retrival strength depends on recency / frequency (base-level activation)as well as relevance to the current query (cosine similarity)
- - Base level activation (power law recency)
  - Recent traces contribute more than older traces.
  - Activation follows ACT-R–style power-law decay.
  - Weights on each trace w<sub>i</sub>​=(t−t<sub>i</sub>​)^(-d<sub>i</sub>)
  - Overall base level activation

    <img width="295" height="162" alt="Screenshot from 2026-02-12 14 30 42@2x" src="https://github.com/user-attachments/assets/1d9fe59e-2356-4df5-81be-5a7878c9821a" />

- - Similarity between query and stored features 
- - Scores actions from retrieved instances 

2. Agent module
Note goal: Agent uses that memory to choose action - we define the agent that's going to use that memory.
- - Similarity to past experiances
- - Base-level decay
- - Reward in memory
- - Maximum activation
- - SoftMax choice (probilistic)
- - RL learning through experiance

3. ToM (theory of mind module)
Note goal: Allows agent to go beyond its belief and simulate another agents belief or decisions.
- - Learning another agents preference
- - Predicting feuture actions
- - Detecting changes in strategy
- - Reasoning about deception or hidden moves 
