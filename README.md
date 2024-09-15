# cifuzz bazel example

This project is already initialized with **cifuzz** and ready to be used. If
the cifuzz.yaml is missing, you can generate it with the following command:

```bash
cifuzz init
```

cifuzz can generate an empty fuzz target for you. You can generate it with the
following command:

```bash
cifuzz create
```

We already include a simple fuzz target in this project. You can start fuzzing
with the following command: It should quickly produce a finding, but slow
enough to see the progress of the fuzzer.

```bash
cifuzz run //src:explore_me_fuzz_test
```

Findings can be shown with the finding command:

```bash
cifuzz findings
```

Coverage can be shown with the coverage command:

```bash
cifuzz coverage
```

To use the LLM features, you can first search for good candidates to fuzz
(requires compile commands):

```bash
bazel run @hedron_compile_commands//:refresh_all
```

Set your LLM configuration:


## Configuration

Currently, configuration is done only via environment variables.

- CIFUZZ_LLM_API_URL - Base URL for the LLM API server.
- CIFUZZ_LLM_API_TOKEN - API token when talking to the LLM API.
  In the BMW LLM client this will be set as the `x-apikey` header.
- CIFUZZ_LLM_API_TYPE - Supported: BMW, OPEN_AI, AZURE, AZURE_AD,
  CLOUDFLARE_AZURE.
- CIFUZZ_LLM_MODEL - LLM model to use.
- CIFUZZ_LLM_TEMPERATURE - Temperature setting for chat completion.
- CIFUZZ_LLM_MAX_TOKENS - Maximum number of tokens for a single chat completion
  request.
- CIFUZZ_LLM_API_HEADER_some_header - Additional headers to add to HTTP
  requests. Multiple possible. "\_" in some-header is replaced by "-" in the
  header.

Only OpenAI:

- CIFUZZ_LLM_AZURE_DEPLOYMENT_NAME - Name of the azure OpenAI deployment.
  Required when setting `CIFUZZ_LLM_API_TYPE` to `AZURE` or similar.
- CIFUZZ_LLM_API_VERSION - OpenAI API version.


```bash
 cifuzz create exploreMe --build-dir .
```

Automatic e2e testing with spark:

```bash
cifuzz spark --build-dir . --build-file cifuzz-spark/BUILD.bazel --include-files "src/**" -v
```
