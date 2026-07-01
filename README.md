# Introduction to the Chaste C++ interface

This repository was created for the [2023 Chaste workshop in Oxford](https://chaste.github.io/workshops/2023-09-11/), adapted for the 2025 Nottingham workshop and now adapted again for the 2026 Sheffield workshop.
It introduces some simple examples of vertex model simulations in C++, and then shows how simulations can be customised by writing new C++ classes within an example user project.

## User Project Structure

The simulations are found in the following test suite:
- [test/TestCustomVertexSimulations.hpp](./test/TestCustomVertexSimulations.hpp)

The custom Chaste classes are defined in the following files:
- [src/SillyVertexBasedDivisionRule.hpp](./src/SillyVertexBasedDivisionRule.hpp)
- [src/SillyForce.hpp](./src/SillyForce.hpp)
- [src/SillySimulationModifier.hpp](./src/SillySimulationModifier.hpp)

## Chaste user projects

* There are a few ways to use Chaste's source code. Professional C++ developers may wish to link to Chaste as an external C++ library rather than use the User Project framework described below. People new to C++ may be tempted to directly alter code in the Chaste source folders; this should generally be avoided as we won't know whether any problems you may run into are down to Chaste or your changes to it!

* Instead of these options, 'User Projects' allow you to use Chaste source code and have the benefit of using the Chaste build/testing framework, by putting User Projects under the projects folder. User Projects work exactly like new Chaste modules (`global`, `heart`, `cell_based`, etc.) and can depend on any of the Chaste modules (or indeed other User Projects). We tend to supply User Projects to accompany and reproduce research articles.

* Instructions on how to create your own User Project from a 'template' project can also be found [here](https://chaste.github.io/docs/user-guides/user-projects/). Alternatively, if you're using Chaste via Docker, you can run the provided script `new_project.sh` (in the `scripts` directory) and pass the name that you want to call your project e.g. `new_project.sh my_chaste_proj`. For the first few stages of this tutorial, you do not need to create your own user project, as the initial setup has already been done for you.

* ⚠️ When you create a new user project, make sure you run the [setup_project.py](https://github.com/Chaste/template_project/blob/main/setup_project.py) script to ensure it relies on the correct Chaste libraries.

* Once you have created the repository on GitHub (with the same name) and committed some changes, use the following commands to push your project to GitHub:
  ```
  git remote add origin https://github.com/<username>/my_chaste_proj.git
  git push -u origin main
  ```

* If the above command gives you the error `fatal: remote origin already exists`, then instead use the commands:
  ```
  git remote set-url origin https://github.com/<username>/my_chaste_proj.git
  git push -u origin main
  ```

* Your project and its revision history is now safely stored on GitHub.

## Practical session

### 1. User project structure & set up

- Look through the structure of the user project and make sure you understand what all the files are there for.
- Note how the various classes in the `src` directory inherit from the base Chaste library classes.
- Set up the workshop user project
  - From your ubuntu terminal (for windows, linux/macosx use native terminal), navigate into your Chaste directory, then the projects directory using the command `cd projects`
  - Clone this repository into the `projects` directory using the command `git clone https://github.com/Chaste/IntroToChasteCpp2026.git`
  - Navigate back to your `build` directory
  - Configure cmake to build your project using `cmake ../src -DChaste_ENABLE_project_IntroToChasteCpp2026=ON -DChaste_ENABLE_project_IntroToChasteCpp2026_TESTING=ON` from the build directory
  - Build the project! `make project_IntroToChasteCpp2026`

### 2. Run the test suite

- Read through the code in [test/TestCustomVertexSimulations.hpp](./test/TestCustomVertexSimulations.hpp) and make sure you undersand what it is doing.
- Compile and run the test suite in [test/TestCustomVertexSimulations.hpp](./test/TestCustomVertexSimulations.hpp). If you followed the previous instructions, the tests should be built already. You will need to re-run `make project_IntroToChasteCpp2026` each time you make changes. To run the tests, use the command `ctest -V -R TestCustomVertexSimulations`
- Open the output in ParaView and see what each simulation has produced.
  - Download the output files from the `output` directory in vscode
  - Follow the instructions from the slides to view the outputs

### 3. Read though the custom classes

- Look at the code in the [src](./src) directory and make sure you understand it.
- Make some modifications to one or more of those classes, and see how that modification affects the output of the relevant test.

### 4. Make a custom class

- Create a custom class. This might be a division rule, force, or simulation modifier similar to the existing custom classes, or, it could be something different such as a new cell writer.

### 5. Write a node based simulation with a custom class

- Take one of the simulations in the test suite in [test/TestCustomVertexSimulations.hpp](./test/TestCustomVertexSimulations.hpp), and re-write it as a node based simulation. You may find one of the tutorials useful: [https://chaste.cs.ox.ac.uk/trac/wiki/UserTutorials#Cell-basedChaste](https://chaste.cs.ox.ac.uk/trac/wiki/UserTutorials#Cell-basedChaste)
- Write a custom class that would make sense for a node based simulation, and add it to your new simulation.

### 6. Try creating your own user project!
- Create your own project repo on GitHub from the user project template [https://github.com/Chaste/template_project](https://github.com/Chaste/template_project)
- Clone your project into the `projects` directory
- Run the `setup_project.py` script
- Add a test file and write your own test that runs a cell-based simulation
