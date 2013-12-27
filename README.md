This repository contains Dart headers and static library files to embed the VM into C/C++ projects.

I use it to embed Dart into Openframeworks via ofxFieldKitDart
(see also: https://github.com/field/ofxFieldKitDart)


## Steps to rebuild Dart static binaries

### Mac OS X:

#### 1. Install depot tools:

```
cd <directory where you want the depot_tools to live>
svn co http://src.chromium.org/svn/trunk/tools/depot_tools
export PATH=$PATH:`pwd`//depot_tools
```

#### 2. Get source with gclient and git svn:

(see also https://code.google.com/p/dart/wiki/GettingTheSource)

```
svn ls https://dart.googlecode.com/svn/branches/bleeding_edge/
mkdir dart-git
cd dart-git
gclient config https://dart.googlecode.com/svn/branches/bleeding_edge/deps/all.deps
git svn clone -rHEAD https://dart.googlecode.com/svn/branches/bleeding_edge/dart dart
gclient sync
gclient runhooks
```

Open Xcode project at dart/runtime/dart-runtime.xcodeproj. Build target 'All', .a binaries will be in dart/xcodebuild/Debug.

To generate the library snapshop binary, run the followinng from xcodebuild/Debug:

#### 3. Generate Library Snapshot

```
./gen_snapshot --snapshot=snapshot_gen.bin
```

#### 4. Copy Files

Copy products over into this repository.
dart/runtime/include/*.h
dart/xcodebuild/Debug/*.a
dart/xcodebuild/Release/*.a