
Jason's Notes:

“Agent Define” the Code Base

- Help on-board faster
- Teach developer and/or agent each new code base
- PR comes out it takes a lot of time / workflows to get through 
- Agent generated code has to be reviewed by humans

How can I make the coding agent really efficient so that it can understand the code base better.

If I have all PRs and all commits and JIRA tickets can the agent/human understand the code history faster.

Can we then use this to find code patterns when designing a new feature or task.  

Alternatives to Neo4J Algorithms
- Cremlin Queries 
- Auto Graph Framework 


General Ideas
- Multiple graphs
    - Repo Graph to relate services together
    - JIRA Graph 
    - Memory Bank Graph 
- Graphs within graphs
- Graphs that morph into other graphs
- Merging graph nodes

Ebay Laptop will be available once we have a contract
Funding will come after that 


Chris's Notes:

agentifying codebase
* limited time for massive/huge legacy codebase
* costly feature development (year+ including A/B testing)
* can I observe codebase and see patterns of commits to learn from (features, style, cross-team collabs,...)
* code review/approval is major blocker
---less cycles and review faster?
* problem statement: how can I make coding agent really efficient in a way that understands the codebase better? (commits, JIRA tickets,...)
Proposal
* not implement immediately at eBay, but show alignment
* research problem (i.e., Jason takes 3 different techniques, which makes coding agent most efficient, submit back to eBay and can learn from it)
* is there anything they can extend from what we are building
Constellize?
* can memory bank approach be used?
* architectural considerations (microservices, connection to other codebases, feature development spans codebases, etc).
* Meeting with Dr. A?
* novelty (directory of memory banks in repos, how to solve problems and allow coding agent to traverse memory banks, PRs and JIRA tickets to determine what changed, etc.)
Research
* brainstorming
* idea that can be impactful at eBay
* multiple graphs (pointers to other graphs, morph/flip based on context?---Jira vs features vs...)
* Neo4J (agents interacting with graphs)