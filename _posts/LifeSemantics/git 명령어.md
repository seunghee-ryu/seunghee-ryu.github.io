## Git global setup
git config --global user.name "류승희"
git config --global user.email "sh.ryu@lifesemantics.kr"

## Create a new repository
git clone http://172.16.0.21:8000/lh_smart_home_health_care/lh.git
cd lh
touch README.md
git add README.md
git commit -m "add README"

## Push an existing folder
cd existing_folder
git init
git remote add origin http://172.16.0.21:8000/lh_smart_home_health_care/lh.git
git add .
git commit -m "Initial commit"

## Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin http://172.16.0.21:8000/lh_smart_home_health_care/lh.git
