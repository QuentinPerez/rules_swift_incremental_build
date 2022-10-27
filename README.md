_This repository exists to help the rules_swift team on a potential incremental build issue._

In a vanilla environment (without bazel), each time there is a change on `AppDelegate.swift:6` it takes **0.1s** to rebuild vs **2-3s** with bazel.

```bash
# no change
❯ bazel build //:App
INFO: Analyzed target //:App (25 packages loaded, 563 targets configured).
INFO: Found 1 target...
Target //:App up-to-date:
  bazel-out/applebin_ios-ios_sim_arm64-fastbuild-ST-4e6c2a19403f/bin/App.ipa
INFO: Elapsed time: 0.225s, Critical Path: 0.01s
INFO: 1 process: 1 internal.
INFO: Build completed successfully, 1 total action

# uncomment the line
sed -i '' "s#//##g" incremental-bug/AppDelegate.swift

# rebuild the app
❯ bazel build //:App
INFO: Analyzed target //:App (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
Target //:App up-to-date:
  bazel-out/applebin_ios-ios_sim_arm64-fastbuild-ST-4e6c2a19403f/bin/App.ipa
---> INFO: Elapsed time: 3.117s, Critical Path: 3.04s <---
INFO: 8 processes: 3 internal, 3 darwin-sandbox, 1 local, 1 worker.
INFO: Build completed successfully, 8 total actions
```

```bash
# build environment
❯ xcode-select -p
/Applications/Xcode-14.0.0.app/Contents/Developer

❯ bazel version
Bazelisk version: development
Build label: 5.3.2
Build target: bazel-out/darwin_arm64-opt/bin/src/main/java/com/google/devtools/build/lib/bazel/BazelServer_deploy.jar
Build time: Wed Oct 19 18:35:48 2022 (1666204548)
Build timestamp: 1666204548
Build timestamp as int: 1666204548
```
