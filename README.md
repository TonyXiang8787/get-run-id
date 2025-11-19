# get-run-id

A GitHub composite action that finds the run ID of a workflow by workflow name and commit SHA.

## Description

This action searches for a successful workflow run matching a specific workflow name and commit SHA. It's useful when you need to reference a specific workflow run ID, for example to download artifacts from that run or create dependencies between workflows.

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `workflow_name` | Name of the workflow to search for (case-sensitive) | Yes | - |
| `sha` | Commit SHA to search for | No | `github.sha` (current commit) |

## Outputs

| Output | Description |
|--------|-------------|
| `run_id` | The run ID of the successful workflow run matching the name and SHA |

## Usage

### Basic Example

```yaml
- name: Get workflow run ID
  id: get_run_id
  uses: TonyXiang8787/get-run-id@v1
  with:
    workflow_name: "Build and Test"

- name: Use the run ID
  run: echo "Run ID is ${{ steps.get_run_id.outputs.run_id }}"
```

### Search for Specific Commit

```yaml
- name: Get workflow run ID for specific commit
  id: get_run_id
  uses: TonyXiang8787/get-run-id@v1
  with:
    workflow_name: "Deploy"
    sha: "abc123def456"
```

## Requirements

- The workflow being searched must have completed successfully
- The workflow name must match exactly (case-sensitive)
- Uses the repository's `GITHUB_TOKEN` automatically (no manual token configuration needed)

## License

This project is licensed under the Mozilla Public License 2.0 (MPL-2.0). See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.
