# CP5231 Project

## First time Setup
```
git clone --recurse-submodules https://github.com/e0002916/CS5231_Project.git
docker-compose up

docker exec --user git -it gitea bash
gitea admin user create --name user1 --password password --email user1@nus.u.edu
# Login with user 'user1' and password 'password' and create empty repo called "repo"
```

## Playback Git
```
cd CS5231_Project_Git_Playback
git log --reverse --pretty=format:"%h" --no-patch > /tmp/playback

while read p; do
 git push http://user1:password@localhost:3000/user1/repo.git $p:refs/heads/main
 sleep 10
done< /tmp/playback
```

## Reset Repo to initial commit
```
git push http://user1:password@localhost:3000/user1/repo.git $(git rev-list --all | tail -n 1):refs/heads/main -f
```

