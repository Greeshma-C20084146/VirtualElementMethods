# VirtualElementMethods
A translation of the code given in Python can be found in this repository:

[The virtual element method in 50 lines of MATLAB. Oliver J. Sutton. Numerical Algorithm](https://dl.acm.org/doi/10.1007/s11075-016-0235-3)

It uses the lowest order Virtual Element Method to solve a toy problem, a 2-D poisson equation on generalised polygonal meshes.

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

The meshes are available for download [here](http://www.netlib.org/numeralgo/).

## Example Usage
    $ # Computing the solution of a 2-D poisson equation on a square mesh and square domain
    $ python3 vem.py -d s meshes/square -o solution.npy --save_plot --title plot.png

## Some Results
Given that this is a translation of the research, the same toy issue that the paper addressed was resolved by this repository:

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/bd8629fd-64cf-40be-b669-de02d2ba8aeb)

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/5c179338-cbe1-4a73-9d2a-f57405bc930e)


Below are the answers to this issue on various square domain meshes.

![image](https://github.com/Greeshma-C20084146/VirtualElementMethods/assets/125087684/96913639-0c55-42a6-bf79-8c45d7a3c272)
				
## Custom boundary conditions and RHS
The code can be modified so that it runs with your own boundary condition and RHS as well!

You can write RHS function definitions and boundary condition functions that are analogous to square_domain_rhs and square_domain_boundary_condition.

In essence, the template looks like this:

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

Now, in vem.py, locate the main function that calls the vem function and modify it to:

    u = vem(mesh_file, my_rhs, my_boundary_condition)
