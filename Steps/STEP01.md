 
# NOOB STEP ONE GET MANIFEST

There are many ways to do this - Hopefully this will
help people to learn a little and to get started.

## 1.0  [Clone manifest from here]( https://android.googlesource.com/?format=HTML)
```
fhem@noobbuilds-laptop ~ $ git clone -b android-8.1.0_r11 https://android.googlesource.com/platform/manifest
Cloning into 'manifest'...
remote: Counting objects: 618, done
remote: Total 7462 (delta 2055), reused 7462 (delta 2055)
Receiving objects: 100% (7462/7462), 7.69 MiB | 13.32 MiB/s, done.
Resolving deltas: 100% (2055/2055), done.
Checking connectivity... done.
```
## 2.0  Change to manifest directory
```
fhem@noobbuilds-laptop ~ $ cd ~/manifest
fhem@noobbuilds-laptop ~/manifest $ git status
On branch android-8.1.0_r11
Your branch is up-to-date with 'origin/android-8.1.0_r11'.
nothing to commit, working directory clean
fhem@noobbuilds-laptop ~/manifest $ git remote -v
origin	https://android.googlesource.com/platform/manifest (fetch)
origin	https://android.googlesource.com/platform/manifest (push)
fhem@noobbuilds-laptop ~/manifest $
```
## 3.0  Use file/tree explorer to delete .git folder in manifest directory --- this will get rid of all history and give us a clean starting point for our manifest.

## 4.0  Initiate new manifest repo for our needs.
```
fhem@noobbuilds-laptop ~/manifest $ git init
Initialized empty Git repository in /home/fhem/manifest/.git/
fhem@noobbuilds-laptop ~/manifest $ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	default.xml

nothing added to commit but untracked files present (use "git add" to track)
```
## 5.0  Add manifest
```
fhem@noobbuilds-laptop ~/manifest $ git add default.xml
fhem@noobbuilds-laptop ~/manifest $ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   default.xml
```
## 6.0  Add branch
```
fhem@noobbuilds-laptop ~/manifest $ git checkout -b o81
Switched to a new branch 'o81'
```
## 7.0  Add our remote and make commit to add manifest. [Pic01](https://i.imgur.com/zWt96EU.png) [Pic02](https://i.imgur.com/SVaFR09.png) [Pic03](https://i.imgur.com/XupWZRg.png)
```
fhem@noobbuilds-laptop ~/manifest $ git remote add noob2xl https://github.com/noob2xl/platform_manifest.git
fhem@noobbuilds-laptop ~/manifest $ git commit -a -m "Initial taimen Oreo 8.1 manifest."
[o81 (root-commit) 2528815] Initial taimen Oreo 8.1 manifest.
 1 file changed, 625 insertions(+)
 create mode 100644 default.xml
```
## 8.0  Push to our git. [Pic04](https://i.imgur.com/bO4RvqA.png) [Pic05](https://i.imgur.com/3wgRVU3.png)
```
fhem@noobbuilds-laptop ~/manifest $ git push -u noob2xl o81
Username for 'https://github.com': fhemaosp
Password for 'https://fhemaosp@github.com': 
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 7.25 KiB | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/noob2xl/platform_manifest.git
 * [new branch]      o81 -> o81
Branch o81 set up to track remote branch o81 from noob2xl.
fhem@noobbuilds-laptop ~/manifest $
```
## 9.0  Edit manifest for our use, check diff, make commit, and push to git. [Example of git diff](https://i.imgur.com/1DoAfGu.png)
```
fhem@noobbuilds-laptop ~/manifest $ git status
On branch o81
Your branch is up-to-date with 'noob2xl/o81'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   default.xml

no changes added to commit (use "git add" and/or "git commit -a")

fhem@noobbuilds-laptop ~/manifest $ git diff
diff --git a/default.xml b/default.xml
index 1d14ac8..97b700f 100644
--- a/default.xml
+++ b/default.xml
@@ -1,13 +1,32 @@
 <?xml version="1.0" encoding="UTF-8"?>
 <manifest>
 
+  <remote  name="github"
+           fetch="https://github.com" />
   <remote  name="aosp"
-           fetch=".."
-           review="https://android-review.googlesource.com/" />
+           fetch="https://android.googlesource.com"
+           review="android-review.googlesource.com" />
+  <remote  name="noob"
+           fetch="https://github.com/noob2xl/"
+           sync-j="6" />
   <default revision="refs/tags/android-8.1.0_r11"
            remote="aosp"
+           sync-c="true"
            sync-j="4" />
 
+
+  <!-- noob repos -->
+  <project path="manifest" name="platform_manifest" remote="noob" revision="o81" />
+
+
+  <!-- noob kernels -->
+
+
+  <!-- noob proprietary vendor blobs -->
+
+
+
+  <!-- aosp repos -->
   <project path="build/make" name="platform/build" groups="pdk" >
     <copyfile src="core/root.mk" dest="Makefile" />
     <linkfile src="CleanSpec.mk" dest="build/CleanSpec.mk" />

fhem@noobbuilds-laptop ~/manifest $ git commit -a -m "Add remotes, headers, track our manifest."
[o81 2aa61af] Add remotes, headers, track our manifest.
 1 file changed, 21 insertions(+), 2 deletions(-)
fhem@noobbuilds-laptop ~/manifest $ git push -u noob2xl o81
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 535 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/noob2xl/platform_manifest.git
   2528815..2aa61af  o81 -> o81
Branch o81 set up to track remote branch o81 from noob2xl.
fhem@noobbuilds-laptop ~/manifest $
```
## 10.0 Add README.md file and push to git.
```
fhem@noobbuilds-laptop ~/manifest $ git status
On branch o81
Your branch is up-to-date with 'noob2xl/o81'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
fhem@noobbuilds-laptop ~/manifest $ git add README.md
fhem@noobbuilds-laptop ~/manifest $ git commit -a -m "Add README.md"
[o81 4afe495] Add README.md
 1 file changed, 8 insertions(+)
 create mode 100644 README.md
fhem@noobbuilds-laptop ~/manifest $ git push -u noob2xl o81
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 397 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/noob2xl/platform_manifest.git
   2aa61af..4afe495  o81 -> o81
Branch o81 set up to track remote branch o81 from noob2xl.
fhem@noobbuilds-laptop ~/manifest $ 
```
