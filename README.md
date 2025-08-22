# In the original repo(s)
git log --author="Your Name" --date=short --pretty=%ad \
| sort | uniq -c | awk '{print $1" "$2}' > ~/counts.txt

# In the current repo
cp ~/counts.txt .

## 2) drop your counts file here (copy from Step A)
cp ~/counts.txt .

## 3) replay: make empty commits dated in the past
while read COUNT DATE; do
  for i in $(seq 1 "$COUNT"); do
    export GIT_AUTHOR_DATE="${DATE}T12:00:00Z"
    export GIT_COMMITTER_DATE="$GIT_AUTHOR_DATE"
    git commit --allow-empty -m "work ${DATE} #$i" >/dev/null
  done
done < counts.txt
