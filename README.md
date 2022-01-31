#  Method Development SOP (proposed)
Best practices for method development in the PurdonLab. Please complete the sign-in exercise after you read through this document. 

## Table of contents
1. [Overview](#overview)
1. [Driver](#driver)
1. [Co-pilot](#co-pilot)

## Overview
This document outlines the standard operating procedures for method / algorithm development process and code review. All novel methods being developed should follow the best practices here. 

Editors: Alex He <mh105@mit.edu>

Last updated: January 31, 2022

## Driver
As the **driver**, you are the main developer for the method. You should follow these suggestions: 

1.	Use git for version control. It can be either GitHub (most likely as private repo) or Partners GitLab under the lab group.
2.	Watch [videos](https://www.youtube.com/watch?v=6OkOmPqumWo) of using git for academic purposes and complete a set of simple exercises we create within the lab for using git. 
3.	Identify a **co-pilot** who will join you for the method development and likely appear as co-authors on publications later. This person should be able to:
    - a.	Understand your method at a theoretical level 
    - b.	Comprehend your description of the code if not reading on their own 
4.	You must write docstrings for all functions you write, however brief, even just a sentence saying what it tries to do. 
5.	Use modular functional programming and object-oriented programming as much as possible. 
6.	Avoid doing things in scripts. Scripts are not re-usable but functions are. You can first experiment with things in scripts, but you should move the method into a function soon. This forces you to think about input and output arguments and clearing all temporary variables in-between runs. 
7.	For core algorithmic steps, try to isolate each step into a dedicated function and do one or more of the following tests: 
    - a.	Hand-evaluate a simple case and hard code as a test case for the step and verify that your code outputs the same values. 
    - b.	Compare against another existing and tested implementation and verify that for the same inputs your code can produce the same outputs. 
    - c.	If neither of the above is feasible, you now must set up a simple test case where you qualitatively understand what the outputs should be – run your code and inspect the results for errors. Check dimensionality, data types, and NaN values. If this is a step that can accept real data, load some real data with noise that you can’t control, run your step and inspect for errors. 
    - d.	Simulation tests and compare against generative parameters. A general idea referred to as posterior predictive checks. This is necessary for an entire algorithm and imperative for publications. 
8.	Integrate test cases from 6 as continuous integration in git, usually in functions named test_xxx() in test_xxx.py. Pytest will automatically run everything following a standard naming convention. The online automation platforms are Travis-CI and GitHub Action (3000hrs per month).
9.	Upon completing a separatable step in algorithm development, commit and push to git repository (called Projects on GitLab). Or you may commit more often.
10.	Avoid putting data on GitHub repositories (called projects on Gitlab) and store code.  
11.	Set up multiple remotes for a single repository that needs to live on both GitHub and Gitlab. Gitlab has unlimited storage space and within Partners but requires VPN. 
12.	For multiple versions of the same code that you need to live in parallel with past versions that you want to keep, consider doing one of these:
    - a.	Add new input arguments with default values like None to support new arguments that were not relevant for old versions 
    - b.	Use a flexible **kwargs in the function header, then you can give different key-value pairs to replay different versions of the code 
    - c.	Consider using releases or tags (works the same way as branches), which will make a static “time machine” copy of the current code. If you need to come back to this old version of the code, you can do git checkout <tag name> to go back in time to repeat an old version of method. 
13.	If adding a significant functionality to your own code base, create a new branch of the original repo master branch and open a pull request. If you are working with someone else’s code base, fork the repo and develop in a named branch (don’t use master or main) of the forked repo. Either way, you should open a pull request, invite your co-pilot as the reviewer to do code review before merging into your primary git branch. [expand here by Amanda]

## Co-pilot 
As the **co-pilot** on the project, you have the following responsibilities: 
  
1.	Join git and open a branch or fork the repo (forking is preferred). 
2.	Assume everything is wrong until proven to you otherwise, including that 1980s paper cited hundreds of times. 
3.	Ask the driver to explain what the algorithm is trying to do in theory and evaluate whether it makes conceptual sense. 
4.	Challenge the driver to prove on paper any step that may not be immediately obvious. If it is an involved step, the driver should have proved it already and you need to re-walk the proof from scratch. 
5.	Ask the driver to explain code implementation of the methods and read the code line by line to understand what it is doing. 
6.	Ask the driver to explain test functions, then the copilot should run the test functions set up by the driver (preferably evaluate key parts of the codes in interactive mode). 
