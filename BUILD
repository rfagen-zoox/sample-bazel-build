load("@python3_deps//:requirements.bzl", "requirement")
load("//tools/python:mypy.bzl", "mypy_binary", "mypy_library", "mypy_test")

# see https://bazelbuild.slack.com/archives/CA31HN1T3/p1681836821518969?thread_ts=1681836640.166589&cid=CA31HN1T3
# for description of these test cases

filegroup(
    name = "always_files",
    srcs = [
        ":random_data.txt",
        ":child.h.template",
        "//ci/cinder/plans:zrte.py",
        "//ci/cinder/plans:zrte_test.py",
    ],
)

filegroup(
    name = "never_files",
    srcs = [
        ":child_child.py",
    ],
)

filegroup(
    name = "parent_data",
    srcs = [
        ":parent_data.txt",
    ],
)

py_binary(
    name = "ignore_parent",
    srcs = ["ignore_parent.py"],
    deps = [
        ":child",
    ],
    tags = ["safety-fw-unaffected"],
)

py_binary(
    name = "parent",
    srcs = [
        "parent.py",
        "parent_helper.py",
    ],
    deps = [
        ":parent_orphan",
        ":parent_data",
        ":ignore_child",
    ],
    tags = ["safety-firmware-affected"],
)

py_binary(
    name = "aunt",
    srcs = ["aunt.py"],
    deps = [
        ":parent_data",
        ":aunt_orphan",
    ],
    tags = ["safety-firmware-affected"],
)

py_binary(
    name = "uncle",
    srcs = ["uncle.py"],
    deps = [
        ":ignore_child",
    ],
    tags = ["safety-firmware-affected"],
)

py_library(
    name = "ignore_child",
    srcs = [
        "ignore_child.py",
        "child.h.template",
    ],
    deps = [
        ":ignore_orphan",
        ":transitive_child",
        ":transitive_sibling",
    ],
    tags = ["safety-fw-unaffected"],
)

py_library(
    name = "ignore_orphan",
    srcs = [
        "ignore_orphan.py",
    ],
    deps = [
        ":transitive_child",
    ],
)

py_library(
    name = "parent_orphan",
    srcs = [
        "parent_orphan.py",
    ],
    deps = [
        ":child",
    ],
)

py_library(
    name = "aunt_orphan",
    srcs = [
        "aunt_orphan.py",
    ],
    deps = [
        ":transitive_child",
    ],
)

py_library(
    name = "child",
    srcs = [
        "child.py",
    ],
    deps = [
        ":transitive_child",
        ":child_child",
    ],
)

py_library(
    name = "child_child",
    srcs = [
        "child_child.py",
    ],
    deps = [
        ":child_child_child",
    ],
)

py_library(
    name = "child_child_child",
    srcs = [
        "child_child_child.py",
    ],
)

py_library(
    name = "transitive_child",
    srcs = [
        "transitive_child.py",
    ],
    deps = [
        ":transitive_sibling_child",
        ],
)

py_library(
    name = "transitive_sibling",
    srcs = [
        "transitive_sibling.py",
    ],
    deps = [
        ":transitive_sibling_pet",
        ],
)

py_library(
    name = "transitive_sibling_pet",
    srcs = [
        "transitive_sibling_pet.py",
    ],
    deps = [
        ":transitive_sibling_child",
        ],
)

py_library(
    name = "transitive_sibling_child",
    srcs = [
        "transitive_sibling_child.py",
    ],
    deps = [
        ":transitive_sibling_child_pet",
    ],
)

py_library(
    name = "transitive_sibling_child_pet",
    srcs = [
        "transitive_sibling_child_pet.py",
    ],
)

