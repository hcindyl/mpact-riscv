# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

workspace(name = "com_google_mpact-riscv")


load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_file", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# Additional bazel rules.
http_archive(
    name = "bazel_skylib",
    sha256 = "b8a1527901774180afc798aeb28c4634bdccf19c4d98e7bdd1ce79d1fe9aaad7",
    urls = ["https://github.com/bazelbuild/bazel-skylib/releases/download/1.4.1/bazel-skylib-1.4.1.tar.gz"],
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

# Google Absail.
http_archive(
    name = "com_google_absl",
    sha256 = "3ea49a7d97421b88a8c48a0de16c16048e17725c7ec0f1d3ea2683a2a75adc21",
    urls = ["https://github.com/abseil/abseil-cpp/archive/refs/tags/20230125.0.tar.gz"],
    strip_prefix="abseil-cpp-20230125.0",
)

# Google protobuf.
http_archive(
    name = "com_google_protobuf",
    sha256 = "4eab9b524aa5913c6fffb20b2a8abf5ef7f95a80bc0701f3a6dbb4c607f73460",
    urls = ["https://github.com/protocolbuffers/protobuf/releases/download/v21.12/protobuf-cpp-3.21.12.tar.gz"],
    strip_prefix="protobuf-3.21.12",
)

# Google re2
http_archive(
    name = "com_google_re2",
    sha256 = "7a9a4824958586980926a300b4717202485c4b4115ac031822e29aa4ef207e48",
    urls = ["https://github.com/google/re2/archive/refs/tags/2023-03-01.tar.gz"],
    strip_prefix = "re2-2023-03-01"
)

# ELFIO header based library.
http_archive(
    build_file = "BUILD.elfio",
    name = "com_github_serge1_elfio",
    strip_prefix = "elfio-3.9",
    sha256 = "767b269063fc35aba6d361139f830aa91c45dc6b77942f082666876c1aa0be0f",
    urls = ["https://github.com/serge1/ELFIO/releases/download/Release_3.9/elfio-3.9.tar.gz"],
)

# Bazel rules for proto.
http_archive(
    name = "rules_proto_grpc",
    sha256 = "fb7fc7a3c19a92b2f15ed7c4ffb2983e956625c1436f57a3430b897ba9864059",
    strip_prefix = "rules_proto_grpc-4.3.0",
    urls = ["https://github.com/rules-proto-grpc/rules_proto_grpc/archive/4.3.0.tar.gz"],
)

# Google test.
http_archive(
    name = "com_google_googletest",
    strip_prefix = "googletest-1.13.0",
    sha256 = "ad7fdba11ea011c1d925b3289cf4af2c66a352e18d4c7264392fead75e919363",
    urls = ["https://github.com/google/googletest/archive/refs/tags/v1.13.0.tar.gz"],
)

# Antlr4 c++ runtime.
http_archive(
    name = "org_antlr4_cpp_runtime",
    build_file = "BUILD.antlr4",
    sha256 = "8018c335316e61bb768e5bd4a743a9303070af4e1a8577fa902cd053c17249da",
    urls = ["https://www.antlr.org/download/antlr4-cpp-runtime-4.11.1-source.zip"],
)

# Antlr4 tool (java).
http_file(
    name = "org_antlr_tool",
    sha256 = "62975e192b4af2622b72b5f0131553ee3cbce97f76dc2a41632dcc55e25473e1",
    url = "https://www.antlr.org/download/antlr-4.11.1-complete.jar",
)

# Additional rules for building non-bazel projects. Antlr4 builds using cmake.
http_archive(
    name = "rules_foreign_cc",
    sha256 = "2a4d07cd64b0719b39a7c12218a3e507672b82a97b98c6a89d38565894cf7c51",
    strip_prefix = "rules_foreign_cc-0.9.0",
    url = "https://github.com/bazelbuild/rules_foreign_cc/archive/refs/tags/0.9.0.tar.gz",
)

# MPACT-Sim repo
http_archive(
    name = "mpact-sim",
    sha256 = "8bff1907a07410cca3dbde8795797fff237bf19f4d3d696df4c5d8219de276b0",
    strip_prefix = "mpact-sim-0.0.1",
    url = "https://github.com/google/mpact-sim/archive/refs/tags/0.0.1.tar.gz",
)

# Binding to tool targets in mpact-sim. This is required for the macros
# in mpact_sim_isa.bzl to work properly when generating code for the
# decoders. These create the //external:decoder_gen and
# //external:bin_format_gen aliases used in mpact_sim_isa.bzl.
bind(
    name = "decoder_gen",
    actual = "@mpact-sim//mpact/sim/decoder:decoder_gen",
)

bind(
    name = "bin_format_gen",
    actual = "@mpact-sim//mpact/sim/decoder:bin_format_gen",
)

# Additional rules for licenses
http_archive(
    name = "rules_license",
    sha256 = "6157e1e68378532d0241ecd15d3c45f6e5cfd98fc10846045509fb2a7cc9e381",
    url = "https://github.com/bazelbuild/rules_license/releases/download/0.0.4/rules_license-0.0.4.tar.gz"
)

load("@rules_foreign_cc//foreign_cc:repositories.bzl", "rules_foreign_cc_dependencies")
rules_foreign_cc_dependencies()

load("@rules_proto_grpc//:repositories.bzl", "rules_proto_grpc_toolchains", "rules_proto_grpc_repos")
rules_proto_grpc_toolchains()
rules_proto_grpc_repos()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()

load("@rules_license//:deps.bzl", "rules_license_dependencies")
rules_license_dependencies()
