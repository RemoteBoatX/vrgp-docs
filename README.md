# Documentation files for the implementation of the VRGP

This repository contains all the documentation and other documents gathered
while working on the VRGP implementation project.

Documentation and documents could refer to:
- documentation about the existing code on the Åboat or the MOC
- documentation about tools (like code editors, languages, frameworks) used by
the team or by the existing implementations of the Åboat and the MOC
- documentation about other non-coding related things (like workflows, project
management, presentations, other team documents)

What the repository should _**NOT**_ contain is:
- code or other types of source files related to the project or the associated
  projects of Åboat and VRGP test implementations

## Internal documentation regarding various environments

This section includes documentation regarding the different environments we will
work in. It mostly contains notes and sample code which should help everyone in
the team get accustomed easily to a tool. It can also serve as a "best
practices" mechanism, in the sense that once we experiment with something and
see what works and what not, we can include that here.

The docs also contain some useful links gathered while working with the specific
environments.

---

### WebRTC

Refer to [the docs on WebRTC](https://github.com/RemoteBoatX/vrgp-docs/tree/main/webrtc).

### WebSockets

Refer to [the docs on WebSockets](https://github.com/RemoteBoatX/vrgp-docs/tree/main/websockets).

### OpenDLV

Refer to [the docs on OpenDLV](https://github.com/RemoteBoatX/vrgp-docs/tree/main/opendlv).

### The Åboat environment

Refer to [the docs on Åboat](https://github.com/RemoteBoatX/vrgp-docs/tree/main/aboat-environment).

### The MOC environment

Refer to [the docs on MOC](https://github.com/RemoteBoatX/vrgp-docs/tree/main/moc-environment).

## External documentation, standards, conventions, workflows

This sections documents the use of conventions and standards by the team. Such
conventions include but are not limited to: code style, documentation style,
different workflows, different project management techniques.

---

### General project workflows

#### Github workflow

- [Short tutorial on Git and Github](https://rogerdudler.github.io/git-guide/)
- [Another tutorial on Git and Github](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)
- [Git workflows comparisons for projects (important read)](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Github Git cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Bitbucket Git cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
- [Gitlab Git cheatsheet](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
- [Boston University Git cheatsheet](https://www.bu.edu/tech/files/2019/06/Git_CheatSheet.pdf)

The team uses Gitflow Workflow as a Github workflow. More info on this can be
found [here](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).

#### Scrum/Kanban-style workflow

Refer to [this issue](https://github.com/RemoteBoatX/tasks/issues/8).

The team uses a Scrum/Kanban workflow, with tasks assigned to each member and
sprints, at the end of which we come together and see the progress being made.

The product is continuously delivered and changes are continuously integrated,
with the product always being available.

---

### Coding related conventions

#### Code style

C++ code should adhere to [Google C++ code style](https://google.github.io/styleguide/cppguide.html).

A tool to check for the C++ code style can be found [here](https://github.com/google/styleguide/tree/gh-pages/cpplint). This tool should
be made available in the CI/CD pipeline, to check for code-style violations on
every commit.

Individual programmers should of course use the linter locally first before
uploading the changes, but integrating the linter into the CI/CD pipeline
additionaly helps.

Additional C++ core guidelines can be found [here](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) (altough a lengthy
document).

#### Comments and code documentation

Code should be commented and documented using [Doxygen](https://www.doxygen.nl/index.html).

For installation and getting started in Doxygen, see [this](https://www.doxygen.nl/manual/index.html).

The documentation should also be generated at commit-time, using the CI/CD
pipeline.

---

#### Testing

[TODO]

---

### Building

The project should be built using [CMake](https://cmake.org/).

Some tutorials on CMake:
- [CMake-tutorial](https://github.com/pyk/cmake-tutorial)
- [A CMake tutorial on medium.com](https://medium.com/@onur.dundar1/cmake-tutorial-585dd180109b)
- [A quick CMake tutorial by JetBrains](https://www.jetbrains.com/help/clion/quick-cmake-tutorial.html)
- [A quite comprehensive CMake tutorial](https://riptutorial.com/cmake)

The CI/CD pipeline should have a rule for building the project and deploying a
zip archive or executable file(s), or other possible artifacts such as Docker
images.

---

### Other CI/CD pipeline tools

This section documents additional tools which could be helpful in a CI/CD
pipeline.

First of all, see [this article](https://www.katalon.com/resources-center/blog/ci-cd-pipeline/) on what a CI/CD pipeline is.

Some resources on Github CI/CD:
- [CI/CD: The what, why and how](https://resources.github.com/ci-cd/)
- [Basic CI/CD pipeline example repo](https://github.com/Link-/ci-cd-intro)
- [Github Actions for C++](https://www.codeproject.com/Articles/5265628/Writing-CI-Pipeline-using-GitHub-Actions-to-Build)
- [Another CI/CD example using Github Actions](https://cwsites.medium.com/ci-cd-with-github-actions-c0998601ee3a)
- [Good CI/CD tutorial, though it's Gitlab specific](https://docs.gitlab.com/ee/ci/)

Apart from the tools mentioned [above](#coding-related-conventions) (i.e. Google C++ code-style,
Doxygen, testing framework), and [CMake](#building) there could be additional
CI/CD tools used to measure code quality. Such tools are discussed below.

---

#### Code coverage

Code coverage could be used to see how much of the code is tested (how many
paths in the code have been tested).

For a general introduction on code coverage, see [this post](https://www.atlassian.com/continuous-delivery/software-testing/code-coverage).

[A good article](https://docs.gitlab.com/ee/user/project/merge_requests/test_coverage_visualization.html) on test coverage visualization (see the section on C/C++).

Some solutions for C++ code coverage:
- [gcov](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html)
- [gcovr](https://gcovr.com/en/stable/) (provides visualization for the tool above, can output Cobertura XML files)
