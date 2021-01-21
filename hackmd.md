---
permalink: /hackmd/
---

# Introduction to conda for (data) Scientists

### Links


- **Welcome!** Please keep this HackMD open 
- this document: https://hackmd.io/@coderefinery/conda 
- workshop page: https://coderefinery.github.io/2021-01-08-coderefinery-online/
- slides: https://hackmd.io/@samumantha/conda-slides
- the course material: https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/index.html
- post-workshop survey: https://carpentries.typeform.com/to/UgVdRQ?slug=2021-01-08-coderefinery-online
- feedback for improving lesson template: https://carpentries.typeform.com/to/EJAMLQT5


### Getting Started with Conda
- If you have any questions, please type it here (better than zoom chat) 


### What are some of the potential benefits from installing software separately for each project? What are some of the potential costs?

Benefits:
- you have exactly the packages you need for that project
- possible to use the desired version of a package and not our computer’s default.
- modularization
- No risk of breaking what you made in one project due to something you've changed later in a different project
- I can switch between projects that have different and sometimes conflicting dependencies
- When going into a project, I can find out what its dependencies are
- work simulatenously in different projects
- reproduce the work as the original
- Possible to reproduce & test independently.
- no conflicts between different versions of the software. 
- You have more control over the packages.
- If I mess up, I can delete the envionment but I did not mess up my operating system.
- On a cluster I can do this without asking anybody to install stuff for me.
- Distribute your code along with all the dependency information (simplify the installation process for other users)
- I don't have to deal with the strange versions of Python Apple provides.
- Good control, be sure you use what you need to solve any problem to avoid confusion



Costs:

- ...
- I have to keep track of the 
- versions, maybe?
- Having multiple copies of same packages
- Having multiple copies of same packages
- long to create every environment.
- Not always straightforward as mentioned
- You need to change enviroto 
- Storage space taken by each environment? +1-
- "I had this awesome package the other day but can't remember where I installed it" 
- You need to maintain the environments for the diffent projects seperately
- Setting up the same base environment / typing lots of install commands over and over again (if you don't know how to automate it)
- Maybe a bit more disk space consumption (can become a problem on shared clusters with disk quota)
- Having multiple copies of same packages but this is the latest one
- Ensure I work in the correct environment today.
- multiple environments might be confusing ... and btw does it mean I install the same package e.g. numpy muliple times for every environment?
- the same code won't work in another project
- Some code will never get updated to new versions, with the risk that new at new at new at new 
- You get more hassle to maintain the project and to keep it up-to-date whenever a new version of a packege is released.
- Environments end up being installed in a different location/disk from the system packages, which may have higher latency
- Having multiple copies of same packages


### Questions

Don't hesitate to ask questions here! We can answer/comment asynchronously.

- Does the speed of working in conda the same as that without conda? 
  - you mean speed of running the code? Yesæ'
    - it is a great question! for many tools that we use via conda, speed is either the same/better or not a concern. there are also optimized libraries available on conda (such as MKL). if you realize, that a specific package is a bit too slow for you, then it may be needed to optimize. but in my experience this is almost never needed.
    - But the speed does not dependet directly on Conda, does it?
      - correct, it does not. but when you conda install, you typically install a pre-built package and the package is compiled for your operating system with a "typical" setup. if you have a untypical computer (supercomputer), it may not be optimally packaged (but most often it's good enough).
        -  Thank you for the nice explanation. I was not aware of this fact.

- Will you later show maybe how I can install in a conda environment with pip a programm? This programm was not available on conda or just in a old version. I don't understand how this works. 
    - Yes we will go through this part too.

- Is the appearance of "(base)" after each command the result of having run conda init bash? This means my bash is now permanently linked to the conda base environment?  What if I don't want this any more?
    - If you refering to the prompt, you will see how to change this later today 
    - We will later learn how to "leave" that environment with `conda deactivate`


- Why does XX put python pip at the end? She is already choosing packages to install in the enviroment?
    - She is installing pip as package inside the environement (not using pip to install something here
        - )
    - Yes, you can either do it in two steps: create environment, then install. Or: like the instructor did: create the environment and list packages in one line.

- Why do I need pip as an extra package in the enviroment? Will this help me later to install packages that are not available on Anaconda, please?
    - Short answer is yes. 
    - this way we can get a well-defined pip instead of relying on pip from "outside" conda which may or may not be there.
    - pip is usually installed with together with python
        - so you probably already have it on your computer
        - if you now create a conda environment without pip
        - and you need to use pip for installing some package (that is not available on Anaconda)
        - it will use the conda unrelated pip to install packages outside of the environment
        - which may create hard to debug issues (package can not be found from within environment even though you may think you have installed it into the environment )
 
  - For most cases, you should be able to install packages using conda. Using pip to install a package inside a conda environment should be your last resort as conda and pip do not seem to behave well when used together, and is not recommended. Source: https://www.anaconda.com/blog/using-pip-in-a-conda-environment 
         - Thank you, I had no clue about this!  


- Is it normal that autocompletion does not suggets "activate" once I type "conda a" and press TAB?
  - this depends on your shell settings. for me it autocompletes.
      - OK, thanks. BTW, on my system autocompletion works well for all non-conda stuff, but not in this example with "conda a+TAB". For example "cond+TAB" does autocomplete to "conda"
  - On gitbash on Winows, it doesn't autocomplete in my experience
     - aha thanks
   - if anyone knows how to enable this autocomplete, please tell us! (mac OS X, bash shell)

- Where is the env installation located? My folder is still empty
  - are you using anaconda or miniconda?
  - anaconda and the anaconda prompt
    - in my case they land in $HOME/miniconda3/envs
    - so in other words by default they are placed in a central place in your home, either the above or under anaconda3/envs.
    - later we will learn how you can specify the location yourself using `--prefix`, then you decide where the environment installation will be.
    - sweet, cheers! 
    

- Is there anything special about conda packages? Do libraries need to be made conda-aware in any way before they can be used within conda or can anything go in an environment?
  - to make libraries conda-installable, they need to be packaged for conda and put on a "registry". a very popular registry is conda-forge: https://conda-forge.org/ - it is outside the scope of this workshop on how to create conda packages, though. the conda-forge page has good references for where to start.
  - most popular scientific packages/libraries have been packaged as conda packages, unless they are distributed more naturally via other registries (example: CRAN for R packages)


 - Is there a more general way to find $PACKAGE_NAME then googling? For instance, is there any keyword-based search? Maybe a search where I can specify compatibility requirements...
     - with `conda search` you can check if the package exists, and which versions are available 
     - If the channel (will learn later) not define you might not find some packages with conda search. In that case you can use https://anaconda.org/anaconda  to search instead of google


- so basically we create our own anaconda just with limited no of packages
  - yes, I would only install the packages that I need, not more. If I later need one more, I add one more. This will make it easier later to share and document my environment so that it can be recreated by others later or by my future me 2 years later. The "smaller" the environment, the more manageable.
      - No need to install Anaconda at all in the end!


- I understood if I don't request the version, the latest one is automatically installed? Do I need to bother with the searching, please?
    - if you do not have any specific requirements for your project, it is often best to go with the latest version
        - do we get the latest if we do not specify the version, or not?
- I was just asking because Anne went to the package websites to check for the latest version. That irritated me.
    - it might also happen that the newest version of a package is not (yet) available from Anaconda.  
    - we will get back to this later (when sharing environments this gets more important)

- (from chat) Is the existence of posible conflicts between packages verified upon creation of an environment (e.g. if one old package version is specified) 
    - yes, conda is looking first at the list you gave and tries to find versions that satisfy all your requirements

- Anne looked up ipython and came up with 7.12 as latest but if we run conda search ipython it shows 7.19 as latest, not 7.12
    - she may have found an older version on the website?
    - in general it may happen sometimes that you find the latest version on the website, but it is not yet available on Anaconda, latest version doe not always overlap with latest version on anaconda. 
    - OR: latest version might not be compatible with the python version installed into an environment

- Is there a way to list all activated environments?
  - we are always only in one environment but the one environment can be "derived" from another 
  - you see the active environment in the beginning of your terminal eg `(machine-learning-env)computername@something:$`
  - if you want to list all environments that you have available, or you have forgotten the name or location of some environment, you can use `conda env list`

- Why does the last digit does not have to be mentioned when specifying the version of a package?
    - the last digit is usually the 'patch' (only bugfixes)
    - the first 2 numbers are 'major' and 'technical' changes, here the iiinter

- Is it possible to rename an environment after creation?
    - i do not think so
    - but you can clone an environment and then give it a new name 
    - In conda (personal experience) renaming or moving environemnts after creating create issues. 
    -`conda create --name new_name --clone old_name`

- How to list all packages that are inside an environment
  - `conda list` within the activated environment

- Do we always need to install pip? (a question that came up in breakout room)
  - No. Most of the time we don't need this. We only need this if you want to use pip inside a Conda environment (which I think is not frequent). So the example that we gave was perhaps a bit unfortunate.

- Is there a way to find out which packages and versions were specified when creating an environment? `conda list` lists all packages, including dependencies.
  - we will soon learn about `--from-history` which makes this more convenient. another thing I do to answer this question to myself few months later is to install from `environment.yml` (which we will see in a moment)

- It seems to me that conda installs everything under ~anaconda/envs so I end up with multiple full installations of packages (python and everything else) taking up increasingly large space. Anyway is it correct to say that conda basically consists of (a) installing stuff under envs and (b) modifying the shell path ?
  - yes this is a good summary. plus figuring out what is compatible.

- What is the reason behind the best practice of explicitly adding version number? I mean, can't I share an environment by sending the print out of 'conda list', or something similar, rather than saying 'conda create my-env blabla=X.Y'? Creating the env with the explicit version numbers equal to the latest one from 'conda search' did exactly the same as not specifying any version number.
  - you may need to specify the versions when trying to run a project with an old code, where latest versions may not work. but in the next hour we will learn a more convenient way to share the environment and also recreating an old environment.

- trick for finding latest version: do a `conda create —name X numba,` wait for the prompt, look up the version of numba that would be installed, and select ’n’ so no environment is created
    - this suggests that not specifying the version number does indeed leads to the latest available

- from our breakout room: running `conda search pandas` resulted in mutliple lines for the latest version (1.20). What are the differences, do we need to choose one explicitely (and how) and what happens if we don't?
    - if you look in the next column starting py3...
    - every version can have a build for a specific python version
    - py39 -> python 3.9
    - it may also happen that some python version is not supported (in my list for example python 3.6 for pandas version 1.2.0 is not available)
    - No need to choose them explicitly, if python is already installed it will choose the version that works for your pyhton version
        - so if you already have python 3.6 it will not choose pandas 1.2.0 but an older version that works with python 3.6
        - if you install python without version specification at same time it will install latest of both that work together, here python 3.9 and pandas 1.2.0



- Why did you install pip if you are going to be using conda install instead?
    - This is to be answered in later episode. I understand the confusion, and this is where we discussed a lot with the lesson developer as well about where to introduce pip.
        - It's OK I can wait -- thanks!  :-)



- can I remove/uninstall a package from the environment?
    - `conda remove package` from within activated environment or `conda remove --name yourenvname package` from outside
    - for one package once in a while it is probably fine, but to be sure that everything still works it may be better to create a new environment without the package you want to remove

- what is the cmd to list all installed packages in an env?
    - `conda list` from within the activated environment
        - Cool, thanks!

- machine-learning-env folder is is 1Gb+!!!
    - maybe we should show different examples :-)
    - good thing is, we can remove these again later and can be glad that we did not install all this into our main system.

- does it make sense to put a conda env inside the git repo of a project that uses that env?
    - I do not think so. It is better to have a environmrnt file (how to create the environemnt) not the the environemnt it self. 
    - Conda uses precompiled binaries in environemnts as well, i.e. an environemnt created on one system amy not work on a nother. As best practice we do no
    - I would gitignore the actual environment folder, but definitely add `environment.yml` to the Git repository (so that others can recreate it on their side).
    - we will learn about environment.yml later

- Who designed this lecture? Somebody wrote higher up "- This is to be answered in later episode. I understand the confusion, and this is where we discussed a lot with the lesson developer as well about where to introduce pip."
    - Mostly https://github.com/davidrpugh with improvements from current instructors
- So David Pugh is the lesson developer referred to?
  - yes, but we also teach it now to give feedback on the lesson, so that we learn something more, and also in future run this multiple times (it always improves lesson if it gets more exposure and feedback)
      
- with `conda create --prefix ./env` you don't use the `name` argument?
    - no, the path you give( here ./env) will be used as a name for the environment
- Cool, 'conda env list' list also the environments created locally with the --prefix!


- Question from breakout room: Does conda cache packages when they are installed across diferent virtual environments? There is a little bit of speed up noticed when the same list of packages are subsequently installed in a different virtual environment after they have been installed once in another virtual environment.
  - yes, second time you install the same package, it does not need to download it again so second install is noticeably shorter (if it is the same packages same built: using pandas 1.2.0 for python 3.7 in one environment does not speed up the download/installation of pandas 1.2.0 for python 3.9)
 
* On a supercomputer/cluster: how to find a good balance between using modules (installed by somebody else) or installing dependencies ourselves using conda
  - it is a balance between covenience/space of using modules and having the flexibility to install dependencies without asking somebody. in any case I recommend to document both module dependencies and conda dependencies, with versions.
  - On HPC systems you might need to load and activate conda first, if yu want to use a conda environment, within the "job script". i.e. one extra step needed 


- 5 min is rather little time to downloand all the packages ... consider more time next time +1
  - good point, I think this was too short and exercises should not be shorter than 10 minutes
    - thanks for the feedback, we will give more time for the next (and last) exercise session. This is very valueable feedback that we will include when revising the workshop contents; 
    - the lesson an exercise material will also be available after the course, with solutions provided. 

* What is exactly now a --prefix in comparison to --name? A name or rather a path? I am refering to the manual where we "Listing the contents of an environment"
    - `--name` creates an environment with a specific name in the default location
    - `--prefix`: specifies the location and now the location is the name.
    - so in a sense, both will define the path but `--name` creates a subfolder in default location, but `--prefix`: you decide where it is.


- We can have acces to this exercises and slides?
    - please see on top of this document for links to the material
      - slides: https://hackmd.io/@samumantha/conda-slides
      - the course material: https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/index.html
    - they are open source and will remain available

* When I run `conda search` I get results from pkg/main and conda-forge. conda-forge seems to be added as a channel to search for packages even if it is not specified. How can I undo that?
    * you can check what channels are looked at with `conda config --get channels` and remove with `conda config --remove channels`, this will adjust your .condarc file where your configurations are stored
    * https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html


- Is consistency between packages coming from different channels guaranteed somehow?
  - consistency meaning compatibility of versions?
      - no. is numpy.x.y from conda-forge exactly the same as numpy.x.y from pgks/main?
  - Compatibility is not gurenteed and you should try to use the official channels when ever possible.  
    - I could create my own channel also and then you would have to trust me that I did it right so better check and use official channels.

- I used mostly "conda install package_name". I understand it comes from the main channel then. Was this bad?
  - this was good. only downside is that the main channel might not have some packages and then you often find them on conda-forge.
  - When following some instlation procedures you might add new channels in your configuration. To find out what are the channels that will be used when you do not specify on use the command `conda config --show channels`

- How to find available channels? (orally asked question)
    - A package you want to install has an official documentation that normally recommends which channel to install from. So this is a good way to use other channels than default, if necessary, rather than specifying many different channels. 


- Can I mix packages from different channels? Looks like I have to do this with pytorch when I want to use it, but have previously installed python from the main-package?
    - it is more save to not mix packages from different channels
        - one solution if you 'have to' would be to create separate environments
        - another to try to find compatible versions within one channel
    - having packages from different channels may result in hard to debug issues
    - If you had to use multiple channles, the priority order is very important. 
- I don't understand who this would work then together. Use two different environments for one project? Or I have to specify the path to the library when I am importing it?
  - there will be only one environment per project with packages assembled from possibly multiple channels and probably best way to deal with this is to put this into `environment.yml` (we will learn about that file in a moment)

- Is your recommendation to switch to conda-forge?
    - depends on your needs.
    - if all packages you are using are available in defaults, stick to defaults
    - What I do: For rerunning an existing project, I normally start with the official one and if it does not contain the packages I need, I try conda-forge. Unless the project documents which one I should use. For a new project, I would have a look at the two channels and compare versions of the packages that I am interested and if conda-forge offers a lot newer packages, I would go for that.

- does every channel name require the keyword --channel? 
  - yes but leaving it out will default to the official one. one can avoid that typing later by putting the channel name into `environment.yml`


- The issues with finding the right channels sound very much like the original problem of finding the right package to install, which was the original problem that the package manager was asked to solve... are we running in circles?
  - ideally this work only needs to be done when starting a project. when rerunning a project you don't need to search anymore if the person has documented this in `environment.yml` (next lesson episode?)
      - this `environment.yml` is mentioned repeatedly... will wwe look into where it is, what it is and so?
            -yes in about 20 min :)
                excellent, thanks!
 
- If I have added conda-forge to my channel list. What is the best way to remove it?
  - This is maybe not best way (I am not an expert): I would create a new environment and remove the other one. Then I am sure there is no weird inconsistency (not claiming that this is what happenes, I just don't know).
  - `conda config --remove channels CHANEL_NAME`
      - To find out the exact CHANEL_NAME `conda config --show channels`
      - Specific answer `conda config --remove channels conda-forge`

- Anne's example shows mixing packages from differnt channels. Does it seem that conda takes care a bit of that?
    - Yes. It will try to solve the dependancies using the first chanel specified first, then the secound and so on
        - Thank you for showing here the priority.


- Can you install inside the environment even if the environment isn’t activated?
    - conda install scipy=1.6 --channel conda-forge --name machine-learning-env
    - or use --prefix path-to-env (for local environment)
    - it takes scipy package from conda-forge channel and installs into machine-learning-env
    - Personal experience. I try to avoid this if possible. Instead I always activate the env first. Because I am sloppy and worry that I will use the wrong name


- Will you discuss how to include my own code, still under development, in a conda environment? In case I don't want to be in the same directory as my .py files all the time? I.e., something like `pip install -e`
  - just so I understand the question: you mean that your code under development is meant to be distributed via conda or only "consume" other conda packages? because `pip install -e .` is good if you plan to distribute your code via PyPI but you want to test it locally in place.
  - Either. There are really two purposes:
      - Install my own code in a conda environment (not download from anaconda cloud or PyPI)
          - yes, I see. testing the conda packaging before putting it on conda-forge for instance. note that you can conda install from a folder on your computer or from a git repo. this can be a good stepping stone before putting it into a registry.
      - Be able to edit the code without running an install command again (edits are automatically used the next time I `import`)
        - I understand the question but don't know the answer (I didn't do enough of this myself yet, mostly only PyPI work) 
        - My answer to the question, if you don't plan to share your code, is to add to your .pythonrc file the path to your package, so every time you open python or ipython or jupyter, your packages will be loaded, whatever directory you start your coding session from. Just a quick fix, but maybe not the best if you plan to share.
    - When I want to test my code and need a conda environment to do it, I place my program (mycode.py) or the compiled binary inside the "bin" folder of the nevironement. This may not be best practice though. The reason not to modify the path instead is that conda acvtivate changes the path


- So when exporting to a .yml, using --file is the same of redirecting to file with '>', right?
  - in my understanding: yes


- funny thing... in Samantha's terminal there were duplicates in the list of dependencies... and I can reproduce it on my system. 'prompt_toolkit=3.0.8' is listed twice
  - interesting! I think the duplications will go away when using `--from-history`
      - indeed!

- I assume you won't cover this here, but are you considering making a lesson on how to make your own conda packages (or Python packaging in general for that matter)? And how to set up your own channels (in the cloud or locally)? Or are there some good materials you can recommend?
    - Yes. Actually we plan to add it in the actual lesson and it would make a second 1/2 day workshop.


- does the order of arguments matter? --name, --file --from-history?
  - I don't think the order matters with the named arguments.


- about the --from-history. It looks like making a .yml using --from-history puts some trust on the channels w.r.t rebuilding all the rest of the packages. Any comment on this? Is it best to just make sure we have all packages in the .yml?
  - after exporting, I would try installing from that exported file into a `--prefix`
  - another thing I do in my work is to only ever install from `environment.yml` and then I know it works. So whenever I need something, I first add it to the file, then install from it.
  - best is to start from miniconda and always use an `environment.yml`. channels you used for installation will be added too.

- Can colleagues at the same institution using the same server or cluster use the same environment if it is installed in a location they can all read (e.g., if one person sets it up, and everybody else who isn't proficient in conda just uses `conda activate`)
    - Yes we use it that way. Make sure to install it using --prefix in a place everyone can access. When it comes to proficieny, we create a file called setup.source, with activating conda it self and the correct environement all in one. So when some one want to use it they do `source PATH/setup.source` and everything good to go (also a unset.source to deactivate)
 
- Does the differences in channel affect the reproducibility?
    - yes, it can if versions are not specified with X.X.X (major, minor and patches)
        - Even with the exact same version number, could you get issues with packages that include binary code (e.g., same version number for the python code in the package, but linked to different binaries for external libraries)? I heard warnings about something like that in the context of mixing packages from the default channel and conda-forge.


- how to recreate a specific environment on supercomputer such as XXX? will it be possible?
    - Yes it is possible to install miniconda on HPCs at XXX.
        - I mean in the automatic job execution
            - Yes (if you mean create an environment in a batch job?)
                - yes exactly as part of the batch job
                    - Then yes. but be aware that install uses 1 processor only (as far as I know) so make sure you do not create an envirpnmet in a parallel job (and good point below about lack of internet availabilitby on some HPC machines and ocmputing node!).
                        - Copy that. Thanks for sharing.
   - Creating envirnments in jobs not recomended (in our system can not as there is no internet in compute nodes) as the resources will be idle untill the env is ready. Intead  install it first and then use it in the job. 
       - so it will use the packages installed in the project-workspace folder. and the batch job reads them directly.

- what is first - environment file and then using it updating packages or
        first updating paackages and then creating an environment file?
    - for experimentation, when I am not sure whether I really need a package, I sometimes install first directly and then create the file once I am sure I want to continue with this.
    - When I am "sure" I need a package, I start with the file, and install from it, then I don't have to remember what I have done.
    - good point: after you test/experiment: delete your environment and re-create it with evironment.yml to make sure you have everything you need.

- Would 'conda env create --file environment.yml --force' be the same as 'conda env create --name NAME --force'?
    - No: without environment.yml, you only create a new environment (name NAME) but with no additonnal packages 
        - ok, I see, then I do not understand the very last point in Samantha's terminal... (I think she missed to add envi)
        - [name=Samantha] Sorry for possible confusion here, without the `--file environment.yml` it would actually work if you have an environment.yml file in the same location where you call the conda env create, but it is not recommended, better be as specific as possible so that you know exactly what you are doing

I don't have nano editor as I use Windows OS. So how do I create YML file?. Should I use notepad?. Thanks
  - you can install nano with conda, but one of the best (and at the same time accessible and easy to learn) editors these days is Visual Studio Code (open source) which I can warmly recommend for creating/editing such files.
  - notepad also works

- There is a difference between 'conda list env' and 'conda env list.'
The first command seems to give me only my created env with the prefix, the other command lists all my env.
I am a bit confused.


### Concluding remarks

- Give feedback to this workshop itself under the Feedback section below.
    - One good thing :+1: 
    - One to be improved
- The Carpentries Post-workshop survey : https://carpentries.typeform.com/to/UgVdRQ?slug=2021-01-08-coderefinery-online
- Feedback about lesson template: https://carpentries.typeform.com/to/EJAMLQT5
- For other workshops on best practice of research software development and management -> CodeRefinery: coderefinery.org
- CodeRefinery's chat channel: coderefinery.zulipchat.com
- Alto also offers few courses online:https://scicomp.aalto.fi/training/scip/intro-linux-aalto-computing/ 



### Feedback

One thing that was particularly good
- Great pace and it was good balance of what was shown and what was not shown.
- typying along and breakroom exercises though perhaps a bit slower pace and a bit more time for the breakrooms to enhance the learning experiences.
- Thank you for this workshop. It was a good introduction to managing conda environements.
- Nice introduction, I wished I had known this 2 years ago :-)
- Clear explanations. My goal for the workshop was to understand if Conda will be useful for me and it was achieved (no, I do not think I will need to learn and incorporate this). Thank you!
- Nice intro starting from the basics!



One thing to improve
- The course page needs anchor links so that we can refer to specific sections instead of "the third orange box on that page"
- structure a bit better the text of the lessons, I had a bit of a problem knowing where you were
- Maybe a bit more time in the breakout rooms
- please mention and show how people shall delete everything they played during the workshop. Lots of space has been taken and most likely they never will use all the env created.
- Time management/allocation can be further optimized, but given that this workshop is still in the development phase this is completely understandable. I did not feel that my time was wasted at all.
- Breaks could be 15 minutes long. In addition, more time for hackmd (less multitasking). So perhaps 30 longer workshop in total.





### Suggestions for material

- check whether the environment name in the "Create a new environment from a YAML file" exercise has already been used before. It would be good to have a new name here so that we can check with `conda env list` whether it has been installed correctly.


### future training on containers

Below some links:

- [https://carpentries-incubator.github.io/singularity-introduction](https://carpentries-incubator.github.io/singularity-introduction)
- [https://carpentries-incubator.github.io/docker-introduction](https://carpentries-incubator.github.io/docker-introduction)
- [https://imperialcollegelondon.github.io/2020-07-13-Containers-Online](https://imperialcollegelondon.github.io/2020-07-13-Containers-Online)

