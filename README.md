# AWS python pipeline design

## Introduction
Xetra (Market Identifier Code: XETR) is a trading venue operated by the Frankfurt Stock Exchange based in Frankfurt, Germany. In 2015, 90 percent of all trading in shares at all German exchanges was transacted through the Xetra trading venue. With regard to DAX listings, Xetra has a 60 percent market share throughout Europe. The prices on Xetra serve as the basis for calculating the DAX, the best-known German share index. 

This project generates a weekly data job to use Python move and process raw data in Xetra S3 Bucket and generate the report file to Target S3 Bucket. The resource data provides ISIN, Date, Time, StartPrice, MaxPrice, MinPrice, EndPrice, and TradedVolume for every minute of the trading day. And we will process the data and get	opening_price,	closing_price,	min_price, max_price, traded_volume	and the percentage_change(pct) for each ISIN and make them to the report file.

## Overview and steps
- Set up a virtual environment and AWS
- Understanding the source data, quick and dirty solutions using Jupyter Notebook
- Functional approach with the quick and dirty solution
- OOP Design principles and further requirements - Configuration, Logging, Meta Data
- OOP Code Design
- Implement class frame and Logging
- Coding (Clean Code, functionality, linting, unit tests, integration tests)
- Performance tuning with profiling and timing
- Create Dockerfile + push docker image to Docker Hub
- Run the application in production using a Minikube and Argo Workflows


 ### Set up a virtual environment
 use pipenv to create and active a virtual environment of Python 3.8
 
 <img src= "images/setup.png">
 
 
 ### Quick and dirty source data
 use Jupyter Notebook to read multiple files, transformations, and save to s3 Bucket in AWS.
 
  <img src= "images/quick_and_dirty.png">
 
 
 ### Functional approach
 create the function in the Adapter layer, Application Layer and creates the main function entry point.
 
   <img src= "images/functional.png">
 
 ### OOP Code Design and Impliment
 add logging(using pyyaml) and Meta data
 create s3BucketConnector(), MetaProcess(), XetraETL(), XetraSourceConfig(NamedTuple), XetraTargetConfig(NamedTuple), S3FileTypes(), MetaProcessFormat() to edit methods.
  
   <img src= "images/class_design.png">
  
 ### Coding
 add Linters (pylint) to clean code and use unit tests(moto package) and integration tests to test each unit and framework.
 
  <img src= "images/clean_code.png">
 
 ### Performance tuning with profiling and timing
 using memory_profiler to improve performance
 
   <img src= "images/profiling.png">


## lesson learned

Apart from learning how to design and implement the project using functional and OOP programming, I learned some details to control and optimize the code. For example, I can use logging and configure files (YAML) to avoid requirements and environment changes to recode and retest. 
Secondly, using a meta file for job control can avoid repeat reports being created. 
Finally, using linters and memory profilers can clean code and improve performance.
