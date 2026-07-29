---
title: Special Issue Proposal — The Semantics of Economic Modelling
authors:
  - name: Society for Computational Economics Working Group on Language and Formal Semantics
abstract: |
  We propose a special issue of ⟨journal name⟩
  on the semantics of economic modelling, that is, statements of what
  model files, toolkits, and estimation specifications mean, fixed
  independently of any solver. Each paper supplies a semantic ontology — a
  syntax, an inventory of the economic objects a representation admits,
  and a map from what is written to those objects — and applies it to
  worked examples. A jointly written comparison paper closes the issue.
exports:
  - format: pdf
    template: ../templates/plain_latex_wide
    output: special-issue-proposal.pdf
  - format: tex
    template: ../templates/plain_latex_wide
    output: special-issue-proposal.tex
---

# Special Issue Proposal — The Semantics of Economic Modelling

## Introduction and Proposal

When economists compute an applied model, its precise *meaning* is distributed, much of it implicitly, across prose, notation, calibration, and code. The paper says "we solve the following model", but its equations underdetermine what its code computes, leaving the reader to fill the gaps from professional convention. The same gaps confront whoever rebuilds the model — to replicate it, to extend it, or to solve it in another toolkit — since every rebuild starts from the same underdetermined description. This means that without a statement of the model's meaning to check against, computational results are hard to cross-verify, and interoperability between implementations becomes difficult.

**Semantic ontologies** are a formal way to codify the meaning of computational models. For our purposes, a semantic ontology consists of the theoretical objects and relations within the model, the computational representations of those objects and relations, and the written forms that record them (a file, a model write-up, a specification), which together constitute a syntax.[^ha] Theory supplies part of the ontology — a general-equilibrium model's objects are precisely defined — but the semantic ontology must map those objects and relations concretely to computational objects and written forms, and state the assumptions under which the mapping holds. Without a written semantic ontology, nothing says which of the theory's objects a given file or function call stands for, and ordinary solver code gives one executable realisation, not a solver-independent statement of what the representation denotes.

While ontologies often stay implicit within a discipline, the proliferation of AI used to write, modify, and translate modelling code makes leaving them unstated costly. Language models already do all three. However, *interpreting or verifying their output requires a statement, independent of the code, of which economic objects are computed and which relations among them enforced.* The same statement turns translation between toolkits, and even the generation of new modelling research, into operations a language model can perform and be checked on, rather than into manual recoding.[^mmb]

Economics is not the first field to need a semantic ontology: manufacturing's Process Specification Language (Grüninger and Menzel 2003; Bock and Grüninger 2005), Modelica for physical systems (Fritzson and Engelson 1998; Modelica Association 2023), planning's PDDL2.1 (Fox and Long 2003), and neuroscience's NeuroML (Gleeson et al. 2010) each attach an explicit, solver-independent meaning to a model representation. Industry has met the same need from the opposite direction, reconstructing never-written conceptual models of the business from its data (AWS Database Blog 2026). Compared with all of these, economics is well placed, because the relations among a model's objects are the theory itself — stated in the paper, but not systematically attached to the files and function calls that compute it.

**Our proposal.** We propose a special issue that collects semantic ontologies for model languages, toolkits, and estimation methods of computational economics. Each paper takes one language, toolkit, or estimation method, states its semantic ontology, and demonstrates it on worked examples of the team's own choosing. The SCE working group will submit a subset of the papers, an open call will invite the rest, and a comparison paper, written jointly by the participating teams, closes the issue.

<!-- [^example]: For example, the sentence "a policy shock raises entrants at date $t$" is satisfied by two different models — the shock may reach the cross-sectional distribution at $t$ or at $t+1$ — and the impulse response differs before any grid or solver is chosen. The code computes one of the two models, and nothing on the page records which. The documented counterpart: Su and Judd (2012) recast one estimator in two computational formulations and return identical estimates, while Dubé, Fox and Su (2012) show a loose inner-loop tolerance changing estimated own-price elasticities by roughly a factor of two. -->

[^ha]: In a heterogeneous-agent model, for instance, the ontology contains the response of decision rules to prices, the cross-sectional distribution decisions induce, and the feedback of that distribution into prices — as relations of the theory and as their computational counterparts.

[^mmb]: The nearest precedent in economics, the Macroeconomic Model Data Base (Wieland et al. 2012), compares models under common variables, common shocks, and a menu of common policy rules while each model keeps its own equations; it standardises comparison, not meaning.

## Guidelines for Articles

An article in the special issue may address a modelling language, a toolkit, an estimation method, a model class, or a combination of these, and works its semantic ontology through at least one example model of its own choosing:

```{raw} latex
\begin{displaybox}[breakable]{Paper areas}
```

- **Modelling languages.** A modelling language is a fixed grammar in which a complete model is written as a file, as in Dynare's model language or Dolo's YAML model files.
- **Toolkits.** A toolkit is a collection of construction calls and classes from which a model is assembled in a programming language, as in HARK's agent classes, the sequence-space Jacobian toolkit (Auclert et al. 2021), or the VFI Toolkit.
- **Estimation methods.** An estimation method is a procedure that computes parameter estimates from a model and data, as in the simulated method of moments or indirect inference.
- **Model classes.** A model class is a family of models built from the same kinds of objects, as in heterogeneous-agent macroeconomies or overlapping-generations economies.

```{raw} latex
\end{displaybox}
```

Every paper considers the components of a semantic ontology relevant to its area of study, choosing from the common format given in Appendix A. The format has five elements: what is written down (the syntax), what is assumed to exist (the ontology), and what stands for and relates to what (the denotation) are the components of a semantic ontology; when the interpretation holds (well-posedness) and what preserves it (equivalence, adequacy, and convergence) are statements about it.

The formalism in which a paper states these components is also not fixed in advance. Where the subject has a syntax, the denotation can be stated in any of the semantics developed for programming languages: denotational semantics assigns to each written form the mathematical object it stands for, using the ordered structures of domain theory (Scott and Strachey 1971); operational semantics defines meaning by rules specifying how a representation executes on an abstract machine (Plotkin 1981); axiomatic semantics defines meaning by the assertions that hold before and after execution (Hoare 1969). An ontology stated without a syntax can be axiomatised in a formal logic, in current practice a description logic (Gruber 1993; Baader et al. 2017), drawn as an entity-relationship or UML class diagram (Chen 1976; Berardi, Calvanese and De Giacomo 2005), or recorded as a knowledge graph (Hogan et al. 2021).

Whichever formalism a paper adopts, the mathematics is already common ground: the Bellman equation is not in question, while what a given Dynare file or HARK model means is. For a language, a toolkit, or an estimation method, the semantic ontology therefore states the map from representations and procedures to the mathematical objects they stand for; a model-class paper states the objects and relations of the mathematics itself. Where the stated ontologies differ across papers, the difference is itself a result for the closing comparison to report.

## Organisation

Papers pass an internal review within the working group [process TBC] and then the journal's ordinary external refereeing. We expect six to eight papers, with a session at the Society's conference between submission and revision.

### Teams and Editors

The working group's members include developers of Dynare, HARK, and the VFI Toolkit. Committed teams: [to be listed — only teams that have agreed in writing]. The working group's papers will come from its subgroups. Akshay Shanker and Matthew McKay chair the working group and coordinate the teams and the internal review. The guest editors (a lead editor and at least one co-editor, neither submitting to the issue) are drawn from outside the working group [names, institutions — TBC]. Papers are submitted through the journal's editorial system, marked for this special issue, and are refereed under the journal's ordinary standards; the guest editors handle every paper, including the comparison paper, subject to the journal's final editorial authority.

### Timeline

Calendar dates TBC on acceptance.

- Call for papers [on acceptance]
- Submissions [+9 months]
- Internal review completed [+12 months; process TBC]
- Referee reports [+15 months]
- Revisions and the comparison paper [+24 months]

## References

Auclert, A., B. Bardóczy, M. Rognlie, and L. Straub (2021). "Using the Sequence-Space Jacobian to Solve and Estimate Heterogeneous-Agent Models." *Econometrica* 89(5), 2375–2408.

AWS Database Blog (2026). "Build a semantic ontology to power AI assistants on AWS — Part 1." 14 July 2026. Accessed 29 July 2026.

Baader, F., I. Horrocks, C. Lutz, and U. Sattler (2017). *An Introduction to Description Logic*. Cambridge University Press.

Berardi, D., D. Calvanese, and G. De Giacomo (2005). "Reasoning on UML Class Diagrams." *Artificial Intelligence* 168(1–2), 70–118.

Bock, C., and M. Grüninger (2005). "PSL: A Semantic Domain for Flow Models." *Software and Systems Modeling* 4, 209–231.

Chen, P. P. (1976). "The Entity-Relationship Model — Toward a Unified View of Data." *ACM Transactions on Database Systems* 1(1), 9–36.

Dubé, J.-P., J. T. Fox, and C.-L. Su (2012). "Improving the Numerical Performance of Static and Dynamic Aggregate Discrete Choice Random Coefficients Demand Estimation." *Econometrica* 80(5), 2231–2267.

Fox, M., and D. Long (2003). "PDDL2.1: An Extension to PDDL for Expressing Temporal Planning Domains." *Journal of Artificial Intelligence Research* 20, 61–124.

Fritzson, P., and V. Engelson (1998). "Modelica — A Unified Object-Oriented Language for System Modeling and Simulation." In *ECOOP '98 — Object-Oriented Programming*, Lecture Notes in Computer Science 1445. Springer, 67–90.

Gleeson, P., S. Crook, R. C. Cannon, M. L. Hines, G. O. Billings, et al. (2010). "NeuroML: A Language for Describing Data Driven Models of Neurons and Networks with a High Degree of Biological Detail." *PLoS Computational Biology* 6(6), e1000815.

Gruber, T. R. (1993). "A translation approach to portable ontology specifications." *Knowledge Acquisition* 5(2), 199–220.

Guarino, N., D. Oberle, and S. Staab (2009). "What Is an Ontology?" In S. Staab and R. Studer (eds.), *Handbook on Ontologies*, 2nd ed. Springer, 1–17.

Grüninger, M., and C. Menzel (2003). "The Process Specification Language (PSL): Theory and Applications." *AI Magazine* 24(3), 63–74.

Harel, D., and B. Rumpe (2004). "Meaningful modeling: what's the semantics of 'semantics'?" *Computer* 37(10), 64–72.

Hoare, C. A. R. (1969). "An axiomatic basis for computer programming." *Communications of the ACM* 12(10), 576–580.

Hogan, A., E. Blomqvist, M. Cochez, C. d'Amato, G. de Melo, et al. (2021). "Knowledge Graphs." *ACM Computing Surveys* 54(4), article 71.

Modelica Association (2023). *Modelica Language Specification*, version 3.6. https://specification.modelica.org.

Plotkin, G. D. (1981). *A Structural Approach to Operational Semantics*. Report DAIMI FN-19, Computer Science Department, Aarhus University.

Scott, D., and C. Strachey (1971). "Toward a mathematical semantics for computer languages." *Proceedings of the Symposium on Computers and Automata*, Polytechnic Institute of Brooklyn, 19–46.

Su, C.-L., and K. L. Judd (2012). "Constrained Optimization Approaches to Estimation of Structural Models." *Econometrica* 80(5), 2213–2230.

Wieland, V., T. Cwik, G. J. Müller, S. Schmidt, and M. Wolters (2012). "A new comparative approach to macroeconomic modeling and policy analysis." *Journal of Economic Behavior & Organization* 83(3), 523–541.

```{raw} latex
\appendix
```

## The Common Format

A paper answers those of the following five questions relevant to its area of study. The first three answers are the components of its semantic ontology; the last two are statements about it — when the interpretation holds, and what preserves it:

```{raw} latex
\begin{displaybox}[breakable]{The common format}
```

1. **Syntax: what is written down.** The set of legal written forms: the model file, the sequence of construction calls, or the specification of an estimation exercise. A language has a full grammar; a toolkit may expose construction calls or classes; an estimation method may have no written form at all, in which case constructing the syntax is itself part of the contribution.
2. **Ontology: what is assumed to exist.** The kinds of economic entity and relation the representation commits to — agents, states, shocks, timing, the equilibrium concept, and which objects determine which — together with the criteria for when two of them are the same (Gruber 1993; Guarino, Oberle and Staab 2009). The ontology is stated in its own terms, without reference to the syntax.
3. **Denotation: what stands for what.** The stated relation between the ontology's objects and their computational representations — value functions on stated spaces, transition operators, systems of equations in sequence space, population parameters — and between those representations and the written forms: each written form stands for its object under an explicit map (Harel and Rumpe 2004). Where a representation is assembled from parts, the map is compositional, the meaning of the whole following from the meanings of the parts.

*The last two answers are not components of the semantic ontology; they are statements about it:*

4. **Well-posedness: when the interpretation holds.** The conditions under which the denotation is well defined: domains, units, timing, information structure, and the parameter restrictions assumed.
5. **Equivalence, adequacy, convergence: what preserves it.** Denotational equivalence: two written forms, one denotation. Adequacy: an implementation computes exactly the object denoted. Convergence: a numerical approximation approaches it as grids and tolerances are refined.

```{raw} latex
\end{displaybox}
```