# VirtualElementMethods
This repository contains a Python translation of the code provided in:

The virtual element method in 50 lines of MATLAB. Oliver J. Sutton. Numerical Algorithm [https://dl.acm.org/doi/10.1007/s11075-016-0235-3]

It solves a toy problem, a 2-D poisson equation on generalized polygonal meshes, using the lowest order Virtual Element Method.

## Usage
    $ python3 vem.py --help
    usage: vem.py [-h] [-d D] [-o O] [--save_plot] [--title TITLE] i

    This script solves 2-D Poisson Equation on general polygonal meshes using
    Virtual Element Method of the lowest order.

    positional arguments:
    i              Path to input mesh

    optional arguments:
    -h, --help     show this help message and exit
    -d D           Specifies the shape of the 2D domain.
                 Possible values are:
                 - s: Square Domain
                 - l: L-Shaped Domain
    -o O           Path to output file
    --save_plot    Flag for saving the plot
    --title TITLE  Title of plot

The meshes can be downloaded from here (http://www.netlib.org/numeralgo/). A copy of the meshes is also provided in this repository in the meshes directory.

## Example Usage
    $ # Computing the solution of a 2-D poisson equation on a square mesh and square domain
    $ python3 vem.py -d s meshes/square -o solution.npy --save_plot --title plot.png

## Some Results
Since this is a translation of the paper, this repository solved the exact toy problem that the paper has taken up, that is,

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/bd8629fd-64cf-40be-b669-de02d2ba8aeb)

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/5c179338-cbe1-4a73-9d2a-f57405bc930e)


The solutions to this problem on different meshes in the square domain are shown below.

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/96913639-0c55-42a6-bf79-8c45d7a3c272)
				
## Custom boundary conditions and RHS
You can customise the code to run it with your own boundary condition and RHS too!

Just take a look at square_domain_boundary_condition and square_domain_rhs, you can write similar boundary condition functions and RHS function definitions.

Basically, the template is as follows:

    # for boundary condition
    def my_boundary_condition(points):
      # points is a list of 2-lists, containing mesh points
    
      results = do_something(points)
      return results

    # for RHS
    def my_rhs(point):
      # here we have a single 2-list as input

      result_rhs = do_something_else(point)
      return result_rhs

Now, in vem.py, go to the main function where the vem function is called and change it to:

    u = vem(mesh_file, my_rhs, my_boundary_condition)
