# Delete secrets from repo history



As I worked through the [Advent of Code challenges](https://github.com/KalindiFonda/Advent-of-Code), I learned that the creator does not appreciate[^1] the publication of the input text. I worked through tips on how to get it off from the repo, and its history from [this reddit thread](https://www.reddit.com/r/adventofcode/comments/18ehed6/re_not_sharing_inputs_psa_deleting_and_committing/)

And settled on this tool: https://pypi.org/project/git-filter-repo/

[^1]: meaning, that if we don't share challenge input, it becomes a tiny bit harder to steal the challenges to use elsewhere (so it's about IP protection)


So, this repo was my testing ground for it, as I didn't want to risk my AoC repo, not even my journal-y commit messages.

This is what worked:
```
pip install git-filter-repo  
git filter-repo --path-glob "2023/*/text.txt" --invert-paths --force
git push --set-upstream git@github.com:KalindiFonda/Advent-of-Code.git main --force
git remote add origin git@github.com:KalindiFonda/Advent-of-Code.git
```

To replace above the name of your input files (mine are called `text.txt`) and the name of your repo. 

It deleted the data files (big challenge input) both in my local repo and github repo, but kept all the commits as they were (deleting any mention of the text.txt files), except if a commit was just the file itself then it deleted the commit too.
