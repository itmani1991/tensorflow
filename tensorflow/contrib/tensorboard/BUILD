# Description:
# TensorBoard module containing volatile or experimental code.

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

# For platform specific build config
load("//tensorflow/core:platform/default/build_config.bzl", "tf_proto_library")
load("//tensorflow:tensorflow.bzl", "py_test")

tf_proto_library(
    name = "protos_all",
    srcs = glob(["**/*.proto"]),
    go_api_version = 2,
    visibility = ["//visibility:public"],
)

# API methods in `tf.contrib.tensorboard` package.
py_library(
    name = "tensorboard",
    srcs = ["__init__.py"],
    srcs_version = "PY2AND3",
    deps = [":plugins"],
)

# API methods in `tf.contrib.tensorboard.plugins` package.
py_library(
    name = "plugins",
    srcs = ["plugins/__init__.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":projector",
        ":trace",
    ],
)

# API methods and protos in `tf.contrib.tensorboard.plugins.projector` package.
py_library(
    name = "projector",
    srcs = ["plugins/projector/__init__.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python:lib",
        "//tensorflow/tensorboard/plugins/projector:protos_all_py",
    ],
)

py_test(
    name = "projector_api_test",
    size = "small",
    srcs = ["plugins/projector/projector_api_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":projector",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:platform",
        "//tensorflow/python:summary",
        "//tensorflow/tensorboard/plugins/projector:protos_all_py",
    ],
)

# API methods and protos in `tf.contrib.tensorboard.plugins.trace` package.
py_library(
    name = "trace",
    srcs = glob(
        ["plugins/trace/**/*.py"],
        exclude = ["**/*test*"],
    ),
    srcs_version = "PY2AND3",
    deps = [
        ":protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
    ],
)

py_test(
    name = "trace_test",
    size = "small",
    srcs = ["plugins/trace/trace_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":trace",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:platform",
    ],
)

filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
        ],
    ),
    visibility = ["//visibility:public"],
)
