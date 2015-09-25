# So what makes Git so special?

(From: https://git-scm.com/book/en/v2/)

## Snapshots, Not Differences

The major difference between Git and any other VCS (Subversion and friends included) is the way Git thinks about its data. Most ofther systems (CVS, Subversion, Perforce, Bazaar, and so on) treat the information they keep as a set of files and the patches with changes made to each file over time.

Instead of patches, Git thinks of the repositories as a set of snapshots. Every time you commit changes to a Git repository it takes a 'picture' of the files in the repository, creating a miniature file system. If files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.

## Git stores data as snapshots of the project over time.

This difference makes Git more like a mini filesystem with some powerful tools built on top of it, rather than simply a VCS.

## Nearly Every Operation Is Local

Most of what you do with Git is done in your local computer.  Because Git stores snapshots of the files at the time you commit your changes in your local hard drive we can do a lot of things locally that, for other VCS, would require network connectivity. This means that there is very little you can’t do if you’re offline or off VPN. If you get on an airplane or a train and want to do a little work, you can commit happily until you get to a network connection to upload. If you go home and can’t get your VPN client working properly, you can still work. 

For example, to browse the history of the project, Git doesn’t need to go out to the server to get the history and display it for you – it simply reads it directly from your local database; you see the project history almost instantly. If you want to see the changes introduced between the current version of a file and the file a month ago, Git can look up the file a month ago and do a local difference calculation, instead of having to either ask a remote server to do it or pull an older version of the file from the remote server to do it locally.

## Git Has Integrity

One of the core tennets of Git is integrity. Every element in a Git repository is [check-summed](https://www.wikiwand.com/en/Checksum) before the item is stored in the repository. Git will then use the checksum to reference to that file in the repository. The checksum functionality is built into Git at the lowest levels and is integral to its philosophy. You can’t lose information in transit or get file corruption without Git being able to detect it.

The mechanism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git. A SHA-1 hash looks something like this:

> 24b9da6552252987aa493b52f8696cd6d3b00373

You will see these hash values all over the place in Git because it uses them so much. In fact, Git stores everything in its database not by file name but by the hash value of its contents.

## Git Generally Only Adds Data

When you do actions in Git, nearly all of them only add data to the Git database. It is hard to get the system to do anything that is not undoable or to make it erase data in any way. As in any VCS, you can lose or mess up changes you haven’t committed yet; but after you commit a snapshot into Git, it is very difficult to lose, especially if you regularly push your database to another repository.

You will never loose all your data. If the server hosting the repository crashes you still have your local copy which you can rebuild the repository from.  If your local copy is destroyed or you delete a local file by mistake you will only loose the changes that haven't been posted to the repository.

## The Three States

Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

This leads us to the three main sections of a Git project: **the Git directory, the working directory, and the staging area.**

The **Git directory** is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer. in Linux and OS X the directory is `.git` and it's stored at the root of the repository. In Windows the director is `git` and it is also stored in the root of the repository

The **working directory** is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

The **staging area is a file**, generally contained in your Git directory, that stores information about what will go into your next commit. It’s sometimes referred to as the “index”, but it’s also common to refer to it as the staging area.

![Three States of Files on Git](images/areas.png)

1. The basic Git workflow goes something like this:
2. You modify files in your working directory.
3. You stage the files, adding snapshots of them to your staging area.
4. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

If a particular version of a file is in the Git directory, it’s considered committed. If it has been modified and was added to the staging area, it is staged. And if it was changed since it was checked out but has not been staged, it is modified. In Git Basics, you’ll learn more about these states and how you can either take advantage of them or skip the staged part entirely.
