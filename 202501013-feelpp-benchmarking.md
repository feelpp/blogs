# Introducing the feelpp.benchmarking framework

In the context of High Performance Computing, it is crucial to understand how applications perform in different systems and architectures. However, finding a benchmarking tool that combines flexibility, robustness, reproducibility of results, and a complete and easy to use pipeline that goes from benchmarking to generating comprehensive reports, can be quite challenging. 

|   |   |
| --- | --- |
| ![Benchmarking Dashboard](https://raw.githubusercontent.com/feelpp/blogs/refs/heads/main/dasbhoard-base.png) | ![Benchmarking Applications](https://raw.githubusercontent.com/feelpp/blogs/refs/heads/main/dashboard-applications.png) |

## Why feelpp.benchmarking?
This is where the *feelpp.benchmarking* tool comes in hand.    
Built on top of [ReFrame](https://reframe-hpc.readthedocs.io/en/stable/), this application was conceived to facilitate and automate benchmarking tasks for HPC users, as well as to provide users and organizations a centralized platform to aggregate and display results in the form of a dashboard.  
With a focus on flexibility, this tool ensures reproducibility of results, and is equipped with a continuous benchmarking pipeline that empowers CI/CD workflows for any application.

Although the framework is still under development, *feelpp.benchmarking* is already functional and is becoming increasingly robust. By focusing on flexibility, modularity and adaptability, it has been set to become a valuable resource for any developer or organization looking to be fully aware of their application’s performance over the course of its development.


## A Key Tool for the HiDALGO2 Urban Buildings Pilot

In the context of the HiDALGO2 project, this open source application is extremely useful for monitoring the pilots’ performance over time and to automatically be able to launch new benchmarks for a given task. For example, the Urban Buildings pilot can be configured to compare its parallel code performance on multiple EuroHPC systems each time a new feature is introduced to the main codebase. That way, it can be guaranteed that the application’s scaling has not been compromised.

## How It Works

The feelpp.benchmarking framework is separated into two main components: executing a benchmark and converting benchmark results into readable reports inside a dashboard. 

In order to perform a benchmark for a given application, users must provide three configuration files, in JSON format: 

- A configuration indicating machine specific options where the application will be executed, such as the environments and platforms to use.  
- A configuration indicating how the benchmark should be done, for example, specifying where the executable is located, the options to pass to the application, and how the tests will be parametrized.  
- A configuration file describing the figures that will be displayed on the dashboard containing benchmark reports.

These configurations are equipped with a placeholder syntax that allows users to refactor fields and create reusable files.  
First, configuration input will be validated and parsed, updating placeholders as needed.   
Then, using ReFrame, execution environments will be set up depending on the indicated configuration and the desired parameters. The benchmarked application will then be launched for each particular environment, fetching performance variables and outputs as needed, and validating the execution of the test by using sanity functions and patterns.   
Finally, the application will store a set of ReFrame generated reports, and will create or update a JSON file describing all performed benchmarks. This file is then used to handle the dashboard generation.  
Depending on the specified machine-application-use case combination, multiple views will be generated as asciidoc files, containing instructions on the rendering of the report figures. The [Antora](https://antora.org) framework will take responsibility in compiling the documentation into an HTML dashboard.   
This part of the workflow is also in charge of aggregating reports depending on the views. For example, it will be possible to see the progression of an application over time, as well as to compare how multiple systems and platforms perform for a specific application.

|   |   |
| --- | --- |
| ![Benchmarking Supercomputers](https://raw.githubusercontent.com/feelpp/blogs/refs/heads/main/dashboard-supercomputers.png) | ![Benchmark Glimpse](https://raw.githubusercontent.com/feelpp/blogs/refs/heads/main/dashboard-benchmark-glimpse.png) |

## Notable Features

The most notable features of the *feelpp.benchmarking* are:

1. General dashboard creation  
   It is possible and easily feasible to use the *render* component of the *feelpp.benchmarking* tool to generate not only a benchmarking dashboard, but also any kind of gallery-like static website. This can be done by simply modifying the input templates and configuring the *Model-View-Controller (MVC)* components. This way, users can adapt the tool to suit their needs.  
     
2. Flexible configuration files  
   Machine, benchmark and figure configuration files support complex parametrization and include a placeholder syntax for easy refactoring and reuse. 

3. Container support and benchmark reproducibility  
   The *feelpp.benchmarking* tool seamlessly integrates Apptainer containers, ensuring compatibility across many HPC systems. The framework ensures, via input configuration, that results are consistent and reproducible. Additionally, the tool guarantees dashboard persistence, allowing users to track performance over time and across different views

4. HPC system integration  
   At the moment, the Discover supercomputer is supported, and many more machines are planned to be integrated into the framework. Integrating a new HPC system can be done easily by describing the hardware, following [ReFrame’s configuration reference](https://reframe-hpc.readthedocs.io/en/stable/config_reference.html) , and configuring access through the CI runners.

5. A Continuous Benchmarking (CB) workflow  
   The benchmarking framework of *Feel++* provides a pipeline that can be directly executed by any application via a REST request, enabling continuous benchmarking for any application through their CI/CD pipelines.

## Future Roadmap

The framework is being actively developed and maintained, and multiple features are planned to be integrated. Some of these include: 

- Supporting exporting data directly from the website in multiple formats (CSV, LaTeX, …).   
- Displaying a profiling analysis of the benchmarked application, if available.  
- Adding support for environments such as *Spack,* and other containers such as Docker.  
- Supporting execution of advanced applications that handle ensemble scenarios and uncertainty quantification. 

## Get Started

We ecourage all developers, researchers, and HPC enthusiasts to explore the *feelpp.benchmarking* framework. By using this tool, you can gain actionable insights into your application’s performance and contribute to its growth and enhancement.

Visit our GitHub repository [http://github.com/feelpp/benchmarking](http://github.com/feelpp/benchmarking) to access the code, detailed documentation and the latest updates, as well as our benchmarking dashboard [http://bench.feelpp.org](http://bench.feelpp.org). Your feedback and contributions are invaluable, as they will help us make this tool more powerful and versatile.
