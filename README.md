# Gradescope Autograder Template
a good template for setting up gradescope autograding with python

- uses github `deploy key` to make your gradescope tests always up to date with your assignment repo
- makes it easy to test locally with your solution using standard `unittest`
- makes sure your solution files are deleted before testing on gradescope, therefore unaccessible to students with `import solution`

TODO:
- maybe make default integration tests such that you write `solution.py` and `solution_template.py` and tests are automatically created

## setup
0. use python 3+ (3.7 is best)
1. install the requirements
```
pip install -r requirements.txt
```
2. to make assignment updating easier, we can submit an assignment test once and from then on have the newest version pulled from github every time the test is run, to do this you need to create a github `deploy_key` that will let gradescope read the repo

follow instructions [here](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys) and put the new key in `~/.ssh/deploy_key`


## making a new assignment
1. create a folder named `assigment$name`
2. in the assignment folder, create a solution template file (or folder) that students will have to complete
3. in the assignment folder, create a solution file (or folder) `$solution`
4. in the assignment folder, write tests for the template making sure that each file starts with `test_`

## running your tests locally
you can run all your tests in the assignment folder with `unittest`
```
python -m unittest *
```

## upload the assignment on gradescope
1. create the assignment zip with `./make_assignment.sh $name $solution`
2. upload the resulting `assignment$name.zip` to gradescope

check assignment 0 for an example, it was created with `./make_assignment.sh 0 solution.py`

## updating the assignment
because we're using the github `deploy_key` you just need to push your changes to this repo and that's it!

the only time you should need to re-run `make_assignment.sh` and reupload the assignment on gradescope is if you change the name of the assignment (`$name`) or the name of the template (`$template`)
