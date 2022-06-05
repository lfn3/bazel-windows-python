load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

rules_python_version = "4f4f792772aa1b7cd85b64f900444c8c1ffc929a"  # Latest @ 2022-06-05

http_archive(
    name = "rules_python",
    sha256 = "dcf15bb0e5c28920104a779e1b1f1f37bccb07af2bbea8492e85beaf808054ef",
    strip_prefix = "rules_python-{}".format(rules_python_version),
    url = "https://github.com/bazelbuild/rules_python/archive/{}.zip".format(rules_python_version),
)

# load("@rules_python//python:repositories.bzl", "python_repository")
# load("@rules_python//python:versions.bzl", "DEFAULT_RELEASE_BASE_URL", "LINUX_NAME", "TOOL_VERSIONS", "get_release_url")

PYTHON_VERSION = "3.8"

# LINUX_PLATFORM = "x86_64-unknown-linux-gnu"

# sha256 = TOOL_VERSIONS[PYTHON_VERSION]["sha256"][LINUX_PLATFORM]

# (release_filename, url, strip_prefix) = get_release_url(LINUX_PLATFORM, PYTHON_VERSION, DEFAULT_RELEASE_BASE_URL, TOOL_VERSIONS)

# LINUX_PYTHON_REPO_NAME = "{name}_{platform}".format(
#         name = LINUX_NAME,
#         platform = LINUX_PLATFORM,
#     )

# python_repository(
#     name = LINUX_PYTHON_REPO_NAME,
#     platform = LINUX_PLATFORM,
#     python_version = PYTHON_VERSION,
#     release_filename = release_filename,
#     sha256 = sha256,
#     strip_prefix = strip_prefix,
#     url = url,
# )

# LOAD_TARGET = "@{repo}//defs".format(repo = LINUX_PYTHON_REPO_NAME)

# load(LOAD_TARGET, )

# register_toolchains("@{name}_toolchains//:{platform}_toolchain".format(
#     name = LINUX_NAME,
#     platform = LINUX_PLATFORM,
# ))

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python3_8",
    # Available versions are listed in @rules_python//python:versions.bzl.
    # We recommend using the same version your team is already standardized on.
    python_version = PYTHON_VERSION,
)

load("@python3_8//:defs.bzl", "interpreter")

# register_toolchains("//win_toolchain:win_toolchain")

load("@rules_python//python:pip.bzl", "pip_parse")

# Create a central repo that knows about the dependencies needed from
# requirements_lock.txt.
pip_parse(
    name = "my_deps",
    python_interpreter_target = interpreter,
    requirements_lock = "//:requirements.txt",
)

# Create a central repo that knows about the dependencies needed from
# requirements_lock.txt.
# pip_parse(
#     name = "my_deps",
#     python_interpreter_target = interpreter,
#     requirements_lock = "//:requirements.txt",
# )

# Load the starlark macro which will define your dependencies.
load("@my_deps//:requirements.bzl", "install_deps")

# Call it to define repos for your requirements.
install_deps()
