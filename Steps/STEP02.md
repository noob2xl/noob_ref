# NOOB STEP TWO -- SYNC UP, PUSH REPO, TRACK REPO LOCALLY

## 1.0  SYNC UP YOUR MANIFEST
```
mkdir noob2xl
cd ~/noob2xl
repo init -u https://github.com/noob2xl/platform_manifest -b o81
repo sync
```
## 2.0  Open terminal in ~/noob2xl/build/make
``` 
fhem@noobbuilds-laptop ~ $ cd '/home/fhem/noob2xl/build/make'
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git status
Not currently on any branch.
nothing to commit, working directory clean
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git remote -v
aosp	https://android.googlesource.com/platform/build (fetch)
aosp	https://android.googlesource.com/platform/build (push)
```
##  Add your branch
```
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git checkout -b o81
Switched to a new branch 'o81'
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git branch
* o81
```
## 3.0  Remove aosp remote and add your remote
```
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git remote rm aosp
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git remote add noob https://github.com/noob2xl/platform_build_make.git
```
## 4.0  Push repo to your github
fhem@noobbuilds-laptop ~/noob2xl/build/make $ git push -u noob o81
Username for 'https://github.com': fhemaosp
Password for 'https://fhemaosp@github.com': 
Counting objects: 127801, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (44781/44781), done.
Writing objects: 100% (127801/127801), 45.35 MiB | 713.00 KiB/s, done.
Total 127801 (delta 82549), reused 127210 (delta 82031)
remote: Resolving deltas: 100% (82549/82549), done.
To https://github.com/noob2xl/platform_build_make.git
 * [new branch]      o81 -> o81
Branch o81 set up to track remote branch o81 from noob.
```
## 5.0  Move terminal to ~/noob2xl/manifst
```
fhem@noobbuilds-laptop ~/noob2xl/build/make $ cd '/home/fhem/noob2xl/manifest'
```
## 6.0  Edit manifest
```
fhem@noobbuilds-laptop ~/noob2xl/manifest $ git status
On branch o81
Your branch is up-to-date with 'noob/o81'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   default.xml

no changes added to commit (use "git add" and/or "git commit -a")
fhem@noobbuilds-laptop ~/noob2xl/manifest $ git diff
diff --git a/default.xml b/default.xml
index ac87589..b30e712 100644
--- a/default.xml
+++ b/default.xml
@@ -17,6 +17,15 @@
 
   <!-- noob repos -->
   <project path="manifest" name="platform_manifest" remote="noob" revision="o81" />
+  <project path="build/make" name="platform_build_make" groups="pdk" remote="noob" revision="o81" >
+    <copyfile src="core/root.mk" dest="Makefile" />
+    <linkfile src="CleanSpec.mk" dest="build/CleanSpec.mk" />
+    <linkfile src="buildspec.mk.default" dest="build/buildspec.mk.default" />
+    <linkfile src="core" dest="build/core" />
+    <linkfile src="envsetup.sh" dest="build/envsetup.sh" />
+    <linkfile src="target" dest="build/target" />
+    <linkfile src="tools" dest="build/tools" />
+  </project>
 
 
   <!-- noob kernels -->
@@ -27,15 +36,6 @@
 
 
   <!-- aosp repos -->
-  <project path="build/make" name="platform/build" groups="pdk" >
-    <copyfile src="core/root.mk" dest="Makefile" />
-    <linkfile src="CleanSpec.mk" dest="build/CleanSpec.mk" />
-    <linkfile src="buildspec.mk.default" dest="build/buildspec.mk.default" />
-    <linkfile src="core" dest="build/core" />
-    <linkfile src="envsetup.sh" dest="build/envsetup.sh" />
-    <linkfile src="target" dest="build/target" />
-    <linkfile src="tools" dest="build/tools" />
-  </project>
   <project path="build/blueprint" name="platform/build/blueprint" groups="pdk,tradefed" />
```
## 7.0  Commit manifest changes
```
fhem@noobbuilds-laptop ~/noob2xl/manifest $ git commit -a -m "Track build/make locally."
[o81 cc7229c] Track build/make locally.
 1 file changed, 9 insertions(+), 9 deletions(-)
```
## 8.0  Push commit to git
```
fhem@noobbuilds-laptop ~/noob2xl/manifest $ git push -u noob o81
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 372 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/noob2xl/platform_manifest
   271c23f..cc7229c  o81 -> o81
Branch o81 set up to track remote branch o81 from noob.
fhem@noobbuilds-laptop ~/noob2xl/manifest $ 
```
