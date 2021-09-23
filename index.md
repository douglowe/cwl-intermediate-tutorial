---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---

<!-- this is an html comment -->

{% comment %} This is a comment in Liquid {% endcomment %}

### For Contributors

Use the _Episodes_ menu above to browse through the pages for
indivual blocks of learning objectives.
These pages can be used for designing challenges/exercises
for the tutorial.

**Note:** the order of these episode pages is arbitrary and
these pages may be removed/rearranged/merged
later in the lesson development process.

You may find it helpful during lesson/exercise design to
refer to [these draft concept maps](https://docs.google.com/presentation/d/1aVdK8LHkgtESBunCQ-p7XmEl8NB9XbgDsH67X0_2HWg/edit#slide=id.g72208cbc10_0_264)
for the tutorial material

> ## Example rendered exercise
>
> This is the body of the challenge.
>
> > ## Solution
> >
> > This is the body of the solution.
> {: .solution}
{: .challenge}

> ## Prerequisites
>
> This tutorial guides you through the the fundamentals of
> designing and building an analysis workflow.
> It assumes no previous knowledge or experience of workflows
> or Common Workflow Language (CWL),
> but does assume some experience with the Unix command line.
>
> Before following this tutorial,
> you should be comfortable working in a Unix command line environment
> and familiar with fundamental commands (`cd`, `mv`, `mkdir`, etc),
> piping and redirection,
> and simple Bash scripting,
> such as might be gained from following the [Software Carpentry][swc]
> lesson, [The Unix Shell][swc-shell].
> You might also have some experience with running
> tasks on a remote machine (by `ssh` connection)
> and in a cluster (high performance computing) environment.
>
> If you have previously written a workflow description,
> in CWL or another langauge,
> you may want to look instead at the [User Guide][cwl-user-guide].
{: .prereq}

### Target Audience

This tutorial is aimed at researchers
and research software engineers
who would like to continue and enhance automating their analyses in workflows.

If you're unsure whether this tutorial is a good fit for you
check the prerequisites listed above.

You may also find our [learner profiles][audience] helpful.
These are also a useful resource during the lesson design process.

### Learning Objectives

#### Goals

Below is a list of draft learning objectives,
(very) roughly broken down into chunks that feel like they belong together.
These chunks _could_ form the basis for splitting tutorial material into episodes.
Most blocks include one objective in __bold__:
this is intended to flag it up as a higher-level objective,
encapsulating multiple smaller,
more fine-grained,
objectives that follow.
The higher-level objectives may be suitable as learning objectives
for the tutorial as a whole
(i.e. they would be shown on the landing page,
used to guide development and structuring of material, etc)
while the "sub-objectives" would apply to specific sections (episodes)
of the tutorial,
and be used to guide the creation of exercises and content of those episodes.

The chunks get a bit less well-defined towards the end.
See [this page][objective-notes] for the original notes these objectives are based on,
created during the March 2020 lesson development sprint.

TODO: remove the 'novice' learner objectives below

After following one of these tutorials, learners will be able to:

- __implement scattering of steps in a workflow__ (lesson-level objective)
  - explain what is meant by the _scatter_ pattern in workflow design, and how it differs from the similar concept of parallel execution
  - identify when the scatter pattern appears in a workflow description
  - (FIXME: does the above cover the intended meaning of the following two points from the lesson development sprint?)
    - running the same program on each file
    - running the same program the same way except for one parameter
- __convert a shell script into a CWL workflow__
  - understand how to convert shell loops to scattering of steps
- __describe operational requirements for running a tool__ (lesson-level objective)
  - identify all the requirements of a tool and define them in the tool description
  - use `runtime` parameters to access information about the runtime environment
  - use `$(runtime.cores)` to define the number of cores to be used
- __be able to include their own script as a step in a workflow__
  - several options for this were identified during the lesson development sprint. we should choose one or two to focus on in the tutorial:
    - make script executable and add to path
        - advantage: quick
        - downside:
            - the scripts are not shipped with the CWL document itself
            - not portable to other execution environment without putting the script first
    - pack the scripts into a docker container and make them executable there:
        - advantage: portable
        - downside:
            - only works for people that are using containers
    - use InitialWorkDirRequirement to list script content directly in the CWLToolWrapper
        - example: https://github.com/CompEpigen/ATACseq_workflows/blob/master/CWL/tools/generate_atac_signal_tags.cwl (bad example as here the scripts are too long, only for short scripts)
        - advantage:
            - portable
            - can be used independent of the dependency management solution
        - disadvantage:
            - explodes the complexity of a CWL tool wrapper
            - having to deal with escapes and so on
    - distribute as seperate package via pip / cran / ...
- customize a workflow at any of the many levels (lesson-level objective?)
    - Change the input object
    - Change the default values at the workflow level
    - Change hard coded values at the workflow level
    - Change default value at the Workflow step level
    - Change hard coded values at the Workflow step level
    - Change default values in the CLT description
    - Change hard coded values in the CLT description
    - Change the container
    - Change the tool source itself

---

Objectives that require further discussion, if (and how) they should be included.
- Know what a sub workflow is, how to make one, and when to use them.
- Work around a bad software container (requires to be run as root user inside the container, expects certain directory paths)
- Know how to use CWL v1.2 [dynamic workflow conditionals](https://www.commonwl.org/v1.2.0-dev2/Workflow.html#WorkflowStepInput)
- Run their workflow on a {Sun Grid Engine, LSF, Slurm,..} HPC system
    - explain the benefit and restrictions of HPC systems (high throughput, network restrictions, etc)
    - provide example options (e.g. Toil)
- Convert a GNU Makefile to a CWL workflow

{% include links.md %}
