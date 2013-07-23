gitTest
=======
How to work on git (my personal experience)

You can work on two type of repository on github
1 - those which you have push permissions
2 - thos which you don't have push permissions and you need a "pull request" to add your developments

While the develop on the repository of type 1 can be faster and simpler, it requires more attention when commit and push.
The type 2 is more safe, but requires more steps.

Let's start from type 2, that covers the h2gglobe case.

# Repository of type 2
First of all, start with copying the entire repository from the central place to your personal github area.
This step is called "fork" and should be done only once.

Go on the github page of the repository you want to copy: for example https://github.com/CMSROMA/gitTest
On the upper right part of the page there is a button "fork".
Select @yourusername as destitation in order to fork into your personal github area.

Now you have the perfect copy of the central repository.

==
The second step is to make a clone of the repository on your local machine (can be lxplus or your own personal computer).
I do:
git clone git@github.com:shervin86/gitTest.git 

you should put your github username instead of shervin86.

==
Now you have a working copy on your CMSSW relase probably.
Few concepts:
 - your are working on a branch that is called "master"
   my advice is to never commit directly on this branch
 - you should create a new branch with a reasonable name (for example "newSelection", please don't use "pippo")
 - move on that branch 
 - start to right the code
 - commit the changes frequently with meaningful messages 
 - if you have finished (only if you have finished!), move to the "master" branch
 - merge the "newSelection" branch with the master
 - then push the updates to your personal copy on github
 - if it's fine and you finished all the changes, make a pull request to merge your work with the central repository

Now, an example, still conceptual without commands:
 - I forked the TopHiggsAnalysis from CMSROMA into my github
 - I cloned my version of TopHiggsAnalysis, I have it on my laptop
 - I have to update 3 things: 1) few cuts in the analysis, 2) the PU reweight for the run dependent MC, 3) fix the macro for the plots
 - I create 3 branches: newSelection, puReweight, plotMacro
 - I'm on the master and I move to the plotMacro to start to work on that
 - I do some changes and I commit them
 - I'm tired and I want to move to the puReweight stuff also if I've not finished with the plotMacro
 - I change the branch (I have to be sure to have committed all the changes for plotMacro before)
 - I do the changes and I commit many times
 - Now the work for puReweight is finished, for plotMacro is ongoing and for newSelection is not yet started
 - I move to the "master" branch, I merge the puReweight and I push to the github repository
 - I don't need the puReweight branch anymore and I delete it
 - now on github only the master has been updated
 - I can push the new branches newSelection and plotMacro to the repository in order to have them saved also on the server
 - another day I can switch to one of the remaining branches to continue to work, then I will merge with the master once finished and I push the master.





Now I'm trying to modify these file

How to import in CMSSW from a personal repository

Structure you repository as a sub-package of CMSSW.
Example: in you repository create a directory named Calibration as the one in CMSSW
Calibration/myFolder

commit into your repository as a specific branch

in a CMSSW release add the CMSSW package in which you want to add your code

git cms-addpkg Calibration
# add your repository in the list of repos (remote branches will be looked also there)
git remote add -f ecalelff https://:@git.cern.ch/kerberos/ecalelf
# create a local branch pointing to the remote one you created
git checkout -b from_ecalelff ecalelff/cmsswMigration
git checkout from-CMSSW_6_2_0_pre8
git merge from_ecalelff
