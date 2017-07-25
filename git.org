init
	Create a new git repository in the current directory
	
add <filename(s)>
	Add <filename(s)> to git or unstaged updates to the staging area / cache.

commit -m 'commit message'
	Commit staged changes to the repo
	
clone <url> <optional:directory>
	Copy an existing repo from url, optionally putting it in
	<directory>
	
status 
	Reports current state of changes in the repo
	
status -s
	Short form version of the state of changes in the repo
	
diff
	Prints changes that aren't yet staged
	
diff --staged || diff --cached
	Prints staged changes that aren't yet committed
	
commit -a
	Automatically stages all tracked files with changes and then
	commits. Allows you to skip manually staging files.
	
rm <filename(s)>
	Stages the removal of <filename(s)> from the repo and from the
	working directory. Will execute on commit.
	
rm --cached <filename(s)>
	Removes <filename(s)> from the cache without deleting it from the
	working directory.
	
mv <from> <to>
	Move a tracked file
	
log
	Lists commits made to the repo in reverse chronological order
	
log -p -2
	Lists commits with differences in each commit, limiting to 2 prior
	commits.


//To reset the local git repo to the latest on the server...
git fetch origin
git reset --hard origin/master
git clean -f
