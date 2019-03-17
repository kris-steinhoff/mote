
```     __  __       _
    |  \/  | ___ | |_ ___
    | |\/| |/ _ \| __/ _ \
    | |  | | (_) | ||  __/
    |_|  |_|\___/ \__\___|
```
*Mote is a small wrapper around git for managing your dotfiles.*

## Installation

Download the script and allow it to execute:

`curl -o mote https://raw.githubusercontent.com/ksofa2/mote/master/mote && chmod +x mote`

You can move it into a directory in your path to make it easier to call. 

## How it works

Mote uses a git repository to track the files you want to version. It does this using the technique described in this excellent blog post: [The best way to store your dotfiles: A bare Git repository](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/). Mote implements the approach described in this post by passing arguments given to it to git along with the additional flags: `--git-dir=$HOME/.mote/dotfiles.git` and `--work-tree=$HOME`. 

It also provides convenient extra subcommands to intialize or clone a repository (see Usage below). These subcommands set up your local repository to be configured with `status.showUntrackedFiles = no` so `mote status` will not list files in your home directory that you haven't explicitly tracked with `mote add`.

## Usage

Mote provides a few convenient subcommands to initialize or clone your dofiles repository and configure it correctly...

  - `mote mote-init`
  - `mote mote-clone <your_git_remote_url>`

Other than those commands, mote is just a wrapper for git. So all normal git commands will work as expected. 

## Example

```
$ mote status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .vimrc

no changes added to commit (use "git add" and/or "git commit -a")
$ mote diff
diff --git a/.vimrc b/.vimrc
index b91355a..b3c1c54 100644
--- a/.vimrc
+++ b/.vimrc
@@ -56,6 +56,7 @@ set fillchars+=vert:\  " use space as vertical split char
 
 set exrc
 set showmode
+set number
 
 set showcmd

$ mote commit -a -m "Add set number"
[master 13e902a] Add set number
 1 file changed, 1 insertion(+)
```
