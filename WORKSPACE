workspace(name = "projects")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# ================================ SKYLIB ==============================================

skylib_version = "1.0.3"

http_archive(
    name = "bazel_skylib",
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
    type = "tar.gz",
    url = "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/{}/bazel-skylib-{}.tar.gz".format(skylib_version, skylib_version),
)

# ================================ JAVA ================================================

RULES_JVM_EXTERNAL_TAG = "4.3"

RULES_JVM_EXTERNAL_SHA = "6274687f6fc5783b589f56a2f1ed60de3ce1f99bc4e8f9edef3de43bdf7c6e74"

http_archive(
    name = "rules_jvm_external",
    sha256 = RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("@bazel_tools//tools/jdk:remote_java_repository.bzl", "remote_java_repository")

remote_java_repository(
    name = "corretto_jdk_21",
    prefix = "corretto",
    sha256 = "b4161b887ebbf68d6400608d2fccedb599bf18fd79e3e9c9dbfc0e27e1ed4ce1",
    strip_prefix = "amazon-corretto-21.jdk/Contents/Home",
    target_compatible_with = [
        "@platforms//cpu:arm64",
        "@platforms//os:macos",
    ],
    url = "https://corretto.aws/downloads/latest/amazon-corretto-21-aarch64-macos-jdk.tar.gz",
    version = "21",
)

register_toolchains("//bazel/jdk:corretto_21_toolchain_definition")
