load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load(
    "@build_bazel_rules_apple//apple:versioning.bzl",
    "apple_bundle_version",
)

swift_library(
    name = "iosapp",
    srcs = [
        "incremental-bug/AppDelegate.swift",
    ],
    module_name = "iosapp",
)

apple_bundle_version(
    name = "version",
    build_version = "0.0.1",
)

ios_application(
    name = "App",
    bundle_id = "com.incremental-bug",
    families = [
        "iphone",
    ],
    infoplists = ["incremental-bug/Info.plist"],
    launch_storyboard = "incremental-bug/Base.lproj/LaunchScreen.storyboard",
    minimum_os_version = "15.0",
    version = ":version",
    deps = [
        ":iosapp",
    ],
)
