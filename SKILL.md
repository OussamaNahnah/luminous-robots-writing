---
name: luminous-robots-writing
description: Draft, revise, and review research text on luminous robots, distributed algorithms, and grid exploration, using precise terminology and clear B2 academic English.
---

# Luminous Robots Writing

Use the academic style of *Synthesizing Algorithms to Avoid an Obstacle with a Swarm of Robots* as a reference: introduce the setting explicitly, explain constructions in order, and connect each claim to its evidence. The guidance below is self-contained; the original paper is not needed. The examples are newly written illustrations, not excerpts or research results.

The current draft determines the model, definitions, notation, and claims. Transfer the reference paper's terminology and writing patterns where they fit. For a paper on grids without obstacles, do not introduce an obstacle, bypass scenario, obstacle-position predicate, or obstacle-related restriction. Do not import the reference paper's number of robots, colors, visibility range, scheduler, chirality, initial configurations, or grid-size bounds without support in the draft.

## Reference glossary and conventions

These meanings describe the reference paper. Use them to interpret matching terms, not to replace a consistent definition in a new draft.

| Term or notation | Meaning and distinction |
| --- | --- |
| Luminous robot; myopic robot | A luminous robot has lights with a finite set of colors; in the reference model it has no other memory. Myopic means that its visibility range is bounded. Neither term alone specifies the scheduler, chirality, or exact visibility range. |
| Anonymous grid; uniform robots | The grid has no coordinates accessible to robots; coordinates may still be used in the analysis. Uniform robots execute the same algorithm. Keep anonymity of the environment distinct from uniformity of the robots. |
| Disoriented; common chirality; self-inconsistent | Disoriented robots have no common compass. Common chirality gives shared handedness, without fixing a global orientation: rotated views are indistinguishable. Self-inconsistent robots may use different rotations in different rounds. Do not replace rotation equivalence with reflection equivalence. |
| Look-Compute-Move (LCM); round | Look captures a local view; Compute selects a direction and possible color change; Move performs the movement or leaves the robot idle. In the reference paper, all robots execute these phases in fully-synchronous rounds. A round and an exploration cycle are different units. |
| Grid, node, wall, obstacle | The finite rectangular grid is a graph whose nodes can be occupied by robots. Walls are its borders. An obstacle occupies a node that robots cannot enter. A hole is see-through; a pole is opaque and distinguishable from a wall. An empty node is traversable and is neither a wall nor an obstacle. |
| Local view; configuration; local configuration | A local view is one robot's observation. A configuration gives the contents of the whole grid at a time. A local configuration projects a configuration onto the nodes visible by at least one robot and omits global coordinates; it is not just one robot's view. |
| Initial; reachable; locally defined | Initial configurations are the permitted starting configurations. Reachable configurations occur in executions from those starts. Locally defined initial configurations depend only on robot colors and relative positions; this does not mean arbitrary initial configurations. |
| Algorithm; rule; valid | An algorithm is a tuple of colors, initial configurations, and rules. A rule combines a view, a direction, and an output color. Valid means deterministic, well-defined despite indistinguishable rotations, and exclusive. Exclusivity forbids both shared-node collisions and simultaneous opposite traversal of the same edge. Validity alone does not establish exploration. |
| Execution; perpetual exploration; terminating exploration | An execution is a sequence of configurations after successive LCM rounds. Perpetual exploration requires every relevant node to be visited infinitely often. Terminating exploration requires exploration followed by stopping. A single complete visit does not establish perpetual exploration. |
| Basis algorithm; extension; scenario; goal | A basis algorithm is the algorithm being extended. In the reference construction, an extension retains its rules and includes the required initial configurations. A scenario guides synthesis through goals: pairs of starting and ending local configurations, with bounding boxes, round bounds, and optional mandatory or forbidden nodes. These are method-specific concepts. |
| Candidate; validated; proved | A candidate is a synthesized algorithm awaiting exploration checks. A validated algorithm has passed the specified simulations. A proof may extend the result to other initial configurations and grid sizes. Always state which property and domain each status covers. |
| Cycle; energy; level | An exploration cycle returns to a previously encountered configuration and covers the grid. The reference energy metric counts movements and color changes; a candidate's level groups it by total energy over the goals. Do not confuse this metric with elapsed time, rounds, or physical energy. |

Reference notation, for recognition rather than mandatory reuse:

- `\grid` denotes $\mathcal{G}=(V,E)$; `\columns` and `\lines` denote the numbers of columns and rows, $\mathcal{C}$ and $\mathcal{L}$. The grid size is columns $\times$ rows. The paper uses both “line” and “row”; use “row” consistently in new prose unless the draft establishes another convention. The paper's “side-by-side” means the same row and consecutive columns.
- $n$ is the number of robots, $\phi$ their visibility range, and `\colors` denotes $\mathit{Col}$, the color set. `\algo`, `\init`, and `\reach` denote an algorithm $\mathcal{A}$, its initial configurations $\mathcal{I}$, and its reachable configurations $\mathcal{R}$. An execution is written $e=(\gamma_t)_{t\geq 0}$.
- Subscripts $b$ and $e$ identify basis and extension algorithms. `\candidates` denotes the candidate set $\mathbb{C}$; `\algos` denotes the simulation-validated set $\mathbb{A}$. `\gridSim` and `\initSim` denote the tested grids $\mathbf{G}^{\mathtt{sim}}$ and starts $\mathcal{I}^{\mathtt{sim}}$. Do not silently identify tested sets with their full domains.
- $L$, $R$, and $F$ are color symbols in the reference examples; the leader uses $L$ or $R$ and the follower uses $F$ in one basis algorithm. They are not universal robot identifiers or required colors.

Use American spellings found in the technical prose: “color,” “colored,” “behavior,” and “modeled.” The paper has some spelling and hyphenation variation; normalize new prose without changing command names or quotations. Use lowercase for ordinary terms such as “luminous robots,” “perpetual exploration,” “leader,” and “follower.” Capitalize Look, Compute, and Move when naming phases; introduce Look-Compute-Move (LCM) before using LCM alone. Retain “fully-synchronous” for the reference setting. Expand other acronyms on first use; do not add FSYNC or another scheduler acronym unless the draft uses it. Use “Section,” “Lemma,” “Theorem,” “Table,” and “Fig.” with numbered references, such as `Lemma~\ref{lem:coverage}`. Use “respectively” for short paired statements; the paper also uses “resp.”, “i.e.”, “e.g.”, and “w.r.t.”, but avoid stacking abbreviations.

## Writing patterns by section

### Sentences, vocabulary, and voice

Use direct declarative sentences and familiar verbs: “consider,” “define,” “assume,” “compute,” “generate,” “test,” “reach,” “satisfy,” and “prove.” Keep precise terms such as “chirality,” “indistinguishable,” “exclusive,” and “perpetual exploration”; explain them at first use rather than replacing them with loose synonyms. Aim for clear B2 English in the surrounding prose.

Most explanatory sentences should make one main point. A useful editing target is roughly 15–25 words, not a rule or a measured property of the paper. Keep longer sentences when needed for a quantified definition or theorem; split chains that mix assumptions, actions, and conclusions. Keep each condition next to the statement it restricts. Use explicit nouns when “it,” “this,” or “they” could refer to several objects.

Use “we” for author choices and reasoning: “We consider…,” “We define…,” “We first generate…,” and “We prove…”. Make the robot, algorithm, or tool the subject when describing its behavior. Use passive voice when the object or result matters more than the actor, as in “The candidates are tested…”. Use present tense for definitions and algorithm behavior; past tense suits experiments already performed. Maintain a restrained academic tone. Correct awkward grammar rather than imitating it; replace unsupported “obviously,” “straightforward,” or promotional adjectives with the actual reason or a review flag.

### Introduction and related work

Follow the paper's progression when the material supports it: research setting and task, difficulty, limits of existing approaches, proposed method, then contributions. Introduce the robot model in accessible prose before relying on notation. State concrete contributions with their assumptions and scope. Describe related work by its task, model, and guarantees, keeping citations attached to the claims they support. Do not invent novelty or optimality claims; “to our knowledge” still requires support.

### Model and definitions

Introduce the environment, robot capabilities, execution model, algorithm, and specification before using them in arguments. Prefer “We consider…” for assumptions, “An X is…” for definitions, and “We say that… if…” for a defined property. Introduce the symbol next to the term and explain a tuple's components in order. Use emphasis at a term's first definition when consistent with the draft's LaTeX style.

Keep neighboring definitions distinct: an algorithm is not an execution; a local view is not a global configuration; valid is not exploration-correct. State quantifiers and the initial-configuration domain explicitly. Preserve “if” versus “if and only if,” “at most” versus “less than,” and existential versus universal claims. If definitions conflict, report the conflict instead of choosing a new model.

### Method and algorithm descriptions

State the objective and inputs, then explain the construction in execution order. The paper repeatedly uses “First…,” “Then…,” “Once…,” and “Finally…” to connect phases. Explain what each phase consumes, produces, and guarantees. Distinguish a designer's choices from automated steps. Use a short enumeration for several stages or constraints, not for every sentence.

For robot behavior, give the condition before the response: when a robot sees a wall, which rule applies, how it moves or changes color, and how exploration resumes. Introduce an example or figure after the general rule. Name limits on search or simulation explicitly. Do not describe a bounded or filtered search as generating all possible algorithms without the relevant restriction.

### Results and discussion

Give the experimental setting and tested domain before interpreting the results. Report quantities with their objects and units: candidates generated, algorithms retained, grids and starts tested, rounds, and durations. Link table or figure references to the specific observation. Follow the paper's pattern of reporting an observation and then explaining the algorithm behavior behind it, when that explanation is supported.

Separate synthesis, simulation validation, proof, and classification. Use “The simulations show… on the tested grids” for evidence with that scope. Use “By Lemma…” or “Theorem… establishes…” only for supplied results. A repeating cycle can establish perpetual behavior for a deterministic fixed instance if it repeats the full configuration and covers every required node; a long run or a position-only repetition is insufficient. Do not invent a cycle certificate when the draft supplies only observations. Comparisons of paths, rounds, or energy measured in simulations retain the tested scope.

### Lemmas and proofs

Start a statement with the objects and assumptions, often “Let…,” followed by the claim. Keep theorem statements separate from their arguments. In proofs, name the technique, fix the objects, handle cases explicitly, and finish by connecting the argument to the exact claim. Use “Indeed,” “By Lemma…,” “Hence,” and “Thus” to mark a reason or consequence, not to hide a missing step.

The reference proof first extends the set of initial configurations, then the grid sizes. Reuse that organization only when the new argument has those obligations. For induction, name the parameter, base cases, induction hypothesis, construction, and property preserved. The reference adds pairs of rows or columns because parity matters; this is not a default step size for another algorithm. In a local indistinguishability argument, identify which views agree, for how long, and why that implies the same actions. For contradiction, state the contrary assumption, construct an allowed execution, and identify the specification it violates. Use “without loss of generality” only with a justified symmetry. A proof sketch may summarize supplied reasoning, but must not present a missing proof as complete.

## Newly written before-and-after examples

### Model definition

Before:

```latex
On a grid without obstacles and with at most one robot per node, a \emph{configuration} is given by a mapping $\gamma:V\to\{\emptyset\}\cup\mathit{Col}$ which says what is on every node, with $\emptyset$ for an empty node and $c\in\mathit{Col}$ for a robot whose color is $c$.
```

After:

```latex
On a grid without obstacles and with at most one robot per node, a \emph{configuration} is a mapping $\gamma:V\to\{\emptyset\}\cup\mathit{Col}$. The value $\emptyset$ denotes an empty node, and $c\in\mathit{Col}$ denotes a node occupied by a robot of color $c$.
```

This revision places the term and notation together, then explains the values without changing the occupancy assumptions.

### Method description

Before:

```latex
We do the generation of candidates in $\mathbb{C}$ using the fixed rule set and after this we do simulations on $\mathcal{T}$, and the fact that a candidate passes these tests is only evidence for the tested instances, as discussed in Section~\ref{sec:validation}.
```

After:

```latex
We first generate the candidates in $\mathbb{C}$ from the fixed rule set. Then, we test them by simulation on $\mathcal{T}$. Passing these tests provides evidence only for the tested instances, as discussed in Section~\ref{sec:validation}.
```

This revision uses ordered actions and direct verbs while preserving the stated limit of simulation evidence.

### Proof paragraph

Before:

```latex
Let $e$ be an execution from $\gamma\in\mathcal{I}$ and suppose every such execution reaches $\mathcal{J}$ in finite time, and since Lemma~\ref{lem:suffix} says that every execution from $\mathcal{J}$ visits every node infinitely often, we can say the same about $e$ because its finite prefix does not affect infinitely many visits.
```

After:

```latex
Let $e$ be an execution from $\gamma\in\mathcal{I}$. By assumption, every such execution reaches $\mathcal{J}$ in finite time. By Lemma~\ref{lem:suffix}, every execution from $\mathcal{J}$ visits every node infinitely often. Hence, the same holds for $e$, since removing a finite prefix does not affect infinitely many visits.
```

This revision separates the assumption, cited result, and conclusion while retaining the universal claim and its justification.

## Drafting and revision rules

- Use the supplied draft and its accompanying definitions and results as the source of technical truth. Preserve new terms and notation that it defines and uses consistently, even when they differ from this glossary. If context is missing, draft only what is supported and flag the missing assumption or definition.
- Preserve technical meaning: quantifiers, bounds, resource counts, scheduler, visibility, orientation, memory, collision rules, initialization, and the claimed domain. Do not strengthen, weaken, or repair a claim silently. Flag an unsupported statement for author review; distinguish a suggested correction from an established fact.
- Keep LaTeX commands, custom macros, labels, citation keys, cross-reference targets, equations, and mathematical notation intact. Preserve command structure and technical arguments; edit prose arguments only as needed for the requested wording. Retain environments, nonbreaking spaces in references, and meaningful comments. Do not introduce a macro that the draft does not define. Propose any necessary technical or structural LaTeX change separately.
- Keep assumptions, definitions, observed results, proved results, and conjectures identifiable. Preserve both positive claims and explicit limits. Simulation evidence does not become a theorem about all grid sizes through a change of wording. If simulation supplies a proof's finite base cases, retain the tested instances, verification criterion, and separate generalization argument.
- For a new section, use the existing draft's terminology and section conventions. Do not invent citations, experimental numbers, lemmas, invariants, or proof steps. Refer to needed evidence in a separate author note rather than inserting fabricated content into paste-ready text.
- Before returning a rewrite, compare it against the input for changed assumptions, scope, claim strength, mathematical content, and LaTeX tokens. Check that every “therefore” has a supplied reason and that simulation findings retain their limits.

## Output

For a rewrite or draft, return paste-ready LaTeX in a fenced `latex` block, keeping commentary outside it. Follow the user's requested scope. Put technical ambiguities or unsupported claims in a separate short note that identifies the passage and the question needing author review. If there are none, omit the note. Do not silently resolve them in the LaTeX.

For a review, identify each relevant passage by its section, label, or a short quotation. Explain the specific language or technical issue and suggest a concrete edit, with LaTeX where useful. Distinguish wording improvements from changes that require the author's technical judgment. Do not present stylistic preference as a correctness error.
