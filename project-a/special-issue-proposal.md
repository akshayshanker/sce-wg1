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

## Structure of the Special Issue

Submissions are invited on, but not restricted to, the following areas, each detailed in Appendix A:

```{raw} latex
\begin{displaybox}[breakable]{Paper areas}
```

- **Model languages.** What a file in a language with a fixed grammar denotes, stated once alongside the grammar.
- **Toolkits.** What each construction call stands for, how meanings combine, and what is required of user-supplied functions.
- **Estimation methods.** What a complete specification of one estimation exercise consists of, and which population parameter it defines.
- **Model classes.** Which objects a class of models is built from, and when two descriptions are the same model.
- **Solvers, translations, and checking.** What a numerical choice, a translation, or code written by a language model preserves of the denoted object.

```{raw} latex
\end{displaybox}
```

Each team states its semantic ontology in the formalism it judges appropriate; no toolkit or formalism is a template for the others, and where the semantic ontologies differ, the difference is a result for the closing comparison to report. For a language, a toolkit, or an estimation method, the semantic ontology concerns the meaning of representations and procedures rather than the mathematics they describe: the Bellman equation is common ground, while what a given Dynare file or HARK model means is not. A model-class paper, by contrast, states the objects and relations of the mathematics itself.

Every paper opens by answering five questions. The first three answers are the components of its semantic ontology; the last two are statements about it — when the interpretation holds, and what preserves it:

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

An ontology stands on its own, in whatever formalism states it: a model-class paper supplies exactly that, the inventory and identity criteria of a class of models. Checking written artefacts, however, needs all the parts: against a file format alone, only well-formedness can be checked, because syntax is all it states; against an ontology with no map into its domain, nothing written can be checked at all; an implementation, a translation, or model code written by a language model is checkable only against the full triple of syntax, ontology, and map. *Semantic ontology* names that combined object, which neighbouring literatures divide between a domain ontology and a formal semantics.[^ssj][^realisation]

[^realisation]: Numerical realisation (the grids, discretisation, and solution method the code applies) is not a fourth part. A finite space that defines the economic problem, a genuinely discrete choice set, is part of the denoted object; a grid used only to approximate a continuous space is part of the numerical realisation, which is judged against that object either exactly or by convergence as grids and tolerances are refined.

[^ssj]: Some frameworks already expose substantial structure: the sequence-space Jacobian toolkit, for example, represents a model as a graph of blocks and their dependencies (Auclert et al. 2021); Appendix A states what remains to be supplied. For the toolkits named in this proposal, we have not found in released versions a complete public map from files and function calls into the domain; a semantic ontology supplies exactly this map.

A paper on solvers, translations, or checking may use semantic ontologies stated elsewhere in the issue rather than supply its own; it then names those it uses and states which claim it establishes: denotational equivalence, adequacy, convergence, or non-representability. The results asked for are theorems where proof is the right evidence, classifications of what a representation can and cannot express, validated translations, and documented reports of checking. The exercise is pragmatic rather than foundational: it formalises the meaning of representations already in use, not a general model theory for economics, and it treats failed translations and non-representability as results rather than defects.

Each paper works its semantic ontology through at least one worked example, a model of its own choosing written out in full (equations, timing, calibration, and the outputs to report) without reference to any solver — a reference specification, whose contents Appendix A states. Papers pass an internal review within the working group [process TBC] and then the journal's ordinary external refereeing. We expect six to eight papers, with a session at the Society's conference between submission and revision.

## Organisation

### Teams and Editors

The working group's members include developers of Dynare, HARK, and the VFI Toolkit. Committed teams: [to be listed — only teams that have agreed in writing]. The working group's papers will come from its subgroups. Akshay Shanker and Matthew McKay chair the working group and coordinate the teams and the internal review; they are not editors of the issue. The guest editors (a lead editor and at least one co-editor, neither submitting to the issue) are drawn from outside the working group [names, institutions — TBC]. Papers are submitted through the journal's editorial system, marked for this special issue, and are refereed under the journal's ordinary standards; the guest editors handle every paper, including the comparison paper, subject to the journal's final editorial authority.

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

Bock, C., and M. Grüninger (2005). "PSL: A Semantic Domain for Flow Models." *Software and Systems Modeling* 4, 209–231.

Ciocchetta, F., and J. Hillston (2009). "Bio-PEPA: A Framework for the Modelling and Analysis of Biological Systems." *Theoretical Computer Science* 410(33–34), 3065–3084.

Dubé, J.-P., J. T. Fox, and C.-L. Su (2012). "Improving the Numerical Performance of Static and Dynamic Aggregate Discrete Choice Random Coefficients Demand Estimation." *Econometrica* 80(5), 2231–2267.

Fox, M., and D. Long (2003). "PDDL2.1: An Extension to PDDL for Expressing Temporal Planning Domains." *Journal of Artificial Intelligence Research* 20, 61–124.

Fritzson, P., and V. Engelson (1998). "Modelica — A Unified Object-Oriented Language for System Modeling and Simulation." In *ECOOP '98 — Object-Oriented Programming*, Lecture Notes in Computer Science 1445. Springer, 67–90.

Gennari, J. H., M. L. Neal, M. Galdzicki, and D. L. Cook (2011). "Multiple Ontologies in Action: Composite Annotations for Biosimulation Models." *Journal of Biomedical Informatics* 44(1), 146–154.

Gleeson, P., S. Crook, R. C. Cannon, M. L. Hines, G. O. Billings, et al. (2010). "NeuroML: A Language for Describing Data Driven Models of Neurons and Networks with a High Degree of Biological Detail." *PLoS Computational Biology* 6(6), e1000815.

Gruber, T. R. (1993). "A translation approach to portable ontology specifications." *Knowledge Acquisition* 5(2), 199–220.

Guarino, N., D. Oberle, and S. Staab (2009). "What Is an Ontology?" In S. Staab and R. Studer (eds.), *Handbook on Ontologies*, 2nd ed. Springer, 1–17.

Grüninger, M., and C. Menzel (2003). "The Process Specification Language (PSL): Theory and Applications." *AI Magazine* 24(3), 63–74.

Hall, A. R., and A. Inoue (2003). "The large sample behaviour of the generalized method of moments estimator in misspecified models." *Journal of Econometrics* 114(2), 361–394.

Harel, D., and B. Rumpe (2004). "Meaningful modeling: what's the semantics of 'semantics'?" *Computer* 37(10), 64–72.

Modelica Association (2023). *Modelica Language Specification*, version 3.6. https://specification.modelica.org.

Ścibior, A., O. Kammar, M. Vákár, S. Staton, H. Yang, Y. Cai, K. Ostermann, S. K. Moss, C. Heunen, and Z. Ghahramani (2018). "Denotational Validation of Higher-Order Bayesian Inference." *Proceedings of the ACM on Programming Languages* 2(POPL), article 60.

Su, C.-L., and K. L. Judd (2012). "Constrained Optimization Approaches to Estimation of Structural Models." *Econometrica* 80(5), 2213–2230.

Wieland, V., T. Cwik, G. J. Müller, S. Schmidt, and M. Wolters (2012). "A new comparative approach to macroeconomic modeling and policy analysis." *Journal of Economic Behavior & Organization* 83(3), 523–541.

```{raw} latex
\appendix
```

## The Paper Areas

This appendix expands the five paper areas and states what a worked example contains. One boundary applies to every area: a mathematical generalisation (an abstract dynamic program, for example) proves theorems over many models at once without stating what any representation means, and on its own it does not meet the call. The declared scope of a semantic ontology must be a coherent public fragment of a named version, sufficient to express the paper's worked examples rather than only the constructs those examples use (a construct is any statement, declaration, or call the syntax admits), and excluded public constructs are listed with the reason for exclusion.

**Model languages.** What a file in a fixed-grammar language denotes is stated once alongside the grammar, so that every model's meaning is an instance of one map; Dynare's model language, Dolo, and HARK's model files are the candidate cases.

**Toolkits.** The cases are toolkits with construction operations rather than a grammar — the sequence-space Jacobian toolkit (Auclert et al. 2021), the VFI Toolkit, HARK's agent classes — and the semantic ontology states what each construction stands for, how the meaning of a combination follows from the meanings of its parts, and what the toolkit requires of any function the user supplies, including where state changes and randomness enter. The sequence-space Jacobian toolkit declares household, firm, and market-clearing blocks with their unknowns, targets, exogenous paths, and wiring; these declarations supply part of the syntax and of the inventory of objects and relations. What remains to be stated is the semantic map: what each block and edge denotes economically, and the conditions under which the assembled graph represents an equilibrium system. A toolkit may appear under both the language and toolkit headings; whether HARK's model files and its agent classes agree on one model is itself a question for a paper.

**Estimation methods.** For a method with no model file, such as the simulated method of moments, there may be no standard declarative specification in advance; constructing one, then stating which population parameter a specification defines and the theorem under which the procedure recovers it, is the paper's contribution. The semantic ontology states the boundary between target and implementation, and theorems or validation establish which computational changes preserve the target: the weighting matrix affects only efficiency under correct specification, but under misspecification in an overidentified model it determines the probability limit (Hall and Inoue 2003, p. 363). A relevant precedent treats Bayesian inference this way (Ścibior et al. 2018): transformations of an inference procedure are proved to preserve its meaning, with convergence and error left to be established separately. The data side belongs to the specification as well: each model quantity answers to a stated measured quantity, and the moments are computed from data by a stated procedure; biosimulation's composite annotations state the physical meaning of model variables through multiple ontologies (Gennari et al. 2011). Where data arrive continuously, from administrative feeds or an experiment still in the field, estimates are recomputed repeatedly, and only a stated specification says whether each recomputation estimates the same object.

**Model classes.** A model-class paper states which objects the class is built from, how they relate, which combinations count as a model, and when two descriptions are the same model — an ontology of the class in Gruber's sense, stated in one formalism and translatable into the representations of the toolkits within its declared scope, with non-representability stated explicitly. Heterogeneous-agent macroeconomics is one case. In the benchmark comparisons of Auclert et al. (2021), sequence-space and state-space computations agree; but their fake-news algorithm does not cover models whose value function depends directly on the distribution of agents, their examples being money search and overlapping generations with mid-life bequests. What each semantic ontology can represent is therefore a question about the objects it commits to, not about numerics. Bio-PEPA manages the same multiplicity, one biochemical syntax yielding stochastic, differential-equation, and model-checking readings (Ciocchetta and Hillston 2009).

**Solvers, translations, and checking.** The area covers three kinds of work: classifying, for a paper's worked examples, which numerical choices leave the denoted object unchanged, which refine an approximation to it, and which change the solution concept; establishing meaning-preserving translation between toolkits, including the cases where none exists and why; and reporting the use of a stated semantic ontology to check implementations, translations, or model code written by a language model, from unit and type validation to equation-residual tests, with the failures reported.

**The worked example.** Each worked example is supplied as a solver-independent reference specification covering its spaces, information and timing, equations, shock laws, calibration, admissibility conditions, solution concept, and designated observables, with reference data and a measurement map for estimation exercises. A semantic ontology may use any formalism, but it maps the representation to the reference object or states a correspondence between its domain and the reference domain; a translation between toolkits is then judged against the example's reference object rather than against either implementation.