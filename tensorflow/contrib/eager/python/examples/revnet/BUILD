licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//tensorflow:internal"])

load("//tensorflow:tensorflow.bzl", "cuda_py_test")

# Model
py_library(
    name = "ops",
    srcs = ["ops.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "config",
    srcs = ["config.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "blocks",
    srcs = ["blocks.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":ops",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "revnet",
    srcs = ["revnet.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":blocks",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "resnet_preprocessing",
    srcs = ["resnet_preprocessing.py"],
    srcs_version = "PY2AND3",
    tags = ["local"],
    deps = [
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "imagenet_input",
    srcs = ["imagenet_input.py"],
    srcs_version = "PY2AND3",
    tags = ["local"],
    deps = [
        ":resnet_preprocessing",
        "//tensorflow:tensorflow_py",
    ],
)

# Tests
cuda_py_test(
    name = "ops_test",
    size = "medium",
    srcs = ["ops_test.py"],
    additional_deps = [
        ":ops",
        "//tensorflow:tensorflow_py",
    ],
    shard_count = 4,
    tags = [
        "oss_serial",
    ],
)

cuda_py_test(
    name = "blocks_test",
    size = "medium",
    srcs = ["blocks_test.py"],
    additional_deps = [
        ":blocks",
        "//tensorflow:tensorflow_py",
    ],
    shard_count = 4,
    tags = [
        "optonly",
    ],
)

cuda_py_test(
    name = "revnet_test",
    size = "medium",
    srcs = ["revnet_test.py"],
    additional_deps = [
        ":blocks_test",
        ":config",
        ":revnet",
        "//tensorflow:tensorflow_py",
    ],
    shard_count = 4,
    tags = [
        "no_pip",  # depends on blocks_test, which is not available in pip package
        "optonly",
        "oss_serial",
    ],
)

# Training
py_library(
    name = "cifar_input",
    srcs = ["cifar_input.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow:tensorflow_py",
    ],
)

py_binary(
    name = "cifar_tfrecords",
    srcs = ["cifar_tfrecords.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow:tensorflow_py",
    ],
)

py_binary(
    name = "main",
    srcs = ["main.py"],
    srcs_version = "PY2AND3",
    deps = [":main_lib"],
)

py_library(
    name = "main_lib",
    srcs = ["main.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":cifar_input",
        ":config",
        ":revnet",
        "//tensorflow:tensorflow_py",
    ],
)

py_binary(
    name = "main_estimator",
    srcs = ["main_estimator.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":cifar_input",
        ":main_lib",
        ":revnet",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "main_estimator_lib",
    srcs = ["main_estimator.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":cifar_input",
        ":main_lib",
        ":revnet",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "main_estimator_tpu_lib",
    srcs = ["main_estimator_tpu.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":cifar_input",
        ":main_lib",
        ":revnet",
        "//tensorflow:tensorflow_py",
    ],
)
