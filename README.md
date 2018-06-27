```
#!/bin/bash
# declare an array called files, that contains 3 values
#!/usr/bin/expect -f

declare -a RepoPaths=(
    "/var/www/html/educomp/kapil/git-test"
#    "/var/www/html/educomp/kapil/git-test"
)
MASTER_BRANCH='master'
GIT_USER="<username>"
GIT_PASS="<password>"

#Loop
for REPO in "${RepoPaths[@]}"
do
  echo "INIT MERGE STEPS FOR REPO: $Path"
  cd $REPO
  URL=$(git remote -v | head -n1 | cut -f2 | cut -d" " -f1)
  CURRENT_BRANCH=$(git rev-parse --abbrev-ref HEAD)

  if [ "$MASTER_BRANCH" == "$CURRENT_BRANCH" ]; then
    echo "ALREADY ON MASTER BRANCH"
  else 
    LAST_COMMIiT=$(git rev-list -1 HEAD)
    PUSH_URL="https://$GIT_USER:$GIT_PASS@${URL:8}"
    echo "PUSH URL = " $PUSH_URL " AND CURRENT BRANCH = " . $CURRENT_BRANCH
    echo Automatically merging commit $LAST_COMMIT from $CURRENT_BRANCH rippling to $MASTER_BRANCH
    echo CHECKOUT BRANCH $MASTER_BRANCH
    git pull $PUSH_URL $CURRENT_BRANCH
    git checkout $MASTER_BRANCH 
    echo TAKE PULL OR $MASTER_BRANCH
    git pull $PUSH_URL $MASTER_BRANCH
    echo GO BACK TO CURRECT BRANCH $CURRENT_BRANCH
    git checkout $CURRENT_BRANCH
    echo MERGE $MASTER_BRANCH INTO $CURRENT_BRANCH
    git merge $MASTER_BRANCH
    echo PUSH MERGE CHANGES TO $CURRENT_BRANCH
    git push $PUSH_URL $CURRENT_BRANCH
  fi
done
```
