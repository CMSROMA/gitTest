gitTest
=======
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
